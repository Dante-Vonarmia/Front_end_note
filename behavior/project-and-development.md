# Project and Development

## Major Coding Standard

{% embed url="https://codeguide.co" %}

{% embed url="https://github.com/airbnb/javascript" %}

## If your client tells you that the website you built for them is running slow, how do you triage this to understand the root cause?

#### A: There are several reason in different ways could cause the reasons:

### 1)    Reason cause by the browser:

* First check error with browsers console tools. Make sure there is nothing blocking. And no error occurred.
* Check the data or files is too big to load or not.
* Check JavaScript or Flash plugin is activated or not. (Recommend use HTML5 media)

### 2)    Reason cause by the project:

* Make sure the components are optimized loaded and rendered.
* No repetitive http requests.
* Make sure use CDN to loading statics assets.
* Check third-parts libs or dependencies.

### 3)    Reason cause by the server-side:

* Use tech such as Redis to solve the High concurrency issues.
* Check the server-side for hosting, balance load, usage or limitation.
* Check cybersecurity. Take basic actions to avoid common cyber attack
* Check database status.

## How do you deal with ambiguous requirements?

To avoid unnecessary requirements. It’s always a good trial to follow the standards from the documents.&#x20;

For some future requirements, we can put them into next version. This is how we stick to the agile development.&#x20;

For different ideas about the requirements, we can use the A/B test and let the users decide what is really need. We might get the user data by tracking and doing statics on their behavior and feedbacks.

## What criteria do you take into account when deciding which framework to use to build a project.

* The model of cloud service. SaaS? PaaS? IaaS?
* The scale of the project. The usage of the application. Devices that covered.
* Standard of highly reusable components.
* Does it help to improve the performance, efficiency, and less redundant code?
* Separate the front-end and back-end gracefully
* Solve the intense coupling problem
* Back-end language
* Agile Development or not. (Future supports or future demands)
* How many developer we have? The budgets? And due day?

