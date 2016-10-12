# Aurora Cloud (Beta)

## Installation instructions

During installation process you will need:
* [Git](https://git-scm.com/downloads)
* [Composer](https://getcomposer.org/download/)
* [Node.js + NPM](https://nodejs.org/en/)

1. Clone aurora-core git repository into your installation root directory
```git
git clone https://github.com/afterlogic/aurora-core.git ./
```
2. Copy `composer.json` and `modules.json` from `https://github.com/afterlogic/aurora-bundle-files.git`

3. Download `composer.phar` from `https://getcomposer.org/composer.phar`

4. Run composer installation process by running the following from command line:
```bash
composer.phar install
```

**NB:** It is strongly advised to run composer as non-root user. Otherwise, third-party scripts will be run with root permissions and composer issues a warning that it's not safe. We recommend running the script as the same user web server runs under.

Also you can clone repositories instead of download zipballs for each package. Specify `--prefer-source` option for that:
```bash
composer.phar install --prefer-source
```

This will install modules described in modules.json. At this moment aurora-bundle-files repository contains configs for Files bundle build.

After that, you need to build static files for current module set.

First of all, install all npm modules via
```bash
npm install
```

Now you can build static files
```bash
gulp styles --themes Default,Funny
```

```bash
gulp langs --langs Arabic,Bulgarian,Chinese-Simplified,Chinese-Traditional,Czech,Danish,Dutch,English,Estonian,Finnish,French,German,Greek,Hebrew,Hungarian,Italian,Japanese,Korean,Latvian,Lithuanian,Norwegian,Persian,Polish,Portuguese-Brazil,Portuguese-Portuguese,Romanian,Russian,Serbian,Slovenian,Spanish,Swedish,Thai,Turkish,Ukrainian,Vietnamese
```

```bash
gulp js1:min --output app
```

```bash
gulp js1:min --output files-pub --modules FilesWebclient
```

Upon installing the product, you'll need to [configure your installation](/docs/{{=productAlias}}/configuration).

**IMPORTANT:**

1. Make sure data directory is writable by web server. For example:
```bash
chown -R www-data:www-data /var/www/aurora/cloud
```

2. It is strongly recommended to runs the product under **https**. If you run it under **http**, the majority of features will still be available, but some functionality aspects, such as authentication with Google account, won't work.

To enable automatic redirect from **http** to **https**, set **RedirectToHttps** to **On** in **data/settings/config.json** file.
