# drush-shrinkdb

Extends Drush sql-sanitize with an option to shrink the database size by wiping older content.

It only supports Drupal 8 for now.

[Features]: #features
[Install]: #install
[Usage]: #usage


### Table of Contents

 * [Features][Features]
 * [Install instructions][Install]
 * [Usage][Usage]


## Features

 * Wipe content in entity tables (base fields, fields and revisions).
 * Currently it provides hardcoded support for node and media entities.
 * More funcionality is planned. See the [TODO list](TODO.md).


### _Screenshots_


```
$ drush help sql-sanitize

Run sanitization operations on the current database. You can add more sanitization to this command by implementing hook_drush_sql_sync_sanitize().

Options:
 --db-prefix                                Enable replacement of braces in sanitize queries.
 --db-url=<mysql://root:pass@127.0.0.1/db>  A Drupal 6 style database URL.
 --sanitize-email=<user+%uid@localhost>     The pattern for test email addresses in the sanitization operation, or "no" to keep email addresses unchanged.  May contain replacement patterns %uid, %mail or %name.
 --sanitize-password=<password>             The password to assign to all accounts in the sanitization operation, or "no" to keep passwords unchanged.
 --shrink-db                                Shrink the database size by wiping content older than given days.
 --shrink-db-days=<15>                      Age (in days) of the contents to preserve. 15 by default.
```


```
$ drush @site sql-sanitize --shrink-db

The following operations will be done on the target database:
 * Wipe content older than 15 days
 * Reset passwords and email addresses in users_field_data table
 * Truncate Drupal's sessions table
```


## Install

### Via git

```
mkdir -p /usr/share/drush/commands
cd /usr/share/drush/commands
git clone https://github.com/jonhattan/drush-shrinkdb.git
cd drush-shrinkdb
composer install
```

### Via drush

```
mkdir -p /usr/share/drush/commands
drush dl drush_shrinkdb
cd /usr/share/drush/commands/drush_shrinkdb
composer install
```

This is system-wide installation. Alternatively you may want to install it
to a specific project or your home directory.

### Via composer

Package `drupal/drush_shrinkdb` is available both at http://packagist.drupal-composer.org and http://packages.drupal.org/8.

You can require it in your composer project as usual:

```
composer require drupal/drush_shrinkdb
```


## Usage

```
drush @site sql-sanitize --shrink-db
drush @site sql-sanitize --shrink-db --shrink-db-days=90
```

## Author Information

Jonathan Araña Cruz - [SB IT Media, S.L](http://sbit.io).
