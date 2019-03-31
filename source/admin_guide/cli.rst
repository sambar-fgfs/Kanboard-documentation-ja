コマンドラインインターフェースについて
======================

Kanboard にはUnixターミナルから利用可能な、シンプルなコマンドラインインターフェースがあります。このツールはローカルPCからのみ使用可能です。

この特徴は、webサーバーの外のプロセスでコマンドを実行するのに便利です。

使用方法
-----

-  ターミナルを開き、Kanboardのインストールされたディレクトリに移動する (例: ``cd /var/www/kanboard``)
-  ``./cli`` or ``php cli`` のコマンドを実行する

.. code:: bash

    Kanboard version master

    使用方法:
      コマンド [オプション] [引数]

    オプション:
      -h, --help            このヘルプメッセージを表示
      -q, --quiet           いかなるメッセージも出力しない
      -V, --version         このアプリケーションのバージョンを表示
          --ansi            出力はANSI形式を強制する
          --no-ansi         出力はANSI形式を強制しない
      -n, --no-interaction  対話的質問を行わない
      -v|vv|vvv, --verbose  vの数が増える毎に詳細に出力する: -v は通常の出力で、-vv はもっと詳細に出力し、そして-vvvはデバッグ用です。

    利用可能なコマンド:
      cronjob                            毎日の cronjob を実行
      help                               コマンドのヘルプを表示
      job                                個々のジョブを実行 (ペイロードは標準入力から読み込み)
      list                               コマンドのリストを表示
      version                            Kanboard のバージョンを表示
      worker                             キューワーカーを実行
     データベース
      db:migrate                         SQL のマイグレーションを実行
      db:version                         データベースのスキーマのバージョンを表示
     エクスポート
      export:daily-project-column-stats  毎日のプロジェクトのコラムの統計を CSV でエクスポート (コラム毎・毎日のタスク数)
      export:subtasks                    サブタスクを CSV でエクスポート
      export:tasks                       タスクを CSV でエクスポート
      export:transitions                 タスクの遷移を CSV でエクスポート
     ロケール
      locale:compare                     アプリケーションの翻訳を fr_FR と比較
      locale:sync                        全ての翻訳を fr_FR を元に同期
     通知
      notification:overdue-tasks         期限切れタスクの通知を送る
     プラグイン
      plugin:install                     リモートの Zip アーカイブからプラグインをインストール
      plugin:uninstall                   プラグインを削除
      plugin:upgrade                     インストール済みのプラグインをすべてアップデート
     プロジェクト
      projects:archive                   1年間触られていないプロジェクトを無効化
      projects:archive-activities        1年以上前のプロジェクトのアクティビティを削除
      projects:daily-stats               すべてのプロジェクトの毎日の統計を計算
     trigger
      trigger:tasks                      Trigger scheduler event for all tasks
     user
      user:reset-2fa                     ユーザーの二要素認証を解除
      user:reset-password                ユーザーのパスワードを変更

利用可能なコマンド
------------------

タスクをCSVでエクスポート
~~~~~~~~~~~~~~~~

使用方法:

.. code:: bash

    ./cli export:tasks <project_id> <start_date> <end_date>

例:

.. code:: bash

    ./cli export:tasks 1 2014-10-01 2014-11-30 > /tmp/my_custom_export.csv

CSVデータは `stdout`に送られます。

サブタスクをCSVでエクスポート
~~~~~~~~~~~~~~~~~~~

使用方法:

.. code:: bash

    ./cli export:subtasks <project_id> <start_date> <end_date>

例:

.. code:: bash

    ./cli export:subtasks 1 2014-10-01 2014-11-30 > /tmp/my_custom_export.csv

タスクの推移をCSVでエクスポート
~~~~~~~~~~~~~~~~~~~~~~~~~~~

使用方法:

.. code:: bash

    ./cli export:transitions <project_id> <start_date> <end_date>

例:

.. code:: bash

    ./cli export:transitions 1 2014-10-01 2014-11-30 > /tmp/my_custom_export.csv

