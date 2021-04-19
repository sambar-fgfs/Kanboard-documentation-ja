設定ファイル
==================

``config.php`` をプロジェクトのルートディレクトリか、``data`` フォルダに追加することで、Kanboardのデフォルト設定をカスタマイズできます。また、``config.default.php``から、``config.php``にリネームすることでも、希望する設定値にできます。.

デバッグモードの有効化/無効化
-------------------------

.. code:: php

    define('DEBUG', true);
    define('LOG_DRIVER', 'file'); // ドライバは、 syslog, stdout, stderr, system ,file です。

    // デフォルトでは、ログは data/debug.logに保存されますが、変更することもできます:
    define('LOG_FILE', '/path/to/debug.log');

-  デバッグモードを有効化する場合、log_driverを定義しなければなりません。
-  デバッグモードのログはすべてSQLクエリで、ページの生成に時間が掛かります。
-  ``system`` ドライバは   `php.ini <http://php.net/manual/en/errorfunc.configuration.php#ini.error-log>`__ 内で設定したビルトインのPHPロガーを使用します。
   デフォルトでは、ログメッセージはwebサーバーのログとして送られます。

プラグイン
-------

プラグインフォルダ:

.. code:: php

    define('PLUGINS_DIR', 'data/plugins');

ユーザーインターフェースからのプラグインのインストールの有効化/無効化

.. code:: php

    define('PLUGIN_INSTALLER', false); // Kanboard v1.2.8 から、デフォルトはfalseです。

プラグインのディレクトリのURLを変更する:

.. code:: php

    define('PLUGIN_API_URL', 'https://kanboard.org/plugins.json');

アップロードされたファイルのフォルダ
-------------------------

.. code:: php

    define('FILES_DIR', 'data/files');

キャッシュのパラメータ
----------------

.. code:: php

    // 利用可能なキャッシュのドライバは"file" と "memory"です。
    define('CACHE_DRIVER', 'memory');

    // キャッシュのドライバを "file" にした場合、キャッシュのフォルダを使用します。 (webサーバのユーザが書込可でなければなりません)
    define('CACHE_DIR', DATA_DIR.DIRECTORY_SEPARATOR.'cache');

URL rewriteの有効化/無効化
--------------------------

.. code:: php

    define('ENABLE_URL_REWRITE', false);

Email の設定
-------------------

.. code:: php

    // ユーザーインターフェースからの email 設定の有効化/無効化
    define('MAIL_CONFIGURATION', true);

    // (通知時に) "From" ヘッダ で使用するメールアドレス
    define('MAIL_FROM', 'notifications@kanboard.local');

    // メールの送信方法を"smtp", "sendmail" , "mail" (PHP のメール関数) から選択
    define('MAIL_TRANSPORT', 'mail');

    // "smtp" での送信を選んだときに使用するSMTPの設定
    define('MAIL_SMTP_HOSTNAME', '');
    define('MAIL_SMTP_PORT', 25);
    define('MAIL_SMTP_USERNAME', '');
    define('MAIL_SMTP_PASSWORD', '');
    define('MAIL_SMTP_HELO_NAME', null); // null (デフォルト)か FQDN が使用できます
    define('MAIL_SMTP_ENCRYPTION', 'ssl'); // "null", "ssl", "tls" が利用できます

    // "sendmail" での送信を選んだときに sendmail コマンドが使用する設定
    define('MAIL_SENDMAIL_COMMAND', '/usr/sbin/sendmail -bs');
    
    // 全ての通知のコピーの送信時に "Bcc" ヘッダーで使用するメールアドレス
    define('MAIL_BCC', '');


データベースの設定
-----------------

.. code:: php

    // 自動的にデータベースのマイグレーションを実施する
    // これをfalseにした場合、Kanboardのアップグレード作業中にSQLのマイグレーションをCLIから手動で行わなければなりません。
    // 同時に複数のプロセスからマイグレーションを実行してはいけません (例: web ページ + バックグラウンドワーカー)
    define('DB_RUN_MIGRATIONS', true);

    // データベースのドライバ: sqlite, mysql, postgres (デフォルトは sqlite )
    define('DB_DRIVER', 'sqlite');

    // Mysql/Postgres でのユーザー名
    define('DB_USERNAME', 'root');

    // Mysql/Postgres でのパスワード
    define('DB_PASSWORD', '');

    // Mysql/Postgres でのホスト名
    define('DB_HOSTNAME', 'localhost');

    // Mysql/Postgres データベース名
    define('DB_NAME', 'kanboard');

    // Mysql/Postgres のポート番号 (null = デフォルトのポート)
    define('DB_PORT', null);

    // Mysql のSSL キー
    define('DB_SSL_KEY', null);

    // Mysql のSSL 証明書
    define('DB_SSL_CERT', null);

    // Mysql のSSL認証局
    define('DB_SSL_CA', null);

