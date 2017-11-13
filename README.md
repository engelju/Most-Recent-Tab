# Most Recent Tab

## Original Text

Firefox extension that adds a keyboard shortcut to switch back to your most recently selected tab. Useful to alternate between two tabs and to easy go back to your last tab if you switch to another briefly.

This is rewrite built on Firefox's new [WebExtensions API](https://hacks.mozilla.org/2017/06/cross-browser-extensions-available-now-in-firefox/), replacing the old Addon SDK version.

It's distributed the [Firefox Addon site](https://addons.mozilla.org/en-US/firefox/addon/most-recent-tab/).

The code is licensed under the Mozilla Public License 2.0.

## Why this fork

I wanted to change the hotkey from Ctrl+Shift+1 to Ctrl+e. I added this with commit `bd5f5df`.

## Developing

See: https://github.com/babyman/quick-tabs-chrome-extension/issues/189.

For testing a webext Extension, you need web-ext: https://github.com/mozilla/web-ext

MDN Links:
- https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Getting_started_with_web-ext
- https://developer.mozilla.org/en-US/Add-ons/WebExtensions/web-ext_command_reference

### web-ext

Install with:

```
npm install --global web-ext
web-ext --version
```

Run your webext:

`web-ext run -v --firefox=nightly`

If you run into the following error:

`Error: spawn /Applications/Firefox.app/Contents/MacOS/firefox-bin ENOENT`

you most likely forgot to add the -firefox flag. See: https://github.com/mozilla/web-ext/issues/628

For more flags available, check the MDN doc. Not all are listed when running `web-ext --help`.
