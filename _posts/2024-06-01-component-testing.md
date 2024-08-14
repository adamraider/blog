---
title: Test behavior, not code structure
subtitle: Use component tests to improve resiliency and overall testing strategy
layout: post
tags: testing software&nbsp;design
---

The design of when and how to split up our code is a useful thing to consider, but how should it influence how we test our software?

Unit-tests are often a starting point for testing, however unit tests can have the unfortunate consequence of being highly coupled to those arbitrary structural decisions. The idea that every class or module needs its own personal test suite encourages brittle testing.

Instead, what would it look like if we focused on testing user-facing APIs and behavior?

When making a change to a feature the directory structure often looks something like the following.

```
foo_feature/
├── footer.js
├── footer_test.js
├── form.js
├── form_test.js
├── title.js
├── title_test.js
├── util.js
├── util_test.js
```

Notice the tests. One test file per module. One or more test cases per method. With this pattern, I often find myself _fighting the existing tests rather than being emboldened by them_.

The problem with this approach is it tightly couples the tests to the arbitrary structure of the code.

## Coupling

A key property of a well written test is that it verifies a requirement of the system is met. If the implementation or code structure of the requirement can change while the test continues to pass, we can consider this test _resilient_. However, if the requirement changes and the test continues to pass, we can consider the test _incorrect_.

Exposing test-only methods or accessing private members in some other form are common coupling culprits that make tests less resilient.

Many UI tests rely on reading from the DOM via element id or CSS class names. Like private members of a class, these should be treated as implementation details. If the style of an element needs to change, or CSS is being consolidated, the test should not break. The name of an internal identifier should be free to change without breaking the test.

{: .callout-note }
Note: Screenshot tests being an exception for asserting visual correctness.

The design of when and what to split up into separate classes has no relevance to the user-facing behavior. Our tests should reflect that and be resilient to refactoring.

Moving code around is not a requirement change, and thus should not break a test. That's not to say that having tests coupled to the structure of your code is _always_ bad. Subroutine/subcomponent unit tests can add value and are inherently tied to structure as they operate below the user-facing API level. The challenge here is being strategic about what subroutines are worth having unit tests for and ensuring that the component as a whole is thoroughly tested. This ensures high confidence that when changing code structure -- thus necessitating changes to unit tests -- something is not accidentally broken in the refactor.

You should be reasonably confident in your system even if most subroutine tests didn't exist. Subroutine tests can augment your overall testing strategy, but should not be a substitute for component level tests.

## Component tests

UI component tests load a subset of the application and do not make HTTP calls to a back-end server. They're functional tests and thus make no assumptions about _how_ the behavior is performed internally. This treats the feature-under-test as a "black box".

While most tests solely interact with the public API of the thing-under-test (there are exceptions), component level tests interact with the user-facing I/O. What can a real user see while using your interface and what is the expected outcome of their interaction?

Well developed component tests also offer your engineering team a high-level executable document that lays out the expected functionality of the feature. Combine this with some screenshot tests and the codebase becomes much more navigable without relying on external documentation.

## How to test like a user

Instead of starting with unit tests that reflect the structure of your code, start with component tests.

Test against the UI (e.g. a button, an input field) and make assertions against user-facing output (e.g. presence or absence of text or interactive element).

Leverage tools like [semantic locators](https://github.com/google/semantic-locators), which allow you to programmatically interact with your page like a user, instead of selecting from the DOM via ids or CSS class names. Not only does this make the test more resilient to change, it adds some accessibility coverage to your test.

Let's say you're testing an e-commerce shop's product page. You may have a component test that looks like this using a semantic-locators-like syntax.

```js
describe("Product details", () => {
  beforeEach(() => {
    const view = new ProductDetails({
      item: ItemSku.HOVERBOARD,
    });
    view.render();
  });

  describe("add to cart", () => {
    beforeEach(() => {
      button(/Add to cart/).click();
    });

    it("shows a confirmation", () => {
      assertOne("{alert 'Hoverboard added to cart'}");
    });

    it("updates quantity", () => {
      assertOne.text("In cart: 1");
    });

    it("shows remove from cart button", () => {
      assertOne.button(/Remove from cart/);
    });
  });
});
```

This test makes no assumptions about the internals of the product details feature. In addition, it tests that we're using appropriate aria-roles and labels for our elements. As an example, "add to cart" may be a button that simply has a + icon in it, this test suite would ensure the icon is appropriately labeled with "add to cart" to screen readers.

This suite also provides a high-level overview to readers about the behavior of the product details page.

By writing tests at the user-facing public API level, developers are empowered to refactor the internals without a worry.

Start with a UI component test at the feature level and augment it with lower-level tests on subroutines on a case-by-case basis.

```
foo_feature/
├── foo_feature_test.js
├── footer.js
├── form.js
├── title.js
├── util.js
```

The structure of tests does not need to match the structure of your code. A module shouldn't necessarily have its own test suite and a new method shouldn't necessarily have its own test case(s).

By prioritizing user-centric component testing and avoiding non-functional coupling, you can ensure a maintainable and robust test suite that empowers confident refactoring.
