# Exo Shield

Exo Shield is [Exo Browser](https://github.com/UhhErix/ExoBrowser)'s built-in blocker, and the one in Exo Launcher's music players: one browser extension that blocks ads, trackers, malware, cookie notices and pop-ups before they load, and keeps Twitch streams free of ad breaks. It is free software under the [GNU General Public License version 3](LICENSE).

It is made from three GPL-3.0 projects, combined by one script:

| Part | Version in Exo Browser 1.4.0 | Project |
| --- | --- | --- |
| uBlock Origin Lite, by Raymond Hill and contributors | 2026.1026.1812 (Edge build) | <https://github.com/uBlockOrigin/uBOL-home> |
| HaGeZi's Multi PRO DNS blocklist | 211,671 sites, October 29, 2026 | <https://github.com/hagezi/dns-blocklists> |
| TTV LOL PRO, by Younes Aassila and contributors | 2.6.2 | <https://github.com/younesaassila/ttv-lol-pro> |

## What Exo Shield changes

`tools/build-shield.mjs` makes `extensions/exo-shield` from the unmodified packages in `vendor/`:

- HaGeZi's Multi PRO list becomes an always-on ruleset (`hagezi-pro.json`), for what pages load, never what you open yourself, with TTV LOL PRO's two rules for Twitch's ad scripts.
- uBlock Origin Lite's annoyance lists (cookie notices, overlays, social and chat widgets, notification prompts) and its tracking-parameter list are on, and Complete filtering is the mode on every site. Every start puts exactly these back.
- No popup, options page or keyboard shortcuts: in Exo Browser it is always on, at its strongest.
- TTV LOL PRO is merged in (`ttv/`) with its ad reports off and no first-run page; one service worker runs both.
- A count of what it blocked on each page, for Exo Browser's Bar (`exo-count.js`, with the `declarativeNetRequestFeedback` permission): the requests its rules blocked or sent to a harmless stand-in, not its exceptions, header changes or tracking parameters taken off a link (`exo-count-skip.json` lists those rules). The number goes only to Exo Browser's window, on this PC.
- Exo's name and icons (`brand/`).

`extensions/exo-shield/NOTICE.txt` says the same in the extension itself.

## Exo Shield core

Each build also makes `out/exo-shield-core`: the same Exo Shield, at the same version, without TTV LOL PRO (its files, its two rules, its Twitch scripts and its proxy and webRequest permissions) or the count for Exo Browser's Bar. [Exo Launcher](https://github.com/UhhErix/ExoLauncher)'s music players use it, since they never load Twitch. `node tools/build-shield.mjs --core` makes only the core, from the `extensions/exo-shield` that's there. Its `NOTICE.txt` and `SOURCE.txt` say what it is made of.

## Build

With Node 22 or newer:

```sh
node tools/build-shield.mjs [path-to-pro-onlydomains.txt]
```

Without a path it downloads HaGeZi's current Multi PRO list, so a new build has newer lists than the one committed here. `extensions/exo-shield` in this repository is exactly the build that ships in Exo Browser 1.3.0 and 1.3.1.

## Licenses

Exo Shield, and each part it is made from, is under the GPL-3.0 ([LICENSE](LICENSE)). uBlock Origin Lite's filter lists keep their own licenses, listed in `extensions/exo-shield/rulesets`. Exo's icons in `brand/` are © Erix (UhhErix), shared under the same GPL-3.0 as part of this program.

Exo Shield is not affiliated with or endorsed by the uBlock Origin, HaGeZi or TTV LOL PRO projects, or by Twitch.
