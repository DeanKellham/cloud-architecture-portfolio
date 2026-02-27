# CN-0001: Decouple Monolith Application into Separate Scalable Tiers, Leveraging AWS-Native Tools

* Status: proposed
* Deciders: Dean Kellham
* Date: 2026-02-20

Technical Story: \[Company N\] have engaged third-party developers to build a bespoke property title case management system, allowing them to refine their business beyond what off-the-shelf tools allow. The developers have built a 3-tier Web application on a single EC2 server, acting largely autonomously. \[Company N\] have requested a full architecture and security review to confirm the application and environment are ready for the upcoming application go-live.

## Context and Problem Statement

We need to review existing environment and recommend the most appropriate solution to leverage AWS-native tools and provide application resilience and scalability.

This decision is visualized in the High-Level Design (HLD) found in Appendix B of the February 2026 Architecture Review.

## Decision Drivers

* Security - ensure the application and environment are secure and ready for production.
* Governance - ensure data complies with best practices around encryption both in transit and at rest.
* Reliability - ensure the application can scale to meet demand, and recover from failure seamlessly.

## Considered Options

* Retain existing monolith EC2 deployment, including its limitations regarding reliability and scalability.
* Refactor the Web and API tiers to containers on AWS Fargate. Migrate the MS SQL database to AWS RDS for SQL. Migrate blob storage from Azure Blob to S3. Employ Amazon CloudWatch and AWS CloudTrail for monitoring and auditing.

## Decision Outcome

Chosen option: "Refactor to AWS-native solutions", because this approach would allow automatic scaling of Web and API tiers independently, while leveraging optimised tools for the database. Using Fargate and RDS would remove the need to maintain underlying compute resources. Leveraging S3 for blob storage over Azure would allow data to avoid having to traverse the public internet.

### Positive Consequences

* Ability to scale and recover Web and API tiers independently.
* Ability to host database on optimised solution, with options for multi-AZ clustering.
* No need to maintain underlying compute resources.
* No need for sensitive data to further traverse the public internet beyond the client and application session.
* CloudWatch and CloudTrail logging to allow alerting on key events.
* Elastic Load Balancer able to drop unnecessary requests before passing load on to target compute resources, and can scale with demand.

### Negative Consequences

* Cost increases while concurrent users is still small. Would need to determine critical threshold whereby cost of operation would reduce under decoupled approach vs single monolith.
* Adds complexity, which may hinder developer's immediate ability to maintain codebase at first - CI/CD pipeline would need to be developed.