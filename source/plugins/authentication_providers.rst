認証プロバイダ
========================

新しい認証のバックエンドは非常に少ない行数のコードで書くことができます。

プロバイダの登録
---------------------

プラグイン中の ``initialize()`` メソッド内で ``AuthenticationManager`` クラス内の ``register()``  メソッドを呼ぶ事ができます:

.. code:: php

    public function initialize()
    {
        $this->authenticationManager->register(new ReverseProxyLdapAuth($this->container));
    }

オブジェクトが提供する ``register()`` メソッドは定義済み認証インターフェースの一つを実装しなければなりません。

これらのインターフェースは ``Kanboard\Core\Security`` 内の名前空間で定義されています:

-  ``Kanboard\Core\Security\PreAuthenticationProviderInterface``
-  ``Kanboard\Core\Security\PostAuthenticationProviderInterface``
-  ``Kanboard\Core\Security\PasswordAuthenticationProviderInterface``
-  ``Kanboard\Core\Security\OAuthAuthenticationProviderInterface``

インターフェースを実装することのみが必要で、あなたはクラスをどのようにも書くことが出来て、またディスク上のどこにでも置くことができます。

ユーザープロバイダ
-------------

認証が成功した時、あなたのドライバはオブジェクトを返してユーザーに再提供しなければなりません。このオブジェクトは ``Kanboard\Core\User\UserProviderInterface`` で実装されていなければなりません。

認証プラグインの例
---------------------------------

-  `Kanboard に含まれる認証プロバイダ <https://github.com/kanboard/kanboard/tree/master/app/Auth>`__
-  `LDAP をサポートした リバースプロキシ認証 <https://github.com/kanboard/plugin-reverse-proxy-ldap>`__
-  `SMS 二要素認証 <https://github.com/kanboard/plugin-sms-2fa>`__
