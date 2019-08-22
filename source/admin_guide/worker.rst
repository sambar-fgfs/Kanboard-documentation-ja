バックグラウンドワーカー
==================

.. 警告:: この機能は誰もメンテナンスしていません。自己責任で使用してください。

設定によっては、HTTPリクエストを同じプロセスで処理している場合、アプリケーションのいくつかの機能は速度低下を引き起こし得ます。Kanboardはイベントを監視しているバックグラウンドワーカーにこれらのタスクを委任することができます。

Kanboardの速度低下を起こしうる機能の例:

-  外部SMTPサーバー経由でEMailを送信しているときに数秒の時間が掛かる
-  外部サービスに通知を送る

この追加の機能にはサーバーにキューデーモンのインストールが必要です。

Beanstalk
~~~~~~~~~

`Beanstalk <http://kr.github.io/beanstalkd/>`__ はシンプルで、ワークキューが早いです。

-  Beanstalkのインストールは、単純に使用しているLinuxディストリビューションのパッケージマネージャーが利用できます。
-  `Kanboard plugin for Beanstalk <https://github.com/kanboard/plugin-beanstalk>`__ をインストールしてください。
-  Kanboardのコマンドラインツールからワーカーを開始するには:
   ``./cli worker``

RabbitMQ
~~~~~~~~

`RabbitMQ <https://www.rabbitmq.com/>`__ は、高可用性インフラに適した堅牢なメッセージングシステムです。

-  RabbitMQ の公式文書に従ってインストールと設定をしてください。
-  `Kanboard plugin for RabbitMQ <https://github.com/kanboard/plugin-rabbitmq>`__ をインストールしてください
-  Kanboardのコマンドラインツールからワーカーを開始するには:
   ``./cli worker``

.. 注意::

    -  Kanboardのワーカーの開始はプロセススーパーバイザー (systemd, upstart or supervisord) を使用すべきです。
    -  ローカルのファイルシステム上にファイルを保存する、あるいはSqliteを使用している場合は、そのプロセスがデータフォルダにアクセスする必要があります。
