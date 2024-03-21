# How to Install Shield for CodeIgniter 4 without composer
**Step 1:** Download the latest version of [Codeigniter4](https://github.com/codeigniter4/framework/releases)<br>
Extract file `framework-4.x.x.zip` in any path (eg. `P:\ShieldTest`)

**Step 2:** Download the latest version of [Settings](https://github.com/codeigniter4/settings/releases)<br>
Extract file `settings-2.x.x.zip` in `P:\ShieldTest\framework-4.x.x\app\ThirdParty`

**Step 3:** Download the latest version of [Shield](https://github.com/codeigniter4/shield/releases)<br>
Extract file `shield-1.0.0-beta.3.zip` in `P:\ShieldTest\framework-4.x.x\app\ThirdParty`

**Step 4:** Edit file `P:\ShieldTest\framework-4.x.x\app\Config\Autoload.php` :

```
    public $psr4 = [
        APP_NAMESPACE => APPPATH, // For custom app namespace
        'Config'      => APPPATH . 'Config',
        // add this lines
        'CodeIgniter\\Settings' => APPPATH . 'ThirdParty/settings-2.1.0/src',
        'CodeIgniter\\Shield' => APPPATH . 'ThirdParty/shield-1.0.0-beta.3/src', 
    ];
```

and add :
```
    public $files = [
        APPPATH . 'ThirdParty/shield-1.0.0-beta.3/src/Helpers/auth_helper.php',
        APPPATH . 'ThirdParty/shield-1.0.0-beta.3/src/Helpers/email_helper.php',
    ];
```

**Step5:** Creating a database and setting it up.<br>
Create a database with a name of your choice(eg. `imshield`).<br>
Make the necessary settings to connect to the database through file `P:\ShieldTest\framework-4.x.x\app\Config\Database.php`.
```
    public $default = [
        'DSN'      => '',
        'hostname' => 'localhost',
        'username' => 'root',
        'password' => '',
        'database' => 'imshield',
        'DBDriver' => 'MySQLi',
        'DBPrefix' => '',
        'pConnect' => false,
        'DBDebug'  => (ENVIRONMENT !== 'production'),
        'charset'  => 'utf8',
        'DBCollat' => 'utf8_general_ci',
        'swapPre'  => '',
        'encrypt'  => false,
        'compress' => false,
        'strictOn' => false,
        'failover' => [],
        'port'     => 3306,
    ];
```

Or you can use file `.env` to set up the database connection (**recommended**).

**Step6:** Now go to the root of your project (`P:\ShieldTest\framework-4.x.x`) and run the following command in the terminal.

```
php spark shield:setup
```

**Done. The shield was installed.**<br>
Read the documentation for more information. Also, don't forget to [use filters for protection all pages](https://shield.codeigniter.com/quick_start_guide/using_session_auth/#protecting-pages).

Source: https://github.com/codeigniter4/shield/discussions/581
