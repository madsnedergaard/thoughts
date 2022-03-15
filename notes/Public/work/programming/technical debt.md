# Technical Debt
_aka tech debt_

A concept that reflects the implied cost of additional rework caused by choosing an easy solution now instead of using a better approach that would take longer
Aka.: **Code or data that future developers will pay a cost for.**


## Symptoms

> difficulties adapting to changing requirements, a slowdown in delivery of new features, and decreased job satisfaction for software developers.



## How to fix it

> Addressing technical debt can easily become a people problem more than a technology problem - which might be at the heart of why many teams struggle with it.

- [[slack week]] (also called engineering week)

## Approach
A “framework” or metrics for considering if adding new tech debt is okay:
(I can’t remember the source)

1. Impact
> Hvor stor påvirkning har denne tech debt? Både i forhold til problemer for end-users og i forhold til udvikler.
> Ex: bugs, manglende features, langsommere udvikling, kræver mere implicit forståelse af systemet

2. Fix Cost
> The second axis has to do with the cost to fix the tech debt. If we decide to fix an issue in our code or data, it will require someone’s measurable time to fix. If it’s a deeply rooted assumption that affects every line of code in the game, it may take weeks or months of engineering time. If it’s a dumb error in a single function, it may be fixable in a matter of minutes. Regardless of the time to implement a fix, though, we also must consider the risk of actually deploying that fix - how much code does it affect? Is everything based on a bug or weird return value?

3. Contagiousness
> The third axis is something I’ve become obsessed with: contagion. If this tech debt is allowed to continue to exist, how much will it spread? That spreading can result from other systems interfacing with the afflicted system, from copy-pasting data built on top of the system, or from influencing the way other engineers will choose to implement new features.




### Related reading
- https://peka.la/pieces/finding-time-for-tech-debt-installments