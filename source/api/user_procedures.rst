ユーザー操作の API プロシージャ
===================

createUser
----------

-  用途: **ユーザーの新規作成**
-  パラメーター:

   -  **username** ユニークでなければなりません (string, 必須)
   -  **password** 少なくとも6文字は必要です (string, 必須)
   -  **name** (string, 任意)
   -  **email** (string, 任意)
   -  **role** (string, 任意。例: app-admin, app-manager, app-user)

-  成功時の返り値: **user_id**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "createUser",
        "id": 1518863034,
        "params": {
            "username": "biloute",
            "password": "123456"
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1518863034,
        "result": 22
    }

createLdapUser
--------------

-  用途: **LDAP認証を行うユーザーの新規作成**
-  パラメーター:

   -  **username** (string, 必須)

-  成功時の返り値: **user_id**
-  失敗時の返り値: **false**

LDAPサーバー上のユーザーがいる場合のみKanboardのユーザーが作成されます。この方法はLDAP認証が "proxy" モードか "anonymous" モードに設定されている場合のみ動作します。

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "createLdapUser",
        "id": 1518863034,
        "params": {
            "username": "my_ldap_user",
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1518863034,
        "result": 22
    }

getUser
-------

-  用途: **ユーザーの情報を取得する**
-  パラメーター:

   -  **user_id** (integer, 必須)

-  成功時の返り値: **ユーザーのプロパティ**
-  失敗時の返り値: **null**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getUser",
        "id": 1769674781,
        "params": {
            "user_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1769674781,
        "result": {
            "id": "1",
            "username": "biloute",
            "password": "$2y$10$dRs6pPoBu935RpmsrhmbjevJH5MgZ7Kr9QrnVINwwyZ3.MOwqg.0m",
            "role": "app-user",
            "is_ldap_user": "0",
            "name": "",
            "email": "",
            "google_id": null,
            "github_id": null,
            "notifications_enabled": "0"
        }
    }

getUserByName
-------------

-  用途: **ユーザーの情報を取得する**
-  パラメーター:

   -  **username** (string, 必須)

-  成功時の返り値: **ユーザーのプロパティ**
-  失敗時の返り値: **null**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getUserByName",
        d"id": 1769674782,
        "params": {
            "username": "biloute"
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1769674782,
        "result": {
            "id": "1",
            "username": "biloute",
            "password": "$2y$10$dRs6pPoBu935RpmsrhmbjevJH5MgZ7Kr9QrnVINwwyZ3.MOwqg.0m",
            "role": "app-user",
            "is_ldap_user": "0",
            "name": "",
            "email": "",
            "google_id": null,
            "github_id": null,
            "notifications_enabled": "0"
        }
    }

getAllUsers
-----------

-  用途: **有効な全てのユーザーを取得する**
-  パラメーター:

   -  **none**

-  成功時の返り値: **ユーザーのリスト**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getAllUsers",
        "id": 1438712131
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1438712131,
        "result": [
            {
                "id": "1",
                "username": "biloute",
                "name": "",
                "email": "",
                "role": "app-user",
                "is_ldap_user": "0",
                "notifications_enabled": "0",
                "google_id": null,
                "github_id": null
            }
        ]
    }

updateUser
----------

-  Purpose: **ユーザーをアップデートする**
-  パラメーター:

   -  **id** (integer)
   -  **username** (string, 任意)
   -  **name** (string, 任意)
   -  **email** (string, 任意)
   -  **role** (string, 任意。例: app-admin, app-manager, app-user)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "updateUser",
        "id": 322123657,
        "params": {
            "id": 1,
            "role": "app-manager"
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 322123657,
        "result": true
    }

removeUser
----------

-  用途: **ユーザーを削除する**
-  パラメーター:

   -  **user_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "removeUser",
        "id": 2094191872,
        "params": {
            "user_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 2094191872,
        "result": true
    }

disableUser
-----------

-  用途: **ユーザーを無効化する**
-  パラメーター:

   -  **user_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "disableUser",
        "id": 2094191872,
        "params": {
            "user_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 2094191872,
        "result": true
    }

enableUser
----------

-  用途: **ユーザーを有効化する**
-  パラメーター:

   -  **user_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "enableUser",
        "id": 2094191872,
        "params": {
            "user_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 2094191872,
        "result": true
    }

isActiveUser
------------

-  用途: **ユーザーが有効かどうか確認する**
-  パラメーター:

   -  **user_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "isActiveUser",
        "id": 2094191872,
        "params": {
            "user_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 2094191872,
        "result": true
    }
