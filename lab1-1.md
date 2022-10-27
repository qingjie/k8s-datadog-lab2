
Progressive Delivery is a term that was term that was coined in 2018 by James Governor from Redmonk, talking with Adam Zimman from LaunchDarkly. They were trying to have a term to convey a set of delivery techniques that were getting popular.

Progressive Delivery includes delivery techniques like canary deployments, feature flags or A/B testing.

![]()

In canary deployments, a new feature gets deployed first to a subset of customers, and after gathering telemetry, it gets deployed to more and more users if the telemetry is positive, or gets rolled back, if telemetry alerts us of possible problems.

Feature flags is a technique in which a new feature is only available to a set of users, for early testing, or for billing purposes.

In A/B testing, two versions of the same feature are released at the same time to experiment which one will perform better, based on a specific criteria.

In all those cases, having a good observability strategy is key to implement Progressive Delivery successfully: if we are unable to gather relevant metrics for our goals, it would be impossible to decide whether a release is successful (and we can continue delivering to more users in the case of canaries), or not.
