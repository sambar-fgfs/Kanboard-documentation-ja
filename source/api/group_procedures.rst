グループのAPIプロシージャ
====================

createGroup
-----------

-  用途: **グループの新規作成**
-  パラメーター:

   -  **name** (string, 必須)
   -  **external_id** (string, 任意)

-  成功時の返り値: **link_id**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "createGroup",
        "id": 1416806551,
        "params": [
            "My Group B",
            "1234"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1416806551,
        "result": 2
    }

updateGroup
-----------

-  用途: **グループの更新**
-  パラメーター:

   -  **group_id** (integer, 必須)
   -  **name** (string, 任意)
   -  **external_id** (string, 任意)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "updateGroup",
        "id": 866078030,
        "params": {
            "group_id": "1",
            "name": "ABC",
            "external_id": "something"
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 866078030,
        "result": true
    }

removeGroup
-----------

-  用途: **グループの削除**
-  パラメーター:

   -  **group_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "removeGroup",
        "id": 566000661,
        "params": [
            "1"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 566000661,
        "result": true
    }

getGroup
--------

-  用途: **グループを取得する**
-  パラメーター:

   -  **group_id** (integer, 必須)

-  成功時の返り値: **グループの連想配列**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getGroup",
        "id": 1968647622,
        "params": [
            "1"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1968647622,
        "result": {
            "id": "1",
            "external_id": "",
            "name": "My Group A"
        }
    }

getAllGroups
------------

-  用途: **全てのグループを取得する**
-  パラメータ: 無し
-  成功時の返り値: **グループのリスト**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getAllGroups",
        "id": 546070742
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 546070742,
        "result": [
            {
                "id": "1",
                "external_id": "",
                "name": "My Group A"
            },
            {
                "id": "2",
                "external_id": "1234",
                "name": "My Group B"
            }
        ]
    }
