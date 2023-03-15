# ESSENTIALS FOR LARAVEL STARTUP

In this path will look into the basic requirments which are required for a web developer to start as laravel developer

### REQUIREMENTS FOR LARAVEL SETUP

- PHP version of choice (used 7.4)
- DBMS of choice (MYSQL,MONGODB etc)
- COMPOSER for setting up projects
- NODE for setting up JS modules
- IDE of choice (preferred VS CODE)

for latest can look into [Laravel Official Documentation](https://laravel.com/docs/10.x)

#### LARAVEL INIT

these are the following ways to setup laravel project

#### using the composer create-project

    composer create-project laravel/laravel example-app

#### using laravel installer

Installing laravel installer and using it every time project is required to be created

    composer global require laravel/installer
    laravel new example-app

Change to newly created project dir and run artisan serve to up the app

     cd example-app
     php artisan serve

##### NOTE to user laravel installer in case of linux composer path will be required to be added in the .bashrc

    export PATH="$PATH:$HOME/.config/composer/vendor/bin"

#### LARAVEL STRUCTURE

laravel: follows MVC patterns

- app: Contains the business logic i.e. Models, Controller, Middleware etc
- config: Contains basic configuration
- database: Contains db related files i.e. drivers and dummy data
- lang: Contains the language files

- public: Entry point for the app i.e. index.php and CSS,images and js files which could be publicly access

- resources: Contains views and all other uncompiled resources i.e js css
  - Views: Contains the pages
- routes: Contains all the routes definition for the application, web.php contains all the route definition for app,api.php contains the api route definition
- Storage: Contains all the logs and user generated files

- Test: Contains the automated test file

- vendor: Contains all the composer dependencies files

- .env: Contains configuration for environment i.e. local,staging,production, accessed using th env();

- .env-example file is replica of .env file to share with other user who gonna use this code as .env file not pushed on git

- artisan: cli use to communicate with different services i.e. using php artisan serve tells to create build on server, to multiple commands executable by artisan type `php artisan` it will show the complete list of available commands, in case any help required for any command
  type `-h` for it i.e. `php artisan serve -h` it will return the help for the command `serve`

## Composer Working

composer create/install packages into our project/directory

#### composer dump-autoload

to regenerat the list of all classes that need to be included in the project we use

    composer dump-autoload

#### composer require

it adds new packages to the composer. json, in project directory

    composer require <package_name >

#### composer install

- If composer.lock does exist.
  - Processes and installs dependencies from the `composer.lock` file.
- If `composer.lock` does not exist.
  - Process package installs from `composer.json`.
  - Creates the `composer.lock` file based on the installed packages.

#### composer update

- Processes dependencies from the `composer.json` file (installs, updates and removes).
- Creates or updates the `composer.lock` file according to the changes.

#### composer upgrade

- command updates only the packages that are listed in your `composer.json`
- also satisfies the constraints defined in the `composer.lock`.

- In other words, it only upgrades to the latest version that is compatible with the version constraints specified in `composer.json` and `composer.lock`.

## Artisan Working

artisan command is responsible for handling different operation in our laravel app, most commonly used are

#### migrate

this allow us to create table in our database. Using migrations can help you keep your database schema in sync with your codebase and make it easier to manage changes over time

#### serve

to start a local development server for your Laravel application without using apache or any other such envoirment on local system

#### route

to view a list of all the registered routes in your Laravel application.

#### make

make command is important command anything laravel has to offer is added using the make command in the project, it give shortcut for creating new files or controller with boilerplate

Some of the commonly used `artisan make` commands include:

- `make:controller`: Generates a new controller class.
- `make:model`: Generates a new Eloquent model class.
- `make:migration`: Generates a new database migration file.
- `make:middleware`: Generates a new middleware class.
- `make:seeder`: Generates a new database seeder class.
- `make:factory`: Generates a new model factory class.
