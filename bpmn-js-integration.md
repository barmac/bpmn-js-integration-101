---
title: bpmn-js-integration 101
author: Maciej Barelkowski
---

# bpmn-js-integration 101

_Maciej Barelkowski_

---

## What is bpmn-js-integration?

* [bpmn-js-integration](https://github.com/bpmn-io/bpmn-js-integration) is a project we run for each bpmn-js release.
* It helps us to confirm that the library can produce valid BPMNs.
* It helps us to prepare BPMN MIWG submissions.

---

## What kind of tests do we run?

* Import tests: Open a diagram, save an SVG, a screenshot, and a BPMN.
* Modeling tests: Open a diagram, perform actions with [bpmn-js-cli](https://github.com/bpmn-io/bpmn-js-cli), save an SVG, a screenshot, and a BPMN
* BPMN MIWG tests: Perform the import tests on the [bpmn-miwg-test-suite](https://github.com/bpmn-miwg/bpmn-miwg-test-suite).
* (Stress test: HTML to run manually)

---

## How does it work?

There are three core components of the tests:

* test runner (mocha, runs in NodeJS process)
* browser (Chrome Headless instrumented with puppeteer)
* in-browser tests (HTML+CSS+JS run in a browser page)

Test results are saved in a `tmp` directory.

---

## Details

1. Generate test descriptors (JSON) and the templates called _skeletons_ in the code (HTML).
2. Open the template in a browser.
3. Listen for messages dispatched from the in-browser test and perform file system actions accordingly.
4. Save test results in the test descriptor.

---

## What changed with the migration?

* The flow is simplified as there is no need for a [PhantomJS script](https://github.com/bpmn-io/bpmn-js-integration/blob/41dad096f58e920932f2fb1e0f85bf5db72c1cc7/test/integration/run-tests.js#L1).
* We no longer use `console.log` for browser-to-NodeJS communication.
* We fixed some issues which were related to the promisification of bpmn-js.

---

## Next steps

* We are now ready to run the integration tests in multiple browsers, e.g. Firefox, Edge, [_Safari?_](https://github.com/puppeteer/puppeteer/issues/5984)).
* We should consider dropping the transpilation step -> the build script was left untouched, so we still use ES5 syntax in browser.

---

## Questions & comments

---

## That's all Folks
