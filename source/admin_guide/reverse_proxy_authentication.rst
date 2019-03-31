リバースプロキシ認証
============================

この認証方法は、しばしば特に大きな組織で `シングルサインオン <https://ja.wikipedia.org/wiki/%E3%82%B7%E3%83%B3%E3%82%B0%E3%83%AB%E3%82%B5%E3%82%A4%E3%83%B3%E3%82%AA%E3%83%B3>`__ (SSO)
に使われます。

この認証は別のシステムで完了するので、Kanboardはパスワードを知らず、あなたも既に認証されていると思うでしょう。

必要要件
------------

同じサーバー上のApache Auth か、 十分な設定がされたリバースプロキシ。

どのように作動しますか?
-------------------

1. リバースプロキシ認証のユーザーは、ユーザー名をHTTPヘッダを通して送ります。
2. Kanboard はユーザー名をリクエストから取得します。

   -  必要に応じ、自動的にユーザーが作成されます。
   -  有効なプロンプトが無いと想定して、新しいKanboardセッションが開かれます。

インストール手順の説明
-------------------------

リバースプロキシのセットアップ
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

この件はこの文書のスコープ外です。リバースプロキシによるユーザーログインが送信するHTTPヘッダを確認すべきで、そこから何かを見つけられるでしょう。

Kanboard の設定
~~~~~~~~~~~~~~~~~~~

カスタム ``config.php`` ファイルを作成するか、 ``config.default.php`` ファイルをコピーします:

.. code:: php

    <?php

    // リバースプロキシ認証を有効/無効にする
    define('REVERSE_PROXY_AUTH', true); // この値をtrueにしてください。

    // HTTP ヘッダーを取得します。指定されない場合、 REMOTE_USERがデフォルトとなります。
    define('REVERSE_PROXY_USER_HEADER', 'REMOTE_USER');

    // 組織で既定のKanboardの管理者を指定します。
    // リバースプロキシによって全てフィルタリングされるべきなので、
    // ブートストラップの管理ユーザーを持つべきです。
    define('REVERSE_PROXY_DEFAULT_ADMIN', 'myadmin');

    // Emailアドレスはデフォルトのドメインであると仮定します。
    // ユーザー名がEmailアドレスで無い場合、自動的に USER@mydomain.comに更新されるでしょう。
    define('REVERSE_PROXY_DEFAULT_DOMAIN', 'mydomain.com');

.. 注意::

    -  プロキシがKanboardを実行しているwebサーバーと同じであるならば、
       `CGI protocol <http://www.ietf.org/rfc/rfc3875>`__ によると、ヘッダーでの名前は ``REMOTE_USER`` になるでしょう。例えば、デフォルトで ``Require valid-user`` をセットするようになっていた場合、 ``REMOTE_USER`` をApacheが追加するでしょう。

    -   ``REVERSE_PROXY_USER_HEADER`` とは違うヘッダーを使用している場合、値の接頭辞は ``HTTP_`` であるべきで、
       それは ``$_SERVER`` 配列から取得されるからです。

    -  Kanboardを動かしているApacheとは別のApacheをリバースプロキシとしている場合、 ``REMOTE_USER``ヘッダーはセットされません (IISとかNginxと同じ動作)

    -  本物のリバースプロキシを持っている場合、`HTTP ICAP draft <http://tools.ietf.org/html/draft-stecher-icap-subid-00#section-3.4>`__
       が提案するヘッダーは ``X-Authenticated-User`` です。これは数多くあるデファクトスタンダードとして採用されたツールです。
