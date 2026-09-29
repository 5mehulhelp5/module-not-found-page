# Magento 2 Custom 404 Not Found Page

Replaces the content of the Magento 2 "page not found" page with a configurable layout: a heading and message you set in the admin, a product search box, links to the store's top-level categories and a contact email. The page keeps Magento's HTTP 404 status and its own header and footer; only the content area changes.

It is meant for store owners who want visitors landing on a dead link to find their way back into the catalogue instead of seeing the default CMS 404 text. Works with the Hyva and Luma themes.

Product page: [kishansavaliya.com/magento-2-not-found-page.html](https://kishansavaliya.com/magento-2-not-found-page.html)

## Features

- Editable heading and subheading text.
- Search box that submits to Magento's catalog search (`catalogsearch/result`).
- "Back to Homepage" and "Go Back" buttons.
- Links to up to six top-level categories of the current store (active, included in the menu, ordered by position).
- Optional contact line with a mailto link to the address you configure.
- Every setting can be set per default, website or store view, so each store view can have its own 404 content.
- Renders with its own inline styles on both Hyva and Luma; no theme files need to be changed.
- No database tables, no cron jobs and no console commands.

## Compatibility

| | |
|---|---|
| Magento Open Source / Adobe Commerce | 2.4.4 to 2.4.8 |
| PHP | 8.1, 8.2, 8.3, 8.4 |
| Themes | Hyva and Luma |

The Composer package requires `magento/framework ^103.0`, `magento/module-store ^101.1`, `magento/module-config ^101.2`, `magento/module-cms ^104.0` and `magento/module-catalog ^104.0`.

## Requirements

- Magento 2.4.4 or later
- PHP 8.1 to 8.4
- `mage2kishan/module-core` (installed automatically by Composer; provides the shared "Panth Extensions" admin tab)

## Installation

```bash
composer require mage2kishan/module-not-found-page
bin/magento module:enable Panth_Core Panth_NotFoundPage
bin/magento setup:upgrade
bin/magento setup:di:compile
bin/magento cache:flush
```

`setup:di:compile` is only needed in production mode. The page styles are inline in the template, so no static content deployment is required.

Check the result with:

```bash
bin/magento module:status Panth_NotFoundPage
```

Then open any URL on your store that does not exist, for example `/this-page-does-not-exist`.

## Configuration

Go to **Stores > Configuration > Panth Extensions > 404 Not Found Page**.

General:

| Setting | Default | What it does |
|---|---|---|
| Enable Custom 404 Page | Yes | Renders the custom content on the 404 page. |

Page Content:

| Setting | Default | What it does |
|---|---|---|
| Heading | Page Not Found | Large heading at the top of the page. |
| Subheading Message | Oops! The page you're looking for doesn't exist or has been moved. | Text shown under the heading. Leave empty to hide it. |
| Show Search Bar | Yes | Shows the search form. |
| Show Popular Links | Yes | Shows the "Browse Categories" links. |
| Show Contact Information | Yes | Shows the "Need help?" line with the contact email. |
| Contact Email | support@example.com | Address used in the contact line. Change this before going live. |

Configuration paths: `panth_notfound/general/enabled`, `panth_notfound/content/heading`, `panth_notfound/content/subheading`, `panth_notfound/content/show_search`, `panth_notfound/content/show_popular_links`, `panth_notfound/content/show_contact_info`, `panth_notfound/content/contact_email`.

Note: the module's layout removes Magento's default 404 content whenever the module is enabled in Magento. Setting "Enable Custom 404 Page" to No therefore hides the custom content and leaves the page with only the header and footer. To get the stock Magento 404 page back, disable the module (see Uninstallation).

## Usage

Nothing else needs to be set up. Whenever Magento serves its "no route" page (`cms/noroute/index`), the module's block renders inside the page wrapper with the configured heading, message, search form, category links and contact line. The response status stays 404 and the page title is set to "404 - Page Not Found".

Category links are read live from the catalog: the direct children of the store's root category that are active and included in the navigation menu, at most six, in position order. If none qualify, the section is left out.

The template can be overridden in a theme at `Panth_NotFoundPage/templates/notfound.phtml`.

## Developer Notes

- Module name: `Panth_NotFoundPage`
- Composer package: `mage2kishan/module-not-found-page`
- PHP namespace: `Panth\NotFoundPage`
- Layout handle: `cms_noroute_index`; block `panth.notfound.page` (`Panth\NotFoundPage\Block\NotFound`)
- Config helper: `Panth\NotFoundPage\Helper\Data`

## Uninstallation

To return to the stock Magento 404 page while keeping the package installed:

```bash
bin/magento module:disable Panth_NotFoundPage
bin/magento cache:flush
```

To remove the package:

```bash
bin/magento module:disable Panth_NotFoundPage
composer remove mage2kishan/module-not-found-page
bin/magento setup:upgrade
bin/magento setup:di:compile
bin/magento cache:flush
```

The module creates no database tables. Its configuration values remain in `core_config_data` until removed.

## Support

- Product page: [kishansavaliya.com/magento-2-not-found-page.html](https://kishansavaliya.com/magento-2-not-found-page.html)
- Contact: [kishansavaliya.com/contact](https://kishansavaliya.com/contact)
- Email: kishansavaliyakb@gmail.com
- Bug reports: [GitHub issues](https://github.com/mage2sk/module-not-found-page/issues)

## Documentation

- [USER_GUIDE.md](USER_GUIDE.md): installation, configuration, customization tips and troubleshooting for store administrators.

## License

Commercial software license. See [LICENSE.txt](LICENSE.txt) in this repository.

## Changelog

See [CHANGELOG.md](CHANGELOG.md).

## Links

- Website: [kishansavaliya.com](https://kishansavaliya.com)
- All extensions: [kishansavaliya.com/magento-extensions.html](https://kishansavaliya.com/magento-extensions.html)
- GitHub: [mage2sk/module-not-found-page](https://github.com/mage2sk/module-not-found-page)
- Packagist: [mage2kishan/module-not-found-page](https://packagist.org/packages/mage2kishan/module-not-found-page)
