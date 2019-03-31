FAQ
==========================

Kanboardをホスティングするのにお勧めのサービスはどこですか？
------------------------------------------------------

Kanboardは、 `Digital Ocean <https://www.digitalocean.com/?refcode=4b541f47aae4>`__ や`Linode <https://www.linode.com/?r=4e381ac8a61116f40c60dc7438acc719610d8b11>`__ ,あるいは `Gandi <https://www.gandi.net/>`__　のような、優れたVPSホスティングサービスでうまく動かせます。

KanboardはデフォルトでSQLiteを使用しているため、最良のパフォーマンスを得るには、disk I/Oが早いサービスを選んでください。共有NFSマウントポイントを使用しているホスティングサービスは避けてください。

.. 注意:: 共有ホスティングサービスの利用は推奨しません。自身のサーバーを利用してください。

どうすれば通知にタスクへのリンクを表示できますか?
---------------------------------------------------

これをするには、アプリケーション設定から自分のKanboardのURLを設定する必要があります。
デフォルトでは何も設定されていないので、リンクは表示されません。

例:

-  http://myserver/kanboard/
-  http://kanboard.mydomain.com/

URLの最後のスラッシュ( ``/`` )を忘れないでください。

KanboardはコマンドラインスクリプトからURLを推測できず、特殊なネットワーク設定な人もいるので、これは手動で設定する必要があります。

“There is no suitable CSPRNG installed on your system” エラーが出る
-----------------------------------------------------------------------

PHP 7.0 以前を使用している場合で、 ``open_basedir`` の制限をしている場合 、OpenSSL拡張を有効にするか、アプリケーションから ``/dev/urandom`` へのアクセスを有効にする必要があります。

URLが間違っていて、Page not found が出る (&amp;)
----------------------------------------------

-  ``?controller=auth&action=login&redirect_query=`` の代わりに、
   ``/?controller=auth&amp;action=login&amp;redirect_query=`` のURLが表示される
  
-  そしてKanboardは “Page not found” エラーを返す

この問題はPHPの設定が原因で、 ``arg_separator.output``  がPHPのデフォルト値で無い場合に発生し、これを修正するには別の方法があります:

可能なら、直接 ``php.ini`` 内の値を変更します :

::

    arg_separator.output = "&"

``.htaccess`` で値をオーバーライドする:

::

    php_value arg_separator.output "&"

さもなくば、KanboardはPHPの値でオーバーライドしようとします。

Apache + PHP-FPM でAPIの認証が失敗する
--------------------------------------------------------

デフォルトでは、Apache下のphp-cgiはHTTP Basic user/passはPHPに通りません。この周りを動かすには、下記の行を ``.htaccess`` に追加してください:

::

    RewriteCond %{HTTP:Authorization} ^(.+)$
    RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]

eAccelerator で共通の問題
------------------------------

Kanboardが `eAccelerator <http://eaccelerator.net>`__ と併用するとうまく動かない。この問題はApacheのクラッシュか空白のページを引き起こします:

::

    [Wed Mar 05 21:36:56 2014] [notice] child pid 22630 exit signal Segmentation fault (11)

この問題を回避する最善の方法は、eAccelaratorを無効にするか、 ``eaccelerator.filter`` の設定パラメータでどのファイルをキャッシュしたいかを手動で定義してください。

`eAccelarator プロジェクトは2012年以降活動しておらずアップデートもされていません。 <https://github.com/eaccelerator/eaccelerator/commits/master>`__
我々は最終バージョンのPHPと、それにバンドルされる `OPcache <http://php.net/manual/en/intro.opcache.php>`__ に切り替えることを推奨します。

PHPビルトインのwebサーバーでKanboardをテストするにはどうすれば良いですか?
------------------------------------------------------

localhost上にApacheのようなwebサーバーをインストールしたくないなら、`PHPに組み込まれたweb サーバー <http://www.php.net/manual/en/features.commandline.webserver.php>`__ によってテストできます:

.. code:: bash

    unzip kanboard-VERSION.zip
    cd kanboard
    php -S localhost:8000
    open http://localhost:8000/

Kanboardをインストールorアップグレードした後に空白のページが表示される
---------------------------------------------------------

