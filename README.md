# quark2llp Theme

**quark2llp** is a Grav 2.1+ theme based on the modernized Quark 2 theme, using [Blades CSS](https://github.com/anyblades/blades), [Font Awesome 7](https://fontawesome.com), and a Cal.com-inspired design system.

## Features

* Modernized Cal.com-inspired design system — monochrome palette, refined shadow hierarchy, generous whitespace
* [Blades CSS](https://github.com/anyblades/blades) v2 foundation (the maintained Pico CSS successor, fully `--pico-*` compatible) — no framework grid, just semantic HTML + CSS custom properties
* **Cal Sans** display + **Inter** body fonts, hosted locally as woff2 (latin + latin-ext subsets)
* [Font Awesome 7](https://fontawesome.com) free icon set (CDN by default, with an option to self-host)
* **Auto / Light / Dark** appearance with `localStorage` persistence and OS-preference fallback — no flash-of-unstyled-content thanks to a pre-paint bootstrap
* Configurable **accent color** via the admin color picker — tints links, focus rings, primary buttons, and other filled accents
* Fully responsive with a full-page mobile navigation overlay
* Multi-level dropdown navigation with hover-bridge and touch support
* Sticky, animated header that condenses on scroll
* Full light-mode **and** dark-mode palettes for every component
* First-class support for the [`github-markdown-alerts`](https://github.com/getgrav/grav-plugin-github-markdown-alerts) plugin (replacing `markdown-notices`)
* Built-in support for on-page navigation (single-page sites)
* Multiple page template types out of the box

### Supported Page Templates

* Default view template `default.md`
* Error view template `error.md`
* Blog view template `blog.md`
* Blog item view template `item.md`
* Comments view template `comments.md`
* Modular view template `modular.md`
  * Features Modular view template `features.md`
  * Hero Modular view template `hero.md`
  * Text Modular view template `text.md`
  * Gallery Modular view template `gallery.md` renders its image grid without additional plugins; images link to their full-size files.
  * Practice modules: Contact and Opening Hours, Services, Practice Team, Parking, Emergency Numbers, and Current Notice

Practice modules are available for single-page modular sites. Add each section as a modular child page using the matching blueprint, then set its menu label and upload any portraits or photos to that page. The Current Notice opens as a dialog, can be dismissed for the current browser session, and remains available from its page button. Add Impressum and Datenschutz destinations in the theme's **Footer Links** option; a custom theme logo is shown in both the header and footer.

# Installation

Install quark2llp by placing its folder in your Grav site's `user/themes` directory. Name the folder `quark2llp` so Grav resolves the theme slug and class correctly.

The theme is designed for Grav 2.1+.

## GPM Installation (Preferred)

If quark2llp is published to GPM, install it from the Grav root with:

    bin/gpm install quark2llp

This installs the theme under `/user/themes/quark2llp`.

## Manual Installation

For a manual installation, place the theme folder under `/your/site/grav/user/themes` and name it `quark2llp`.

You should now have all the theme files under

    /your/site/grav/user/themes/quark2llp

## Default Options

quark2llp comes with a few default options that can be set site-wide. These options are:

```yaml
enabled: true                 # Enable the theme
header-fixed: true            # Causes the header to be sticky at the top of the browser
header-animated: true         # Allows the fixed header to condense when scrolled
header-transparent: false     # Lets the header sit transparent over a hero, filling in once scrolled
sticky-footer: true           # Causes the footer to stay pinned to the bottom of short pages
theme-mode: auto              # Default appearance before the user makes a choice: auto | light | dark
accent-color: '#242424'       # Hex color used for links, focus rings, and filled accents (charcoal by default)
blog-page: '/blog'            # The route to the blog listing page, used for a blog-style layout with sidebar
custom_logo:                  # A custom logo instead of the default Grav mark (see below)
custom_logo_mobile:           # A custom logo to use for the mobile overlay
fontawesome:
  enabled: true               # Load Font Awesome 7 free
  local: false                # true = expect css/fontawesome/all.min.css in the theme; false = load from CDN
```

To make modifications, copy `user/themes/quark2llp/quark2llp.yaml` to `user/config/themes/quark2llp.yaml`, or use the Admin plugin.

> [!IMPORTANT]
> Do not modify the theme's `quark2llp.yaml` file directly or your changes will be lost with any updates.

## Appearance (Light / Dark / Auto)

quark2llp ships with a three-state appearance toggle in the header. The user's choice is stored in `localStorage` under `quark2llp-theme`; existing `quark2-theme` preferences are migrated automatically. When the mode is **Auto**, the theme follows the operating system's `prefers-color-scheme` preference and reacts live to OS-level changes.

The default state for first-time visitors is controlled by the `theme-mode` option above.

A pre-paint inline script in `partials/base.html.twig` sets `data-theme` before the first browser paint, eliminating any flash between light and dark on initial load.

## Accent Color

The `accent-color` option accepts any hex color (picker available in the admin) and drives:

* `--q2-link` — text and underline color for links
* `--q2-accent` — filled accents (primary buttons, etc.)
* `--q2-focus-ring` — translucent focus outline, derived via `color-mix(in oklab, …, transparent)`

Dark mode lightens the accent slightly to keep it readable on the dark canvas. Leave the default `#242424` for the pure monochrome look.

## Custom Logos

To add a custom logo, put the logo file into `user/themes/quark2llp/images/logo`. Standard image formats are supported (`.png`, `.jpg`, `.gif`, `.svg`, etc.). Then reference the logo via the YAML like so:

```yaml
custom_logo:
    - name: 'my-logo.png'
custom_logo_mobile:
    - name: 'my-mobile-logo.png'
```

Alternatively, use the drag-n-drop **Custom Logo** field in quark2llp theme options.

SVG logos are inlined and inherit `currentColor`, so they automatically adapt to light/dark mode when you set `fill="currentColor"` on their paths.

Your logo lives inside the theme folder and is left alone when you update quark2llp.

## Page Overrides

Pages can override some default options by setting `body_classes`; the theme merges these with the defaults. For example:

```yaml
body_classes: "header-transparent"
```

On a particular page will ensure that page has those options enabled (assuming they are false by default).

## Hero Options

The hero template allows some options to be set in the page frontmatter. This is used by the modular `hero` as well as the blog and item templates to provide a more dynamic header.

```yaml
hero_classes: text-light parallax overlay-dark-gradient hero-large
hero_image: road.jpg
hero_align: center
```

The `hero_image` should point to an image file in the current page folder. When a hero image is present, the theme automatically darkens the overlay and forces white text for legibility.

## Features Modular Options

The features modular template provides the ability to set a class on the features, as well as an array of feature items. For example:

```yaml
class: offset-box
features:
    - header: Crazy Fast
      text: "Performance is not just an afterthought, we baked it in from the start!"
      icon: fighter-jet
    - header: Easy to build
      text: "Simple text files means Grav is trivial to install, and easy to maintain"
      icon: database
    - header: Awesome Technology
      text: "Grav employs best-in-class technologies such as Twig, Markdown &amp; Yaml"
      icon: cubes
    - header: Super Flexible
      text: "From the ground up, with many plugin hooks, Grav is extremely extensible"
      icon: object-ungroup
    - header: Abundant Plugins
      text: "A vibrant developer community means over 200 themes available to download"
      icon: puzzle-piece
    - header: Free / Open Source
      text: "Grav is an open source project, so you can spend your money on other stuff"
      icon: money-bill
```

Icons use Font Awesome 7 free names — see the [Font Awesome icon gallery](https://fontawesome.com/icons?d=gallery&m=free).

## Text Modular Options

The text box provides a single option to control if any image found in the page folder should be left or right aligned:

```yaml
image_align: right
```

## Blog Listing Options

The blog listing template responds to a few per-page header options:

```yaml
show_breadcrumbs: true        # Show the breadcrumbs (requires the breadcrumbs plugin)
show_sidebar: false           # Show the sidebar with related posts, archives, etc.
show_pagination: true         # Show the pagination below the listing
```

When `show_sidebar` is true but no sidebar plugins are enabled, the sidebar gracefully collapses so the cards take the full width.

## Customization

### Custom CSS

The theme loads `css/custom.css` last. Any rules placed there win over the theme's own styles without needing `!important`. This is the safest place to add site-specific tweaks without modifying the theme itself (so you can still pull in theme updates).

### Design tokens

All colors, radii, and shadows are defined as CSS custom properties on `:root` and `:root[data-theme='dark']` in `css/theme.css` (prefix: `--q2-`). Override them in `custom.css` to re-skin without touching the theme source.

### Custom fonts

The fonts are driven by three CSS variables, set on `:root` in `css/theme.css`:

```css
--pico-font-family-display;      /* Cal Sans — headings and other display text */
--pico-font-family-sans-serif;   /* Inter — body copy and UI text */
--pico-font-family-monospace;    /* code, pre, kbd, samp */
```

Every heading, paragraph, button, and label reads its font from one of these, so you can swap the display or body face for the whole theme from `custom.css` with a single line — no need to hunt through the stylesheet:

```css
:root {
  --pico-font-family-display: "Playfair Display", serif;
  --pico-font-family-sans-serif: "Helvetica Neue", system-ui, sans-serif;
}
```

If your replacement face is not a system font, load it first (a `@font-face` block in `custom.css`, or a `<link>` to a hosted stylesheet) the same way the bundled Cal Sans and Inter faces are declared in `css/fonts.css`.

### Updating the CSS foundation

The base CSS comes from [Blades CSS](https://github.com/anyblades/blades) and ships pre-built as `css/blades.min.css`. The version is pinned in `package.json`. To rebuild it:

    npm install      # installs the pinned Blades release + the minifier
    npm run build    # writes css/blades.min.css

To move to a newer Blades release:

    npm update @anyblades/blades && npm run build

`node_modules` is git-ignored and only the built `css/blades.min.css` is committed, so sites installing the theme need no Node toolchain.

## Disqus / JSComments dark-mode workaround

quark2llp's accent tints use the modern CSS `color-mix(in oklab, …)` function. Browsers serialize the computed result as `oklab(…)` (or `color(srgb …)` for `in srgb`). Disqus's embed.js ships an older color parser that does not understand either form, and it throws an exception sampling computed styles, which prevents the comments thread from initializing on first paint in dark mode. (Light mode works because the un-mixed accent stays as plain hex.)

This is a Disqus-specific issue and the rest of the theme has no reason to compromise on `color-mix`, so the fix is opt-in. If you embed Disqus (typically via the [JSComments plugin](https://github.com/getgrav/grav-plugin-jscomments)) and want dark mode to work, copy `partials/base.html.twig` into your child theme (or override it inline) and add the following block just after the existing `:root[data-theme='dark']` style block:

```twig
{% if config.plugins.jscomments.enabled %}
<style>
  #disqus_thread {
    --q2-accent: {{ q2_mix_white(accent, 80) }};
    --q2-link: {{ q2_mix_white(accent, 75) }};
    --q2-focus-ring: {{ q2_mix_alpha(accent, 45) }};
  }
</style>
{% endif %}
```

The `q2_mix_white(hex, pct)` and `q2_mix_alpha(hex, pct)` Twig functions are shipped by the theme (registered in `quark2llp.php`) and return pre-resolved `rgb(…)` / `rgba(…)` strings. Scoping the override to `#disqus_thread` keeps the rest of the page on full `oklab` mixing, and only the Disqus widget sees the pre-resolved values that its parser understands.

## License

MIT
