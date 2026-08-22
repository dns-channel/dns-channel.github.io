# dns-channel.github.io

Source for the information page of the **#dns** channel on the [Libera.Chat](https://libera.chat/)
IRC network.

The channel topic in #dns was getting too long to hold everything people kept asking for, so the links,
version numbers and reading material live here instead: a single, curated, hand-maintained page
about DNS software, services and documentation.

- **Live site:** <https://dns-channel.github.io/> (also mirrored to `dns-channel.info`)
- **Channel:** the `#dns` channel on Libera.Chat

## What's on the page

| Section | Contents |
| --- | --- |
| New root hints | How to fetch current root hints with `dig`/`drill`/`kdig`, plus the IANA sources |
| New root DNSSEC KSK | Notes and links about the October 2018 root trust anchor rollover |
| Software → Nameservers or proxies | Authoritative servers, recursors, proxies and load balancers, with current versions and a short "what it is" |
| Software → Tools | CLI, web and GUI tooling: lookup, DNSSEC validation, delegation checking, benchmarking, packet capture and stats |
| Service providers → Authoritative | Hosted authoritative DNS providers |
| Service providers → Recursor | Public and hosted recursive resolvers |
| Reading material | RFCs, books, articles, presentations and other background reading |
| Why does this site exist? | The short history above |

## Repository layout

```
index.html    the entire site: one hand-written HTML 4.01 Transitional document
.travis.yml   CI job that mirrors index.html to the dns-channel.info FTP host
README.md     this file
```

There is no build step, no framework and no dependencies. `index.html` is the site.
Open it directly in a browser to preview a change.

## How it's published

Two independent paths, both from `master`:

1. **GitHub Pages** serves `index.html` at `dns-channel.github.io` on push.
2. **Travis CI** (`.travis.yml`) uploads the same file to `ftp.dns-channel.info` using the
   `FTP_USERNAME` / `FTP_PASSWORD` secrets, restricted to the `master` branch.

## Contributing

Pull requests are welcome, and most of them are small: a bumped version number, a new tool, or a
link that has since gone dead.

**Adding or updating an entry**

Entries are plain table rows. Keep them alphabetical within their table and match the surrounding
style:

```html
<tr><td><a target="_blank" href="https://example.org/">Name</a></td><td>1.2.3</td><td>cli: one-line description of what it does</td></tr>
```

- The **Version** column is the current stable release; leave it empty for hosted web services that
  don't publish one.
- Use `target="_blank"` on outbound links, as the rest of the page does.
- The **Type** column is a one-line description of what the entry does. In the Tools table it is
  prefixed with how you actually interact with the thing, so a reader scanning the table can tell at
  a glance whether it is something to install or something to open in a browser:

  | Prefix | Meaning |
  | --- | --- |
  | `cli:` | A command-line program, or a library shipping command-line utilities. You install and run it locally. |
  | `web:` | A hosted service you use in a browser. Nothing to install, but you are handing your query to a third party. |
  | `gui:` | A desktop or graphical application. |
  | `server:` | Something you run as a long-lived service rather than invoking per query. |

  Combine them with `&amp;` when an entry is genuinely both, as in `cli &amp; web:` for something
  that is a hosted site *and* a package you can run yourself. Add a further note after the prefix
  when the interface needs qualifying, as `cli &amp; ncurses interactive:` does.

  The Nameservers or proxies table does not use these prefixes: everything in it is a server, so its
  Type column describes the role instead (`authoritative`, `validating resolver`, `proxy`, and so on).

**Dead links**

The page deliberately keeps historically interesting but defunct projects. Rather than deleting
them, note that the link is broken and add a [Web Archive](https://web.archive.org/) link, following
the existing entries for Posadis, SANS and DNSBajaj.

**Style constraints**

- The document declares HTML 4.01 Transitional and is kept valid against it. Attributes that don't
  exist in that DTD are not used, even when GitHub hands you a snippet containing them.
- No CSS framework, no JavaScript, no external assets. The page should stay readable in any browser
  and load instantly.
- Anchors (`<a name="...">`) are linked from the table of contents at the top; if you add a section,
  add it there too.

Open a PR against `master` and it will be picked up by both publishing paths once merged.
