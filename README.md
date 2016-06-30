# DF
[![Travis build status](https://img.shields.io/travis/acquia/df/8.x-1.x.svg)](https://travis-ci.org/acquia/df) [![Scrutinizer code quality](https://img.shields.io/scrutinizer/g/acquia/df/8.x-1.x.svg)](https://scrutinizer-ci.com/g/acquia/df)

DF is a distribution consisting of modules, themes and libraries. It highlights powerful features created by the Drupal community. It is intended to be used as a starterkit for promoting enterprise-ready solutions.

### Installation

Although Drush make files are still made available, we recommend using Composer to install DF.

  ``composer install``

DF and its dependencies will be downloaded into the current working directory. If nothing fails, you will see a 'docroot' with Drupal in it.

We provide a build script that wraps the composer install command and moves everything into a target directory as well.

  ``./build.sh ~/Destination``

You can also add in commands for composer here. We suggest using the --no-dev option unless you want to run behat and have DF manage your version of Drush used on the site.

  ``./build.sh ~/Destination --no-dev``

At this point, you will need to prepare your settings.php file just as you would for a normal Drupal install.

We recommend Acquia Dev Desktop running ``PHP 5_6`` and using the ``Import local Drupal site...`` function.

Now use the ``site-install`` command to install Drupal with the DF installation profile.

  ``drush si df``

Enable a DF Scenario using the ``enable-scenario`` command.

  ``drush es dfs_tec``

If everything worked correctly, you should see console output that some migrations ran.

You may now login to your site.

  ``drush uli -l http://mysite.dd``

You may also reset the content of a DF Scenario if it is enabled.

  ``drush rs dfs_tec``
  
### Using the Zurb Foundation Sub Theme

To motify the CSS/JS you must use the scss files. You will find various different SCSS files in SCSS directory that root. There are specifc ones for the theme in base & layout. All the variables are set in _settings.scss, you will also be able to override variables there.

To compile scss you will need a few things installed on your machine:
- NPM [IF you need to install](http://blog.npmjs.org/post/85484771375/how-to-install-npm)
- Bower ``npm install -g bower``

Then you will need to run:
- ``npm install``
- ``bower install``

if you need to update the vendor js, I added in some gulp files that make that easy.
- ``gulp copy`` will copy the bower_component files for zurb and motion ui
- ``gulp concat`` will concatenate all the files into a single vendor.all.js file and put it in your js/ folder where its already being called by drupal

Once that is installed, start the gulp file which will watch for scss changes:
- ``npm start``

### Behat tests

When built via Composer, DF includes a copy of Behat, Mink and the Drupal
Extension to Behat and Mink in the /bin folder located outside of the docroot.
Alternatively, you may install and use the Drupal Extension globally by
following the instructions at:
http://behat-drupal-extension.readthedocs.io/en/3.1/globalinstall.html

Selenium is required to run the JavaScript tests. You can download Selenium from
http://www.seleniumhq.org and run it with:

``java -jar selenium.jar``

Note that you may require a newer version of Java which can be downloaded from
http://www.oracle.com/technetwork/java/javase/downloads/index.html.

Before running any tests you must edit the behat.local.yml file, located within
DRUPAL_ROOT/profiles/df, replacing "base_url" with the URL to your site.

In order to run the tests, you must be in the DRUPAL_ROOT/profiles/df directory.

  ``cd DRUPAL_ROOT/profiles/df``

Check that behat is installed and running.

  ``behat --help``

Execute a batch of tagged features that apply to all DF Scenarios.

  ``behat --tags=df``

Execute a batch of tagged features for a specific DF Scenario.

  ``behat --tags=dfs_dev``

If you're using the copy of Behat included with DF, then substitute "behat" in
the above examples with:

``/path/to/MYPROJECT/bin/behat``
