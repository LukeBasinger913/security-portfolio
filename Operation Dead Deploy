# [Operation Dead Deploy: "Investigating a Rogue Test Environment"]

## Scenario
A junior intern was granted access to create a test environment without knowledge of the company's governance standards. They deployed the environment and then abandoned it. I assessed damage, 
identified the governance failure and documented the evidence. 

The resource was deployed improperly. Governance flagged it as non-compliant but did not prevent its creation, indicating a gap in the policy configuration.

## Environment
live multi-user Azure training tenant with Reader access.

## Investigation
Stage 1: Locating the offender
I reviewed the resource group and found a resource that did not follow the required naming convention. This is pattern recognition at scale, and it surfaces anomalies in environments too large to review line by line.
Stage 2: Inspect the payload
I read the resource's tags, which show ownership, cost, and lifecycle information.
Stage 3: Trace the deployment
Azure records who deployed each resource, when, and with what parameters. This provides non-repudiation. I compared that data to the alert timestamps.
Stage 4: Why didn't policy stop this?
A naming convention policy was in place, but its effect was set to Audit. The violation was logged but not blocked. To prevent this in the future, the effect should be changed to Deny, which blocks the creation of any resource. 
That doesn't meet the standard.

## What broke / what surprised me
I needed time to get used to how granular Azure's scopes are. I would think I was viewing a resource's tags, but I was actually viewing the tags on the resource group or subscription. Once I got my bearings, 
Navigation made much more sense.

## Findings and recommendations
Starting the naming policy in Audit mode was reasonable because it avoided disrupting existing workflows. However, the Audit should be a temporary phase. I recommend setting a timeline for moving the policy to Deny so all 
future resources meet the standard. Deployments and policy rollouts should follow that same schedule.

## What I learned
- Azure policy effects matter. Audit only reports non-compliance, while Deny enforces compliance
- Tags and deployment history show who created a resource, when, and why, which makes accountability possible.
- Settings can exist at the resource, resource group, or subscription level, so always check which scope you're reviewing.
- What I'd Do differently: Confirm my scope before reading tags or settings, and work from a checklist to avoid mixing up levels.
- Overall: This was my first time working in a fully configured Azure environment, and it gave me hands-on experience with governance and investigation. 
