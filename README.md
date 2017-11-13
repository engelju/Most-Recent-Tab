# Most Recent Tab

## Original Text

Firefox extension that adds a keyboard shortcut to switch back to your most recently selected tab. Useful to alternate between two tabs and to easy go back to your last tab if you switch to another briefly.

This is rewrite built on Firefox's new [WebExtensions API](https://hacks.mozilla.org/2017/06/cross-browser-extensions-available-now-in-firefox/), replacing the old Addon SDK version.

It's distributed the [Firefox Addon site](https://addons.mozilla.org/en-US/firefox/addon/most-recent-tab/).

The code is licensed under the Mozilla Public License 2.0.

## Why this fork

I wanted to change the hotkey from Ctrl+Shift+1 to Ctrl+e. I added this with commit `bd5f5df`.

However, it turned out, that this wasn't doable. I kept getting an error when trying to build this webext, that this extension was invalid:

```
$ web-ext run -v --firefox=nightly --browser-console
...
[firefox/index.js][debug] Firefox stdout: 1510571385506	addons.webextension.<unknown>	ERROR	Loading extension 'null': Reading manifest: Error processing commands.most-recent-tab-command.suggested_key.default: Value "Ctrl+e" must either: match the pattern /^\s*(Alt|Ctrl|Command|MacCtrl)\s*\+\s*(Shift\s*\+\s*)?([A-Z0-9]|Comma|Period|Home|End|PageUp|PageDown|Space|Insert|Delete|Up|Down|Left|Right)\s*$/, match the pattern /^\s*((Alt|Ctrl|Command|MacCtrl)\s*\+\s*)?(Shift\s*\+\s*)?(F[1-9]|F1[0-2])\s*$/, or match the pattern /^(MediaNextTrack|MediaPlayPause|MediaPrevTrack|MediaStop)$/
...
WebExtError: installTemporaryAddon: Error: unknownError: Could not install add-on at '/Users/julieengel/tmp/Most-Recent-Tab': Error: Extension is invalid
    at /usr/local/lib/node_modules/web-ext/dist/webpack:/src/firefox/remote.js:116:27
    at Client.handleMessage (/usr/local/lib/node_modules/web-ext/node_modules/firefox-client/lib/client.js:161:7)
    at Client.readMessage (/usr/local/lib/node_modules/web-ext/node_modules/firefox-client/lib/client.js:220:10)
    at Client.onData (/usr/local/lib/node_modules/web-ext/node_modules/firefox-client/lib/client.js:186:16)
    at emitOne (events.js:115:13)
    at Socket.emit (events.js:210:7)
    at addChunk (_stream_readable.js:252:12)
    at readableAddChunk (_stream_readable.js:239:11)
    at Socket.Readable.push (_stream_readable.js:197:10)
    at TCP.onread (net.js:589:20)
```

Turns out, changing the shortcut to Ctrl+e wasn't doable. So I decided to change it to Ctrl+Shift+e with `226f97b`.
For the exact regex, see: https://dxr.mozilla.org/mozilla-central/source/browser/components/extensions/schemas/commands.json#11

However, this webext seems to use `Alt+P`: https://github.com/jayesh-bhoot/pin-unpin-tab/blob/master/manifest.json
I have no idea, how they can use that. Maybe it doesn't actually work, I havent tested it.

## Developing

See: https://github.com/babyman/quick-tabs-chrome-extension/issues/189.

For testing a webext Extension, you need web-ext: https://github.com/mozilla/web-ext

MDN Links:
- https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Getting_started_with_web-ext
- https://developer.mozilla.org/en-US/Add-ons/WebExtensions/web-ext_command_reference
- https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Porting_a_legacy_Firefox_add-on

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
