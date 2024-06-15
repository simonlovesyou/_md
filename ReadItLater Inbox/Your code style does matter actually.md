---
tags:
  - article
  - code
modified: 2024-06-15T19:57:22+02:00
---


# [Your code style does matter actually](https://www.epicweb.dev/your-code-style-does-matter-actually)

A lot of people say you should just use the **default configuration for [Prettier](https://prettier.io/)** and your life is going to be so much better. And while I can appreciate that perspective, I think that there are actual configuration options that are **superior to the defaults** that are built into Prettier.

Lots of you feel like there's no reason to give a whole lot of time and energy around arguing about these things. It's better to just let the tool do its job. And you're right honestly. I wouldn't spend a lot of time arguing with people about this (which is why I'm writing it in a blog post I can just send people to in the future). There are a couple of formatting things with regard to the way we write our JavaScript and our TypeScript code that I think are worth talking about.

## The Epic Web Dev Configuration Package

So recently I updated the ESLint or the Prettier config for Epic web dev. I made[](https://github.com/epicweb-dev/config)

[`@epic-web/config`](https://github.com/epicweb-dev/config)

to hold the configuration for ESLint, Prettier, and TypeScript and in the future could manage more config. Recently I made a change to the arrow parens option. I changed it from `avoid` to `always`. So basically effectively changing it completely. Incidentally, this is the default configuration but I like to include my configuration explicitly so that I can communicate that this was an intentional choice and not just something I didn't consider.

I [shared this on 𝕏](https://x.com/kentcdodds/status/1801429520161116197) and as expected got a fair bit of push back. So I want to justify this decision (and a couple others as well).

### Controversial Configurations

-   **Arrow Parens**: I set the arrow parens option to `always`. This means that even if a function has a single argument, parentheses will be used.
-   **Semicolons**: My semicolon configuration might raise some eyebrows. I set `semi` to `false`, which means I don't use semicolons in my code.
-   **Trailing Commas**: I use trailing comma and I set that to `all`. I always have trailing commas for function arguments, objects, arrays, etc.

These three configurations in particular are the ones that I wanted to talk about here.

## The Reasoning Behind the Choices

The reason that these configurations are set in the way that they are is actually described in [the decision document](https://github.com/epicweb-dev/config/blob/main/docs/decisions/006-arrow-parens.md) for when I made the change to the arrow parens option:

> We want to avoid extra work required to refactor code as much as possible.

It's the classic "lazy developer" approach. Do the thing that results in as little work now and in the future as possible.

If we can accept the fact that each one of these options is syntactically correct and will actually function, then the decision between which we use actually doesn't matter a whole lot in regard to what the end state of the code looks like after formatting. However, the experience of changing that code is where the end state actually matters.

### Trailing Commas

Let's start with the less controversial one... trailing commas. If you have a long list of items and you need to change the order, if you don't have a trailing comma, you got to add a comma before you can move the last one. For example:

`   `

`const people = [`

`{ id: 1, name: 'Bob', age: 8 },`

`{ id: 2, name: 'Alice', age: 11 },`

`{ id: 3, name: 'Charlie', age: 15 },`

`{ id: 4, name: 'Dave', age: 7 },`

`{ id: 5, name: 'Eve', age: 13 }`

`]`

`   `

If I wanted to move Eve above Dave, I would first have to add a comma to Eve, then move the line. I call this "comma babysitting." But by having a trailing comma, I can simply move Eve.

And Prettier can add the trailing comma for me automatically. It's no extra work when I write it and it saves me work when I refactor it.

Is it a lot of work? No. Am I a whining developer? Probably. But it's just another thing that would be nice to not need to worry about.

Additionally, if I add another item to the end of the array, I have to add a comma first and the git diff will show two lines were changed which is annoying.

I think this is a pretty common one though. Let's get spicier...

### The Case Against Semicolons

First off, I want to call out that by not using semicolons, we are not relying on [automatic semicolon insertion](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#automatic_semicolon_insertion). We have build tools and things that are going to compile our code and minify it and everything, they'll add the semicolons for us automatically.

Another issue people have with leaving off semicolons is you can start a line with a bracket or a parentheses and that can cause problems if the previous line doesn't have a semicolon. We're not gonna have those problems because we use the [`no-unexpected-multiline`](https://eslint.org/docs/latest/rules/no-unexpected-multiline) rule from ESLint (not to mention prettier makes the code look funny if you try that). For example, if you were to write something like this:

`   `

`let firstPerson`

`const people = [`

`{ id: 1, name: 'Bob', age: 8 },`

`{ id: 2, name: 'Alice', age: 11 },`

`{ id: 3, name: 'Charlie', age: 15 },`

`{ id: 4, name: 'Dave', age: 7 },`

`{ id: 5, name: 'Eve', age: 13 }`

`]`

`[firstPerson] = people`

`   `

Prettier would rewrite it to look like this:

`   `

`let firstPerson`

`const people = ([`

`{ id: 1, name: 'Bob', age: 8 },`

`{ id: 2, name: 'Alice', age: 11 },`

`{ id: 3, name: 'Charlie', age: 15 },`

`{ id: 4, name: 'Dave', age: 7 },`

`{ id: 5, name: 'Eve', age: 13 },`

`][firstPerson] = people)`

`   `

Which makes it much more obvious something weird is happening. This is just a non-issue.

Sure, ok, so the problems aren't really problems. Great. But why turn off semicolons? Turning off semicolons makes the process of refactoring our code easier by not having to babysit the semicolons. For example:

`   `

`const people = [`

`{ id: 1, name: 'Bob', age: 8 },`

`{ id: 2, name: 'Alice', age: 11 },`

`{ id: 3, name: 'Charlie', age: 15 },`

`{ id: 4, name: 'Dave', age: 7 },`

`{ id: 5, name: 'Eve', age: 13 },`

`];`

`const olderThanTenAges = people`

`.map(person => person.age)`

`.filter(age => age > 10);`

`   `

Notice that the final chained operation has a semicolon. If I decided to do the filter before the map I have to first remove the semicolon, then move the line. I call this "semicolon babysitting". However, if I don't have semicolons then I simply move the line.

It's small, but it's also just one less thing to worry about when refactoring code and it shows up in enough situations like this one and others that it's enough reason to set `semi` to `false`.

### Parentheses for Arrow Functions

The same principle applies with parentheses for arrow functions. If you don't have parentheses around a function because it only has one argument, then that is perfectly valid JavaScript. But when you go to refactor that, let's say that you decide to add a type or destructure the argument, you have to manually add parentheses before you can do that. Can you guess what I call this? "Parentheses babysitting."

If you always have parentheses, you can write your function however you like and Prettier will add the parentheses for you automatically.

Again, you don't have to write the parentheses yourself, prettier can add them for you. So it's no extra work for you. It just saves you time if you later need to refactor your code into something that requires the parentheses.

## Conclusion

All of these rules and things, while they don't directly affect the user experience (which is the only thing that really matters), they're just extra chores you have to do if you configure them differently than the way I have them configured. As you're configuring your formatter, think about how you can configure it in such a way to **save you time and reduce babysitting** of things like semicolons, parentheses, and commas.

**Stop babysitting**.

Even if you disagree with everything that I've said, at least I've explained my own reasoning for the configuration that we have for the Epic Web projects.

Cheers!