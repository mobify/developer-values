```
               `:-.
              -yyyyys+:`
             /yyyyyyyyy`  +o+/:-.
           `oyyyyyyyyy-  :hhhhhhhs
          `syyyyyyyyy+   yhhhhhhhy
      `-/oyyyyyyyyyyo   :hhhhhhhhs
   -/oyyyyyyyyyyyyyo`   shhhhhhhhs
 +yyyyyyyyyyyyyyyy+    `hhhhhhhhho
 +yyyyyyyyyyyyyy+.     .hhhhhhhhho
 `yyyyyyyyys+/.         yhhhhhhhhhs`
  -yso+/-.`             .yhhhhhhhhhy.
          ```.....`      `shhhhhhhhhy.
    -://++++++++++++/-`    /yhhhhhhhhy.
    /++++++++++++++++++/.   `ohhhhhhy+`
    :++++++++++++++++++++/-`  -shhs:`
    `+++++++++++++++++++++++-`  -`
     `......-...-/+++++++++++/`
                  `-/+++++++:`
                     `.:/+:`
```

# Mobify Developer Values

## What is the purpose of this document?

Why do we build software? Ultimately, it's to provide value to people.
Sometimes, it can be hard to justify certain approaches to building software.
The purpose of this document is to relate the "how" to build software to the
"why" by relating our processes to our company values.

The Developer Values are a living document. Everyone can contribute and as
our company and culture evolve, so should this document.

### This document will be helpful for:

- Code reviews. Our culture spreads via reviews and this document should
  help us conduct them consistently.
    - [Here is a useful page that explains what the purpose of a code review is](https://mobify.atlassian.net/wiki/pages/viewpage.action?pageId=50266690#OurSoftwareDesign&DevelopmentProcess-CodeReviews)
    - [Here is a great article on the importance of code review](http://glen.nu/ramblings/oncodereview.php)
- Onboarding.
- Guiding discussions about the best way to implement. That is, the proposed
  approach should match the values.
- Helping with career growth.

### What the document is not:

- A set of rules. This is a guidebook, not strict set of rules that must be
  obeyed at all costs. For a great video on why to avoid blindly following
  rules, checkout [Beyond PEP8](https://www.youtube.com/watch?v=wf-BqAjZb8M).
- Permanent. This is a living document that is always welcome to pull requests.

## A Developer's Perspective on Mobify's Core Values

### Customers First

#### [Write tests](http://stackoverflow.com/questions/67299/is-unit-testing-worth-the-effort).

Testing speeds up development by reducing the danger of future change.

Testing leads to better code. *Nothing refactors a giant method better than
trying to write a test for it!*

Testing gives us the confidence to experiment and deploy to production. This
is especially important with complex code like [`mobify/capturejs`](https://github.com/mobify/capturejs).
A strong [test suite](https://github.com/mobify/capturejs/blob/master/tests/capture-tests.js)
let's us make improvements without worrying about breaking edgecases.

Favour writting tests when:
* You do something silly. Write tests to avoid doing it again.
* We discover a regression. Write tests to make sure we don't do it again.
* You're working on something that cannot break. Eg. our login form.
  Write tests to make sure no one ever breaks that!

[Be pragmatic about where you're testing to get the highest return](http://david.heinemeierhansson.com/2014/tdd-is-dead-long-live-testing.html).

#### Use staging / testing environments.
- We should always test in an environment as close to production as possible before going live – this allows us to spot any bugs, and resolve them before we flip that switch and turn it on for everyone.

#### [Follow our best practices](https://mobify.atlassian.net/wiki/display/PLAT/Coding+and+Design+Best+Practices).

#### Fail Gracefully.
- Adaptive.js/mobify.js projects fail gracefully by reverting to the desktop site in the event of an exception or network error.
- If Web Push is down, the worst thing that happens is that you can't send or receive
  push notifications. It will not impact the critical flows of our customers sites.
- [Ensure failed analytics calls (caused by adblockers) don't cause main application
  business logic to fail](https://mobify.atlassian.net/wiki/display/PLAT/Best+Practices+to+avoid+content+being+blocked+by+ad+blockers).
- Occasionally, things are going to blow up. It's important to have appropriate fail-safes to allow us to resolve issues as quickly as possible. Some examples of that are:
    - Kill switches or [circuit breakers](http://martinfowler.com/bliki/CircuitBreaker.html).
    - Forced updates to websites/apps when certain changes being made are not
      backwards-compatible.
    - Being able to rollback quickly (for example, make sure microservices are served off
      a domain you control. [Not doing this has bit us in the past](https://github.com/mobify/btr-adaptivejs/blob/6ed7d4bb9137e81efa63bfc28eda3ac397a2445c/assets/js/ui/view-scripts/hybrid/fb.js#L7))
- When things do blow up, have a [post-mortem](https://codeascraft.com/2012/05/22/blameless-postmortems/). Post-mortems are our best way of evaluating what processes caused failure to happen, and what we can do to prevent it from happening again in the future. [Here is a list of post-mortems](https://mobify.atlassian.net/wiki/display/PLAT/Post-Mortems).

#### Build reliable services.
- We want to be able to comfortably sleep at night without worrying about services falling over. That means:
    - Setting up monitoring and alerting
    - Setting up failover databases/servers
    - Practicing failures through [Failure Fridays](https://mobify.atlassian.net/wiki/questions/82280579/answers/82280618)
    - Ensuring every major service has a [Holy Shit Handbook](https://mobify.atlassian.net/wiki/display/SYS/The+Holy+Shit+Handbook).

#### Build Minimum Viable Products (MVPs)
- When beginning a new feature with a high amount of ambiguity or uncertainty about whether it will really be a hit, think "What is the MVP for this" that is, what is the minimum amount of work we can do to deliver the value of this feature to the user.
- In other words: Don't gold plate before validating your idea.

#### Release early, release often
- The best way to debug software in production is by releasing it and identifying the bug right away, rather then waiting a month and then completely forgetting how things worked.
- Caveat: Release within reason. You can ship a backend feature multiple times a day, but you might not want to release 5 versions of Adaptive.js in a day. Use discretion.

#### A feature in the hands of our customers is worth more than 5 PRs.
- When working on a team, it can be easy to crank away on your own features. Resist the urge! It's more important to get some work merged and in the hands of users then it is to have a bunch of work piled up for review. [This article on code review](http://glen.nu/ramblings/oncodereview.php) explains it best.

#### Build Secure Software
- Do our best to ensure that Mobify does not add new attack vectors to our customer's sites.
- Follow [Mobify's software security policy](https://mobify.atlassian.net/wiki/questions/60817443/what-is-mobifys-software-security-policy).

### Invent

#### Don't be afraid to push the boundaries of technology, but [be conservative with your tech stack](http://mcfunley.com/choose-boring-technology).
- What this means is that the things you are building should be pushing boundaries, not the things you are building them with. [Here is a list of technology decisions we have evaluated in the past](https://mobify.atlassian.net/wiki/questions/77168927/what-should-i-consider-when-evaluating-a-new-service-feature-or-technology-what-criteria-do-we-use-in-our-decisions).


#### [Follow our best practices](https://mobify.atlassian.net/wiki/display/PLAT/Coding+and+Design+Best+Practices).
- for many things, we've already solved them.



#### Have an idea you want to pursue?
- Customer/Product Improvements:
    - Hop in the Product chat room or find a Product Manager to chat with.
    - Build it at [one of our various Hackathons](https://mobify.atlassian.net/wiki/display/PLAT/Hackathon).
    - [Design sprints](https://mobify.atlassian.net/wiki/questions/77169565/what-is-a-design-sprint-what-design-sprints-has-mobify-conducted-in-the-past-where-can-i-find-the-best-practices-around-running-a-design-sprint)
- Software Improvements - new patterns, libraries, frameworks, or services to improve existing products.
    - Reach out to your peers (Infrastructure Guild, Eng Meeting, Eng Room, Science Fair, Astro/Web Dev Sync)
- Self Improvements
    - If it’s an idea that aligns with your career growth plan (learn a new language, write a blog post, speak at a conference), be sure to ask your lead how they can support you in achieving your goals.

### Always Grow

#### Constantly strive to become a better developer.
- Always be learning.
    - Use your [education budget](https://mobify.atlassian.net/wiki/display/OPS/Education+Benefit). It's there for you to level up in areas that might be hard to level up at in your day to day work.
    - Constantly learn new languages, techniques, frameworks, methodologies, leadership skills, domain knowledge, etc. Doing it in a structured way (a course/tutorial, join or start a [Mobify Study Group](https://mobify.atlassian.net/wiki/display/MOB/Technical+Reading+Groups)) is preferred over reading endless Hacker News articles.
- Teach others and help them grow in their abilities.
    - Teach your co-workers. Good venues for this are [Science Fair or the Engineering Meeting](https://mobify.atlassian.net/wiki/display/DEV/Engineering+Home).
    - Teach the community - for example speak at meetups ([VanJS)](http://www.meetup.com/vancouver-javascript-developers/), [VanPy](http://www.meetup.com/vanpyz/), [Web Performance](http://www.meetup.com/Vancouver-Web-Performance/), etc) or write blog posts.
    - Transfer knowledge whenever possible. If someone encounters a problem it is better to guide them to a solution rather then solving it for them.
- [Code reviews](https://mobify.atlassian.net/wiki/questions/79527980/answers/81789067) and Pair Programming are excellent strategies for learning new tricks.
    - Ensure people with different skill levels and skill sets are reviewing your code, it's a great opportunity for cross-pollination.
    - Get your code reviewed by the CTO at our [Engineering Office Hours](https://docs.google.com/document/d/1fvL30nvx1Yr2i--dTyytExnrokwrBQlPmXX2ZM06ukU/edit).
    - As the person receiving feedback, strive to be as open to the feedback as possible. This will help maximize learning. (Note: that is not a license for reviewers to completely disregard the feelings of the person who wrote the code - we believe that relationships are more important than process or tools).

#### Be a software craftsman/craftswoman.
- Take pride in how you build the software and your craftsmanship regardless of how the product does in the market. This doesn't mean gold-plating everything, often you should act pragmatically. Shipping value to users is the most important thing, but make sure to take the time to reflect on what you build, and do a post mortem and always make sure you're not
repeating the mistakes of the past.
- Ensure you challenge designs that you see problems with instead of implementing them without questioning.

#### Reach out to domain experts.
- We value a collaborative development environment where we seek expertise from domain area experts. We have a wealth of expertise on the team with very talented folks - talk to them instead of making the mistake yourself! If you are unsure who to chat with, feel free to reach out to folks in the Engineering room on Slack, or reach out to your lead.

#### Be solutions focused
- Rather than thinking "Wow, I can name 20 things that are awful with this design", try to be solutions focused. "There are 20 improvements we could make to this! X is done this way, but it could be better if we made it more like Y". There are many reasons why a piece of software was built the way it was built, and harping on how it was built doesn't get us any closer to solving the problem at hand.

#### [Build and work on your career growth plan](https://docs.google.com/document/d/1P3XOEu6AYWph7hStaBybR1yIac5pexGChykZh_X9CGM/edit#)

### Simplify

#### [Keep it Simple, Silly (KISS)](https://en.wikipedia.org/wiki/KISS_principle)
- Simple is better than complex.

#### [You Ain't Gonna Need It (YAGNI)](http://martinfowler.com/bliki/Yagni.html)
- Don't build stuff until you need it.
- Design software for ease of extension and contraction. A great way to do this is to optimize for "[throwaway-ability](http://mcfunley.com/data-driven-products-now)".
    - e.g. make the new thing modular and self contained, and not require modifications to shared dependencies. Once it's clear things are going to stick, then think about refactoring things once it is clear that they are going to "stick".

#### Avoid re-inventing the wheel
- [Look for existing solutions](https://medium.com/@kuomarc/don-t-build-it-in-house-there-is-an-api-for-that-c929b8677137)  (libraries, snippets, services) before rolling your own. If they exist, someone at Mobify will likely know - reach out to the Engineering team early and often!
    - For services, checkout our [best practices](https://mobify.atlassian.net/wiki/display/SYS/Service+Best+Practices).
    - For front-end web apps, checkout our [best practices](https://mobify.atlassian.net/wiki/questions/85917798/what-are-our-best-practices-for-building-front-end-web-application).

### Communicate

#### Don't be a lonesome cowboy/cowgirl coder.
- Ask for feedback early and regularly. Embrace critique.
- Embrace feedback in the code review process.
- Use the [30/90% principle](https://42floors.com/blog/startups/thirty-percent-feedback) when giving feedback.
- Seek opportunities to work with others and learn from them. There are lots of smart colleagues around you :).

#### Readability counts.
- Code is written once but read often. There is a good chance someone will have to figure out what it does, mostly likely you, twelve months from now. Take care to write your code in such a way that your future self can iterate on new features and address bugs much faster.
- Follow the [Mobify Style Guide](https://github.com/mobify/mobify-code-style). It contains best practices, as well as linter tools for various commonly used languages - we highly recommend using those tools instead of hearing about code style issues in PR reviews! Please feel free to open up PRs against it - our style guide is an always-evolving document!
- Explicit is better than implicit.
- Your code should "fit” with the rest of the codebase. Use an idiomatic style that is understood by the rest of the team.
- Write comments!
    - Code that reads like pseudo code doesn't need comments, but complex logic does.
    - Comments explain what  the code is doing and why  it's doing it, but not usually how  it's doing it.
    - Comments shouldn't repeat what your code should already be saying. As long as you're being explicit with your variable naming, something like this is not necessary:

      ```
      // if we are running in an app, do "blah”
      if (isRunningInApp)
      ```

#### Write [Minimum Viable Documentation](https://mobify.atlassian.net/wiki/pages/viewpage.action?pageId=50266690#OurSoftwareDesign&DevelopmentProcess-MinimumViableDocumentation)
- All modules/libraries/plugins/etc. should have documentation that explains:
    - Setup
    - Usage
    - Deployment
    - Testing
    - Contributing
    - Roadmap/Changelog
- Good documentation enables others to get up and running without your involvement.
- Documentation should be updated as you write your software (or [even before you write it](http://tom.preston-werner.com/2010/08/23/readme-driven-development.html)))
- You should be able to answer the majority of questions from users with a link to a document.

#### Be in touch with the dev community
- Go to meetups and conferences and share what you've learned with the rest of the team.
- Write blog posts or speak at meetups and conferences.

#### Diversity and Collaboration

> Be excellent to each other... and... PARTY ON, DUDES! - [*Abraham Lincoln*](https://en.wikiquote.org/wiki/Bill_%26_Ted%27s_Excellent_Adventure)

We value diversity and collaboration. Our best work is done together, when all
voices are heard.

> * Be friendly and patient.
> * Be welcoming.
> * Be considerate.
> * Be respectful.
> * Be mindful of the words you choose.
> * When we disagree, try to understand why.
> – [*Django Code of Conduct*](https://www.djangoproject.com/conduct/)

To understand what we're trying to become, it may be useful to understand what
we're trying to avoid. See effects of [contempt](http://blog.aurynn.com/86/contempt-culture)
and [competition](https://medium.com/tech-diversity-files/if-you-think-women-in-tech-is-just-a-pipeline-problem-you-haven-t-been-paying-attention-cb7a2073b996#.yjrp4mqkb) on environments.

#### Favour experimentation over argument

#### Be excellent to each other!

### Be Entrepreneurial

#### Prototype
- Think we should do X? Build a prototype and convince people. Email discussions, Science Fair or the Engineering Meeting are excellent avenues for this.

#### Improve Process

The way we're doing things today is based on information we had in the past.

New people, tools and understanding changes the context in which the decision
was made.

The way we decided to do things last year, last month or even last week might
not be the best way to go forward today.

If you have idea for how to improve a process, work with your team/lead/peers to
make it happen!

#### Ownership
- For a service, app or site that goes live, no one is going to fix your production bug but you. At Mobify, we practice DevOps, meaning engineers are responsible for both building software, and making it operate live in production. There is no central Operations team for running/maintaining production code, although we do have a DevOps guild that gets together to discuss our different services.

### Build to Last

#### Build systems that are easy to maintain.
- Code is written once but read often, meaning more time is spent maintain software than there is in writing it.
- "Standardize how things are deployed" (for example, it's better to put a new service onto Heroku than to just run it on a physical machine in the office).
- Be consistent. The projects which are the easiest to work on are the ones that have a consistent code style and structure. It's problematic when the style across different parts of the codebase is completely different. To do this, refer to other parts of this document, as well as the [Mobify Code Style repo](https://github.com/mobify/mobify-code-style).

#### Don't repeat yourself (DRY)
- Extract common or shared functionality into utility functions, and if needed across multiple projects, extract into libraries or frameworks.
- Re-use the things you've built and avoid copying and pasting. For example we don't want duplicated functionality in our functions, classes, modules, systems. We also want to avoid duplication and share code across sites/apps/systems.

#### Scouts Rule

> Try and leave this world a little better than you found it. – [*Robert Baden-Powell*](https://en.wikipedia.org/wiki/Robert_Baden-Powell,_1st_Baron_Baden-Powell)

Continuously improve through iteration.

Can that function you touched be refactored? Can the doc strings of the module
you changed by updated? Are there inconsistencies in naming of files you're
editing?

Try and leave this code a little better than you found it.

*Be wary cleanup doesn't hide the intent of your change!*

#### Build testable and well tested software
- Test that the functionality you implemented works and fulfills the requirements. Also make sure that you didn't introduce regressions.
- Software should have basic unit tests and continuous integration tests.
- Make sure that any code that goes into production has been tested in a "real” environment, for example:
    - For JavaScript client libraries/frameworks, understand what devices are the most important for the code that you're writing. Once you have that understanding, test your code on these platforms with real devices. Using just Saucelabs or simulators is sometimes not enough.
    - For back-end code test on a staging environment that mirrors production very closely.

## Outro, the Zen of Mobify

* Be excellent to each other.
* Be concise.
* Avoid acronyms or jargon where words would do.
* Favour small diffs over big bangs.
* Why argue when you can experiment?
* Open by default.
* Small, empowered teams are unstoppable. Let's make more of those.
* New problems don't require new technology.
* Don't take this all too seriously.
