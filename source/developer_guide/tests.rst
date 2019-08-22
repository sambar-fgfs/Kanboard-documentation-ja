自動テスト
===============

`PHPUnit <https://phpunit.de/>`__ がKanboardの自動テストに使用されます。

異なるデータベース(Sqlite, MySQL, PostgreSQL) を横断して、どれでも同じ結果が得られるようにテストができます。

必要要件
------------

-  Linux/Unix マシン
-  PHP
-  PHPUnit がインストールされていること
-  Mysql と Postgresql (任意)
-  Selenium (任意)
-  Firefox (任意)

単体テスト
----------

Sqlite を使用したテスト
~~~~~~~~~~~~~~~~

Sqlite のテストはメモリ上のデータベースで行い、ファイルシステムへの書き込みは行いません。

PHPUnit の設定ファイルは ``tests/units.sqlite.xml`` です。Kanboardのディレクトリから、``phpunit -c tests/units.sqlite.xml`` コマンドを実行してください。

例:

.. code:: bash

    phpunit -c tests/units.sqlite.xml

    PHPUnit 5.0.0 by Sebastian Bergmann and contributors.

    ...............................................................  63 / 649 (  9%)
    ............................................................... 126 / 649 ( 19%)
    ............................................................... 189 / 649 ( 29%)
    ............................................................... 252 / 649 ( 38%)
    ............................................................... 315 / 649 ( 48%)
    ............................................................... 378 / 649 ( 58%)
    ............................................................... 441 / 649 ( 67%)
    ............................................................... 504 / 649 ( 77%)
    ............................................................... 567 / 649 ( 87%)
    ............................................................... 630 / 649 ( 97%)
    ...................                                             649 / 649 (100%)

    Time: 1.22 minutes, Memory: 151.25Mb

    OK (649 tests, 43595 assertions)

MySql を使用したテスト
~~~~~~~~~~~~~~~~

ローカルホスト上にMySQLかMariaDBがインストールされている必要があります。

デフォルトでは、以下の資格情報を使用します:

-  ホスト名: **localhost**
-  ユーザー名: **root**
-  パスワード: none
-  データベース: **kanboard_unit_test**

実行ごとにデータベースは破棄され、再度生成されます。

PHPUnit の設定ファイルは ``tests/units.mysql.xml`` です。Kanboardのディレクトリから、``phpunit -c tests/units.mysql.xml`` コマンドを実行してください。

PostgreSQL を使用したテスト
~~~~~~~~~~~~~~~~~~~~

ローカルホスト上にPostgreSQLがインストールされている必要があります。

デフォルトでは、以下の資格情報を使用します:

-  ホスト名: **localhost**
-  ユーザー名: **postgres**
-  パスワード: none
-  データベース: **kanboard_unit_test**

ユーザー ``postgres`` に、データベースの生成と破棄を許可する必要があります。実行の都度データベースは再度生成されます。

PHPUnit の設定ファイルは ``tests/units.postgresql.xml`` です。Kanboardのディレクトリから、``phpunit -c tests/units.postgresql.xml`` コマンドを実行してください。

結合テスト
-----------------

結合テストは主にAPIのテストに使用されますテストスイートはコンテナ内でアプリケーションを実行するために実際にHTTPコールを生成します。

.. _requirements-1:

必要要件
~~~~~~~~~~~~

-  PHP
-  コンポーザー
-  Unix系のOS (Mac OS か Linux)
-  Docker
-  Docker Compose

結合テストを実行する
~~~~~~~~~~~~~~~~~~~~~~~~~

結合テストはDockerコンテナを使用します。それは3つの異なる環境であっても、個々のデータベース毎にテストをする為です。

これらのコマンドで各々のテストスイートを実行できます。

.. code:: bash

    # Sqliteでのテスト
    make integration-test-sqlite

    # Mysqlでのテスト
    make integration-test-mysql

    # PostgreSQLでのテスト
    make integration-test-postgres

受入テスト
----------------

受入テスト (もしくは end-to-end テスト、機能テスト) はSeleniumを使用してブラウザ上のUIが実際に機能するかテストします。

これらのテストの実行を指示するには  `Selenium Standalone Server <http://www.seleniumhq.org/download/>`__ がインストールされている必要があり、また互換性のあるバージョンのFirefoxが必要です。

PHPUnit の設定ファイルは ``tests/acceptance.xml`` です。SeleniumとKanboardを同時に実行するには、Kanboardのディレクトリで ``make test-browser`` を実行してください。テストスイートを初期化して、Firefoxを自動的に開き、受入テストで指定されたアクションを実行します。

例:

.. code:: bash

    $ make test-browser
    PHPUnit 4.8.26 by Sebastian Bergmann and contributors.

    ..

    Time: 5.59 seconds, Memory: 5.25MB

    OK (2 tests, 5 assertions)

Travis-CI を使用した継続的インテグレーション
-------------------------------------

メインのリポジトリにコミットがプッシュされた後に、その都度様々なバージョンのPHPで単体テストが実行されます。

-  PHP 7.0
-  PHP 5.6

各バージョンのPHPで、サポートされている3つのデータベースでテストされます: Sqlite,Mysql とPostgresql です。

Travis-CIの設定ファイルは Kanboard のルートディレクトリにある ``.travis.yml`` です。
