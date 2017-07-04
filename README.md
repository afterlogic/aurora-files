# Aurora Files (Beta)

Aurora Files is an open-source file storage platform, built to give you an ability to create your own cloud storage on your hardware by your rules. The file storage can be accessed from web browser or using native clients for Windows, iOS and Android operating systems. Alternatively you can use third-party WebDAV clients. For more informaition please visit [Aurora File home page](https://afterlogic.org/aurora-files).
Look at Aurora Files [live demo](http://aurora-files.afterlogic.com/).

![Afterlogic Webmail Pro 8: Message List](https://afterlogic.org/images/products/aurora-files/aurora-files-folder-list.png)

## Installation instructions

During installation process you will need:
* [Git](https://git-scm.com/downloads)
* [Composer](https://getcomposer.org/download/)
* [Node.js + NPM](https://nodejs.org/en/)

1. Download and unpack the latest version of aurora-files into your installation root directory (currently it's version 0.5.0)
`https://github.com/afterlogic/aurora-framework/archive/0.5.0.zip`

2. Download `composer.phar` from `https://getcomposer.org/composer.phar`

3. Run composer installation process by running the following from command line:
    ```bash
    php composer.phar install
    ```

    **NB:** It is strongly advised to run composer as non-root user. Otherwise, third-party scripts will be run with root permissions and composer issues a warning that it's not safe. We recommend running the script as the same user web server runs under.

5. Next, you need to build static files for current module set.

    First of all, install all npm modules via
    ```bash
    npm install ./modules/CoreWebclient
    ```
    and install gulp-cli module globaly 
    ```bash
    npm install --global gulp-cli
    ```

6. Now you can build static files
    ```bash
    gulp styles --themes Default,Funny
    ```

    ```bash
    gulp js:min
    ```
  
7. Now you are ready to open a URL pointing to the installation directory in your favorite web browser.

8. Upon installing the product, you'll need to [configure your installation](https://afterlogic.com/docs/aurora-files/configuration).


**IMPORTANT:**

1. Make sure data directory is writable by web server. For example:
    ```bash
    chown -R www-data:www-data /var/www/aurora/data
    ```

2. It is strongly recommended to runs the product under **https**. If you run it under **http**, the majority of features will still be available, but some functionality aspects, such as authentication with Google account, won't work.

To enable automatic redirect from **http** to **https**, set **RedirectToHttps** to **On** in **data/settings/config.json** file.

**Protecting data directory**

All configuration files of the application and user data are stored in data directory, so it's important to [protect data directory](https://afterlogic.com/docs/aurora-files/security/protecting-data-directory) to make sure that users cannot access that directory over the Internet directly. 
