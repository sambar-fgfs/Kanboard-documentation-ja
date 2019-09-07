LDAP ライブラリ
============

LDAPの統合を容易にするため、 Kanboard は自身で LDAP ライブラリを持ちます。このライブラリは共通の動き方をすることができます。

クライアント
------

クラス: ``Kanboard\Core\Ldap\Client``

LDAP サーバーへの接続は簡単で、以下のメソッドを使用します:

.. code:: php

    use Kanboard\Core\Ldap\Client as LdapClient;
    use Kanboard\Core\Ldap\ClientException as LdapException;

    try {
        $client = LdapClient::connect();

        // Get native LDAP resource
        $resource = $client->getConnection();

        // ...

    } catch (LdapException $e) {
        // ...
    }

LDAP のクエリ
------------

クラス:

-  ``Kanboard\Core\Ldap\Query``
-  ``Kanboard\Core\Ldap\Entries``
-  ``Kanboard\Core\Ldap\Entry``

LDAP ディレクトリへのクエリの例:

.. code:: php


    $query = new Query($client)
    $query->execute('ou=People,dc=kanboard,dc=local', 'uid=my_user', array('cn', 'mail'));

    if ($query->hasResult()) {
        $entries = $query->getEntries(); // Return an instance of Entries
    }

一つのエントリーを読み込む:

.. code:: php

    $firstEntry = $query->getEntries()->getFirstEntry();
    $email = $firstEntry->getFirstValue('mail');
    $name = $firstEntry->getFirstValue('cn', 'Default Name');

複数のエントリーを読み込む:

.. code:: php

    foreach ($query->getEntries()->getAll() as $entry) {
        $emails = $entry->getAll('mail'); // Fetch all emails
        $dn = $entry->getDn(); // Get LDAP DN of this user

        // Check if a value is present for an attribute
        if ($entry->hasValue('mail', 'user2@localhost')) {
            // ...
        }
    }

ユーザーのヘルパー
-----------

クラス: ``Kanboard\Core\Ldap\User``

一人のユーザーについて1行で取得:

.. code:: php

    // Return an instance of LdapUserProvider
    $user = User::getUser($client, 'my_username');

グループのヘルパー
------------

クラス: ``Kanboard\Core\Ldap\Group``

グループについて1行で取得:

.. code:: php

    // Define LDAP filter
    $filter = '(&(objectClass=group)(sAMAccountName=My group*))';

    // Return a list of LdapGroupProvider
    $groups = Group::getGroups($client, $filter);
