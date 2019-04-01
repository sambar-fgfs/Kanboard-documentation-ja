Kanboard を Heroku でデプロイする
=========================

Kanboardを無料で `Heroku <https://www.heroku.com/>`__ で試すことができます。
このワンクリックインストールボタンを使用するか、以下の手順に従って手動で構築することができます:

|デプロイ|

必要要件
------------

-  無料アカウントで良いので、Heroku アカウント
-  Heroku コマンドラインツールがインストールされている

手動構築手順の説明
-------------------

.. code:: bash

    # 最新の開発版を入手する
    git clone https://github.com/kanboard/kanboard.git
    cd kanboard

    # Herokuにコードをpushする (git over HTTP が使用できない場合、SSHも使用可能)
    heroku create
    git push heroku master

    # Postgresql データベースと共に新しい dyno を起動する 
    heroku ps:scale web=1
    heroku addons:add heroku-postgresql:hobby-dev

    # ブラウザを開く
    heroku open

制限事項
-----------

Heroku上のローカルディスクストレージは一時的なものです:

-  アップロードしたファイルは再起動後は恒久的ではありません。望むならば `Amazon S3 <https://github.com/kanboard/plugin-s3>`__ のようなクラウドストレージにインストールしたプラグインのファイルを保存できます。
-  webインターフェース経由でインストールされたプラグインはローカルファイルシステム上に保存されます。自身のKanboardのコピーにプラグインを含めて展開することもできます。

Kanboardのいくつかの特徴は、毎日のバックグラウンドジョブの実行を必要とします。

.. |デプロイ| image:: https://www.herokucdn.com/deploy/button.png
   :target: https://heroku.com/deploy?template=https://github.com/kanboard/kanboard
