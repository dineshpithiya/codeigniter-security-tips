# CodeIgniter Security tips

>Remote Code Execution
This type of an attack allows the hacker to execute unwanted code from a remote location using shell scripting or other measures. This is counter measured by using two things. At first, the htaccess file should be set to allow access to only certain directories, which pose minimum threat if hacked, such as the img/.<br />
```RewriteCond $1 !^(index\.php|img|robots\.txt)```

> Secondly, each .php file in CodeIgniter is protected with the line on the top.<br />
```<? php if ( ! defined('BASEPATH')) exit('No direct script access allowed');```

>SQL Injection
This type of attack is highly common on the web. A SQL injection occurs when an attacker exploits the front-end and the post data to retrieve secure data from the database. According to CodeIgniter manual, it becomes evident that your web application is automatically safe from SQL injection as the POST data is retrieved in the controller using ```$this->input->post``` (‘’); which is automatically filtered by CodeIgniter.

>XSS Attacks
An XSS or Cross Site scripting attack is unarguably the common reason for the demise of web applications. A XSS attack works by a hacker crafting a malicious URL into the browser in order to compromise the security of the application. CodeIgniter has a built in XSS filter which is initialized automatically.
If you want the filter to run automatically every time it encounters POST or COOKIE data you can enable it by opening your application/config/config.php file and setting this:<br />
```$config['global_xss_filtering'] = TRUE;```
This filter will prevent any malicious JavaScript code or any other code that attempts to hijack cookie and do malicious activities. To filter data through the XSS filter, use the xss_clean() method as shown below.<br />
```$data = $this->security->xss_clean($data);```
```$config['csrf_protection'] = TRUE;```

>error_reporting
In production environments, it is typically desirable to disable PHP's error reporting by setting the internal error_reporting flag to a value of 0. This disables native PHP errors from being rendered as output, which may potentially contain sensitive information.

>Validate the data
CodeIgniter has a Form Validation Class that assists you in validating, filtering, and prepping your data.

>Database Error
Even if you have turned off the PHP errors, MySQL errors are still open. You can turn this off in application/config/database.php. Set the db_debug option in $db array to FALSE as shown below.<br />
```$db['default']['db_debug'] = FALSE;```

>Error log
Another way is to transfer the errors to log files. So, it will not be displayed to users on the site. Simply, set the log_threshold value in $config array to 1 in application/cofig/config.php file as shown below.<br />
```$config['log_threshold'] = 1;```

>Using the Encrypt Library<br />
```$config['encryption_key'] = "YOUR KEY";```

>Overall security testing
A Google Chrome extension called Websecurify is a cool piece of software that tests the security of any web application against around 20 top attack types. You can download Websecurify from [here].(https://chrome.google.com/webstore/detail/websecurify/emclbdbpcnhmopfkidjhlinikkohlkpn)
