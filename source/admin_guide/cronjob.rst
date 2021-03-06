Cron ジョブ
========

正しく働くには、Kanboardは毎日の基本的なバックグラウンドジョブの実行を必要とします。しばしばUnixプラットフォーム上では、このプロセスは ``cron`` が実行します。

このバックグラウンドジョブはこれらのために必要です:

-  レポートと統計(個々のプロジェクトの毎日の統計の計算)
-  期限切れタスクの通知の送信
-  イベント"タスクのためのバックグラウンドジョブ（毎日）" に接続された、自動アクションの実行

Unix・Linuxプラットフォーム上での設定
-----------------------------------------

Unix/Linux上では、これらのcronjobを設定するには複数の方法があります。これはUbuntu 14.04での例です。他のシステムでも手順はよく似ています。

webサーバーのユーザーのcrontabを編集する:

.. code:: bash

    sudo crontab -u www-data -e

毎日午前8時にcronjobを実行する例:

.. code:: bash

    0 8 * * * cd /path/to/kanboard && ./cli cronjob >/dev/null 2>&1

注意: Sqliteを使用している場合はcronjobのプロセスにデータベースに書き込み権限を与える必要があります。通常、webサーバーのユーザーでcronjobを実行すれば十分です。

Microsoft Windows Server での設定
-----------------------------------------

反復タスクを設定する前に、Kanboard CLI スクリプトを実行するバッチファイル(*.bat)を作成してください。

ここに (``C:\kanboard.bat``) の例を示します:

::

    "C:\php\php.exe" -f "C:\inetpub\wwwroot\kanboard\cli" cronjob

**PHPの実行ファイルのパスとKanboardのスクリプトのパスは実際のインストールに合わせなければなりません。**

Windows タスクスケジューラーを設定してください:

1. “管理ツール”を開く
2. “タスクスケジューラ”を開く
3. 右枠内の “タスクの作成”を選択する
4. 例えば、“Kanboard” のように名前を入力する
5. Sqliteを使用している場合は、'セキュリティオプション"の下で、データベースに書き込みできるユーザーを選択する (おそらく、 IIS_IUSRS の設定に依存)
6. "トリガー"を作成し、「毎日」と時間帯を、例えば深夜帯になるように選択してください。
7. 新しい操作の追加で、"プログラムの開始"を選択し、先に作成したバッチファイルを選択してください。

URLを呼び出す設定
------------------------------

利用中のホスティングサービスがCLIアクセスを提供していない場合、URLの呼び出しによってcronjobを実行できます。URLはwebhookトークンを利用することで保護されており、追加のセキュリティのためにHTTPSを経由して呼び出すべきです。

Cron job のURL (URL rewriteが有効な場合)は:
``https://domain.tld/cronjob?token=WEBHOOK_TOKEN_HERE`` です。
