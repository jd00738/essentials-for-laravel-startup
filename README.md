# ESSENTIALS FOR LARAVEL STARTUP

---

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

## Migrations

[Migration Official Documentation](https://laravel.com/docs/10.x/migrations#main-content)

### Key Points

- Migrations are the blueprints of the tables of our app

- Instead of creating tables manually, we can use migrations to do it for us

- With migrations, there's no duplication of effort

- Additionally, it can be done easily from the terminal of the IDE

## NOTE:

`before running migration .env file is required to be updated with the DB connection`

migration is init by the help of artisan, get to the project directory, and run below command in the terminal.

    php artisan migrate

one the command is been executed it laravel will generate some default tables in the DB

migrations files will also be created in the app, which can be access by searching or can be found at database->migrations folder

these files contains the core structure of the tables, these files are contins `table` realted Classess with 2 functions `up & down`.

Below is the script for those functions `up` functions creates the blueprint of the table where `down` function used to drop the table

       public function up()
    {
        Schema::create('users', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('email')->unique();
            $table->timestamp('email_verified_at')->nullable();
            $table->string('password');
            $table->rememberToken();
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('users');
    }

in functions `Schema` static function are used to handle the table in `up` we se `Schema::creat()` functionality which take arguments i.e. `newTableName` and `Blueprint` for that table

## Blueprint table

this is helping in the setting up the table properties as well as there datatypes

#### table->id();

it will genereate the `int` based ID column with primaryKey constraint in the DB

#### $table->string('name');

it will generate `string|varchar` based `name` column in the DB

#### $table->string('email')->unique();

it will generate `string|varchar` based `email` column with unique constraint in the DB

#### $table->timestamp('email_verified_at')->nullable();

it will generate `DateTime` based `email_verified_at` column with nullable properties in the DB

#### $table->rememberToken();

it will generate `remember_token` column, typically used to store a token that can be used to "remember" a user's authentication session.

#### $table->timestamps();

it will genereate `dateInserted` and `dateUpdated` columns in the database

## Createing New Migration

when ever it's required to add a new columnn a new migration will be added using the `make` command of artisan i,e.

    php artisan make:migration create_my_table

now the naming convention matters allot it will create a new migration with the name of `create_my_table` having the current timestamp as prefix in it where 'my' will be setted as the name of the table

follwoing properties are settled in the up function of newly created migration

        public function up()
    {
        Schema::create('my', function (Blueprint $table) {
            $table->string("title");
            $table->string("description");
            $table->timestamps();
        });
    }

after running migration table `my` will be creted having following columns i.e. `title, description, created_at, updated_at` in it

### Rollback Migrations

while wrting the migration if any atribute or related field is missed we can roll back migration and again create the new migration, below is the command which will roll back the migration done by the user

    php artisan migrate:rollback

and after that will again call

    php artisan migrate

the track of migration is based on the batch the migration run first time will have batch 1 in the table while the new migrations will have batch 2 and when `rollback` command is called will only effect the batch 2 `migration`

## Elequent Model

- ORM stands for Object Relational Mapping
- It allows to access tables through code using the table object
- Each table is represented by `Model` class

below command will help in creating the model using artisan

    php artisan make:model my

the newly created model can be found at `app->Models->my.php`

### tinker

to test the the model and it's working will open tinker by using the below command

    php artisan tinker

This will open up a REPL (Read-Eval-Print Loop) shell where you can interactively test and manipulate your application's models and data

run the following commands to interect with the models

> $my = new App\Models\my
>
> = App\Models\my {#3610}
>
> $my->title="test"
>
> = "test"
> $my->description="Why"
>
> = "Why"
>
> $my
>
> = App\Models\my {#3610
> title: "test",
> description: "Why",
> }
>
> $my->save()
