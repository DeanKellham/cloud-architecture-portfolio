# IN-0001: Deploy \[RMM\] "Device Location Update" Script to AWS using Lambda and S3

* Status: accepted
* Deciders: Dean Kellham, \[Redacted\]
* Date: 2026-02-27

Technical Story: \[Company\] have been historically bad with updating us when devices move site. With the migration from \[Old RMM\] to NinjaOne, we were interested in a feature that could automatically assign \[Company\] devices to the correct location based on their subnet / public IP. This is achievable using a small PowerShell / Python script that runs on a schedule, and leverages the NinjaOne API.

## Context and Problem Statement

We need somewhere to host a small PowerShell / Python script that can be run on a schedule. this script needs to pull data from a CSV table.

## Decision Drivers

* Maintainability - how easy is it to update as new sites are added?
* Cost - can we leverage infrastructure already deployed?
* Speed of deployment

## Considered Options

* On-Premises using existing Windows Servers. PowerShell & Task Scheduler.
* AWS using Lambda function, S3, and EventBridge Scheduler.
* AWS ECS using Containerised application and S3.

## Decision Outcome

Chosen option: "AWS using Lambda function, S3, and EventBridge Scheduler", because Lambda is perfectly suited for the <1 minute runtime of this simple script, the solution removes any reliance on our on-premises infrastructure (that we'd like to move away from), and the small footprint keeps this solution within Lambda's free tier.

### Positive Consequences

* Additional AWS exposure for colleagues
* Reliable scheduling of task
* No underlying server downtime or maintenance
* NinjaOne Devices update Location to match real-world location
* Monitorable via CloudWatch if required

### Negative Consequences

* Potential small cost associated with tiny S3 Bucket (<$1 per month) and EventBridge Schedule (<$1 per month)
* Maintaining list of site IPs in CSV - SOPs to be updated to update list in S3

## Links

* [Example Script](https://github.com/TawTek/MSP-Automation/blob/main/NinjaOne/Move-DeviceLocationPublicIP.ps1)
* ![HLD](assets/IN-0001-ninjaone-device-location-update-script.png)
