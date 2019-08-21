カテゴリのAPIプロシージャ
=======================

createCategory
--------------

-  用途: **カテゴリの新規作成**
-  パラメーター:
-  **project_id** (integer, 必須)

   -  **name** (string, 必須, プロジェクトごとにユニークでなければならない)

-  成功時の返り値: **カテゴリのID**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "createCategory",
        "id": 541909890,
        "params": {
            "name": "Super category",
            "project_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 541909890,
        "result": 4
    }

getCategory
-----------

-  用途: **カテゴリの情報を取得する**
-  パラメーター:

   -  **category_id** (integer, 必須)

-  成功時の返り値: *カテゴリのプロパティ**
-  失敗時の返り値: **null**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getCategory",
        "id": 203539163,
        "params": {
            "category_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {

        "jsonrpc": "2.0",
        "id": 203539163,
        "result": {
            "id": "1",
            "name": "Super category",
            "project_id": "1"
        }
    }

getAllCategories
----------------

-  用途: **全ての利用可能なカテゴリを取得する**
-  パラメーター:

   -  **project_id** (integer, 必須)

-  成功時の返り値: **カテゴリのリスト**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getAllCategories",
        "id": 1261777968,
        "params": {
            "project_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1261777968,
        "result": [
            {
                "id": "1",
                "name": "Super category",
                "project_id": "1"
            }
        ]
    }

updateCategory
--------------

-  用途: **カテゴリのアップデート**
-  パラメーター:

   -  **id** (integer, 必須)
   -  **name** (string, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "updateCategory",
        "id": 570195391,
        "params": {
            "id": 1,
            "name": "Renamed category"
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 570195391,
        "result": true
    }

removeCategory
--------------

-  用途: **カテゴリの削除**
-  パラメーター:

   -  **category_id** (integer)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "removeCategory",
        "id": 88225706,
        "params": {
            "category_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 88225706,
        "result": true
    }
