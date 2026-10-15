# Eizport: Move your WordPress content. Not your mess.

> Pick the pages, products or posts you need — or just ask your AI agent. They arrive on the other site with their images, their settings and their homepage: no database dump, no broken images, no search-and-replace.

Free and open source. No account, no upsell, no “pro” version.

Version 1.0.1 · WordPress 7.0+ · PHP 7.4+ · GPLv2 or later

- Demo video (captions in https://eizport.github.io/video/demo.en.vtt): https://eizport.github.io/video/demo.mp4
- Try it in WordPress Playground: https://playground.wordpress.net/?blueprint-url=https://raw.githubusercontent.com/eizport/eizport/trunk/playground/blueprint.json
- Download: https://github.com/eizport/eizport/releases/latest/download/eizport.zip
- Source: https://github.com/eizport/eizport
- Docs: https://eizport.github.io/docs/ (all as Markdown: https://eizport.github.io/llms-full.txt)

## What's new in 1.0.1

- Fixed: Settings → Export → "As plugin: allow importing again" is saved.
- Scripts and styles of the classic Export screen, the importer and the Export and Settings screens are enqueued files.
- Keeping a Playground copy, which writes a file, needs the Export form's nonce.
- readme: an "External services" section on what is sent to WordPress.org, WordPress Playground and GitHub, and when.

## Sound familiar?

- **Images break after the import.** WordPress’s export only points to your media. The importer has to download every file from the old site — and if it’s offline, slow or behind a login, you get gray boxes.
- **The homepage is gone.** Settings never travel with WordPress’s export. Your static homepage, posts page, shop and checkout pages arrive as ordinary pages, and you rebuild the site by hand.
- **Migration plugins bring the junk.** Copying the whole database brings transients, logs, sessions and the tables of plugins you deleted years ago — and overwrites the site you were importing into.

## How it works

1. **Choose what moves** — On Tools → Export, check the content types or the exact items. What they use — the products a page shows, the settings that point to it — comes up as a suggestion.
2. **Get one complete file** — Content, media files, the settings that point to it and each post as readable .html — in one .wxrz or .zip.
3. **Import it anywhere** — Tools → Import opens the WordPress Importer you already know, dressed like the Export screen — or install the file as a plugin and click Run import. Media comes from the file, IDs are remapped, settings are set.

## Built for AI agents, not bolted on

Every export, import, copy and setting is an ability of the WordPress Abilities API — typed input, typed output, permissions and safety hints. Connect an agent over MCP and ask in plain words; or call the same abilities over REST, PHP and WP-CLI.

- 12 abilities with JSON schemas an agent can read
- Read-only and destructive actions flagged for the agent
- Permissions are WordPress’s: export, import, manage_options
- Docs for agents too: llms.txt and every page as Markdown

Example conversation over MCP:

- **You:** Export the homepage with its images and the basic settings as a .zip, and give me the link.
- **Agent:** calls `eizport/get-items` with `{ "type": "page", "search": "Home" }` — Found “Home” (ID 43) — it’s the homepage.
- **Agent:** calls `eizport/export` with `{ "types": { "page": { "ids": [ 43 ] } }, "options": { "groups": [ "basics" ] }, "zip": true }` — Done: home.zip (31 KB) with the page, 3 images, the homepage setting and the Basics. The link expires in a day.

More: https://eizport.github.io/docs/developers/ai-agents/

## Not a full migration. Not a bare export.

Copying the whole database drags along transients, logs, sessions and old plugins’ tables, and overwrites the target site. WordPress’s export leaves out media files, settings and the images content uses. Eizport takes only what you choose, and everything that depends on it.

| | Full-site migration | WordPress’s export | Eizport |
| --- | --- | --- | --- |
| What goes | The whole database and every file | One content type, or everything | What you choose, and what it depends on |
| Leftovers | Transients, logs, sessions, old plugins’ tables, spam | None | None: never transients, keys or caches |
| Media files | All of them | Not in the file — downloaded from the old site | Only the items’ media, inside the file |
| Media used in content | Yes, with everything else | Only attached and featured | Yes, attached or not |
| Settings | All, including the site’s URLs and users | None | The ones you choose; homepage, shop… follow their pages |
| IDs and URLs | Search-and-replace afterwards | Posts remapped; settings lost | Posts and settings remapped on import |
| Target site | Overwritten | Merged | Merged |

## Take exactly what you need — nothing else

Posts, pages, products, forms, attachments and options sit in one list. Move a store’s catalog without the blog, or a landing page without the rest. You see what each row exports before you click.

- Several content types at once
- Variations come with their products; reviews when you want them
- Nothing checked? Everything goes, as you expect

More: https://eizport.github.io/docs/exporting/export-screen/

## Hand-pick items — what they use is suggested

Open any type in a side panel, search it, filter it by status or category, and tick exactly the items you want: they join the export at once. The homepage, the shop and the checkout wear badges, and the products a page shows come up as suggestions, so you never leave a key piece behind.

- Your selection survives search and paging
- Products shown by blocks, and their reviews, suggested
- A Selected filter to review what you picked

More: https://eizport.github.io/docs/exporting/choosing-items/

## Your homepage is still your homepage

Pick a page that is the homepage, the shop or the checkout, and the settings that point to it are suggested — check Options and they come along, remapped to the new page on import. Add any other option one by one.

- Linked settings: homepage, posts page, shop, cart, checkout…
- IDs remapped to the imported pages
- Site URLs, keys, users and plugins never leave

More: https://eizport.github.io/docs/exporting/options/

## Ship a whole working site in one .zip

Export a WordPress Playground bundle with your content, its media, the theme and the plugins you choose — premium and custom ones too, not only the directory’s. Playground runs in the browser, so even a copy made on your laptop’s local server opens on playground.wordpress.net with one link.

- Works from localhost: Playground runs in your browser
- Any installed theme or plugin, premium or custom
- Or run it offline: npx @wp-playground/cli server --blueprint=site.zip

More: https://eizport.github.io/docs/formats/playground-zip/

## Send a plugin that imports itself

Turn on “As plugin” and the file becomes a plugin with the bundle inside. On the other site, install it like any plugin: its screen under Tools checks that Eizport and the WordPress Importer are there — with links to install them — and imports the bundle with Run import. No file to upload, no importer screen; when it’s done, it offers to delete itself.

- No upload, no importer screen
- Checks what it needs, with install links
- Deactivates and deletes itself when done

More: https://eizport.github.io/docs/exporting/as-plugin/

## Set it once. Every export follows.

Bring the media your content uses or only what’s attached, choose when linked settings join, make bundles plain .zip files anyone can open — and save your favorite export as the default, for you or the whole team.

- Save as default, per user or site-wide
- Plain .zip bundles on request
- WordPress’s Export screen untouched, or classic, if you prefer

More: https://eizport.github.io/docs/settings/export-settings/

## Every export kept — briefly, and out of sight

Each export is kept as a copy you can download again, open in Playground or import back. Online, its link works like a password: a random token no one can guess. Search engines are told to stay away, direct access to the folder is blocked, and a cron job deletes the copy when its time is up.

- Random 16-character token in every link
- robots.txt, noindex and a locked folder
- Expires on its own — 1 hour to 1 week, set in Settings

More: https://eizport.github.io/docs/settings/copies/

## Made for

- **Agencies and freelancers** — Move a finished section from staging to production, or a template page set from one client site to the next — without touching the rest.
- **Store owners** — Copy a product catalog with its images, variations and shop pages to a new store, merged into what’s already there.
- **Theme and plugin makers** — Package demo content with your theme or plugin as a Playground .zip, ready for reviewers and buyers.
- **Developers and AI agents** — Script every export and import through the Abilities API, REST or WP-CLI — or let an agent do it over MCP.

## Formats

| Format | File | Media files | Settings | Content as .html | Best for |
| --- | --- | --- | --- | --- | --- |
| WXR XML | `.xml` | No | No | No | WordPress’s own export, unchanged |
| WXRZ | `.wxrz` | Yes | Yes | Yes | Moving content between sites |
| WXR ZIP | `.zip` | Yes | Yes | Yes | When people will open the file |
| Playground | `.zip` | Yes | Yes | Yes | A runnable site: content, theme, plugins |
| As plugin | `.zip` | Yes | Yes | Yes | Import with one click on the other site |

## Works with

Support for a plugin is a compatibility built on public hooks. WooCommerce has one; the others weren’t tested, so here is what to expect from how they store their data.

### WooCommerce — Supported

- Products, variations, orders and coupons
- Shop, cart, checkout and account pages follow their pages
- Products shown by blocks suggested; reviews in their own row

### Advanced Custom Fields — Not officially supported yet · not tested

- Field values travel with the posts (custom fields)
- IDs inside fields (images, relationships) aren’t remapped
- Field groups: export them with ACF’s own tools

### Elementor — Not officially supported yet · not tested

- Designs travel with their pages (_elementor_data)
- Image IDs and URLs inside designs aren’t remapped
- Site kit and templates: Elementor’s Import / Export Kit

What to expect from each: https://eizport.github.io/docs/developers/compatibilities/

## For developers

Every step is an ability of the WordPress Abilities API (REST, PHP, MCP). Export a page as a .zip bundle over REST:

```bash
curl -u admin:APP_PASSWORD -X POST \
  https://example.com/wp-json/wp-abilities/v1/abilities/eizport/export/run \
  -H "Content-Type: application/json" \
  -d '{"input":{"types":{"page":{"ids":[43]}},"zip":true}}'
```

Give your plugin’s page a role:

```php
add_filter( 'eizport_linked_options', function ( $linked ) {
	$linked['my_landing_page'] = array(
		'label' => 'Landing page',
		'with'  => array( 'my_landing_enabled' ),
	);
	return $linked;
} );
```

## Questions people ask

### Is it really free?

Yes. Free and open source under the GPL, with no account, no license key and no paid version holding features back.

### Will it overwrite the site I import into?

No. It imports with the WordPress Importer, which adds the content to the site. Only the settings you chose to export are set.

### Does the old site need to be online?

No. The media files travel inside the bundle, so the importer never downloads anything from the old site.

### What about my private settings?

Site URLs, the admin email, keys and salts, users and roles, active plugins, transients and caches are never exported — whatever you pick.

### Do I need the plugin on the other site?

To import a bundle, yes (plus the free WordPress Importer). Exported “as plugin”, the file tells you so and links to both. Plain .xml exports import anywhere, as usual.

### Can the other site import without uploading a file?

Yes: export “as plugin”. Install that .zip like any plugin, click Run import on its screen under Tools, and it deletes itself when done.

### Which plugins are supported?

WooCommerce: products, orders, coupons, shop pages, galleries and reviews. Advanced Custom Fields and Elementor aren’t officially supported yet and weren’t tested: their data travels with the posts, but IDs inside it aren’t remapped.

## Stop rebuilding after every import.

Install it in a minute, export what you need, and let it arrive complete. Download: https://github.com/eizport/eizport/releases/latest/download/eizport.zip

## FAQ

### Is it safe to import a bundle from someone else?

Only import files you trust, as with any WXR file. When a bundle is opened, only the files its manifest lists are written, only under a private folder, only with file types WordPress allows to be uploaded (never PHP), and never outside that folder. The folder is deleted when the import ends or is abandoned.

### Which plugins are supported?

WooCommerce, with its own support: products, orders and coupons, its pages as linked settings, product galleries, the products its blocks show (suggested) and product reviews. Advanced Custom Fields and Elementor aren't officially supported yet and weren't tested: their data travels in custom fields, which the export carries, but IDs inside them aren't remapped on import. The docs explain what to expect: https://eizport.github.io/docs/developers/compatibilities/

### What is an "as plugin" file?

A plugin .zip that holds the bundle. Install it on the other site (Plugins → Add Plugin → Upload Plugin) and open its screen under Tools: it checks that Eizport and the WordPress Importer are there, imports the bundle with one click, and then offers to delete itself.

### Is there a size limit?

Uploads are limited by your server's PHP settings (upload_max_filesize and post_max_size), which apply to the compressed file. A bundle may expand to 512 MB by default; developers can change it with the eizport_wxrz_max_bytes filter.

### Does it send data anywhere?

Not to its authors: Eizport has no service of its own. It uses WordPress.org's plugin and theme information and downloads, as WordPress does, and opens WordPress Playground only when you click to; see "External services" for what is sent and when. When importing a bundle, the importer's attachment downloads are answered from the bundle on your own server.

### What does the Playground blueprint do?

It installs the plugins and themes in the .zip and imports the WXR with Playground's own importer. With media or content files, they are written into Playground first and a temporary must-use plugin answers the importer's downloads from the media files and puts each .html file into its post, and a second one sets the settings when the import ends, with their IDs mapped; all of it is removed after the import. The WordPress Importer is installed by Playground itself, from WordPress.org.

### Who can download a Playground copy?

Anyone with its link: the file name ends in a random 16-character token, so it can't be guessed, and it is served only until it expires (a day by default; see the plugin's Settings, where it can also be "until deleted"), then deleted. On a site on your computer (like localhost), the link only works in your own browser. Don't keep copies of content that must stay private.

### Where are the files kept?

In wp-content/uploads/eizport/tmp/: Playground copies, and the folders of bundles being imported. Everything there is temporary, and the tmp folder itself is deleted once it is empty. Uninstalling the plugin deletes uploads/eizport/ and the plugin's settings.

### Where is the source code?

The PHP is in the plugin, readable. The Export and Settings screens' JavaScript in build/ is compiled; each file ships next to its unminified version, and its source (TypeScript, in routes/ and src/) is at https://github.com/eizport/eizport — build it with npm ci && npm run build (@wordpress/build).
