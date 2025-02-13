---
description: It's also good question to ask back.
---

# Role and Responsibilities

> The following questions will indicate how big the projects the candidate has been involved in.

## What tools suite do you use for your project and why?

* Good: "Webpack, React router and TypeScript", "Try list some major features"
* Bad: "Parcel, NextJS and JS++"

## What testing strategy do you use?

* Good: "I use TDD for logic and automated UI tests for the rest"
* Bad: "I mostly do manual testing/TDD"

## How do you handle component reuse?

* Good: "I refactor when I see duplication but some components are generic"
* Bad: "I always try to write generic components"

## When do you use server side rendering and why?

* Good: "I used it in Node. Server side process/validate data. Client-end render/interact data"
* Bad: "I always use it because it speeds up the loading time"

## What tasks do you run and how?

* Good: "I try to use a task runner and Webpack for bundling"
* Bad: "I mostly use Webpack loaders"

## When do you use component based testing and why?

* Good: "I use Enzyme but only for generic components since I use UI testing mostly"
* Bad: "I use Enzyme and I try to test all my components"

## Do you use TDD and how?

* Good: "I find it hard to use TDD for components so I use it for logic."
  * Doing manual test is just standard part of development &#x20;
  * Doing TDD for react components costs lots of efforts. &#x20;
  * It's not feasible to write a large-scale SAP &#x20;
  * Mocking frameworks are essential in the TDD process.
  * Small coverage of each unit test. Detect flaws efficiently down through layers.
* Bad: "I use TDD as much as I can"

## What state do you put where and why?

* Good: "I only put shared data on the store and private data on the state"
* Bad: "I always put my state on the store"

## Whats more important, clean code or good enough?

* Good: "I try to write clean code but sometimes I need to hack things together"
* Bad: "Clean code"

## How do you handle bundling performance?

* Good: "There are loaders for it but mostly I try to reduce the bundling process"
* Bad: "What do you mean?"

## How do you handle multiple component variants in the same codebase?

* Good: "I raise awareness in the company and take action after that"
* Bad: "I try to refactor them in to generic components"

## How do you handle feature toggling?

* Good: "I use a config file or similar"
* Bad: "What do you mean?"

## How do you avoid component duplication?

* Good: "It is hard to solve this so I talk to the teams and use good names"
* Bad: "I write generic components and put them in Storybook"

## How do you handle A/B testing?

* Good: "I create a temporary component in isolation"
* Bad: "What do you mean?"

## How do you handle branding/themes?

* Good: "I try to avoid them / I use a variant prop in the components"
* Bad: "I use Material ui themes"

## How do you handle translations?

* Good: "We get them from a external tool"
* Bad: "I have never worked with them / we use translation files"
