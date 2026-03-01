# CQ-0002: Decoupling Maintenance Routing from Application Logic via ALB Listener Rules

* Status: accepted
* Deciders: Dean Kellham, [Redacted]...
* Date: 2026-02-15

Technical Story: Putting [Company Q]'s web application into maintenance mode previously required developers to modify application code, merge changes, and trigger a CI/CD pipeline deployment. This caused unnecessary delays during urgent incidents and wasted valuable engineering effort on infrastructure-level routing.

## Context and Problem Statement

We need a rapid, infrastructure-level toggle to display a static "Maintenance Mode" page during planned downtime or unexpected outages. The solution must decouple this routing logic from the application code, require zero CI/CD pipeline runs to activate, and operate at the edge to prevent unnecessary traffic from reaching the compute tier.

## Decision Drivers

* Operational Agility - reducing the time it takes to toggle maintenance mode from ~30 minutes (code deployment) to < 5 seconds.
* Decoupling - separating infrastructure routing responsibilities from software developer workflows.
* Cost & Efficiency - stopping traffic at the load balancer prevents the compute tier from processing requests during an outage or maintenance window.
* Simplicity - leveraging existing infrastructure rather than introducing new services.

## Considered Options

* Application-level routing (Status Quo). Rejected due to reliance on CI/CD pipelines, developer intervention, and inability to handle underlying compute failures.
* Route53 DNS failover to a static S3 website. Rejected because DNS propagation delays (TTL) mean the toggle is not instantaneous, leading to a poor user experience.
* AWS Application Load Balancer (ALB) Fixed Response Listener Rules.

## Decision Outcome

Chosen option: **AWS Application Load Balancer (ALB) Fixed Response Listener Rules**. 
We configured a custom listener rule on the existing ALB containing the HTML payload for the maintenance page. By default, this rule sits at a low priority (e.g., position 99). To activate maintenance mode, an administrator simply changes the rule's priority to position 1, instantly intercepting all traffic before it reaches the target groups.

### Architecture Diagram

```mermaid
graph TD
    User((End User)) --> R53[Route 53 DNS]
    R53 --> ALB[Application Load Balancer]
    
    ALB --> |Evaluates Listener Rules| Rules{Rule Priority}
    
    Rules -->|Priority 1: Active| Maint[Fixed Response: 503 Maintenance Page]
    Rules -->|Priority 99: Default| App[Target Group: EC2 / ECS Compute]
    
    style Maint fill:#f9d0c4,stroke:#e05252
    style App fill:#d4edda,stroke:#28a745
````

### Positive Consequences

* Agility: Toggling maintenance mode is now instantaneous and can be done via the AWS Console or a simple CLI script.
* Cost: Incurs zero additional AWS charges, as the ALB is already provisioned and fixed responses are included in standard ALB pricing.
* Efficiency: Completely removes the development team from routine infrastructure maintenance tasks.
* Reliability: The maintenance page will serve successfully even if the underlying EC2/ECS compute tier is completely offline.

### Negative Consequences

* The HTML payload is stored within the ALB rule, which has character limits. The maintenance page must be kept lightweight (inline CSS/minimal JS).