-  サーバーに要求するものが全て入っているか確認する
-  PHPとApacheのエラーログを確認する
-  ファイルに正しくアクセス権が割り当てられているか確認する
-  aggressive OPCode キャッシュを使用している場合、webサーバーかphp-fpmをリロードする

データベースのマイグレーションの問題を解決する
---------------------------------

-  Kanboardをアップグレードした時、SQLのマイグレーションは自動的に実行されます。
-  Postgres と Mysqlは, 現在のスキーマのバージョン番号をテーブル``schema_version``に保存し、SQLiteは ``user_version`` として保存します。
-  マイグレーションは ``app/Schema/<DatabaseType>.php`` ファイル内で定義されます。
-  個々の関数はマイグレーションのものです。
-  個々のマイグレーションはトランザクションとして実行されます。
-  万が一マイグレーションでエラーが起きた場合、ロールバックが行われます。

アップグレード時には:

-  いつもデータのバックアップを取ってください。
-  複数のプロセスで並行してマイグレーションを実行しないでください。

もし、 "Unable to run SQL migrations […]” エラーが発生した場合、下記の要領で手動で修復してください:

1. 使用しているデータベースに応じて、 ``app/Schema/Sqlite.php`` or ``app/Schema/Mysql.php`` を開く
2. マイグレーションを失敗した関数に移動する
3. その関数内で定義されているSQLクエリを手動で実行する
4. もしエラーが発生した場合、正確なSQLエラーを添えてissueをバグトラッカーに報告してください。
5. 全てのマイグレーションのSQL文を実行したら、スキーマのバージョン番号をアップデートする。
6. その他のマイグレーションを実行する。

Microsoft IIS とInternet Explorerにおいてログインできない
--------------------------------------------------------------

正し認証情報を入力していても毎回 **"Username or password required"** エラーが発生してログインできない場合、セッションに問題が起きています。 

例えば、これらに該当する既知の問題があります:

-  ドメイン名にアンダースコア(_)を使用している:
   ``kanboard_something.mycompany.tld``
-  Microsoft Windows Server と IISを使用している
-  ブラウザにIEを使用している

解決法: **有効なドメイン名とされないため、アンダースコアをドメイン名に使用しない** 

解説:IEはアンダースコアを含むドメイン名のcookieを受け付けず、従って有効で無い。

参照:

-  https://support.microsoft.com/en-us/kb/316112

添付ファイルのサイズ上限を変更するには?
------------------------------------

ファイルのアップロードサイズ上限はKanboard自身では定義しておらず、webサーバーとPHPの設定によります。

``php.ini`` の、以下の行を変更してください:

.. code:: 

    # Set size limit to 20MB
    upload_max_filesize = 20M
    post_max_size = 20M

Nginxを使用している場合、以下の値を定義する:

.. code::

    client_max_body_size 20M;

`<http://nginx.org/en/docs/http/ngx_http_core_module.html#client_max_body_size>`_ を参照願います。

テーブル名のプレフィックスのカスタマイズはできますか?
-----------------------------------------------

簡潔な答え: No.

- Kanboardは自身のデータベースを使用するように設計されています。
- そのために既存のコードを変更するには、変更箇所が多すぎます。
- 複数のソフトウェアで同じデータベースを使用するのは悪い習慣です (共有ホスティングサービスは推奨しません。)

なぜ公式にネイティブなモバイルアプリケーションが無いのですか?
---------------------------------------------------

ネイティブモバイルアプリケーションの開発はコミュニティで行っています。

- 個々のプラットフォーム(iOS/Android)・デバイスのタイプ(スマートフォン/タブレット)向けにネイティブモバイルアプリケーションを開発するには、多くの作業とお金が必要です。
- これにはwebアプリケーションの開発とは違ったスキルが必要になります。
- 高品質なアプリケーションを開発するには、個々のプラットフォームごとに公式なSDKを使わなければなりません。結局、同じアプリケーションを2回開発することになります。
- 無料のソフトウェアであっても、モバイルアプリをストア(App Store/Play Store)で配布するのには費用が掛かり、配布者が支払わなければなりません。
- Web UIは反応が良く、完璧では無くても何かを素早く確認できます。
- 小さい画面でボードを使うのは実用的ではありません。
