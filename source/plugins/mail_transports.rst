Mail 送信
==============

デフォルトでは、 Kanboard は3つの標準的なメールの送信をサポートしています:

-  Mail (PHP mail 関数)
-  SMTP
-  Sendmail コマンド

プラグインAPIによって、Email送信の方法を追加することができます。例えば、HTTP APIを使ってメールを送信するプラグインを追加することができます。

実装
--------------

あなたのプラグインは ``Kanboard\Core\Mail\ClientInterface`` インターフェースで実装し、また ``Kanboard\Core\Base`` から拡張しなければなりません。

実装しなければならないメソッドは ``sendEmail()`` だけです:

.. code:: php

    interface ClientInterface
    {
        /**
         * HTML emailを送信する
         *
         * @access public
         * @param  string $recipientEmail
         * @param  string $recipientName
         * @param  string $subject
         * @param  string $html
         * @param  string $authorName
         * @param  string $authorEmail
         */
        public function sendEmail($recipientEmail, $recipientName, $subject, $html, $authorName, $authorEmail = '');
    }

新しいメール送信を登録するには、 ``Kanboard\Core\Mail\Client`` クラスの ``setTransport($transport, $class)`` メソッドを使用してください:

.. code:: php

    $this->emailClient->setTransport('myprovider', '\Kanboard\Plugin\MyProvider\MyEmailHandler');

2つめの引数は絶対的な名前空間を含むコンクリートクラスです。

メール送信プラグインの例
----------------------------------

-  `Sendgrid <https://github.com/kanboard/plugin-sendgrid>`__
-  `Mailgun <https://github.com/kanboard/plugin-mailgun>`__
-  `Postmark <https://github.com/kanboard/plugin-postmark>`__
