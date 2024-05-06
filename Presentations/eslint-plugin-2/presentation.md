---
tags:
  - presentation
  - tech-talk
  - eslint
duration: 10–20min
theme: simple
modified: 2024-05-03T11:53:39+02:00
---

# Custom eslint plugins

_or how to translate domain/team/company practices to eslint plugins_

note: 

---

# Why?

_Why would you need a custom eslint plugin when there's a huge eslint-plugin community?_
+ Domain specific rules
+ Company specific rules

note:
There are vast eslint plugins that can help you keep consistent code style and or to avoid confusing code, like sorting import statements or using confusing javascript syntax.

But there are certain things that may not be easily expressable with off the shelf eslint plugins, like domain & company specific rules.

---

<!-- .slide: style="text-align: left;" -->

# Examples

## Domain specific <!-- element class="fragment" data-fragment-index="0" --> 
+ GDPR-protection.
+ Ensure strings are localized.

## Company specific <!-- element class="fragment" data-fragment-index="3" --> 
+ Forbid the usage of certain utility functions in favor of native methods.
+ Do not use abbreviations for service names.

---

## Abstract Syntax Tree

<iframe src="https://astexplorer.net/" />

---

# Demo!