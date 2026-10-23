# Eizport: Move your WordPress content. Not your mess.

> Pick the pages, products or posts you need — or just ask your AI agent. They arrive on the other site with their images, their settings and their homepage: no database dump, no broken images, no search-and-replace.

Free and open source. No account, no upsell, no “pro” version.

Version 1.1.0 · WordPress 7.0+ · PHP 7.4+ · GPLv2 or later

- Demo video (captions in https://eizport.github.io/video/demo.en.vtt): https://eizport.github.io/video/demo.mp4
- Try it in WordPress Playground: https://playground.wordpress.net/?blueprint-url=https://raw.githubusercontent.com/eizport/eizport/trunk/playground/blueprint.json
- Install: https://wordpress.org/plugins/eizport/ (or `wp plugin install eizport`)
- Source: https://github.com/eizport/eizport
- Docs: https://eizport.github.io/docs/ (all as Markdown: https://eizport.github.io/llms-full.txt)

## What's new in 1.1.0

- Added: Playground options: a Language group — the Playground .zip opens in the site's language (the default), yours or English, with the translations of WordPress, the themes and the plugins (fetched from WordPress.org, or this site's inside the .zip).
- Added: Block themes: templates and template parts edited in the Site Editor on rows of their own (Editor templates, Editor template parts), item by item with a preview. They travel in the WXR with the images they use; on import each replaces the same template of the same theme instead of adding a copy ("Header 2"), and its navigations, images and links point to the ones on the other site.
- Added: Elementor, with its own exporter and importer: a row of its own exports the site settings (the Kit) and templates in Elementor's formats; pages built with Elementor carry their design as post_content/<slug>.json; on import, Elementor's own import brings them in, with the images the bundle brought, templates and links pointing to the items there, and a later delivery updates instead of adding copies; also in Playground.
- Added: Advanced Custom Fields (ACF): a row of its own exports its post types, taxonomies and field groups in ACF's own export format, imported before the content (updated by key); the fields that store IDs (image, file, post object, relationship, page link, taxonomy, user) are remapped on import, also in Playground; field groups, linked posts and the media of image and file fields are suggested or come along.
- Added: Bundles say which Eizport made them and the oldest that reads them: a bundle that needs a newer Eizport is refused with a message that says which version (on the upload, wp eizport import, the import ability and a bundle plugin's screen, which offers Update now); bundles from 1.0.x still import. The WordPress Importer must be 0.9.6 or newer; a version newer than the tested one imports with a warning. The manifest names its JSON Schema (https://eizport.github.io/schemas/1.1/manifest.json): editors check a manifest edited by hand, and the import checks it against the same schema.
- Added: Multisite: each site of a network exports and imports on its own — saved defaults per site, files in the site's uploads, links mapped between subsites — and uninstalling cleans every site.
- Added: Export the site's look on rows of its own, item by item — Customizer theme mods and custom CSS rules, the Site Editor's style groups and CSS rules, widgets (classic and block) — with a preview of each and the media they use. On import, CSS rules are added to the other site's CSS (at the end, at the start, or replacing it) between head/tail comments named after the file; theme mods, style groups and widgets join the other site's instead of replacing them.
- Added: Export navigation menus on their own row — classic menus with their items and theme locations, and block navigations — and bring them back on import, pointing to the imported pages.
- Added: Playground options: must-use plugins — the ones chosen go in the Playground .zip with the folders they load, and the blueprint writes them before the import (not the platform's loaders nor Eizport's own).
- Added: Playground options: the button (renamed from "Themes and plugins") also sets where the Playground .zip opens — the home page, the dashboard, a page of the site (as a relative path) or a path —, its two groups open one at a time.
- Changed: The plugin's row on the Plugins screen keeps only Settings: no "Import .wxrz" or "Install the WordPress Importer" link — importing starts from Tools → Import.
- Changed: A bundle plugin's screen is one screen, with or without Eizport: Eizport is one more line in Before importing (Install Now, Activate or Update now, done right there), and what needs it waits — What it holds dimmed, Update existing and Run import disabled. The screen is no longer an item under Tools: Run import, on the plugin's row on the Plugins screen, opens it. Tools → Import lists it too, set apart from the other importers, and shows the list while it waits. "Update existing" names the content types the export holds — on the Export screen, the importer's step 1 and a bundle plugin's screen — and isn't offered with none.
- Changed: The Options row's Basics and Appearance groups no longer carry the theme mods (they have their own row) and now carry the block themes' site logo; imported theme mods are merged into the site's instead of replacing them.
- Changed: What a file holds no longer decides on its own: an import sets the options of the groups, the theme mods and the widgets, and any other option in the file only when whoever imports checks it (step 1 of the importer, a bundle plugin's screen) or names it (--options, the ability's options); WP-CLI and the ability update existing items only when asked. Options, theme mods and widget fields named like secrets (passwords, tokens, API and license keys) are never exported nor listed. On a network, a site administrator's Playground .zip takes only the plugins active on that site and the themes it may use.
- Changed: Bundles are plain .zip files by default (Settings → Export → "Bundle as .zip" now on), inside a plugin made as plugin too; turned off, they are .wxrz as before.
- Fixed: Imported content keeps working with its media and pages: the IDs in Image, Gallery, Cover, Media & Text, File, Video and Audio blocks, in navigation links and in block widgets point to the imported items, not to the other site's.
- Fixed: Links to the source site in imported content — pages, products, categories, navigation links, menus' custom links, widgets — point to this site after an import, in new and updated items.
- Fixed: An attachment the site already has gets its URLs in the imported content pointed to the file here on every import, not only with "Update existing" on.
- Fixed: Checked with the WordPress Importer 0.9.7: an edited image's link to its original is mapped on import instead of dropped (or left pointing at the exporting site's ID with 0.9.6).
- Fixed: The Playground .zip installs a theme or plugin from the WordPress.org directory only in a version the directory has; a development, beta or RC copy goes inside the .zip. Without Eizport, a bundle plugin installs it from the plugin directory.
- Fixed: An export of chosen types carries its terms in full — description, parent and term meta (a product category's thumbnail and display type), with their ancestors — not only their names.
- Fixed: The Playground .zip installs plugins active or inactive as they are on the site, instead of activating them all.
- Fixed: A .zip bundle is read in blocks against its real size (an entry that says it is small but inflates to more is refused, and no entry is loaded whole in memory), and needs PHP's ZipArchive; "Run import" only runs for a bundle plugin active on the site; the Playground landing page only opens a path of the exported site; uninstall also removes the note of imported widgets.
- Fixed: Importing a file made elsewhere is safer for users who may not post unfiltered HTML (a site admin on a network): templates, template parts and widgets from the file go through the same HTML filter as other content, custom CSS needs the right to edit CSS, Advanced Custom Fields items need ACF's own capability and never bring PHP callbacks, an existing page keeps its Elementor design unless the import updates existing items, and a malformed source address in the file never rewrites links.

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

Install it in a minute, export what you need, and let it arrive complete. Install: https://wordpress.org/plugins/eizport/

## FAQ

### Is it safe to import a bundle from someone else?

Only import files you trust, as with any WXR file. When a bundle is opened, only the files its manifest lists are written, only under a private folder, only with file types WordPress allows to be uploaded (never PHP), and never outside that folder. The folder is deleted when the import ends or is abandoned.

### Which plugins are supported?

WooCommerce, with its own support: products, orders and coupons, its pages as linked settings, product galleries, the products its blocks show (suggested) and product reviews. Advanced Custom Fields (ACF), with its own support too: its post types, taxonomies and field groups on a row of their own, in ACF's export format, imported before the content, and the fields that store IDs (image, file, post object, relationship, page link, taxonomy, user) remapped on import. Elementor, with its own support as well, through Elementor's own exporter and importer: its site settings (the Kit) and templates on a row of their own, each page's design as a .json file, and on import the images, templates and links inside them pointing to the items on the other site. The docs explain what to expect: https://eizport.github.io/docs/developers/compatibilities/

### What is an "as plugin" file?

A plugin .zip that holds the bundle. Install it on the other site (Plugins → Add Plugin → Upload Plugin) and click Run import on its row on the Plugins screen: it checks that Eizport and the WordPress Importer are there, imports the bundle with one click, and then offers to delete itself.

### Does it work on multisite?

Yes. Activate it on the network or on each site: every site exports and imports on its own (its files in its own uploads folder, its own saved defaults), links are mapped between subsites, and uninstalling cleans every site. Site administrators export and import; WordPress filters imported content for those who can't post unfiltered HTML. Docs: https://eizport.github.io/docs/getting-started/multisite/

### Is there a size limit?

Uploads are limited by your server's PHP settings (upload_max_filesize and post_max_size), which apply to the compressed file. A bundle may expand to 512 MB by default; developers can change it with the eizport_wxrz_max_bytes filter.

### Does it send data anywhere?

Not to its authors: Eizport has no service of its own. It uses WordPress.org's plugin and theme information and downloads, as WordPress does, and opens WordPress Playground only when you click to; see "External services" for what is sent and when. When importing a bundle, the importer's attachment downloads are answered from the bundle on your own server.

### What does the Playground blueprint do?

It installs the plugins and themes in the .zip, sets the language chosen (with its translations), writes the must-use plugins chosen (with the folders they load) and imports the WXR with Playground's own importer. With media or content files, they are written into Playground first and a temporary must-use plugin answers the importer's downloads from the media files and puts each .html file into its post, and a second one sets the settings when the import ends, with their IDs mapped; all of it is removed after the import. The WordPress Importer is installed by Playground itself, from WordPress.org.

### Who can download a Playground copy?

Anyone with its link: the file name ends in a random 16-character token, so it can't be guessed, and it is served only until it expires (a day by default; see the plugin's Settings, where it can also be "until deleted"), then deleted. On a site on your computer (like localhost), the link only works in your own browser. Don't keep copies of content that must stay private.

### Where are the files kept?

In wp-content/uploads/eizport/tmp/: Playground copies, and the folders of bundles being imported. Everything there is temporary, and the tmp folder itself is deleted once it is empty. Uninstalling the plugin deletes uploads/eizport/ and the plugin's settings.

### Where is the source code?

The PHP is in the plugin, readable. The Export and Settings screens' JavaScript in build/ is compiled; each file ships next to its unminified version, and its source (TypeScript, in routes/ and src/) is at https://github.com/eizport/eizport — build it with npm ci && npm run build (@wordpress/build).
