LDAP のグループの同期
==========================

.. 注意::

    - ネストグループは実装されていないので、もしこの機能が必要ならプルリクエストを送ってください。

必要要件
------------

-  LDAP認証が正しく設定されている
-  使用しているLDAPサーバーが ``memberOf`` か ``memberUid`` (PosixGroups) をサポートしている

LDAPグループに基づいて自動的にユーザーの役割を定義する
----------------------------------------------------

設定ファイル内でこれらの定数を使用します:

-  ``LDAP_GROUP_ADMIN_DN``: アプリケーションの管理者を識別するための名前
-  ``LDAP_GROUP_MANAGER_DN``: アプリケーションでのプロジェクト管理者を識別する名前

Active Directory の例:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: php

    define('LDAP_GROUP_ADMIN_DN', 'CN=Kanboard Admins,CN=Users,DC=kanboard,DC=local');
    define('LDAP_GROUP_MANAGER_DN', 'CN=Kanboard Managers,CN=Users,DC=kanboard,DC=local');

-  “Kanboard Admins” のメンバーは、 “管理者” の役割を持ちます
-  “Kanboard Managers” のメンバーは “プロジェクト管理者” の役割を持ちます
-  それ以外のすべての人は “ユーザー” の役割を持ちます

OpenLDAP と Posix Groups による例:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: php

    define('LDAP_GROUP_BASE_DN', 'ou=Groups,dc=kanboard,dc=local');
    define('LDAP_GROUP_USER_FILTER', '(&(objectClass=posixGroup)(memberUid=%s))');
    define('LDAP_GROUP_ADMIN_DN', 'cn=Kanboard Admins,ou=Groups,dc=kanboard,dc=local');
    define('LDAP_GROUP_MANAGER_DN', 'cn=Kanboard Managers,ou=Groups,dc=kanboard,dc=local');

LDAPサーバーが ``memberOf`` の代わりに  ``memberUid`` を使用する場合、 ``LDAP_GROUP_USER_FILTER`` を  **定義しなければなりません** 。この例に出ているすべてのパラメータは必須です。

自動的にプロジェクトでの権限のためにLDAPグループを読み込む
------------------------------------------------------

この機能はLDAPのグループとKanboardのグループを自動的に同期することを可能にします。各々のグループに個々のプロジェクトの役割を割り当てられます。

プロジェクトの権限ページで、オートコンプリートのフィールドでグループを入力でき、Kanboardは有効化済みの外部プロバイダのグループを検索できます。

ローカルのデータベース上にそのグループが存在しない場合、自動的に同期されます。

-  ``LDAP_GROUP_PROVIDER``: LDAPグループプロバイダを有効にする
-  ``LDAP_GROUP_BASE_DN``: LDAPディレクトリでのグループ識別名
-  ``LDAP_GROUP_FILTER``: LDAP フィルターを使用するために実行するクエリ
-  ``LDAP_GROUP_ATTRIBUTE_NAME``: グループ名を取得するために使用するLDAP 属性

.. _example-for-active-directory-1:

Active Directory の例:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: php

    define('LDAP_GROUP_PROVIDER', true);
    define('LDAP_GROUP_BASE_DN', 'CN=Groups,DC=kanboard,DC=local');
    define('LDAP_GROUP_FILTER', '(&(objectClass=group)(sAMAccountName=%s*))');

先に例示したフィルターによって、Kanboardはクエリにマッチするグループを検索します。あなたがエンドユーザーなら、オートコンプリートのボックスに "My group" と入力するとKanboardは ``(&(objectClass=group)(sAMAccountName=My group*))`` にマッチするすべてのグループを返します。

-  注意1:  ``*`` の特殊文字がここで重要になり、 **それ以外の部分は完全一致とされます** 。
-  注意2: この機能はLDAP認証が "proxy" モードか "anonymous" モードに設定されている場合のみ互換性があります。

` 更なるActive Directory のLDAPフィルターの例  <http://social.technet.microsoft.com/wiki/contents/articles/5392.active-directory-ldap-syntax-filters.aspx>`__

.. _example-for-openldap-with-posix-groups-1:

OpenLDAP と Posix Groups による例:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: php

    define('LDAP_GROUP_PROVIDER', true);
    define('LDAP_GROUP_BASE_DN', 'ou=Groups,dc=kanboard,dc=local');
    define('LDAP_GROUP_FILTER', '(&(objectClass=posixGroup)(cn=%s*))');
