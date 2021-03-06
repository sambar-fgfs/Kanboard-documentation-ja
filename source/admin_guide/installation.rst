インストール手順の説明
=========================

.. 注意:: 先に進む前に :ref:`システム要件 <requirements>` を確認してください。

アーカイブよりインストール (安定版)
---------------------------------

1. PHPがインストールされたWebサーバーが必要です。
2.  `ソースコード <https://github.com/kanboard/kanboard/releases/latest>`_ をダウンロードして、 ``kanboard`` ディレクトリを適切な場所にコピーしてください。
3.  ``data`` ディレクトリがwebサーバーのユーザーが書き込み出来ることを確認してください。
4. ブラウザで http://yourpersonalserver/kanboard を開いてください。
5. デフォルトのログイン名とパスワードは **admin/admin** です。
6. ソフトウェアの使用を開始してください。
7. パスワードの変更を忘れないようにしてください。

``data`` フォルダには以下のものが保存されます:

-  Sqlite のデータベース: ``db.sqlite``
-  デバッグファイル: ``debug.log`` (デバッグモードが有効で、ドライバが ``file`` の場合)
-  アップロードされたファイル: ``files/*``
-  画像サムネイル: ``files/thumbnails/*``

リモートのデータベース (Mysql/Postgresql) を使用し、かつ(AWS S3 の類の)オブジェクトストレージを使用している場合、必ずしもローカルの恒久的なデータフォルダや、フォルダのアクセス権の変更は必要ありません。

Gitリポジトリからインストール (開発版)
---------------------------------------------

1. ``git clone https://github.com/kanboard/kanboard.git``
2. 上述の3番に進む

注意: この方法は **現在開発中のバージョン** をインストールするため、自己責任で使用してください。

.. 警告::  **セキュリティ対策:**

    -  デフォルトのユーザー名/パスワードの変更を忘れないようにしてください。
    -  ``data`` ディレクトリへはURLから誰でもアクセス出来るようにしないでください。``.htaccess`` ファイルと、 ``web.config`` ファイルはApache/IIS向けに含まれており、それ以外のwebサーバーには手動で設定しなければならない。
