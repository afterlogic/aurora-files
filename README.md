# Aurora Cloud (Beta)


## Installation instructions

During installation process you will need:
- [Git](https://git-scm.com/downloads)
- [Composer](https://getcomposer.org/download/)
- [Node.js + NPM](https://nodejs.org/en/)

1. Clone aurora-core git repository into your installation root directory
```  
git clone https://github.com/afterlogic/aurora-core.git ./
```

2. Copy `composer.json` and `modules.json` from `https://github.com/afterlogic/aurora-bundle-files.git`

3. Download `composer.phar` from `https://getcomposer.org/composer.phar`

4. Run composer installation process from command line with 
```bash
composer.phar install
```

This will install modules described in modules.json. At this moment aurora-bundle-files repository contains configs for Files bundle build.

After that, you need to build static files for current module set.

First of all, install all npm modules via
```
npm install
```
Now you can build static files
```
gulp styles --themes Default,Funny
```
```
gulp langs --langs Arabic,Bulgarian,Chinese-Simplified,Chinese-Traditional,Czech,Danish,Dutch,English,Estonian,Finnish,French,German,Greek,Hebrew,Hungarian,Italian,Japanese,Korean,Latvian,Lithuanian,Norwegian,Persian,Polish,Portuguese-Brazil,Portuguese-Portuguese,Romanian,Russian,Serbian,Slovenian,Spanish,Swedish,Thai,Turkish,Ukrainian,Vietnamese
```
```
gulp js1:min --output app
```
```
gulp js1:min --output files-pub --modules FilesWebclient
```

Now you are ready to configure you fresh installation of AfterLogic platform.

## Support


