---
modified: 2024-06-15T19:55:16+02:00
---

# [require(esm) in Node.js](https://joyeecheung.github.io/blog/2024/03/18/require-esm-in-node-js/)

Recently I landed experimental [support for `require()`\-ing synchronous ES modules in Node.js](https://github.com/nodejs/node/pull/51977), a feature that has been long overdue. In the pull request, [I commented](https://github.com/nodejs/node/pull/51977#issuecomment-1994837735) with my understanding about why it did not happen sooner before this pull request in 2024. This post expands on that comment a bit more.

The opinions in this post are my own and reflect my perception of the ESM development in Node.js as a long-time bystander. I do not represent any group or the project here - representation of the Node.js project only comes from consensus among the collaborators. There is no specific individual who can speak for the project on their own.

## The headaches of `ERR_REQUIRE_ESM`

It might be obvious for those who have been dealing with `ERR_REQUIRE_ESM` why supporting loading ESM in `require()` is something long overdue, but in case there’s any non-Node.js user who just stumbled upon this post by chance, here’s my understanding about the ESM situation in Node.js and why I (and many others) thought that pull request was necessary.

Since ESM was shipped in Node.js, for many years, it was possible to `import cjs`, but not possible to `require(esm)`. The frustration of `ERR_REQUIRE_ESM` has bothered many and probably has been the primary source of wasted hours in the Node.js ecosystem. If package authors wanted to make sure that both CJS and ESM users can consume their package, they either had to continue shipping their modules as CJS, or ship both the CJS and ESM version i.e. as dual modules (which can lead to some problems, still, this has been a very common practice) with conditional exports information in their package.json.

Meanwhile, many transpilers (e.g. the TypeScript compiler) are still configured to generate CJS code as their final output (probably also to maximize consumption). Users of these transpilers write their code in ESM syntax but they don’t not necessarily know that their code is eventually run as CJS by Node.js. And when their code uses a third-party module that’s real ESM, which could not be `require()`\-d, they would see an `ERR_REQUIRE_ESM`. This could be very confusing since they might assume that their code was run as real ESM.

## The synchronicity of ESM

Naturally, one might ask: why can’t `require()` just support loading ESM?

For a very long time, the answer from the Node.js project had been something like this (to quote the documentation before my pull request):

> Using require to load an ES module is not supported because ES modules have asynchronous execution.

That had also come up in several semi-official communications. And it was always talked about in such an affirmative tone, so that was what I believed, too - despite being a long-time Node.js contributor, ESM or the user module loader in Node.js was never my jam. When it comes to a component that I am not very familiar with myself, I would just believe what the documentation says, like everyone else.

But this was one of the situations where the documentation and other communications were misleading - maybe they were only talking what happened in Node.js’s ESM, not what the ESM itself was designed to be. Last year when I was browsing the V8 code [to fix a memory leak](https://joyeecheung.github.io/blog/2023/12/30/fixing-nodejs-vm-apis-2/), I found out by chance that ESM itself was not actually designed to be unconditionally asynchronous. Rather, it was designed to be only conditionally asynchronous - only when the graph contains top-level `await`.

Then it would seem very natural for `require()` to at least support ESM graphs that contains no top-level `await`. While some libraries might have valid reasons to use top-level `await`, it’s probably not that common a thing - indeed, when I later tested my `require(esm)` PR on high-impact ESM-only packages in the npm registry, none of ~30 that I tested contained top-level `await` - and supporting synchronous modules in `require()` would probably already be enough to make a lot of headaches in the ecosystem go away.

But ESM has been designed like this for a very long time. There must’ve been other people who realized this before me, right? Well yes, of course.

## Synchronous `require(esm)` in 2019

The idea of supporting synchronous ESM graphs in `require()` was by no means new. I later found out that it was already brought up in 2019 in [a pull request that tried adding support for `require()`\-ing .mjs files](https://github.com/nodejs/node/pull/30891). The pull request itself tried to take care of top-level `await` by spinning the event loop in the loader (and the way it did this was unsafe, which was why it was closed). While the idea of only supporting synchronous graphs and not spinning the loop [was mentioned](https://github.com/nodejs/node/pull/30891#issuecomment-565604651), the pull request seemed to have derailed and never ended up in that direction. After this, there were no more attempts at a synchronous `require(esm)`, at least none that I could found that was shared in the form of a pull request (there were some later attempts at `require(esm)`, but they still assumed that ESM was unconditionally asynchronous).

The theoretical foundation for syntax-based synchronous evaluation of ESM on the specification side [was already settled in 2019](https://github.com/tc39/proposal-top-level-await/pull/61). When I later talked to (non-Node.js) people who work on ESM stuff, it seemed to be a common knowledge. It seems over time, a myth was developed in Node.js about how "ESM is async, CJS is sync, so CJS cannot load ESM“, all the time while in standard bodies, the ES spec took special care to ensure that ESM is only conditionally async, and the W3C spec used it to ensure that [Service Workers only allow synchronous module evaluation](https://github.com/w3c/ServiceWorker/issues/1407). Had the syntax-based synchronicity in specifications been more widely known, there probably would’ve been a lot more attempts after 2019, and the documentation would not have talked about ESM being asynchronous as if it was unconditional.

But then why was this relatively unknown to those who didn’t work on ESM in Node.js?

## The ESM silo

After dwelling on this a bit, I think the reason why the synchronicity of ESM didn’t lead to a synchronous `require(esm)` in Node.js sooner was more cultural than technical. There seemed to be a [silo problem](https://en.wikipedia.org/wiki/Information_silo) between those who worked on the ESM implementation in Node.js/communication with the standard bodies and those who didn’t.

Normally in Node.js, most decision making is done based on consensus among 100+ collaborators i.e. committers who gained their status through a nomination process based on contributions to the project. When consensus cannot be reached within collaborators, the decision goes to the Node.js TSC. The Node.js TSC is a subset of the more active Node.js collaborators and it can make decisions by simply voting and taking the option that wins by simple majority.

The early development of ESM in Node.js, however, used a different process. The implementation and the decisions making of ESM in Node.js were delegated to the modules group, which consisted of not only Node.js collaborators but also community members (e.g. package authors, standard body participants, and other kinds of stakeholders). Node.js TSC mostly acted as a rubber stamp on their consensus when it came to ESM decisions.

Due to the nature of the topic, the discussions in the modules group tended to end up very heated. While the composition of the group intended to make the decision making more inclusive, the separated setup and all the heated discussion made it harder for collaborators (and TSC members) outside the group to keep up with what was going on there or to participate. I myself definitely tried to stay out of ESM in Node.js at that time - it seemed like they already got more than enough opinions there.

As a result, silos were developed. If a debate was never escalated out of the group, it can become a niche knowledge among those who worked on ESM in Node.js, or even just among those who were in that specific debate. I think that was what happened to the debate about synchronous `require(esm)`. At least as far as I remember, the debate about a synchronous `require(esm)` was never raised to the TSC. The people involved in the debate could not reach consensus, it sort of just dwindled among those who were aware of it, and others started to assume that it was not possible.

Another factor in the delay of synchronous `require(esm)` was that changes to the ESM loader in Node.js tend to attract more debates than any other systems, which could drive contributors away. I’ve been contributing to Node.js for 7 years, but I rarely touched the ESM loader until last year - and last year I was just fixing bugs/memory leaks which were uncontroversial, not changing how ESM is supposed to work in Node.js per-se, which tends to be controversial. This probably also prevented more people from hacking on the loader and making `require(esm)` happen sooner. At least when I was started looking into `require(esm)` last year, I definitely did not want to be too loud about it to avoid drawing unnecessary debates before any technical progress was even made.

## The ESM loader

While I said that I think a synchronous `require(esm)` in Node.js didn’t happen earlier mostly because of cultural reasons, some smaller technical factors probably also contributed to the delay.

The ESM loader itself is quite a beast at this point. When I started contributing to Node.js I found the CJS loader to be really difficult to grok - that was before Node.js had a ESM loader. A few years later, when I happened to be fixing some memory leaks in the vm API, which were caused by ESM integration (I talked about them in [previous blog posts](https://joyeecheung.github.io/blog/2023/12/30/fixing-nodejs-vm-apis-3/)), I had to really dig into the ESM loader in Node.js for the first time. And I was amazed by how the ESM loader was even more complex than the CJS loader (almost 3x more code). This probably comes from years of organic growth of the loader and it seems to really need some cleaning up.

The ESM loader was implemented largely in JavaScript - while I do think JavaScript has its advantages when implementing certain APIs like streams, this could really work against you if you try to use it to implement a core part of JavaScript itself in a runtime, like a ESM loader. To prevent prototype pollution, internally Node.js uses a special copy of JavaScript built-ins in its JavaScript code, and this hurts readability a lot. The loader is split in multiple files in a way that lead to circular dependencies everywhere, and some of the code need to actively defends against [TDZs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#temporal_dead_zone_tdz), making the code even more difficult to read. The rather complex JavaScript codebase also makes the ESM loader impose a lot of random, unnecessary asynchronicity on the loading process. A substantial part of the ESM support is provided by V8, which is only exposed to the JavaScript layer via C++/JS bindings. It seems over time the JavaScript part started confine itself with what was provided by the C++/JS bindings, instead of making full use of what V8 provides.

These technical issues in the ESM loader also have other consequences - e.g. in performance. Some may assume that being able to always load asynchronously (and, in parallel if the module contain multiple `import`s) would make the loading faster. But when I tested `require(esm)` on that ~30-ish ESM-only npm packages and comparing to `import esm`, the former (which uses dedicated synchronous routines) [is actually ~1.22x faster](https://github.com/nodejs/node/pull/51977#issuecomment-1995209126).

## Restarting synchronous `require(esm)`

Around the end of last year, after I found out that the evaluation of ESM can be synchronous based on syntax, and it was only Node.js throwing the asynchronicity into the loading process, @GeoffreyBooth and I started to talk about restarting synchronous `require(esm)`. ESM in Node.js is still a very scary subject to me, even to this day, but the agony of `ERR_REQUIRE_ESM` has been so bad that it seems to be worth the risk of getting into these taxing debates to get the ball rolling again.

That said I wouldn’t take the risk if it’s a very high-hanging fruit - which was what I thought before I really looked into the ESM loader. At that time there was an ongoing effort to “make the ESM loader the only loader in Node.js”, and due to the complexities mentioned before, the estimation was that it could take quite some time to refactor the ESM loader to a shape that supports this. So I’d rather just leave it to others who are more faimilar with the ESM loader to do that refactoring.

In late February in 2024, when I was working on [a ccache-like thing for both the CJS and ESM loaders](https://github.com/nodejs/node/issues/47472) and digging into them again, I noticed that there seemed to be a simpler way to implement it - just drop the “make the ESM loader the only loader in Node.js” idea (of which I was skeptical already), and implement a few dedicated routines for the CJS loader to support synchronous `require(esm)`. The fewer existing ESM loader code it uses, the easier it would be.

So that led to [this PR](https://github.com/nodejs/node/pull/51977). The major difference between this and the PR in 2019 was that this tried to keep the scope of `require(esm)` small and only supported loading synchronous ESM. As it turned out, this is not a controversial idea among collaborators/TSC at all and landed without much pushbacks (it derailed a tiny bit due to the discussions about loader hooks, but at least we agreed that hooks support could be left for follow-ups and `require(esm)` itself should be back on track).

## What’s next?

The feature is still experimental under the flag `--experimental-require-module` and there is still some work that needs to be done before it goes out of experiments.

There probably still are some edge cases that it needs to take care of. I tried to test a bunch of edge cases in the PR, but obviously there are just too many possibility of module graphs to test them all in one PR. The initial iteration was already enough to load most high-impact ESM-only npm packages that I’ve tested. We can continue polishing this as we get user feedback about it.

Another thing that needs to be solved is support for custom loader hooks. The current loader hooks are again unconditionally async. This imposes a tremendous overhead via the use of workers to make the main thread block on the loaders. While it’s better than having no loader hooks at all, performance-wise and capability-wise this is just nowhere near what `require()` monkey-patching offers, and `require()` monkey-patching has been used by so many popular packages that I think we really need to provide a comparable alternative for users to migrate to. In my opinion the next step should be developing an in-thread and synchronous variant of the loader hooks that support both `require()` and `import`. This could make `require()` monkey-patching no longer necessary, and enable more users to migrate from CJS to ESM.

Currently `require(esm)` only supports ESM explicitly labeled as ESM - either via the `.mjs` extension, or a `"type": "module"` field in `package.json` for the `.js` extensions. This is already enough to support loading ESM-only packages in npm. It is possible to implement falling back to ESM loading when a `.js` file with ESM syntax appears without `"type": "module"` field in its closest `package.json`, but this is in general something users should avoid - ESM syntax detection incurs an overhead and once you have enough ESM modules in your project, you probably don’t want Node.js to waste time guessing what your module type is, when you could’ve saved the cost with just one explicit `"type": "module"` field in your `package.json`.

Support for top-level await in entry points is still possible - we could just fallback to the asynchronous loading for the entry point in that case, since the exports of the entry point goes nowhere anyway. That can be done already via the `--experimental-detect-module` and it is more of an implementation detail to move the fallback within the CJS loader now that it supports loading ESM.

Thanks Bloomberg, who has been sponsoring my work over the years, for supporting my work on fixing this agony.