LDAP 認証
===================

必要要件
------------

-  PHP LDAP 拡張が有効であること
-  LDAP サーバー:
   -  OpenLDAP
   -  Microsoft Active Directory
   -  Novell eDirectory

ワークフロー
--------

LDAP認証が有効な場合、ログインプロセスは下記のように働きます:

1. 最初に、データベースを使用してユーザーの認証を試みます。
2. データベース内にユーザーが見つからない場合、LDAP認証を行います。
3. LDAP認証が成功した場合、デフォルトではLDAPユーザーとしてマークされ、パスワード不要でログイン出来るローカルユーザーが自動的に作成されます。

LDAP サーバーから自動的にフルネームとEMailアドレスを取得します。

認証タイプ
--------------------

+-----------+----------------------------------------------------------+
| タイプ    | 概要                                                     |
+===========+==========================================================+
| ローカル  | Kanboardのデータベースにパスワードが保存されるユーザー   |
| ユーザー  |                                                          |
+-----------+----------------------------------------------------------+
| リモート  | 別のシステムによって管理されるユーザー                   |
| ユーザー  | (例:LDAP サーバー)                                       |
+-----------+----------------------------------------------------------+

.. 注意::

    推奨する認証方法は ``Proxy`` です。

Anonymous モード
~~~~~~~~~~~~~~

.. code:: php

    define('LDAP_BIND_TYPE', 'anonymous');
    define('LDAP_USERNAME', null);
    define('LDAP_PASSWORD', null);

これはデフォルトの値ですが、いくつかのLDAPサーバーはセキュリティ上の理由によりanonymous ブラウズを容認しません。

Proxy モード
~~~~~~~~~~

特定のユーザーをLDAPディレクトリのブラウズに使用します:

.. code:: php

    define('LDAP_BIND_TYPE', 'proxy');
    define('LDAP_USERNAME', 'my proxy user');
    define('LDAP_PASSWORD', 'my proxy password');

User モード
~~~~~~~~~

この方法はエンドユーザーから供給された認証情報を使用します。

例えば、Microsoft Active Directoryはデフォルトではanonymousブラウジングを許容していませんが、proxyユーザーを使用したくない場合にこの方法が使用できます。

.. code:: php

    define('LDAP_BIND_TYPE', 'user');
    define('LDAP_USERNAME', '%s@kanboard.local');
    define('LDAP_PASSWORD', null);

このケースでは、 ``LDAP_USERNAME``  定数はLDAPユーザーネームを使用するパターンマッチングになっており、例えば:

-  ``%s@kanboard.local`` は、 ``my_user@kanboard.local`` に置き換えられます
-  ``KANBOARD\\%s`` は、  ``KANBOARD\my_user`` に置き換えられます

ユーザーのLDAPフィルター
----------------

設定パラメータの ``LDAP_USER_FILTER`` は、LDAPディレクトリからユーザーを見つけるのに使用されます。

例:

-  ``(&(objectClass=user)(sAMAccountName=%s))`` は、
   ``(&(objectClass=user)(sAMAccountName=my_username))`` に置き換えられます
-  ``uid=%s`` は ``uid=my_username`` に置き換えられます

その他の例は  `filters for Active
Directory <http://social.technet.microsoft.com/wiki/contents/articles/5392.active-directory-ldap-syntax-filters.aspx>`__ を参照願います。

Kanboardへのアクセスをフィルタリングする例:

``(&(objectClass=user)(sAMAccountName=%s)(memberOf=CN=Kanboard Users,CN=Users,DC=kanboard,DC=local))``

この例では、 "Kanboard Users"  グループのメンバーだけがKanboardに接続できます。

Microsoft Active Directory の例
--------------------------------------

我々のドメイン名が ``KANBOARD`` (kanboard.local) で、プライマリコントローラが ``myserver.kanboard.local`` の場合を述べます。

最初の例はproxy モードです:

.. code:: php

    <?php

    // LDAP 認証を有効にする (デフォルトは false)
    define('LDAP_AUTH', true);

    define('LDAP_BIND_TYPE', 'proxy');
    define('LDAP_USERNAME', 'administrator@kanboard.local');
    define('LDAP_PASSWORD', 'my super secret password');

    // LDAP サーバーのホスト名
    define('LDAP_SERVER', 'myserver.kanboard.local');

    // LDAP プロパティ
    define('LDAP_USER_BASE_DN', 'CN=Users,DC=kanboard,DC=local');
    define('LDAP_USER_FILTER', '(&(objectClass=user)(sAMAccountName=%s))');

