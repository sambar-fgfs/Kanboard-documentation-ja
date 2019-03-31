MySQL/MariaDB
=============

デフォルトではKanboardは Sqlite にデータを保存します。しかし、Sqliteの代わりにMySQLかMariaDBを使うこともできます。

必要要件
------------

-  MySQL 5.6以上 or MariaDB 10以上
-  PHP 拡張 ``pdo_mysql`` がインストールされている

MySQL の設定
-------------------

データベースの作成
~~~~~~~~~~~~~~~~~

最初のステップで、MySQLサーバー上にデータベースを作成します。
例えば、MySQLクライアントからこのようにします:

.. code:: sql

    CREATE DATABASE kanboard CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

.. 注意:: Kanboard1.2.3以降では、utf8に替えてutf8mb4を使用します。

それからデータベースに必要なアクセス権を割当てることができます:

.. code:: sql

    GRANT ALTER, CREATE, DELETE, DROP, INDEX, INSERT, REFERENCES, SELECT, UPDATE ON kanboard.* TO 'USERNAME'@'HOST' IDENTIFIED BY 'PASSWORD';

設定ファイルの作成
~~~~~~~~~~~~~~~~~~~~

``config.php`` にはこれらの値が含まれるべきです:

.. code:: php

    <?php

    // Sqliteの代わりにMySQLを使用するよう選択する
    define('DB_DRIVER', 'mysql');

    // SQLサーバーのパラメータ
    define('DB_USERNAME', 'REPLACE_ME');
    define('DB_PASSWORD', 'REPLACE_ME');
    define('DB_HOSTNAME', 'REPLACE_ME');
    define('DB_NAME', 'kanboard');

注意: また、テンプレートファイルを ``config.default.php``から、``config.php``にリネームすることもできます。

SQLダンプのインポート (別の方法)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Kanboardの初回実行時には、個々のデータベースのマイグレーションを一つづつ実行しますが、通常そのプロセスは設定に従います。

いかなるタイムアウトの可能性も排除するため、SQLスキーマをインポートすることでデータベースの初期化を行うことができます:

.. code:: bash

    mysql -u root -p my_database < app/Schema/Sql/mysql.sql

``app/Schema/Sql/mysql.sql`` ファイルは、データベースの最終バージョンに相当するSQLダンプです。

Unix socket接続を使用したいなら、下記を試してください:

.. code:: php

    define('DB_HOSTNAME', '127.0.0.1;unix_socket=/var/run/mysqld/mysqld.sock');

SSL の設定
-----------------

MySQLのSSL接続を有効化するには、これらのパラメータを定義しなければなりません。

.. code:: php

    // MySQL SSL キー
    define('DB_SSL_KEY', '/path/to/client-key.pem');

    // MySQL SSL 証明書
    define('DB_SSL_CERT', '/path/to/client-cert.pem');

    // MySQL SSL 認証局
    define('DB_SSL_CA', '/path/to/ca-cert.pem');
