LDAP User Profile Photo
=======================

Kanboard はLDAPサーバーからユーザーの画像を自動的にダウンロードします。

この機能はLDAP認証が有効で、 ``LDAP_USER_ATTRIBUTE_PHOTO`` のパラメータが定義されている場合のみ有効になります。

設定
-------------

``config.php`` 内で、画像の保存に使用するLDAP属性を設定しなければなりません。

.. code:: php

    define('LDAP_USER_ATTRIBUTE_PHOTO', 'jpegPhoto');

通常、 ``jpegPhoto`` か ``thumbnailPhoto`` の属性が使用されます。
保存可能な画像はJPEGとPNGフォーマットです。

ユーザープロファイルの画像をアップロードするために、 Active Directoryの管理者は  `AD Photo
Edit <http://www.cjwdev.co.uk/Software/ADPhotoEdit/Info.html>`__ のようなソフトウェアを利用できます。

.. 注意::

    プロフィール画像は **ユーザーが今まで画像をアップロードしていない場合、ログイン時にダウンロードされるだけです**。

    ユーザーの写真を変更するには、ユーザープロフィールから以前の画像を手動で削除してください。