2つ目の例は user モードです:

.. code:: php

    <?php

    // LDAP 認証を有効にする (デフォルトは false)
    define('LDAP_AUTH', true);

    define('LDAP_BIND_TYPE', 'user');
    define('LDAP_USERNAME', '%s@kanboard.local');
    define('LDAP_PASSWORD', null);

    // LDAP サーバーのホスト名
    define('LDAP_SERVER', 'myserver.kanboard.local');

    // LDAP プロパティ
    define('LDAP_USER_BASE_DN', 'CN=Users,DC=kanboard,DC=local');
    define('LDAP_USER_FILTER', '(&(objectClass=user)(sAMAccountName=%s))');

OpenLDAP の例
--------------------

我々のLDAPサーバーが ``myserver.example.com`` で、すべてのユーザー情報が ``ou=People,dc=example,dc=com`` に保存されているものとします。

この例は、anonymous bindingを使用します。

.. code:: php

    <?php

    // LDAP 認証を有効にする (デフォルトは false)
    define('LDAP_AUTH', true);

    // LDAP サーバーのホスト名
    define('LDAP_SERVER', 'myserver.example.com');

    // LDAP プロパティ
    define('LDAP_USER_BASE_DN', 'ou=People,dc=example,dc=com');
    define('LDAP_USER_FILTER', 'uid=%s');

LDAPS (SSLによる暗号化) の例
----------------------------------

いくつかの LDAP サーバーは "LDAPS" 接続 (ポート:636) のみに設定されます。これはTLSとは異なり、平分で開始されますが(ポート:デフォルトで389)、その後同チャンネル上で暗号化をセットアップします。

PHP に LDAPS 使用を指示するために、後述する例のようにLDAPサーバーの前に "ldaps://"  のプレフィックスを付ける必要があります。

我々の LDAP サーバーは ``myserver.example.com`` で、LDAPS経由でのアクセスのみ可能です。だいたいの場合はサーバー証明書の検証をしたくないので、TLSを使用したくありません。

この例は、anonymous bindingを使用します。

.. code:: php

    <?php

    // LDAP 認証を有効にする (デフォルトは false)
    define('LDAP_AUTH', true);

    // LDAP サーバーのホスト名
    define('LDAP_SERVER', 'ldaps://myserver.example.com');

    // デフォルトでは、 ldaps:// 様式のURLには検証が必要ですfalseにすると検証をスキップします。
    define('LDAP_SSL_VERIFY', false);

    // LDAP START_TLS を有効にする
    define('LDAP_START_TLS', false);;

Disable Automatic Account Creation
----------------------------------

デフォルトでは、Kanboardはユーザーアカウントが見つからない場合に自動的にアカウントを作成します。

ユーザーアカウントを手動で作成する場合、Kanboardを使用する人を制限するためにこの動作を無効化できます。

``LDAP_ACCOUNT_CREATION`` の値を ``false`` にするだけです:

.. code:: php

    // 自動的にユーザーアカウントを作成
    define('LDAP_ACCOUNT_CREATION', false);

同期
---------------

デフォルトでは、Kanboard はユーザー名を除くすべてのフィールド (role, name, email...) を同期します。

この挙動を変更したい場合、この設定パラメータを使用してください:

.. code:: bash

    // この例では、LDAPからKanboardにフィールド "username" と "role" を同期しません。
    define('EXTERNAL_AUTH_EXCLUDE_FIELDS', 'username,role');

トラブルシューティング
---------------

SELinux の制限
~~~~~~~~~~~~~~~~~~~~

SELinuxが有効な場合、ApacheからLDAPサーバーに届くようにしなければなりません。

-  SELinuxをpermissiveモードか無効に切り替えることができます(非推奨)
-  全てのネットワーク接続を許容することができ、例えば
   ``setsebool -P httpd_can_network_connect=1`` か、それ以上の制限的なルールを持たせることができます。

いずれにせよ、Redhat/CentOSの公式文書を参照願います。

デバッグモード
~~~~~~~~~~

LDAP認証が正しくセットアップできない場合、デバッグモードを有効にして、ログファイルを見ることができます。
