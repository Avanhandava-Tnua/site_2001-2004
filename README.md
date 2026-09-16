# avanhandava.org — 2004, reconstructed

A browsing copy of the website of Grupo Escoteiro e Distrito Bandeirante
Avanhandava (São Paulo), as it stood in 2004. Rebuilt from a backup of the
original FrontPage site, with assets recovered from the Internet Archive.

Entry points: [`index.html`](index.html) (Flash intro),
[`frame.htm`](frame.htm) (the site), [`period.html`](period.html) (800×600).

## Publish it

1. Push these files to the **root** of a public repository.
2. **Settings → Pages → Source → Deploy from a branch → `main` / `(root)`.**
3. Wait a minute or two for the first build.

`.nojekyll` is included and must stay: it stops Jekyll from processing the
tree, which matters because filenames here contain spaces, parentheses and
accented characters.

## Does it work on its own?

Yes, in a normal browser, with no help from oldweb.today:

- 229 resources crawl clean. Six dead links remain, all of them either files
  that exist in no copy anywhere (`servicos.htm`, two `iton/` pages) or hrefs
  that were already malformed in 2004 (`Www.vhf.org`).
- The Flash intro plays, through Ruffle.
- Typography uses the genuine Verdana, Tahoma, Comic Sans MS, Arial Black,
  Times New Roman and Courier New, with Arimo standing in for Arial.
- `period.html` frames the site at 800×600, the resolution it was drawn for.

What will not work in any browser, because the services behind them no longer
exist: the chat (`www2.avanhandava.org`), the webmail sign-in
(`avanhandava.zzn.com`), the guestbook, and the search box. The site links out
to 60 hosts, most of them long gone.

## View it in a period browser

Once live, [oldweb.today](https://oldweb.today/) can load it in a real Internet
Explorer 5 on Windows 98. Omit the timestamp from the hash and it fetches the
live URL through Webrecorder's proxy instead of the Wayback Machine:

```
https://oldweb.today/?browser=ie5#/https://<user>.github.io/<repo>/frame.htm
```

The two external resources this build uses — Google Fonts and Ruffle — are
injected from script behind a feature test rather than written as plain tags:

```js
if (!window.WebAssembly || !window.addEventListener) return;
```

IE5 has neither, so it fetches neither and nothing blocks rendering. It falls
back to the real Arial, Verdana, Comic Sans MS and Tahoma that Windows 98
already ships, and to the image's real Flash 9 plugin for `apresentação.swf`.
Modern browsers get both. One build serves both.

## Anonymisation

Every phone number and every password in this copy is **fake**, randomised to
the same length and character shape as the original and derived
deterministically, so the same original always yields the same fake.

- 184 real phone numbers replaced, across `madrich/telefones.htm`,
  `madrich/chanichim.htm`, `madrich/hadracha.htm`, and the group's own number
  in `indice.htm` and `quemsomos.htm`.
- 31 username/password pairs in `madrich/index.htm` replaced. That "login" was
  never security: the credentials sat in the page source, and `madrich.htm` was
  always reachable directly.

Not touched, because they are neither phone numbers nor passwords: the 48
personal **e-mail addresses** in `madrich/telefones.htm`, and the **names and
dates of birth** of 49 people in `madrich/chanichim.htm` who were children
in 2003.
