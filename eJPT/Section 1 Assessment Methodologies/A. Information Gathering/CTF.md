## Notes from Lab Enviroment

A website is accessible at http://target.ine.local. Perform reconnaissance and capture the following flags.

- Flag 1: This tells search engines what to and what not to avoid.
- Flag 2: What website is running on the target, and what is its version?
- Flag 3: Directory browsing might reveal where files are stored.
- Flag 4: An overlooked backup file in the webroot can be problematic if it reveals sensitive configuration details.
- Flag 5: Certain files may reveal something interesting when mirrored.
### Tools
Firefox
Curl
HTTrack

### Note
In this lab, the flag will follow the format: FLAG1{MD5Hash} OR FL@G1{MD5Hash}. For example, FLAG1{0f4d0db3668dd58cabb9eb409657eaa8}. You need to submit only the MD5 hash string, excluding the braces. For instance: 0f4d0db3668dd58cabb9eb409657eaa8.


## Flag 1

This tells search engines what to and what not to avoid.

![[Pasted image 20250406222937.png]]

## Flag II

What website is running on the target, and what is its version?

```bash
┌──(root㉿INE)-[~/websites]
└─# curl -s http://target.ine.local | grep generator
<meta name="generator" content="WordPress 6.5.3 - FL@G2{25817159773f4c8e80e9093181c85ee5}" />

```

Here, I took help of ChatGPT and Got this 


### Check the Meta Generator Tag in the HTML

Most WordPress sites include a meta tag in the `<head>` that shows the version.

```bash
curl -s https://example.com | grep -i "generator"`
```


## Flag 3

Directory browsing might reveal where files are stored.

![[Pasted image 20250406224343.png]]
## Flag 4

An overlooked backup file in the webroot can be problematic if it reveals sensitive configuration details.

### **Solution**
So, I ran wpscan on this website as it is running wordpress site & I got this

![[Pasted image 20250406223355.png]]

```bash
┌──(root㉿INE)-[~]
└─# cat Downloads/wp-config.bak            
<?php
/**
 * The base configuration for WordPress
 *
 * The wp-config.php creation script uses this file during the installation.
 * You don't have to use the website, you can copy this file to "wp-config.php"
 * and fill in the values.
 *
 * This file contains the following configurations:
 *
 * * Database settings
 * * Secret keys
 * * Database table prefix
 * * ABSPATH
 *
 * @link https://wordpress.org/documentation/article/editing-wp-config-php/
 *
 * @package WordPress
 */

// ** Database settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define( 'DB_NAME', 'test' );

/** Database username */
define( 'DB_USER', 'test' );

/** Database password */
define( 'DB_PASSWORD', 'test' );

/** Database hostname */
define( 'DB_HOST', 'localhost' );

/** Database charset to use in creating database tables. */
define( 'DB_CHARSET', 'utf8' );

/** The database collate type. Don't change this if in doubt. */
define( 'DB_COLLATE', '' );

/**#@+
 * Authentication unique keys and salts.
 *
 * Change these to different unique phrases! You can generate these using
 * the {@link https://api.wordpress.org/secret-key/1.1/salt/ WordPress.org secret-key service}.
 *
 * You can change these at any point in time to invalidate all existing cookies.
 * This will force all users to have to log in again.
 *
 * @since 2.6.0
 */
define('AUTH_KEY',         '}Mq^#|v{n0fQ6Vn[tr 6e4glzi:OVs/9(IQ .7f^dp3ym4,th-O$Qx.]|2+(t(sE');
define('SECURE_AUTH_KEY',  'S_LKQ#*}p*U}kdX[GNNVM2*0YISNQ&zrFl jEUNq5T}0Zg|,sO|yB68^|N*1nS-p');
define('LOGGED_IN_KEY',    '`tz-Uz9Ixka,5z0J BD0l/zfU|r2|;9BGL5l~A1RQtZMwh=JftaU$2)$FI%v};|E');
define('NONCE_KEY',        '|>ZN961k>aHWJ*R8#&x+rR>3g|<[:G 8B+rqPH WrWet1SC60+ LL/S+=[G-&g7)');
define('AUTH_SALT',        '+<2l=;osCL(L)zV[=uvr[}2^j-16(gFq18V<m|fP<R{7DV`^=O&bb3fxY+Jf|-;C');
define('SECURE_AUTH_SALT', 'HG&/Q/ceR-$;?jCL}<cL4@LKzDjv,M=K-gR<]iHiAqcHQO+rXcWn/jMt0#K,uWq%');
define('LOGGED_IN_SALT',   'REsFv+OsL*qd=yV<oPaAXeYj@f)A[/Wm5-?|_4d::(;dXcps`rgJf]t4B0Q3)RcH');
define('NONCE_SALT',       ' Q.:O=pFDTA-lNBe%kjJu(mp7$cQrF|IZ _hOWDA&Q18w6CL(<{+1$a-ZJ~<(!_;');


/** FLAG4{c01b691291024b02938bc206547fe740} */


/**#@-*/

/**
 * WordPress database table prefix.
 *
 * You can have multiple installations in one database if you give each
 * a unique prefix. Only numbers, letters, and underscores please!
 */
$table_prefix = 'wp_';

/**
 * For developers: WordPress debugging mode.
 *
 * Change this to true to enable the display of notices during development.
 * It is strongly recommended that plugin and theme developers use WP_DEBUG
 * in their development environments.
 *
 * For information on other constants that can be used for debugging,
 * visit the documentation.
 *
 * @link https://wordpress.org/documentation/article/debugging-in-wordpress/
 */
define( 'WP_DEBUG', false );

/* Add any custom values between this line and the "stop editing" line. */



/* That's all, stop editing! Happy publishing. */

/** Absolute path to the WordPress directory. */
if ( ! defined( 'ABSPATH' ) ) {
        define( 'ABSPATH', __DIR__ . '/' );
}

/** Sets up WordPress vars and included files. */
require_once ABSPATH . 'wp-settings.php';
define('WP_HOME', 'http://X.X.X.X');

define('WP_SITEURL', 'http://X.X.X.X');

define('WP_HTTP_BLOCK_EXTERNAL', true);

```


### Flag 5

Certain files may reveal something interesting when mirrored.

**Solution:**

This was one was a pain in the a** because I had to mirror the whole site using `httrack` and look in every configuration file and finally got the flag

```bash
┌──(root㉿INE)-[~/websites/target/target.ine.local]
└─# cat xmlrpc0db0.php | grep FLAG
                        <api name="FLAG5{7dd2a76392af4322ba406c1031f80707}" blogID="1" preferred="false" apiLink="http://target.ine.local/xmlrpc.php" />

```

![[Pasted image 20250406224049.png]]