LDAP の設定
-------------

.. code:: php

    // LDAP 認証を有効にする (デフォルトは false )
    define('LDAP_AUTH', false);

    // LDAP のサーバーのホスト名
    define('LDAP_SERVER', '');

    // LDAP のサーバーのポート番号 (デフォルトで 389)
    define('LDAP_PORT', 389);

    // デフォルトでは、 ldaps:// 様式のURLには検証が必要ですfalseにすると検証をスキップします。
    define('LDAP_SSL_VERIFY', true);

    // LDAP START_TLS を有効にする
    define('LDAP_START_TLS', false);

    // Kanboard はデフォルトではユーザーの重複回避のため、ldapのユーザー名は小文字になります (データベースは大文字と小文字を区別します )
    // 大文字を使いたい場合はtrueにしてください。
    define('LDAP_USERNAME_CASE_SENSITIVE', false);

    // LDAPの認証タイプ: "anonymous", "user" or "proxy"
    define('LDAP_BIND_TYPE', 'anonymous');

    // proxyモードで使用する LDAP password
    // userモードで使用する LDAPユーザー名のパターン
    define('LDAP_USERNAME', null);

    // proxyモードで使用する LDAP password
    define('LDAP_PASSWORD', null);

    // LDAP のユーザー識別名
    // ActiveDirectoryでの例: CN=Users,DC=kanboard,DC=local
    // OpenLDAPでの例: ou=People,dc=example,dc=com
    define('LDAP_USER_BASE_DN', '');

    // LDAP でユーザーアカウントの検索に使用するパターン
    // ActiveDirectoryでの例: '(&(objectClass=user)(sAMAccountName=%s))'
    // OpenLDAPでの例: 'uid=%s'
    define('LDAP_USER_FILTER', '');

    // グループ内でのユーザーのフィルターに使用するLDAP属性
    // 'username' or 'dn'
    define('LDAP_GROUP_USER_ATTRIBUTE', 'username');

    // LDAP 属性でのユーザー名
    // ActiveDirectoryでの例: 'samaccountname'
    // OpenLDAPでの例: 'uid'
    define('LDAP_USER_ATTRIBUTE_USERNAME', 'uid');

    // LDAP 属性のユーザーのフルネーム
    //ActiveDirectory の例: 'displayname'
    // OpenLDAPでの例: 'cn'
    define('LDAP_USER_ATTRIBUTE_FULLNAME', 'cn');

    // LDAP 属性のユーザーのemailアドレス
    define('LDAP_USER_ATTRIBUTE_EMAIL', 'mail');

    // LDAP 属性でユーザーのプロフィールからグループを見つける
    define('LDAP_USER_ATTRIBUTE_GROUPS', 'memberof');

    // LDAP 属性のユーザーのアバター画像 : サムネイル写真 or Jpeg画像
    define('LDAP_USER_ATTRIBUTE_PHOTO', '');

    // LDAP 属性のユーザーの言語。例: 'preferredlanguage'
    // 言語を同期させないため、空の文字列を入れる
    define('LDAP_USER_ATTRIBUTE_LANGUAGE', '');

    // 自動でLDAP ユーザーの作成を許容する
    define('LDAP_USER_CREATION', true);

    // 新規ユーザーをマネージャーにする
    define('LDAP_USER_DEFAULT_ROLE_MANAGER', false);

    // システム管理者のLDAP 識別名
    // Example: CN=Kanboard-Admins,CN=Users,DC=kanboard,DC=local
    define('LDAP_GROUP_ADMIN_DN', '');

    // マネージャーのLDAP 識別名
    // Example: CN=Kanboard Managers,CN=Users,DC=kanboard,DC=local
    define('LDAP_GROUP_MANAGER_DN', '');

    // LDAP グループプロバイダをプロジェクトの権限設定に使用する
    // エンドユーザーはユーザーインターフェースからLDAPグループをブラウズできるようになり、特定のプロジェクトへのアクセスを許可します。
    define('LDAP_GROUP_PROVIDER', false);

    // グループのLDAP Base DN
    define('LDAP_GROUP_BASE_DN', '');

    // LDAP グループフィルター
    // ActiveDirectoryの例: (&(objectClass=group)(sAMAccountName=%s*))
    define('LDAP_GROUP_FILTER', '');

    // LDAP ユーザーグループフィルター
    // このフィルターが設定されている場合、Kanboardはユーザーグループを LDAP_GROUP_BASE_DN から探します。
    // OpenLDAP の例: (&(objectClass=posixGroup)(memberUid=%s))
    define('LDAP_GROUP_USER_FILTER', '');

    // LDAP 属性のグループ名
    define('LDAP_GROUP_ATTRIBUTE_NAME', 'cn');

