Every so often I go back and read




When doing tech support, I tried to read everything I could about approaching problems. [Joel Spolsky](http://www.joelonsoftware.com/articles/customerservice.html) is awesome as always. He reminds us you can fix problems two ways:

1. Superficial immediate solution, also known as a bandaid solution. Call centers and outsourced support with little communication to devs.

2. Solving longterm but going in depth into the problem, analyzing it to prevent it from happening again. As Joel says, this means you're left with only the really odd bugs, whcih is fine because they are rare and you can afford them with little added resource.

This is incredibly great of course. However, as a dev I've helped fix those odd bugs, and it's a nightmare that usually leads down a few nasty roads. Deep bugs nestling in the edge cases of hash functions. Compilers that break when a bit flips every so often. A slave database that copies stale data only 1/10000000 of the time. Or even... Caching bugs.

There is a secret third way to fix problems which is infinitely unbelievable and much much harder to do. I've only encountered it a few times, but it's so amazing it brings new light to what tech support actually means.

3. Restructure the problem, get rid of the service.

Throw it away. Be it a feature or process, just try to get rid of it. If there are pain points in the system, then what if they didn't exist in the first place?




Of course change on this size is very difficult (not just the users, but the makers, the managers, etc.). It's almost a paradigm shift. There will be a few things you'll need to do:

1. Gather the data on when these problems happen, how dangerous or rough is the problem, how many people are using this feature, etc.
2. How many people use this part of the system?
3. Alternatives
4. Challenge the business rules, do we really need this? What if our partners used this?

If these things sound like huge things, they are actually part of a tech support person's job. To help push change to product for the better through communication and users' experiences.

Support agents, specifically tech support people, understand better than anyone how the system works and where their pain points are.

There are of course some preconditions to this working:

Backing it all up with real data.
Having the flexibility to work to changing/simplifying the feature.
Working towards simplifying teh feature is always better. Less people have to look at it, it's easier to debug.



e.g. We had a localization product called String-thing.

We built String to help people localize technical content

While focusing on otehr aspects of ______, we support string-thing people

Working on other parts of the site, that's a pain

We removed String-thing for many reasons

-=(Poof)=- All problems and issues are gone!

Summary: It's really important to push product changes. As a tech support engineer you have access to user opinions and code, so you can make an educated decision back up with user data. This saves everyone time in the long run.



