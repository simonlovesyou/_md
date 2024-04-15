---
tags:
  - presentation
  - tech-talk
  - eslint
duration: 10–20min
modified: 2024-04-15T19:40:42+02:00
---

# writing a custom eslint-plugin
_or how to design a nuclear reactor_

---

## Bikeshedding

_or the law of triviality_ <!-- element class="fragment" -->

note:  or the law of triviality, is a term coined by C. Northcote Parkinson's. He provides an example of a fictional committee whose job is to design a nuclear power plant. The committee runs through the power plant proposal quickly; it’s too advanced for anyone to really dig into the details, and most of them don’t know much about the topic in the first place. One person in the committee who has enough experience isn't certain how to explain it to the others. Another suggests a redesigned proposal, but it seems like such a huge task that the rest decline to consider it. The discussion then moves to the bike shed. Everyone in the committee voices their opinions on what materials to use and how to save money. They spend more time on the bike shed than the power plant.

This seems silly, but it highlights an interesting common behavior; the complexity of a power plant cannot be fully grasped by an average single person while just about everyone can imagine a bikeshed. So, when demonstrating personal contribution to a proposal or an idea, it's so much easier to endlessly discuss the simple things that you understand and where you might have an opinion rather than the complex questions that require more effort.

 The term gained popularity thanks to Danish software developer [Poul-Henning Kamp](https://en.wikipedia.org/wiki/Poul-Henning_Kamp) who used the term “bike shed discussion” to describe the phenomenon in open source projects, where the amount of discussion a subject receives is inversely proportional to its importance. This issue is rife in the software industry (and of course every other industry) and agonising hours have been wasted debating or worrying about matters that ultimately have little relevance.

As genuine consultants, we of course want to contribute to the design of the proverbial nuclear reactor rather than the bike shed. How can we avoid bikeshedding?

First we need to identify some examples of bike shedding

---

## Some examples of bikeshedding are ...

+ Color and Style Preferences
	+ "Should we rename this constant as SCREAMING_UPPERCASE?"
+ Formatting and whitespace
	+ "Can you add a newline at the end of this file?"
+ Naming conventions
	+ "`getUserFullName` is probably more descriptive than `getUserName` for this use case"
 + Personal preferences
	 + "Can we make this function into two separate functions? It's more readable to me"
 + Minor optimizations
	 + Can we use `Array#reduce` instead of `Array#map` & `Array#filter` to not iterate over the list twice?

---

## How to avoid bikeshedding

Express _all_ conventions you've agreed on as a company/team as eslint rules. 
<!-- element class="fragment" -->

note: This will move the burden of nagging about conventions from the reviewer to the developer implementing this change.

---

## What about product/domain/company conventions?

Real life example from my time at Klarna.

## 