# CQ-0001: Right-sizing Production RDS Instance for Cost Optimisation

* Status: accepted
* Deciders: Dean Kellham, [Redacted]...
* Date: 2026-02-13

Technical Story: The [Application] Production Database (MariaDB) was historically scaled up to a db.m5.8xlarge in response to performance issues. Following a root-cause analysis and application remediation, the instance was left over-provisioned, running at a high annual cost of ~$61,800 with average CPU utilization below 5%.

## Context and Problem Statement

We need to reduce the significant cloud spend for the [Company Q] environment without compromising the performance or stability of the critical [Application] application.

## Decision Drivers

* Cost - reduce wasted spend on idle compute and memory.
* Stability - ensure new instance can ahndle peak loads without excessive temporary tables created to disk.
* Modernization - leverage newer AWS hardware generations for better price-performance ratios.

## Considered Options

* Retain db.m5.8xlarge - zero risk but no cost reduction.
* Downsize to db.m5.4xlarge - stay within the same instance family while reducing costs by ~47%. Does not leverage newer hardware.
* Downsize to db.m7i.4xlarge - downsize and migrate to newest Intel-based AWS instance types. Deliver similar cost saving of ~47% but also achieve better performance, with higher IOPS and network throughput.

## Decision Outcome

Chosen Option: "Migration to db.m7i.4xlarge", because the m7i family offers superior performance compared to the m5 family. By moving to a 4xlarge in the 7th generation, we effectively halved the provisioned resources while maintaining a "performance buffer" that resulted in only ~11% peak CPU utilization.

### Positive Consequences

* Financial - immediate reduction in annual spend of $29,000 (~47%).
* Financial - opens up future savings options via RDS Savings Plans on gen 7.
* Performance Gains - higher IOPS offered by gen 7 instances reduces the impact of temp tables to disk that do still occur.

### Negative Consequences

* 30 minute maintenance window for modification.
* Reduction of Headroom - "emergency" overhead is reduced, however mitigated with sensible CloudWatch alarms.