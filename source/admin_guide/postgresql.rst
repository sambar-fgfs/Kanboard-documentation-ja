Postgresql
==========

デフォルトではKanboardは Sqlite にデータを保存しますが、Postgresqlの使用も可能です。

必要要件
------------

-  Postgresql 9.3以上
-  -  PHP 拡張 ``pdo_pgsql`` がインストールされている (Debian/Ubuntu:``apt-get install php5-pgsql``)

設定
-------------

``pgsql`` コマンドで空のデータベースを作成する:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: sql

    CREATE DATABASE kanboard;

設定ファイルの作成
~~~~~~~~~~~~~~~~~~~~

``config.php`` にはこれらの値が含まれるべきです:

.. code:: php

    <?php

    // Sqliteの代わりにPostgreSQLを使用するよう選択する
    define('DB_DRIVER', 'mysql');// We choose to use Postgresql instead of Sqlite
    define('DB_DRIVER', 'postgres');

    // SQLサーバーのパラメータ
    define('DB_USERNAME', 'REPLACE_ME');
    define('DB_PASSWORD', 'REPLACE_ME');
    define('DB_HOSTNAME', 'REPLACE_ME');
    define('DB_NAME', 'kanboard');

注意: また、テンプレートファイルを ``config.default.php``から、``config.php``にリネームすることもできます。

SQLダンプのインポート (別の方法)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Kanboardの初回実行時には、個々のデータベースのマイグレーションを一つづつ実行しますが、通常そのプロセスは設定に従います。

いかなるissueもしくはタイムアウトの可能性を排除するため、SQLスキーマをインポートすることでデータベースの初期化を行うことができます:

.. code:: bash

    psql -U postgres my_database < app/Schema/Sql/postgres.sql

``app/Schema/Sql/postgres.sql.sql`` ファイルは、データベースの最終バージョンに相当するSQLダンプです。
