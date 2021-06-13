URL Rewriting
=============

KanboardはURL rewritingが有効/無効にかかわらず動作可能です。

-  URL rewriteで書き換えられたURLの例: ``/board/123``
-  それ以外: ``?controller=board&action=show&project_id=123``

KanboardをApache上で使用していて、rewriteモードが有効な場合、自動的に分かりやすいURLを使用します。“404 Not Found”を返された場合、少なくとも DocumentRootへ.httaccessファイルが効くように、以下のようにオーバーライドする必要があります。

.. code:: sh

    <Directory /var/www/kanboard/>
        AllowOverride FileInfo Options=All,MultiViews AuthConfig
    </Directory>

URL ショートカット
-------------

-  タスク #123 を表示: **/t/123**
-  プロジェクト #2 のボードを表示: **/b/2**
-  プロジェクト #5 のカレンダーを表示: **/c/5**
-  プロジェクト #8 のリストビューを表示: **/l/8**
-  プロジェクト #42 のプロジェクト設定を表示: **/p/42**

設定
-------------

デフォルトでは、KanboardはApacheがrewriteが有効かチェックします。

WebサーバーのURL rewriteの自動検出を回避するには、以下のように設定ファイルに記述します。

.. code:: php

    define('ENABLE_URL_REWRITE', true);

この定数を ``true`` にした場合:

-  また、コマンドラインツールからも変換されたURLを生成します。
-  NginxかMicrosoft IISのような、Apacheではないwebサーバーを使用しているなら、あなた自身がURL rewitingの設定をしなければなりません。

注意: Kanboard はこの設定ができていない場合、いつでも従来通りのURLにフォールバックします。この設定は任意です。

Nginx での設定例
---------------------------

Nginxの設定ファイルの ``server`` セクションで使用可能な例:

.. code:: bash

    index index.php;

    location / {
        try_files $uri $uri/ /index.php$is_args$args;

        # If Kanboard is under a subfolder
        # try_files $uri $uri/ /kanboard/index.php;
    }

    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/var/run/php5-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_index index.php;
        include fastcgi_params;
    }

    # Deny access to the directory data
    location ~* /data {
        deny all;
        return 404;
    }

    # Deny access to .htaccess
    location ~ /\.ht {
        deny all;
        return 404;
    }

Kanboard 内の``config.php`` では:

.. code:: php

    define('ENABLE_URL_REWRITE', true);

Kanboardがサブフォルダに入っているときの例:

::

    server {
        listen 443 ssl default_server;
        listen [::]:443 ssl default_server;

        root /var/www/html;
        index index.php index.html index.htm;
        server_name _;

        location / {
            try_files $uri $uri/ =404;
        }

        location ^~ /kanboard {

            location /kanboard {
                try_files $uri $uri/ /kanboard/index.php$is_args$args;
            }

            location ~ ^/kanboard/(?:kanboard|config.php|config.default.php) {
                deny all;
            }

            location ~* /kanboard/data {
                deny all;
            }

            location ~ \.php(?:$|/) {
                fastcgi_split_path_info ^(.+\.php)(/.+)$;
                fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
                fastcgi_param PATH_INFO $fastcgi_path_info;
                fastcgi_param HTTPS on; # Use only if HTTPS is configured
                include fastcgi_params;
                fastcgi_pass unix:/var/run/php5-fpm.sock;
            }

            location ~ /kanboard/\.ht {
                deny all;
            }
        }
    }

先ほどの例を参考に、あなたの環境に合わせて設定してください。

Lighttpd での設定例
------------------------------

1. "mod_rewrite" を有効にする
.. code::
    
    server.modules += (
        "mod_rewrite",
        ...
        ...
    )
1. lighttpd.confの関連するセクションにurl rewritesを追記する(この例では、ホストは example.com)。 また、assetsディレクトリを保持し、faviconを固定する場合では:
.. code::
    
    $HTTP["host"] == "example.com" {
      server.document-root = "/var/www/kanboard/"
      url.rewrite-once = (
        "^(/[^\?]*)(\?.*)?" => "/index.php$2",
        "^/assets/.+" => "$0",
        "^/favicon\.png$" => "$0",
      )
    }

1. Lighttpd config を再読み込みする: 
.. code::
    
    /etc/init.d/lighttpd reload
    
IIS での設定例
-------------------------

1.  `ここ <http://www.iis.net/learn/extensions/url-rewrite-module/using-the-url-rewrite-module>`__ からIISの Rewrite モジュールをダウンロードしてインストールする:
2. インストール先フォルダに web.config ファイルを作る :

.. code:: xml

    <?xml version="1.0"?>
    <configuration>
        <system.webServer>
            <defaultDocument>
                <files>
                    <clear />
                    <add value="index.php" />
                </files>
            </defaultDocument>
            <rewrite>
                <rules>
                    <rule name="Kanboard URL Rewrite" stopProcessing="true">
                        <match url="^(.*)$" ignoreCase="false" />
                        <conditions logicalGrouping="MatchAll">
                            <add input="{REQUEST_FILENAME}" matchType="IsFile" ignoreCase="false" negate="true" />
                        </conditions>
                        <action type="Rewrite" url="index.php" appendQueryString="true" />
                    </rule>
                </rules>
            </rewrite>
        </system.webServer>
    </configuration>

Kanboard 内の``config.php`` では:

.. code:: php

    define('ENABLE_URL_REWRITE', true);

先ほどの例を参考に、あなたの環境に合わせて設定してください。
