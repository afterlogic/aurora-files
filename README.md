[![Build Status](https://travis-ci.org/afterlogic/aurora-files.svg?branch=master)](https://travis-ci.org/afterlogic/aurora-files)

# Aurora Files

Aurora Files is an open-source file storage platform, built to give you an ability to create your own cloud storage on your hardware by your rules. The file storage can be accessed from web browser or using native clients for Windows, iOS and Android operating systems. Alternatively you can use third-party WebDAV clients. For more informaition please visit [Aurora File home page](https://afterlogic.org/aurora-files).
Look at Aurora Files [live demo](https://aurora-files.afterlogic.com/).

![Afterlogic Aurora Files: Files List](https://afterlogic.org/images/products/aurora-files/aurora-files-folder-list.png)

Aurora Files includes Paranoid Encryption module which provides strong AES-256 browser-based encryption. File content is transmitted to the server in encrypted form only, encryption keys are never transmitted to the server at all. Thus, even if the entire data from the server was stolen, your encrypted data is still safe: any data on the server cannot help decrypt encrypted files without the keys.

## Installation instructions

During installation process you will need:
* [Git](https://git-scm.com/downloads)
* [Composer](https://getcomposer.org/download/)
* [Node.js + NPM](https://nodejs.org/en/)
    
    **Note!** Version of npm above 3 is required

1. Download and unpack the latest version of Aurora Files into your installation root directory
[`https://github.com/afterlogic/aurora-files/archive/latest.zip`](https://github.com/afterlogic/aurora-files/archive/latest.zip)

We're assuming that you wish to install the latest stable version of the product. If you're looking for the latest code (e.g., to contribute changes), the following steps needs to be taken:

- Instead of unpacking the archive, clone the repository into the installation directory:
```
git clone https://github.com/afterlogic/aurora-files.git INSTALL_FOLDER_PATH
```
- change modules' versions in `composer.json` file to "dev-master"

1. `composer.phar` file is available in repository, but you can download its latest version 2 from [`https://getcomposer.org/composer.phar`](https://getcomposer.org/composer.phar)

2. Run composer installation process by running the following from command line:
    ```bash
    php composer.phar install
    ```

    **NB:** It is strongly advised to run composer as non-root user. Otherwise, third-party scripts will be run with root permissions and composer issues a warning that it's not safe. We recommend running the script as the same user web server runs under.

3. Next, you need to build static files for the current module set.
      First of all, install all npm dependencies via
      ```bash
      npm install
      ```
      then install the dependencies required for adminpanel to work 
      ```bash
      cd modules/AdminPanelWebclient/vue
      npm install
      npm install -g @quasar/cli
      ```
	  or you can execute all the actions mentioned above by using the following command
	  ```
	  chmod +x builder.sh
	  ./builder.sh -t npm
	  ```

4. Now you can build static files. Run the following commands in main directory
      ```bash
	  npm run styles:build --themes=Default,DefaultDark,DeepForest,Funny,Sand
      npm run js:build
	  npm run js:min
      ```
      and build adminpanel 
      ```bash
      cd modules/AdminPanelWebclient/vue
      npm run build-production
      ```
	  or use all-in-one command
	  ```
	  ./builder.sh -t build
	  ```
5. In case you want to use the product in development mode and work with JS, you need to run webpack dev server. But before that rename .env.dist to .env and specify the Web API host. For example, `http://localhost/aurora/`.
Please note that if the backend responds on a domain other than localhost, you will have to specify custom headers in the index.php file to avoid CORS blocking cross-domain requests.

    Now you can run webpack dev server:
    ```
    npm run serve
    ```

    This will compile JS script files. If you need to work with CSS, you need to run the following command:
    ```
    npm run styles:watch --themes=Default,DefaultDark,DeepForest,Funny,Sand
    ```

    You can modify the themes list and specify the themes you are currently working with.
    
6. Now you are ready to open a URL pointing to the installation directory in your favorite web browser. Be sure to add `/adminpanel/` to main URL to access admin interface.

7. Upon installing the product, you'll need to [configure your installation](https://afterlogic.com/docs/aurora-files/configuration).


**IMPORTANT:**

1. Make sure data directory is writable by web server. For example:
    ```bash
    chown -R www-data:www-data /var/www/aurora/data
    ```

2. It is strongly recommended to runs the product under **https**. If you run it under **http**, the majority of features will still be available, but some functionality aspects, such as authentication with Google account, won't work.

To enable automatic redirect from **http** to **https**, set **RedirectToHttps** to **On** in **data/settings/config.json** file.

**Protecting data directory**

All configuration files of the application and user data are stored in data directory, so it's important to [protect data directory](https://afterlogic.com/docs/aurora-files/security/protecting-data-directory) to make sure that users cannot access that directory over the Internet directly. 

# Licensing
This product is licensed under AGPLv3. The modules and other packages included in this product as dependencies are licensed under their own licenses.

NB: Afterlogic Aurora modules which have dual licensing are licensed under AGPLv3 within this product.
