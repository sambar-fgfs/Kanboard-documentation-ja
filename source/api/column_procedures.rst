カラムの API プロシージャ
=====================

getColumns
----------

-  用途: **プロジェクトに与えられた全てのカラムの情報を取得する**
-  パラメーター:

   -  **project_id** (integer, 必須)

-  成功時の返り値: **カラムのプロパティ**
-  失敗時の返り値: **空のリスト**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getColumns",
        "id": 887036325,
        "params": [
            1
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 887036325,
        "result": [
            {
                "id": "1",
                "title": "Backlog",
                "position": "1",
                "project_id": "1",
                "task_limit": "0"
            },
            {
                "id": "2",
                "title": "Ready",
                "position": "2",
                "project_id": "1",
                "task_limit": "0"
            },
            {
                "id": "3",
                "title": "Work in progress",
                "position": "3",
                "project_id": "1",
                "task_limit": "0"
            }
        ]
    }

getColumn
---------

-  用途: **一つのカラムについて取得する**
-  パラメーター:

   -  **column_id** (integer, 必須)

-  成功時の返り値: **カラムのプロパティ**
-  失敗時の返り値: **null**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getColumn",
        "id": 1242049935,
        "params": [
            2
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1242049935,
        "result": {
            "id": "2",
            "title": "Youpi",
            "position": "2",
            "project_id": "1",
            "task_limit": "5"
        }
    }

changeColumnPosition
--------------------

-  用途: **カラムの位置を変更する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **column_id** (integer, 必須)
   -  **position** (integer, 必須, 正の数であること)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "changeColumnPosition",
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

updateColumn
------------

-  用途: **カラムのプロパティのアップデート**
-  パラメーター:

   -  **column_id** (integer, 必須)
   -  **title** (string, 必須)
   -  **task_limit** (integer, 任意)
   -  **description** (string, 任意)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "updateColumn",
        "id": 480740641,
        "params": [
            2,
            "Boo",
            5
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 480740641,
        "result": true
    }

addColumn
---------

-  用途: **新しいカラムを追加する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **title** (string, 必須)
   -  **task_limit** (integer, 任意)
   -  **description** (string, 任意)

-  成功時の返り値: **column_id**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "addColumn",
        "id": 638544704,
        "params": [
            1,
            "Boo"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 638544704,
        "result": 5
    }

カラムの削除
------------

-  用途: **カラムの削除**
-  パラメーター:

   -  **column_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "removeColumn",
        "id": 1433237746,
        "params": [
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
