スイムレーンのAPIプロシージャ
=======================

getActiveSwimlanes
------------------

-  用途: **プロジェクトの有効なスイムレーンのリストを取得する(有効ならば、デフォルトのスイムレーンを含む)**
-  パラメーター:

   -  **project_id** (integer, 必須)

-  成功時の返り値: **スイムレーンのリスト**
-  失敗時の返り値: **null**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getActiveSwimlanes",
        "id": 934789422,
        "params": [
            1
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 934789422,
        "result": [
            {
                "id": 0,
                "name": "Default swimlane"
            },
            {
                "id": "2",
                "name": "Swimlane A"
            }
        ]
    }

getAllSwimlanes
---------------

-  用途: **プロジェクトの全てのスイムレーン(有効か無効かを問わない)のリストを取得し、スイムレーンの位置順にソート**
-  パラメーター:

   -  **project_id** (integer, 必須)

-  成功時の返り値: **スイムレーンのリスト**
-  失敗時の返り値: **null**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getAllSwimlanes",
        "id": 509791576,
        "params": [
            1
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 509791576,
        "result": [
            {
                "id": "1",
                "name": "Another swimlane",
                "position": "1",
                "is_active": "1",
                "project_id": "1"
            },
            {
                "id": "2",
                "name": "Swimlane A",
                "position": "2",
                "is_active": "1",
                "project_id": "1"
            }
        ]
    }

getSwimlane
-----------

-  Purpose: **スイムレーンをIDから取得する**
-  パラメーター:

   -  **swimlane_id** (integer, 必須)

-  成功時の返り値: **スイムレーンのプロパティ**
-  失敗時の返り値: **null**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getSwimlane",
        "id": 131071870,
        "params": [
            1
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 131071870,
        "result": {
            "id": "1",
            "name": "Swimlane 1",
            "position": "1",
            "is_active": "1",
            "project_id": "1"
        }
    }

getSwimlaneById
---------------

-  Purpose: **スイムレーンをIDから取得する**
-  パラメーター:

   -  **swimlane_id** (integer, 必須)

-  成功時の返り値: **スイムレーンのプロパティ**
-  失敗時の返り値: **null**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getSwimlaneById",
        "id": 131071870,
        "params": [
            1
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 131071870,
        "result": {
            "id": "1",
            "name": "Swimlane 1",
            "position": "1",
            "is_active": "1",
            "project_id": "1"
        }
    }

getSwimlaneByName
-----------------

-  Purpose: **スイムレーンを名前から取得する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **name** (string, 必須)

-  成功時の返り値: **スイムレーンのプロパティ**
-  失敗時の返り値: **null**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getSwimlaneByName",
        "id": 824623567,
        "params": [
            1,
            "Swimlane 1"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 824623567,
        "result": {
            "id": "1",
            "name": "Swimlane 1",
            "position": "1",
            "is_active": "1",
            "project_id": "1"
        }
    }

changeSwimlanePosition
----------------------

-  用途: **プロジェクトのスイムレーンの位置を変更する(有効なスイムレーンのみ)**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **swimlane_id** (integer, 必須)
   -  **position** (integer, 必須, 正の数であること)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "changeSwimlanePosition",
        "id": 99275573,
        "params": [
            1,
            2,
            3
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 99275573,
        "result": true
    }

updateSwimlane
--------------

-  用途: **スイムレーンのプロパティのアップデート**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **swimlane_id** (integer, 必須)
   -  **name** (string, 必須)
   -  **description** (string, 任意)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "updateSwimlane",
        "id": 87102426,
        "params": [
            "1",
            "1",
            "Another swimlane"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 87102426,
        "result": true
    }

addSwimlane
-----------

-  用途: **新しいスイムレーンを追加する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **name** (string, 必須)
   -  **description** (string, 任意)

-  成功時の返り値: **swimlane_id**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "addSwimlane",
        "id": 849940086,
        "params": [
            1,
            "Swimlane 1"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 849940086,
        "result": 1
    }

removeSwimlane
--------------

-  用途: **スイムレーンを削除する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **swimlane_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "removeSwimlane",
        "id": 1433237746,
        "params": [
            2,
            1
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1433237746,
        "result": true
    }

disableSwimlane
---------------

-  用途: **スイムレーンを無効化する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **swimlane_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "disableSwimlane",
        "id": 1433237746,
        "params": [
            2,
            1
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1433237746,
        "result": true
    }

enableSwimlane
--------------

-  用途: **スイムレーンを有効化する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **swimlane_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "enableSwimlane",
        "id": 1433237746,
        "params": [
            2,
            1
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1433237746,
        "result": true
    }