毎日の要約データをCSVでエクスポート
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

エクスポートされたデータは標準出力に表示されるでしょう:

.. code:: bash

    ./cli export:daily-project-column-stats <project_id> <start_date> <end_date>

例:

.. code:: bash

    ./cli export:daily-project-column-stats 1 2014-10-01 2014-11-30 > /tmp/my_custom_export.csv

期限切れのタスクの通知を送る
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

通知を有効にしたすべてのユーザーにemailを送信します。

.. code:: bash

    ./cli notification:overdue-tasks

追加のパラメータ:

-  ``--show``: 送信する通知を表示
-  ``--group``: グループの全ての期限切れタスクを一人のユーザーに一通のEmailで送信する
-  ``--manager``: すべての期限切れタスクをプロジェクト管理者に一通のEmailで送信
-  ``-p|--project プロジェクトID|識別子``: 指定したプロジェクトのみの通知を送信

また、``--show``フラグを使用することで、期限切れタスクを表示することもできます。

.. code:: bash

    ./cli notification:overdue-tasks --show
    +-----+---------+------------+------------+--------------+----------+
    | Id  | Title   | Due date   | Project Id | Project name | Assignee |
    +-----+---------+------------+------------+--------------+----------+
    | 201 | Test    | 2014-10-26 | 1          | Project #0   | admin    |
    | 202 | My task | 2014-10-28 | 1          | Project #0   |          |
    +-----+---------+------------+------------+--------------+----------+

プロジェクトでふるい分ける場合の例:

.. code:: bash

    ./cli notification:overdue-tasks --project 123

もしくは、プロジェクト識別子を定義済みならば:

.. code:: bash

    ./cli notification:overdue-tasks --project MY_PROJECT

毎日の統計を計算する
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

このコマンドはプロジェクト毎に統計を計算します:

.. code:: bash

    ./cli projects:daily-stats
    Run calculation for Project #0
    Run calculation for Project #1
    Run calculation for Project #10

タスクのトリガー
~~~~~~~~~~~~~~~~~

このコマンドは、"daily cronjob event"を個々のプロジェクトの未完了タスクに送ります。

.. code:: bash

    ./cli trigger:tasks
    Trigger task event: project_id=2, nb_tasks=1

ユーザーのパスワードを変更する
~~~~~~~~~~~~~~~~~~~

.. code:: bash

    ./cli user:reset-password my_user

画面の指示に従ってパスワードを入力・確認してください。パスワードの文字は画面に表示されません。

ユーザーの二要素認証を削除する
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: bash

    ./cli user:reset-2fa my_user

プラグインをインストールする
~~~~~~~~~~~~~~~~

.. code:: bash

    ./cli plugin:install https://github.com/kanboard/plugin-github-auth/releases/download/v1.0.1/GithubAuth-1.0.1.zip

注意:インストールされたファイルは、コマンドを実行したユーザーと同じアクセス権に設定されます

プラグインを削除する
~~~~~~~~~~~~~~~

.. code:: bash

    ./cli plugin:uninstall Budget

プラグインを更新する
~~~~~~~~~~~~~~~~~~~

.. code:: bash

    ./cli plugin:upgrade
    * Updating plugin: Budget Planning
    * Plugin up to date: Github Authentication

バックグラウンドのワーカーを実行する
~~~~~~~~~~~~~~~~~~~~~

.. code:: bash

    ./cli worker

個々のジョブを実行する (たいていデバッグ目的)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: bash

    echo 'RAW_JOB_DATA' | ./cli job

データベースのマイグレーションを実行する
~~~~~~~~~~~~~~~~~~~~~~~~~~~

``DB_RUN_MIGRATIONS`` パラメーターを ``false`` に設定した場合、データベースのマイグレーションを手動で行う必要があります。

.. code:: bash

    ./cli db:migrate

データベースのスキーマのバージョンを確認する
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: bash

    ./cli db:version
    Current version: 95
    Last version: 96
