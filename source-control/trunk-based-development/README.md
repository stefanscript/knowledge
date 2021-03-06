# Trunk Based Development

Refs:
[https://trunkbaseddevelopment.com/](https://trunkbaseddevelopment.com/)

## Summary

A source-control branching model, where developers collaborate on code in a single branch called "trunk" (master or main),
resist any pressure to create other long-lived development branches by employing documented techniques. They
therefore avoid merge hell, do not break the build.

Very small teams can commit direct to the trunk. 
At scale is best done with short-lived feature branches (max couple of days)

## Branch by abstraction technique
Branch by abstraction is a technique for "longer to complete" changes in the trunk (e.g. 5 days to complete)

##### Rules
1. there are also a lot of developers already depending on the code that is subject to the longer to complete change, and 
we don not want them to be slowed down
2. No commit to shared repository should jeopardize the ability to go live

#### Ideal steps (let us say there is code that is 'to be replaced', code 'to be introduced'.)
1. Introduce an abstraction around the code that is to be replaced, and commit that for all to see. This can take
multiple commits. 
2. Write a second implementation of the abstraction for the to-be-introduced code, and commit that, but maybe 
"turned off" within the trunk so that other developers do not depend on it yet. The abstraction from #1 may also
be occasionally tweaked, but must follow the same rule - do not break the build.
3. Flip the software "off" switch to "on" for the rest of the team, and commit that.
4. Remove the to-be-replaced implementation.
5. Remove the abstraction.


## Feature Flags

Feature Flags allow to control the capabilities of a application in a decisive way. 
They are meant to be short lived.

There are many ways to passing feature flag intentions at runtime:

    if args.contains("--withOneClickPurchase") {
      purchasingCompleting = new OneClickPurchasing();
    }
    
or config

    bootContainer.addComponent(classFromName(config.get("purchasingCompleting")));

You want to avoid if/else conditions in the code where a path choice would be 
made. Hence the emphasis on an abstraction.

#### CI pipelines
Ideally all permutation are ran and tested in parallel.

#### Runtime switchable
Sometimes setting flags at launch time is not enough. Runtime flags need to be persistent, a restart 
of the app should not fallback to defaults.

#### Build flags
Affect the application as it is being build.

#### A/B testing and betas
Pushing code that's turned off into production, allows you to turn it on for ephemeral reasons - you
 want a subset of users to knowingly or unknowingly try it out. A/B testing (driven by marketing) is 
 possible with runtime flags. So is having beta versions of functionality/features available to groups.

#### Tech Debt - pitfall
Flags get put into applications but get forgotten, when they should be cleaned up after a while. The is also 
the fact that the app works just fine with the flags in place, the business only cares about the next priorities/features. 


## Branch for releases

- Created from trunk (master) just before deployment (just in time basis)
- Should not receive continued development work
- Can receive cherry picked merges from trunk
- Continuous Delivery teams (high output) release from trunk, 
if fixes are required they are pushed from trunk (they choose a roll-forward strategy for solving it);
 they don't release from release branches,
 
#### Late creation of release branches
Some teams release from a tag on the trunk and do not create a branch at that time. 
Branches can be created retroactively (with effect from a date in the past).

#### Fix production bugs on Trunk
The best practice for trunk based development is to reproduce the bug on the trunk, write a test and fix it,
have it verified on the CI server, cherry pick that to the release branch have the CI server verity that too.
Note: a cherry pick merge is not a regular one.
##### Cherry-picks from the trunk to branch ONLY
Bugs should be fixed on trunk and cherry picked to release branches. They should not be fixed on release branches.
Why? Because you might forget to push it back to trunk. Special cases where the bug can't be replicated on trunk
can occur so fixes on release branches can be done but steps must be taken to ensure the branch is re-merged into trunk.

#### Release branches deletion
Release branches are deleted some time after release activity from them ceases. Not straight away but some time after 
release.
