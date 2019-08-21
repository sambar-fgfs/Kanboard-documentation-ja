グループメンバーのAPIプロシージャ
===========================

getMemberGroups
---------------

-  用途: **ユーザーが所属している全てのグループを取得する**
-  パラメーター:

   -  **user_id** (integer, 必須)

-  成功時の返り値: **グループのリスト**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getMemberGroups",
        "id": 1987176726,
        "params": [
            "1"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1987176726,
        "result": [
            {
                "id": "1",
                "name": "My Group A"
            }
        ]
    }

getGroupMembers
---------------

-  用途: **グループの全てのメンバーを取得する**
-  パラメーター:

   -  **group_id** (integer, 必須)

-  成功時の返り値: **ユーザーのリスト**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getGroupMembers",
        "id": 1987176726,
        "params": [
            "1"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1987176726,
        "result": [
            {
                "group_id": "1",
                "user_id": "1",
                "id": "1",
                "username": "admin",
                "is_ldap_user": "0",
                "name": null,
                "email": null,
                "notifications_enabled": "0",
                "timezone": null,
                "language": null,
                "disable_login_form": "0",
                "notifications_filter": "4",
                "nb_failed_login": "0",
                "lock_expiration_date": "0",
                "is_project_admin": "0",
                "gitlab_id": null,
                "role": "app-admin"
            }
        ]
    }

addGroupMember
--------------

-  用途: **グループにユーザーを追加する**
-  パラメーター:

   -  **group_id** (integer, 必須)
   -  **user_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "addGroupMember",
        "id": 1589058273,
        "params": [
            1,
            1
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1589058273,
        "result": true
    }

removeGroupMember
-----------------

-  用途: **グループからユーザーを削除する**
-  パラメーター:

   -  **group_id** (integer, 必須)
   -  **user_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "removeGroupMember",
        "id": 1730416406,
        "params": [
            1,
            1
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1730416406,
        "result": true
    }

isGroupMember
-------------

-  Purpose: **Check if a user is member of a group**
-  パラメーター:

   -  **group_id** (integer, 必須)
   -  **user_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "isGroupMember",
        "id": 1052800865,
        "params": [
            1,
            1
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1052800865,
        "result": false
    }
