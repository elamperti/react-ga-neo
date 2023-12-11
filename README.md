# React GA Neo [![npm version](https://badge.fury.io/js/react-ga-neo.svg)](https://www.npmjs.com/package/react-ga-neo)

A fork of `react-ga4` with a few more features sprinkled on top.

<!-- TOC depthFrom:2 depthTo:3 -->

- [Install](#install)
- [Usage](#usage)
  - [Migrating from old react-ga](#migrating-from-old-react-ga)
- [Example](#example)
- [Reference](#reference)
  - [Extending](#extending)
- [Debugging](#debugging)
- [License](#license)

<!-- /TOC -->

## Install

This package is available at npm as [`react-ga-neo`](https://www.npmjs.com/package/react-ga-neo).

```sh
npm install react-ga-neo
```

## Usage

```js
import ReactGA from "react-ga-neo";

ReactGA.initialize("G-XXXXXXXXXX"); // Your GA4 measurement id
```

### Migrating from old react-ga

Simply replace `react-ga` with `react-ga-neo` and remove `ReactGA.pageview()` calls.

```js
// import ReactGA from "react-ga";
import ReactGA from "react-ga-neo";
```

A few old methods may not be available. You may use `ReactGA.gtag()` or `React.ga()` as last resort to call `gtag`/`ga` directly. Alternatively, you can [extend the library](#extending). Pull requests with improvements are welcome! :)

## Example

Check out [the tests](src/ga4.test.js) for more examples.

```js
// Multiple products (previously known as trackers)
ReactGA.initialize([
  {
    trackingId: "your GA measurement id",
    gaOptions: {...}, // optional
    gtagOptions: {...}, // optional
  },
  {
    trackingId: "your second GA measurement id",
  },
]);

// Send pageview with a custom path
ReactGA.send({ hitType: "pageview", page: "/my-path", title: "Custom Title" });

// Send a custom event
ReactGA.event({
  category: "your category",
  action: "your action",
  label: "your label", // optional
  value: 99, // optional, must be a number
  nonInteraction: true, // optional, true/false
  transport: "xhr", // optional, beacon/xhr/image
});
```

## Reference

#### ReactGA.initialize(GA_MEASUREMENT_ID, \[options\])

| Parameter           | Notes                                                                                                                   |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| GA_MEASUREMENT_ID   | `string` Required                                                                                                       |
| options.nonce       | `string` Optional Used for Content Security Policy (CSP) [more](https://developers.google.com/tag-manager/web/csp)      |
| options.testMode    | `boolean` Default false                                                                                                 |
| options.titleCase   | `boolean` Default true                                                                                                  |
| options.gtagUrl     | `string` Default `https://www.googletagmanager.com/gtag/js`                                                             |
| options.gaOptions   | `object` Optional [Reference](https://developers.google.com/analytics/devguides/collection/analyticsjs/field-reference) |
| options.gtagOptions | `object` Optional                                                                                                       |

#### ReactGA.set(fieldsObject)

| Parameter    | Notes             |
| ------------ | ----------------- |
| fieldsObject | `object` Required |

#### ReactGA.event(name, params)

This method signature is NOT for `UA-XXX`

| Parameter | Notes                                                                                                                         |
| --------- | ----------------------------------------------------------------------------------------------------------------------------- |
| name      | `string` Required A [recommended event](https://developers.google.com/tag-platform/gtagjs/reference/events) or a custom event |
| params    | `object` Optional                                                                                                             |

#### ReactGA.event(options)

| Parameter              | Notes                               |
| ---------------------- | ----------------------------------- |
| options                | `object` Required                   |
| options.action         | `string` Required                   |
| options.category       | `string` Required                   |
| options.label          | `string` Optional                   |
| options.value          | `number` Optional                   |
| options.nonInteraction | `boolean` Optional                  |
| options.transport      | `'beacon'\|'xhr'\|'image'` Optional |

#### ReactGA.send(fieldsObject)

| Parameter    | Notes             |
| ------------ | ----------------- |
| fieldsObject | `object` Required |

#### ReactGA.gtag(...args)

Used to call `gtag()` directly (see [official documentation](https://developers.google.com/tag-platform/gtagjs/reference) for details).

#### ReactGA.ga(...args)

DEPRECATED.

### Extending

```js
import { ReactGAImplementation } from "react-ga-neo";

class MyCustomOverriddenClass extends ReactGAImplementation {}

export default new MyCustomOverriddenClass();
```

## License

MIT
