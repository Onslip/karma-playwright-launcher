# @onslip/karma-playwright-launcher

[![npm version](https://badge.fury.io/js/%40onslip%2Fkarma-playwright-launcher.svg)](https://badge.fury.io/js/%40onslip%2Fkarma-playwright-launcher)

Provides six browsers to [Karma](https://karma-runner.github.io/):

* `Chromium`
* `ChromiumHeadless`
* `Firefox`
* `FirefoxHeadless`
* `WebKit`
* `WebKitHeadless`

Powered by [Playwright](https://github.com/microsoft/playwright).

## Device emulation

Playwright supports [device emulation](https://playwright.dev/docs/emulation) to control various aspects of the browser.
This is probably more important for E2E testing than unit testing, but some configuration (like locale and timezone) may
be useful for unit testing as well.

You can control these settings by providing `device` and/or [`contextOptions`](https://playwright.dev/docs/next/api/class-browser#browsernewcontextoptions) in `karma.conf.js`.

```js
    ...
    customLaunchers: {
        iPhone: {
            base: 'WebKit',
            displayName: 'iPhone',
            device: 'iPhone 6',
            contextOptions: {
                locale: 'sv-SE'
            }
        }
    },

    browsers: [
        'iPhone',
    ],
    ...
```

## Non-bundled browsers

The "real" Chrome, Edge or custom versions of the browsers can be configured by providing
[`launchOptions`](https://playwright.dev/docs/api/class-browsertype#browsertypelaunchoptions) in your Karma
configuration. The browsers must be downloaded and installed manually.

```js
    ...
    customLaunchers: {
        EdgeHeadless: {
            base: 'ChromiumHeadless',
            displayName: 'EdgeHeadless',
            launchOptions: {
                channel: 'msedge'
            }
        }
    },

    browsers: [
        'ChromiumHeadless',
        'EdgeHeadless',
        'FirefoxHeadless',
        'WebKitHeadless',
    ],
    ...
```

Valid values for the `channel` option are: `chrome`, `chrome-beta`, `chrome-dev`, `chrome-canary`, `msedge`,
`msedge-beta`, `msedge-dev`, `msedge-canary`.

## Older browsers

Each Playwright release bundles specific versions of Chromium, Firefox and WebKit. If you use
[Yarn](https://classic.yarnpkg.com/en/docs/selective-version-resolutions/) or
[pnpm](https://pnpm.io/package_json#pnpmoverrides), it's possible you may lock the version of the `playwright` package
in order to force a specific version. [npm](https://github.com/npm/rfcs/blob/latest/accepted/0036-overrides.md) does not
support this yet, but there is a [package](https://www.npmjs.com/package/npm-force-resolutions) available that might work.

See the [Playwright Release Notes](https://playwright.dev/versions/) for what browsers are bundled.

## History

### 0.3.0

* Martin Blom: Now uses the Karma decorators and event handling instead of a custom class.

### 0.2.1

* Martin Blom: Fixed typo. Bumped rev.

### 0.2.0

* Martin Blom: Publish forked package as `@onslip/karma-playwright-launcher`.
* Martin Blom: Added device emulation support.

### 0.1.1

* Martin Blom: Relaxed required playwright version and added note about pinning.

### 0.1.0

* Martin Blom: Provide both headful and headless browsers, support custom launch options.
* Emil Björklund: Add guard for missing browser.

### 0.0.1

* Joel Einbinder/Endy Jasmi: Original version, published as `karma-playwright-launcher`.
