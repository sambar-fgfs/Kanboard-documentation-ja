Email の設定
===================

ユーザー設定
-------------

KanboardのユーザーがEMail通知を受け取るためにしなければならない事:

-  ユーザープロフィールで通知を有効にする
-  有効なメールアドレスをプロフィールに登録する
-  通知を受け取るプロジェクトのメンバーになる

注意: 操作を実行したログインユーザーには通知は送信されず、それ以外のプロジェクトメンバーのみが通知を受け取ります。

Email の配送
----------------

複数のEmailの配送方法が利用可能です:

-  SMTP
-  Sendmail
-  PHP ネイティブのメール機能
-  外部プラグインで提供されている、その他の方法: Postmark, Sendgrid, Mailgun

サーバーの設定
---------------

デフォルトでは、KanboardはPHPにバンドルされているメール機能をEmailの送信に利用します。既にサーバーがEmailを送れるように設定済みの場合、それ以上の設定が必要ありません。

しかしながら、別の方法も利用可能で、それはSMTPプロトコルとSendmailです。

SMTP の設定
~~~~~~~~~~~~~~~~~~

``config.default.php`` を ``config.php`` にリネームして、以下の値を変更してください:

.. code:: php

    // "smtp"をメール送信方法として選択する
    define('MAIL_TRANSPORT', 'smtp');

    // サーバーの設定を定義する
    define('MAIL_SMTP_HOSTNAME', 'mail.example.com');
    define('MAIL_SMTP_PORT', 25);

    // SMTPサーバーの認証の設定(必須ではない)
    define('MAIL_SMTP_USERNAME', 'username');
    define('MAIL_SMTP_PASSWORD', 'super password');

また、TLS か SSL による安全な接続も利用できます:

.. code:: php

    define('MAIL_SMTP_ENCRYPTION', 'ssl'); // "null", "ssl", "tls" が利用できます

いくつかのサーバーはHELO(EHLO)コマンドを利用してホスト名に基づくemailの通信を拒否しています(RFC 5321を参照
HELOコマンドで(完全限定ドメイン名である)ホスト名を提供する事を明示するには:

.. code:: php

    define('MAIL_SMTP_HELO_NAME', null); // null (デフォルト)か FQDN が使用できます


Sendmail の設定
~~~~~~~~~~~~~~~~~~~~~~

デフォルトのsendmailコマンドは ``/usr/sbin/sendmail -bs`` ですが、設定ファイルでカスタマイズできます。

例:

.. code:: php

    // "sendmail" をメール送信方法として選択する
    define('MAIL_TRANSPORT', 'sendmail');

    // "sendmail" コマンドを変更する必要がある場合、この値を置き換える
    define('MAIL_SENDMAIL_COMMAND', '/usr/sbin/sendmail -bs');

PHP ビルトインのメール機能
~~~~~~~~~~~~~~~~~~~~~~

これはデフォルトでの設定です:

.. code:: php

    define('MAIL_TRANSPORT', 'mail');

送信者の Email アドレス
~~~~~~~~~~~~~~~~~~~~

デフォルトでは、送信者アドレスが``notifications@kanboard.local`` になっています。これはこのアドレスに返信できません。

設定ファイルの ``MAIL_FROM`` の値を変更することで、このアドレスを変更できます。

.. code:: php

    define('MAIL_FROM', 'kanboard@mydomain.tld');

SMTPサーバーの設定がデフォルトのアドレスを受け付けない場合に便利です。

トラブルシューティング
---------------

設定が正しいにも関わらず、メールが送られてこない場合:

-  迷惑メールフォルダをチェックする
-  デバッグモードを有効にし、 ``data/debug.log`` を確認して、エラーを正確に確認する
-  サーバーかホスティングサービスがメール送信を許可しているか確認する
-  SELinuxを使用している場合、PHPにメール送信を許可する
