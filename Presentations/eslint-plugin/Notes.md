---
modified: 2024-03-29T22:44:07+01:00
---

The topic I'm here tonight to talk about is how to write a custom eslint-plugin. Unfortunately my topic is a bit shy and refuses to just come out from the get go, so I have to be a hype man to some extent to convince you that the topic is important before they are willing to come out, so please bear with me:

General structure:
1. [[Bikeshedding]], or the law of triviality, is a term coined by C. Northcote Parkinson's. He provides an example of a fictional committee whose job is to design a nuclear power plant. The committee runs through the power plant proposal quickly; it’s too advanced for anyone to really dig into the details, and most of them don’t know much about the topic in the first place. One person in the committee who has enough experience isn't certain how to explain it to the others. Another suggests a redesigned proposal, but it seems like such a huge task that the rest decline to consider it. The discussion then moves to the bike shed. Everyone in the committee voices their opinions on what materials to use and how to save money. They spend more time on the bike shed than the power plant.
	1. This seems silly, but it highlights an interesting common behavior; the complexity of a power plant cannot be fully grasped by an average single person while just about everyone can imagine a bikeshed. Thus, when demonstrating personal contribution to a proposal or an idea, it's so much easier to endlessly discuss the simple things that you understand and where you might have an opinion rather than the complex questions that require more effort.
	2. The term gained popularity thanks to Danish software developer [Poul-Henning Kamp](https://en.wikipedia.org/wiki/Poul-Henning_Kamp) who used the term “bike shed discussion” to describe the phenomenon in open source projects, where the amount of discussion a subject receives is inversely proportional to its importance. This issue is rife in the software industry (and of course every other industry) and agonising hours have been wasted debating or worrying about matters that ultimately have little relevance.
	3. Bike-shedding in pull-request can be a significant time sink and can distract from the primary goals of a pull request review, which are to ensure code quality, correctness, and alignment with project goals. It is of outmost importance to focus on high-impact feedback while being mindful of the broader context and objectives can help avoid these pitfalls.
	4. ![[Screenshot 2024-03-29 at 22.18.22.png]]
	5. Some examples of bikeshedding are 
		4. Color and Style Preferences
		5. Formatting and whitespace
		6. Naming conventions
		7. Personal preferences
		8. Minor optimizations
		9. Library choices
	6. How do I avoid bikeshedding? My personal rule is that unless we can express my feedback in an eslint-rule I shouldn't provide that feedback.
	7. But there may be things that within your domain or company where minor details are important. The color of a button might be essential for making applications usable for people with disabilities. These adjustments can have a profound impact on user experience and inclusivity.