API 認証
==================

.. 警告:: Kanboard v1.2.8 以降では、ユーザーが2要素認証を利用するにはAPIキーを有効化しなければなりません。

API エンドポイント
------------

URL: ``https://YOUR_SERVER/jsonrpc.php``

デフォルトの方法 (HTTP Basic)
---------------------------

アプリケーションの資格情報
~~~~~~~~~~~~~~~~~~~~~~~

-  Username: ``jsonrpc``
-  Password: 設定ページにあるAPIトークン

ユーザーの資格情報
~~~~~~~~~~~~~~~~

-  Username: ユーザー名
-  Password: ユーザーのパスワードor個人のアクセストークン

APIは `RFC2617 <http://www.ietf.org/rfc/rfc2617.txt> `__ で説明されるHTTP Basic 認証スキームを使用します。

カスタム HTTP ヘッダー
------------------

もしサーバーが非常に特殊な設定をしている場合、代替のHTTPヘッダーを認証に使用できます。

-  ヘッダー名は何でも良く、例えば ``X-API-Auth`` のようにできます。
-  ヘッダーの値は ``ユーザー名:パスワード`` をBase64でエンコードしたものです。

設定:

1. ``config.php`` 内でカスタムヘッダーを定義します:
   ``define('API_AUTHENTICATION_HEADER', 'X-API-Auth');``
2. 資格情報を Base64 でエンコードしてください。 PHPでの例は、
   ``base64_encode('jsonrpc:19ffd9709d03ce50675c3a43d1c49c1ac207f4bc45f06c5b2701fbdf8929');``
3. curlでテストします:

.. code:: bash

    curl \
    -H 'X-API-Auth: anNvbnJwYzoxOWZmZDk3MDlkMDNjZTUwNjc1YzNhNDNkMWM0OWMxYWMyMDdmNGJjNDVmMDZjNWIyNzAxZmJkZjg5Mjk=' \
    -d '{"jsonrpc": "2.0", "method": "getAllProjects", "id": 1}' \
    http://localhost/kanboard/jsonrpc.php

認証エラー
--------------------

資格情報が正しくない場合、 ``401 Not Authorized`` と、対応するJSONレスポンスを返します。

認可エラー
-------------------

接続しているユーザーがリソースへのアクセスを許可されていないなら、 ``403 Forbidden``を返します。
