# Mobify Developer Values

## What is the purpose of this document?

Why do we build software? Ultimately, it's to provide value to people.
Sometimes, it can be hard to justify certain approaches to building software.
The purpose of this document is to relate the "how" to build software to the
"why" by relating our processes to our values.

Developer values are also never finished - just as we should look back on our
old code with shame, so should we with the Developer values.

### This document will be helpful for:

- Code reviews. Our culture spreads via reviews and this document should
  help us conduct them consistently.
    - [Here is a useful page that explains what the purpose of a code review is](https://mobify.atlassian.net/wiki/pages/viewpage.action?pageId=50266690#OurSoftwareDesign&DevelopmentProcess-CodeReviews)
    - [Here is a great article on the importance of code review](http://glen.nu/ramblings/oncodereview.php)
- Onboarding.
- Guiding discussions about the best way to implement. That is, the proposed
  approach should match the values, however technologically clever it might be.
- Helping with career growth.

### What the document is not:

- A set of rules. This is a guidebook, not strict set of rules that must be
  obeyed at all costs. For a great video on why to avoid blindly following
  rules, checkout [Beyond PEP8](https://www.youtube.com/watch?v=wf-BqAjZb8M).
- Permanent. Developer values are also never finished - just as we should look back on our old code with shame, so should we with the Developer values.

## A Developer's Perspective on Mobify's Core Values

### Customers First

- Build Reliable Products
    - [Write tests](http://stackoverflow.com/questions/67299/is-unit-testing-worth-the-effort).
        - Despite seeming like they slow down development, it's our experience that it speeds up overall
          development because it significantly reduces the danger of future changes, meaning we can
          ship future changes quicker and with greater confidence.
        - For example - [capture.js](https://github.com/mobify/capturejs)
          is a very complicated piece of code that needs a bug fix every
          once and awhile. With [tests](https://github.com/mobify/capturejs/blob/master/tests/capture-tests.js),
          we can quickly make changes and ship with confidence.
        - Tests also help us write better code. Nothing helps refactor a
          giant method better than writing a test for it!
    - Use staging / testing environments.
    - Follow Mobify's best practices for the type of product/feature you are creating. You can find these best practices [here](https://mobify.atlassian.net/wiki/display/PLAT/Coding+and+Design+Best+Practices).
    - Fail gracefully. Build systems with failure in mind. Ensure that failures don't break the customer's experience. This has served us well in the past:
        - Adaptive.js/mobify.js projects fail gracefully by reverting to the desktop site in the event of an exception or network error.
        - PRE fails gracefully if the back-end has problems, etc.
    - Occasionally, things are going to blow up. It's important to have appropriate fail-safes to allow us to resolve issues as quickly as possible. Some examples of that are:
        - Kill switches or [circuit breakers](https://www.google.com/url?q=http://martinfowler.com/bliki/CircuitBreaker.html&sa=D&usg=AFQjCNHQ2hZxw-qeoCGrYN1aRrKer0Q0hw).
        - Forced updates.
        - Being able to rollback quickly.
    - When things do blow up, have a [post-mortem](https://codeascraft.com/2012/05/22/blameless-postmortems/). Post-mortems are our best way of evaluating what processes caused failure to happen, and what we can do to prevent it from happening again in the future. [Here is a list of post-mortems](https://mobify.atlassian.net/wiki/display/PLAT/Post-Mortems).
    - We should build our services reliably. We want to be able to comfortably sleep at night without worrying about services falling over. That means setting up monitoring and alerting, failover databases/server, practicing failures through [Failure Fridays](https://mobify.atlassian.net/wiki/questions/82280579/answers/82280618), and ensuring every service has a [Holy Shit Handbook](https://mobify.atlassian.net/wiki/display/SYS/The+Holy+Shit+Handbook).
- Build Minimum Viable Products (MVPs)
    - When beginning a new feature with a high amount of ambiguity or uncertainty about whether it will really be a hit, think "What is the MVP for this" that is, what is the minimum amount of work we can do to deliver the value of this feature to the user.
    - In other words: Don't gold plate before validating your idea.
- Ship features in incremental chunks as soon as possible.
    - The best way to debug software in production is by releasing it and identifying the bug right away, rather then waiting a month and then completely forgetting how things worked.
    - Caveat: Release within reason. You can ship a backend feature multiple times a day, but you might not want to release 5 versions of Adaptive.js in a day. Use discretion.
- A feature in production is worth more than 5 PRs.
    - When working on a team, it can be easy to crank away on your own features. Resist the urge! It's more important to get some work merged and in the hands of users then it is to have a bunch of work piled up for review. [This article on code review](http://glen.nu/ramblings/oncodereview.php) explains it best.
- Build Secure Software
    - Do our best to ensure that Mobify does not add new attack vectors to our customer's sites.
    - Any public facing service/system you implement should follow Mobifys Best Practices. You can find these best practices [here](https://mobify.atlassian.net/wiki/display/PLAT/Coding+and+Design+Best+Practices).

### Invent

- Don't be afraid to push the boundaries of technology, but [be conservative with your tech stack](http://mcfunley.com/choose-boring-technology). What this means is that the things you are building should be pushing boundaries, not the things you are building them with. [Here is a list of technology decisions we have evaluated in the past](https://mobify.atlassian.net/wiki/questions/77168927/what-should-i-consider-when-evaluating-a-new-service-feature-or-technology-what-criteria-do-we-use-in-our-decisions).
- For ideas you want to pursue:
    - Customer Improvements - new products or services.
        - Hop in the Product chat room or find a Product Engineer
        - Hackathons are a great way to get progress on features.
        - [Design sprints](https://mobify.atlassian.net/wiki/questions/77169565/what-is-a-design-sprint-what-design-sprints-has-mobify-conducted-in-the-past-where-can-i-find-the-best-practices-around-running-a-design-sprint)
- Software Improvements - new patterns, libraries, frameworks, or services to improve existing products.
    - Reach out to your peers (Infrastructure Guild, Eng Meeting, Eng Room, Science Fair, Astro/Web Dev Sync)
- Self Improvements
    - If it's an idea that aligns with your career growth plan (learn a new language, write a blog post, speak at a conference), be sure to ask your lead how [they can support you in achieving your goals](https://docs.google.com/document/d/1P3XOEu6AYWph7hStaBybR1yIac5pexGChykZh_X9CGM/edit#heading=h.ihmua81v0tbp).

### Always Grow

- Constantly strive to become a better developer.
    - Always be learning.
        - Use your [education budget](https://mobify.atlassian.net/wiki/display/OPS/Education+Benefit). It's there for you to level up in areas that might be hard to level up at in your day to day work.
        - Constantly learn new languages, techniques, frameworks, methodologies, leadership skills, domain knowledge, etc. Doing it in a structured way (a course/tutorial) is preferred over reading endless Hacker News articles.
    - Teach others and help them grow in their abilities.
        - Teach your co-workers. Good venues for this are [Science Fair or the Engineering Meeting](https://mobify.atlassian.net/wiki/display/DEV/Engineering+Home).
        - Teach the community - for example speak at meetups or write blog posts.
    - [Code reviews](https://mobify.atlassian.net/wiki/questions/79527980/answers/81789067) are an excellent opportunity to learn new tricks.
        - As the person receiving feedback, strive to be as open to the feedback as possible. This will help maximize learning. (Note: that is not a license for reviewers to completely disregard the feelings of the person who wrote the code - we believe that relationships are more important than process or tools).
- Be a software craftsman. But also don't forget to be pragmatic.
    - Take pride in how you built the software and your craftsmanship regardless of how the product does in the market. This doesn't mean gold-plating everything, often you should act pragmatically. Shipping value to users is the most important thing. But, make sure to take the time to reflect on what you build, do a post mortem and always make sure you're not repeating the mistakes of the past.
- Reach out to domain experts.
    - We value a collaborative development environment where we seek expertise from domain area experts. We have a wealth of expertise on the team with very talented folks - talk to them instead of making the mistake yourself! If you are unsure who to chat with, feel free to reach out to folks in the Engineering room on HipChat, or reach out to your lead.
- Be solutions focused
    - Rather than thinking "Wow, I can name 20 things that are awful with this design", try to be solutions focused. "There are 20 improvements we could make to this! X is done this way, but it could be better if we made it more like Y". There are many reasons why a piece of software was built the way it was built, and harping on how it was built doesn't get us any closer to solving the problem at hand.

### Simplify

- [Keep it Simple, Silly (KISS)](https://en.wikipedia.org/wiki/KISS_principle)
    - Simple is better than complex.
- [You Ain't Gonna Need It (YAGNI)](http://martinfowler.com/bliki/Yagni.html)
    - Don't build stuff until you need it.
    - Design software for ease of extension and contraction. A great way to do this is to optimize for "[throwaway-ability](http://mcfunley.com/data-driven-products-now)".
        - e.g. make the new thing modular and self contained, and not require modifications to shared dependencies. Once it's clear things are going to stick, then think about refactoring things once it is clear that they are going to "stick".
- Avoid re-inventing the wheel
    - [Look for existing solutions](https://medium.com/@kuomarc/don-t-build-it-in-house-there-is-an-api-for-that-c929b8677137)  (libraries, snippets, services) before rolling your own. If they exist, someone at Mobify will likely know - reach out to the Engineering team early and often!
        - For services, checkout our [best practices](https://mobify.atlassian.net/wiki/display/SYS/Service+Best+Practices).
        - For front-end web apps, checkout our [best practices](https://mobify.atlassian.net/wiki/questions/85917798/what-are-our-best-practices-for-building-front-end-web-application).

### Communicate

- Don't be a lonesome cowboy/cowgirl coder.
    - Ask for feedback early and regularly. Embrace critique.
    - Embrace feedback in the code review process.
    - Use the [30/90% principle](https://42floors.com/blog/startups/thirty-percent-feedback) when giving feedback.
    - Seek opportunities to work with others and learn from them. There are lots of smart colleagues around you :).
- Readability counts.
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

- Write [Minimum Viable Documentation](https://mobify.atlassian.net/wiki/pages/viewpage.action?pageId=50266690#OurSoftwareDesign&DevelopmentProcess-MinimumViableDocumentation) ("MVD”). It's important to have minimal viable documentation for every module/library/plugin/product/etc that you create. It should probably be the [README](https://github.com/mobify/split-test/blob/master/README.md) of the project.
- Be in touch with the dev community
    - Go to meetups and conferences and share what you've learned with the rest of the team.
    - Write blog posts or speak at meetups and conferences.
- Collaborate, don't compete
    - We have a very collaborative culture. There are a number of reasons why this is preferable:
        - [Competitive cultures tend to not bode well for creating diverse teams.](https://medium.com/@racheltho/if-you-think-women-in-tech-is-just-a-pipeline-problem-you-haven-t-been-paying-attention-cb7a2073b996#c63a).
- Favour experimentation over argument

### Be Entrepreneurial

- Think we should do X? Build a prototype/come with code and convince people it's a good idea. Email discussions, Science Fair or the Engineering Meeting are excellent avenues for this.
- Be proud of what you are building. If for example, you realize that a particular design is not going to be possible to do in a performant way, do not simply build it anyways because that's what design wants. It's your job to communicate that the design will need to change in order to keep the quality bar high.
- Ownership.
    - For a service, app or site that goes live, no one is going to fix your production bug but you. At Mobify, we practice DevOps, meaning engineers are responsible for both building software, and making it operate live in production. There is no central Operations team for running/maintaining production code, although we do have a DevOps guild that gets together to discuss our different services.

### Build to Last

- Build systems that are easy to maintain.
    - Code is written once but read often, meaning more time is spent maintain software than there is in writing it.
    - "Standardize how things are deployed" (for example, it's better to put a new service onto Heroku than to just run it on a physical machine in the office).
    - Be consistent. The projects which are the easiest to work on are the ones that have a consistent code style and structure. It's problematic when certain parts of the codebase have obviously been written by two or more people. To do this, refer both to this document, as well as the [Mobify Code Style repo](https://github.com/mobify/mobify-code-style).
- Don't repeat yourself (DRY)
    - Extract common or shared functionality into utility functions, and if needed across multiple projects, extract into libraries or frameworks.
    - Re-use the things you've built and avoid copying and pasting. For example we don't want duplicated functionality in our functions, classes, modules, systems. We also want to avoid duplication and share code across sites/apps/systems.
- The Boy Scouts Rule
    - Leave the campground better than you've found it.  Always check a module in cleaner than you found it.
    - Try to improve code quality every time you work on a project.
    - Fix formatting, spelling, do small refactorings…  But do this in moderation - if it's too hard to actually see the meat of the changes, you should probably move your cleanup changes to a separate branch.
    - Continuous improvement through iteration: Improve the code base slowly but surely.
- Build testable and well tested software
    - Test that the functionality you implemented works and fulfills the requirements. Also make sure that you didn't introduce regressions.
    - Software should have basic unit tests and continuous integration tests.
    - Make sure that any code that goes into production has been tested in a "real” environment, for example:
        - For JavaScript client libraries/frameworks, understand what devices are the most important for the code that you're writing. Once you have that understanding, test your code on these platforms with real devices. Using just Saucelabs or simulators is sometimes not enough.
        - For back-end code test on a staging environment that mirrors production very closely.
