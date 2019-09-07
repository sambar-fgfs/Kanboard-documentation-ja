プラグインのスキーマのマイグレーション
========================

Kanboard は自動的にデータベースのマイグレーションを行います。マイグレーションは **Schema** フォルダに保存されている、データベースのドライバーと同じファイル名のものでなければなりません :

.. code:: bash

    Schema
    ├── Mysql.php
    ├── Postgres.php
    └── Sqlite.php

個々のファイルはマイグレーションの全てを含んでいます。ここにSqliteの例を示します:

.. code:: php

    <?php

    namespace Kanboard\Plugin\Something\Schema;

    const VERSION = 1;

    function version_1($pdo)
    {
        $pdo->exec('CREATE TABLE IF NOT EXISTS something (
            "id" INTEGER PRIMARY KEY,
            "project_id" INTEGER NOT NULL,
            "something" TEXT,
            FOREIGN KEY(project_id) REFERENCES projects(id) ON DELETE CASCADE
        )');
    }

-  定数 ``VERSION`` はスキーマの最新版です。
-  ``version_1()``, ``version_2()``, 等の個々の関数でマイグレーションをします。
-  ``PDO`` インスタンスは最初の引数をパスします・
-  全ての事はトランザクション内部で実行され、何か問題があればロールバックが実行され、ユーザーにはエラーが表示されます。

Kanboardは データベースに保存されているバージョンとスキーマ内で定義されているバージョンを比較します。バージョンが違う場合、Kanboard は最新版に到達するまで個々のマイグレーションを一つ一つ行います。
