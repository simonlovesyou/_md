[[ReadItLater]] [[Article]]

# [The Art of Code Review](https://kettanaito.com/blog/the-art-of-code-review)

## Introduction

Hi! My name is Artem, and I am a software engineer who spent the last 2,5 years developing a multi-country e-commerce solution with millions of euro of annual revenue. During that journey I had a chance to work with more than 15 front-end engineers of different seniority level, teaching them what I knew and learning from them what I didn’t. Today I would like to share my experience being a code reviewer, and give you some pieces of advice to become a good one.

I have been known for my notorious code reviews within the team, which some people hated, and others hated even more. In the end, it’s a joy to see the people who despised my reviews coming back and thanking me for a great time we both spent improving. Undoubtedly, my reviewing skills have a long way to go, but the positive feedback I’ve received over time motivated me to write this article. I would like to explore what made people love and hate my reviews, and how you can learn from that to become a better reviewer in your team.

---

## Code review is a part of development

I will start from assuring you that a code review by no means bears a lesser priority in your work than actual coding. I would argue that it’s even more important, since it’s one of the most useful feedback loops you can get for free. A flaw in the logic discovered at the review phase can save unnecessary stress for you and wasted money for your customer.

![Image of a man behind computers](https://kettanaito.com/blog/the-art-of-code-review/man-computer-TL4PR3KX.svg)

Understanding an importance of a code review as a part of your job is great, but make sure the other team members are on the same page with you. That doesn’t concern developers only, but project managers, scrum masters, product owners, and, most importantly, clients.

Code review is not a voluntary activity, but a righteous duty that must be accounted, respected, and paid.

Don’t be afraid to dive deeper into the code you’re reviewing, open a source code and browse through the related files to understand the nature of the changes better. With more pull requests behind your back, you will be able to perform that much faster, thus, delivering a profound in-depth feature analyzis. On the contrary, neglecting things in a review may backfire into much more work that it would’ve taken to get your head around the changes.

Here are a few arguments I find useful when explaining how code review contributes to a product:

-   It ensures quality of the code, thus, quality of a product;
-   It reduces the amount of technical debt in the future, making the maintenance cost lower;
-   It provides knowledge sharing between developers, resulting into more effective work, and eliminating the bus factor.

---

## Polite reviewer, sensible issuer

Be polite in your code reviews. We are all humans doing our job and we strive to do it the best we can. While this sounds obvious, you may find a lot about your colleague if you ask them for a code review at 5PM on Friday before their long-awaited vacation.

![Image of a woman and a man pair programming](https://kettanaito.com/blog/the-art-of-code-review/pair-programming-J32AE7GR.svg)

One of the hardest parts of giving a code review is when your suggestions are taken as a personal offense. It’s understandable that nobody likes to spend a week on a feature and hear that they need to redo everything. That hurts for both the issuer and the reviewer. **Let’s not do that**.

In my practice such situations happen for two reasons, which I'm going to describe below.

### Reason #1: Bad start

This often happens to people who rush into development without properly thinking the changes through. I am strongly convinced that a day of thinking saves a week of work.

Don’t be afraid to ask and discuss! It either confirms your approach, or saves a week of work in a wrong direction.

While this is feasible in a team, those who work alone may struggle to get their ideas evaluated. Bear in mind that there are plenty of people who can help you. You are not alone.

**Here are the links to some of my favorite engineering communities:**

-   [Reactiflux](https://discord.gg/yNcseDS)
-   [Nodeiflux](https://discord.gg/y5ksVAS)

### Reason #2: The way you say it

There is a fine line between “it's aweful, redo it” and a meaningful explanation of why there is a better way to do it. Remember that a reviewer’s role is to act as a fresh pair of eyes. Trying to understand the changes, and showing compassion when something needs to be reworked, are the keys to maintaining healthy working relationship between the issuer and the reviewer.

Code review is a conversation, not a queue of commands.

It’s a good gesture to include technical explanations and links to useful articles or resources whenever requesting a change. Because a change request shouldn’t be taken as your sole desire, but as a necessary measure that benefits everybody. Had the time been critical, it’s useful to give your colleague a hand or, perhaps, pair program to achieve the common goal, which is a quality code being merged. Turning an unpleasing fact of redoing your work into a supportive opportunity to learn is a great twist of events!

---

## Review logic, not semicolons

There was a time I had been evaluating missing commas and semicolons during my reviews. What a shame. This is redundant and contributes to absolutely nothing, but it’s a good example of how a technical debt is paid by wasting everybody’s time. We didn’t have any code auto-formatting, and people often ignored ESLint warnings in the console. Eh, those dark times.

![Image of two women near a big typewriter](https://kettanaito.com/blog/the-art-of-code-review/typewriter-YWBAEYNN.svg)

Automation reduces the amount of needless checks, and let’s you focus on the logic behind the changes, rather than syntax errors and typos.

Using tools like [Prettier](https://prettier.io/) and integrating linter checks into your CI can filter out typos and syntax issues as the first automated part of any pull request. That also helps to keep a codebase unified without putting to much thought into it. Time saved by automating the routine can be well spent on verifying the actual logic behind the changes.

---

## Dealing with big changes

Developing a big product may lead into big pull request. The more massive the scope of a change becomes, the harder it is to evaluate its affect. Nobody wants to spend an entire day reviewing a single pull request, having a bunch of other tasks to finish.

![Image of a man behind a computer, and a Git commit tree](https://kettanaito.com/blog/the-art-of-code-review/version-control-GJIGQRDJ.svg)

Plan your work in small, deliverable, meaningful pieces. Iterate and learn from your planning.

However, the scope of a feature isn’t the only factor that affects a pull request’s size. There is also a technical depth, which may render you changing hundreds of files simply to adjust the hue of that one tiny icon.

Have a clear picture of your changes prior to making them. Think it through and discuss with your colleagues whenever in doubt.

What if a feature is small and has a clear development plan in mind, yet still requires to change the half of the entire codebase? How to handle that?

I can recommend an approach we’ve used for such pull requests in our team that we called **intermediate code reviews**. It aims to resolve the amount of changes a reviewer should evaluate, thus resulting into short iterative review sessions. As an issuer, that means a rule to create a pull request, no matter the changes status, not later than the next morning after the first commit. For a reviewer it acts as a rule to always resolve assigned pull requests not later than the next morning. Of course, any necessary communication could also take place so that things are reviewed sooner, or later.

To eradicate huge diffs in your version control system try to issue pull requests from a child feature branch into a single parent feature branch. That way each review iteration ends with the changes being merged into the parent branch. Once the work is done, you can often merge parent branch into your master branch without any preceding code review.

---

## Afterword

Please take all my suggestions with the grain of salt. I understand that a single approach may work differently for different teams, and that’s perfectly fine. It never hurts to know how others do — at worst you can learn from their mistakes.