# Debugging

## What's your best practice in HTML debugging

> **Debugging isn't scary**\
> Debugging doesn't have to be scary though — the key to being comfortable with writing and debugging any programming language or code is **familiarity** with both the language and the tools.

### Permissive code

HTML itself doesn't suffer from syntax errors because browsers parse it permissively, meaning that the page still displays even if there are syntax errors. \
Browsers have built-in rules to state how to interpret incorrectly written markup, so you'll get something running, even if it is not what you expected. This, of course, can still be a problem!

Generally when something wrong in code, there are two main types of error:

* **Syntax errors**: These are spelling errors in your code that actually cause the program not to run, like the Rust error shown above. These are usually easy to fix as long as you are familiar with the language's syntax and know what the error messages mean.
* **Logic errors**: These are errors where the syntax is actually correct, but the code is not what you intended it to be, meaning that program runs incorrectly. These are often harder to fix than syntax errors, as there isn't an error message to direct you to the source of the error.

