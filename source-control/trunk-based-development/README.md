### Trunk Based Development

Refs:
[https://trunkbaseddevelopment.com/](https://trunkbaseddevelopment.com/)

#### Summary

A source-control branching model, where developers collaborate on code in a single branch called "trunk" (master or main),
resist any pressure to create other long-lived development branches by employing documented techniques. They
therefore avoid merge hell, do not break the build.

Very small teams can commit direct to the trunk. 
At scale is best done with short-lived feature branches (max couple of days)

#### Branch by abstraction technique
Branch by abstraction is a technique for "longer to complete" changes in the trunk (e.g. 5 days to complete)

##### Rules
1. there are also a lot of developers already depending on the code that is subject to the longer to complete change, and 
we don not want them to be slowed down
2. No commit to shared repository should jeopardize the ability to go live

#### Ideal steps
1. Introduce an abstraction around the code that is to be replaced, and commit that for all to see. This can take
multiple commits. 
2. Write a second implementation of the abstraction for the to-be-introduced code, and commit that, but maybe 
"turned off" within the trunk so that other developers do not depend on it yet. The abstraction from #1 may also
be occasionally tweaked, but must follow the same rule - do not break the build.
3. Flip the software "off" switch to "on" for the rest of the team, and commit that.
4. Remove the to-be-replaced implementation.
5. Remove the abstraction.
