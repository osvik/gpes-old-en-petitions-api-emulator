# EN old API emulator

**This script emulates the old EN API but stores petition signups outside EN.** You can store petition data in BigQuery or SQlite.

This script is useful if you have **legacy petitions** and need to have them running in 2019 **without changing the code** to the new API.  With this script, in your old petitions, you might just need to change the receiving URL from `https://e-activist.com/ea-action/action` to the receiving URL your PHP server. 

Please note this script was developed for the Spanish Office, so it will need small adjustments before it can be used by other NROs. If you use it, you’ll need to manually export the signups to your CRM or mailing app. 

## Install

**Important**: To adapt this script to your field names, modify `index.php` in this repository. Please note you'll need to adjust your database fields as well.

### 1 - Install this script and the libraries

Install Composer and the required libraries with the command:

```bash
curl -sS https://getcomposer.org/installer | php
php composer.phar require google/cloud-bigquery
php composer.phar require catfan/Medoo
```

Download this repository with Git:

`git clone https://github.com/greenpeace/gpes-old-en-petitions-api-emulator.git`


### 2 - Configure the database

To store the signups you can use **Bigquery** or **SQLite**. See how to:

* Configure [Google Cloud and Big Query](BIGQUERY.md)
* Configure [SQLite](SQLITE.md)

Follow the instructions in one of the the links above and continue bellow.

### 3 - Upload the files to the server

* `index.php`
* `config.php`
* `input.php`
* `insert.php`
* `testing-html.html`
* `testing-js.html`

The `vendor` folder, obtained with composer, should be uploaded as well. 

## Test it!

1. With your browser, visit [testing-js.html](testing-js.html) in your server. 
2. Confirm there's data in your new petitions database. 
3. Test the html form redirection by submitting the form in [testing-html.html](testing-html.html).
4. Confirm again that your last form test is in the database.

If you use **BigQuery**, you can check your database with the query:

```sql
#standardSQL
SELECT * FROM `gpes_en_old_api.signups` ORDER BY signed_time;
```

And if you use **SQLite** you can download your database file and open it in your computer with an [SQLite client](http://sqlitebrowser.org/).

## Point your forms to your new API

In your forms, change the receiving URL from `https://e-activist.com/ea-action/action` to the receiving URL your PHP server. It should be the `index.php` file or it's parent folder.

Normally you should do this twice: in the html and in the javascript.