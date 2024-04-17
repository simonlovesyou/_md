[[ReadItLater]] [[Article]]

# [Why your performance work is not seen](https://dev.to/viniciusdallacqua/why-your-performance-work-is-not-seen-11of)

If you are reading this, chances are you care about performance. Also, chances are, you have played around and established some form of Lab [or](https://www.debugbear.com/) [RUM](https://www.rumvision.com/) [solutions](https://speedcurve.com/) to start capturing data about your application. If you haven’t, [I have just the article for you](https://engineering.atspotify.com/2022/09/from-development-to-real-users-how-to-create-a-web-performance-story/). You have run Lighthouse reports and time after time you have seen that there are a few, or sometimes lots, of improvements that could be done, but it just seems to not reach a point where you can actually focus on fixing those problems and get long lasting, meaningful, improvements to your users. Or establish a continuous process, or governance, to track and iterate over your application’s progress. That backlog seems to never reach a point where performance tasks are moved to working items, and, unless something is on fire, most of your reports don’t translate into the right value being delivered.

This article represents some of my findings over many years creating or collaborating with performance efforts whilst establishing a governance around our work. And some of those points I’m very much still experimenting with or establishing them into my current workflow, so tag along and let's discuss those findings.

## [](https://dev.to/viniciusdallacqua/why-your-performance-work-is-not-seen-11of#making-sure-to-maximize-value-from-your-tooling)Making sure to maximize value from your tooling

### [](https://dev.to/viniciusdallacqua/why-your-performance-work-is-not-seen-11of#shaping-a-better-lab-tooling)Shaping a better Lab tooling

There are many great articles on Lab testing, so this article is not going to cover lab data setup and how it differs from your field data. But if there is a key takeaway is this: Lab data is a great way to avoid significant regressions from ever being shipped to real users, and one of the best ways to get those early hints is to set up performance budgets. Having a direct correlation between lab metrics and code changes allows for the correlation of improvements or regressions.

Having a good setup for your lab data means [creating guardrails](https://www.speedcurve.com/blog/continuous-web-performance/) that will alert you of any regressions. And creating meaningful budgets is also important to ensure your application progress over time is measured and compared over its own trends. Setting up KPIs/SLOs and budgets when your metrics are way above the ‘good’ threshold may be daunting and create too much friction or analysis paralysis whilst trying to ship something meaningful. Setting up a good governance process means assessing achievable meaningful progress over time. Sometimes you have to set your thresholds based on your own starting points to iterate over and quickly deliver results over time.

### [](https://dev.to/viniciusdallacqua/why-your-performance-work-is-not-seen-11of#extracting-more-out-of-rum-tooling)Extracting more out of RUM tooling

There are great options when it comes to RUM tools for developers to choose from, and sometimes teams can even build tailor made in-house solutions to monitor their Field Data. But to extract the most value out of any RUM tool you need to cover a few points from the engineering and product perspective. For a tool is only as useful as how much your teams are willing to use them in their processes to extract its value. And for teams shipping features to a product, value does not only come from developer focused metrics, but product focused too.

Teams may struggle having to aggregate data points from different tools to extract correlations between that performance improvement and actual value shipped to users. Sometimes the only thing preventing teams from building correlations is the tools they use, or how they use the tools available.

Correlations are a great way to prove value for a performance governance process. And any value that is only focused on developer experience may incur a risk of being one sided, thus not translating into more value for your users which in turn may translate to less buy-in from the product side.

You may also want to segment your data based on market and user base. Not all markets behave the same, and not all markets have the same priority or use to your product. When it comes to shipping the best value, you have to ensure long tail users of markets that are not your top priority are not skewing percentiles if you only use global data as context. Whilst improving experience for all your users is always an overarching goal, it is not always a possible one to prioritize from a product perspective.

Your percentile distribution also matters. Focusing in one percentile may blindside and miss improvements achieved for other parts of your distribution. Visualizing the data in its entire distribution will help understand where the most impact is being made and identify improvements made across the user base for a segment. There’s an [awesome talk by Tim Vereecke](https://www.youtube.com/watch?v=YzkdiTPxRM4) that shows this in great detail.

All application metrics can be observed and segmented through different product lenses. The key is to trace correlations, for the bigger a metric context is, the harder it is to correlate actual value and usage to your users. This way, you can ensure that your performance governance can also drive and inform product level decisions and prioritization.

### [](https://dev.to/viniciusdallacqua/why-your-performance-work-is-not-seen-11of#trends-and-historical-data)Trends and historical data

On Lab and RUM setups it is important not only to have performance in place, but to observe your metrics through historical data. Assessing trends and understanding evolution over time is important to avoid having your metrics creeping up past your budget levels.

Historical data also comes in the form of documentation. Same with any good incident remediation process, an important step to avoid recurring regressions on any team is to document those. Building and sharing knowledge around your product’s regression and understanding why they happen is a key step in a healthy governance process.

## [](https://dev.to/viniciusdallacqua/why-your-performance-work-is-not-seen-11of#how-to-strengthen-your-performance-governance)How to strengthen your performance governance

### [](https://dev.to/viniciusdallacqua/why-your-performance-work-is-not-seen-11of#metrics-and-kpi-slas)Metrics and KPI / SLAs

Core web vitals offer a great standardized set of metrics, and those are a great starting point to extract value out of your website metrics. But at some point in your governance structure you may need to assess which metrics better correlate to your product’s value at that time. Not all pages have the same importance and not all features the same usage, so building KPIs and SLOs using all of web vitals metrics may not be optimal. Choosing a subset of those metrics based on usage trends and patterns of your app and features can be a powerful way to create KPIs between the engineering side of your team and product. And SLAs between your team and downstream teams and services to ensure metrics don’t degrade over time. This process also needs to be iterative to fine tune and adjust as trends around your product metrics and usage evolves over time.

Product teams can also extract great value establishing their own metrics, to better represent their product and user journeys.

### [](https://dev.to/viniciusdallacqua/why-your-performance-work-is-not-seen-11of#buyin-from-management)Buy-in from management

To establish a governance process, you first need to prove there’s value in integrating another process into any team’s workflow. And one way to prove there’s value is via correlations.

We can always start from the point that Web Vitals [directly translate to better SEO](https://developers.google.com/search/docs/appearance/core-web-vitals). But this alone may not always directly translate to a governance process. SEO ranking is only a factor, and better ranking does not only come from Web Vitals metrics. A key metric that most product teams need to track somehow is conversion, though conversion metrics can have many different underlying meanings. Correlating product facing metrics such as click-through and conversion rates with your performance trends is a key factor to align the two sides of your team and product areas for continuous buy-in from management.

Data is always undeniable, and delivering value that you can trace and correlate to product metrics is a great way to use data.

Finally, your performance governance is a continuous process and as such it needs to matter not only to your engineering side of the company but also to your product and users. Setting up a meaningful process is to fine tune your tools and metrics to better represent your product and users. Another key step is to publicize your progress, internally and externally. There’s always great learnings to be shared from regressions and improvements, documenting and sharing those helps cement your governance progress. So measure, experiment, ship, report and repeat!