リバースプロキシ認証の設定
-------------------------------------

.. code:: php

    // リバースプロキシ認証の有効化/無効化
    define('REVERSE_PROXY_AUTH', false);

    // ユーザー名に使用するヘッダ名
    define('REVERSE_PROXY_USER_HEADER', 'REMOTE_USER');

    // ユーザー名に使用するヘッダ名
    define('REVERSE_PROXY_EMAIL_HEADER', 'REMOTE_EMAIL');

    // 管理者のユーザー名。デフォルトは空白
    define('REVERSE_PROXY_DEFAULT_ADMIN', '');

    // Emailアドレスとして設定するように使用するデフォルトのドメイン
    define('REVERSE_PROXY_DEFAULT_DOMAIN', '');

RememberMe 認証の設定
----------------------------------

.. code:: php

    // remembarme認証の有効化/無効化
    define('REMEMBER_ME_AUTH', true);

セキュアHTTPヘッダのセクション
----------------------------

.. code:: php

    // "Strict-Transport-Security" HTTP ヘッダの有効化/無効化
    define('ENABLE_HSTS', true);

    // "X-Frame-Options: DENY" HTTP ヘッダの有効化/無効化
    define('ENABLE_XFRAME', true);

ログ生成
-------

デフォルトでは、Kanboardは何もログを生成しません。ログ生成を有効にしたいならば、ログドライバをセットしなければなりません。

.. code:: php

    // 利用可能なログドライバ: syslog, stderr, stdout or file
    define('LOG_DRIVER', '');

    // ログドライバを "file" にした場合のログファイル名
    define('LOG_FILE', __DIR__.DIRECTORY_SEPARATOR.'data'.DIRECTORY_SEPARATOR.'debug.log');

総当たり攻撃からの保護
----------------------

.. code:: php

    // 3 回認証に失敗した場合にcaptcha認証を行う
    define('BRUTEFORCE_CAPTCHA', 3);

    // 6回認証に失敗した後はアカウントをロックする
    define('BRUTEFORCE_LOCKDOWN', 6);

    // アカウントのロック期間(分)
    define('BRUTEFORCE_LOCKDOWN_DURATION', 15);

セッション
-------

.. code:: php

    // セッションの有効期間 (秒指定。 0 の場合、ブラウザを閉じるまで)
    // http://php.net/manual/ja/session.configuration.php#ini.session.cookie-lifetime も参照のこと
    define('SESSION_DURATION', 0);

    // セッションハンドラ: db or php
    //    db: セッション情報はデータベース内に保存される(デフォルト)
    //    php: セッション情報はPHP内部のセッションハンドラに保存される
    // 詳細は https://www.php.net/manual/en/session.customhandler.php を参照願います。
    define('SESSION_HANDLER', 'db');

HTTP クライアント
-----------

HTTPプロキシの設定:

.. code:: php

    define('HTTP_PROXY_HOSTNAME', '');
    define('HTTP_PROXY_PORT', '3128');
    define('HTTP_PROXY_USERNAME', '');
    define('HTTP_PROXY_PASSWORD', '');
    define('HTTP_PROXY_EXCLUDE', 'localhost'); // Only for cURL

自己署名証明書を許容するには:

.. code:: php

    // falseにすると、自己署名証明書を許容する
    define('HTTP_VERIFY_SSL_CERTIFICATE', true);

様々な設定
----------------

.. code:: php

    // markdownテキスト中でhtmlエスケープをさせる
    define('MARKDOWN_ESCAPE_HTML', true);

    // 代替のAPI認証ヘッダ。デフォルトはRFC2617で定義されたHTTP Basic認証。
    define('API_AUTHENTICATION_HEADER', '');

    // ログインフォームの非表示。全てのユーザーがGoogle/Github/リバースプロキシ認証を使用する場合に有用。
    define('HIDE_LOGIN_FORM', false);

    // (外部シングルサインオン認証を使用している場合のための)ログアウト無効化
    define('DISABLE_LOGOUT', false);

    // 自動テスト用に、データベースに保存されているトークンをオーバーライドするAPIトークン
    define('API_AUTHENTICATION_TOKEN', 'My unique API Token');

    // TOTP (二要素認証) のissuer name
    define('TOTP_ISSUER', 'Kanboard');

    // 外部認証を使用している時に同期させないコンマ区切りのリストのフィールド
    define('EXTERNAL_AUTH_EXCLUDE_FIELDS', 'username');
