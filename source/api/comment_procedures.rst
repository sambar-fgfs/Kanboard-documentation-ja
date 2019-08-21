コメントのAPIプロシージャ
======================

createComment
-------------

-  用途: **新しいコメントを作成する**
-  パラメーター:

   -  **task_id** (integer, 必須)
   -  **user_id** (integer, 必須)
   -  **content** 本文をMarkdown で記述 (string, 必須)

-  成功時の返り値: **comment_id**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "createComment",
        "id": 1580417921,
        "params": {
            "task_id": 1,
            "user_id": 1,
            "content": "Comment #1"
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1580417921,
        "result": 11
    }

getComment
----------

-  用途: **コメントの情報を取得する**
-  パラメーター:

   -  **comment_id** (integer, 必須)

-  成功時の返り値: **コメントのプロパティ**
-  失敗時の返り値: **null**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getComment",
        "id": 867839500,
        "params": {
            "comment_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 867839500,
        "result": {
            "id": "1",
            "task_id": "1",
            "user_id": "1",
            "date_creation": "1410881970",
            "comment": "Comment #1",
            "username": "admin",
            "name": null
        }
    }

getAllComments
--------------

-  Purpose: **全ての利用可能なコメントを取得**
-  パラメーター:

   -  **task_id** (integer, 必須)

-  成功時の返り値: **コメントのリスト**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getAllComments",
        "id": 148484683,
        "params": {
            "task_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 148484683,
        "result": [
            {
                "id": "1",
                "date_creation": "1410882272",
                "task_id": "1",
                "user_id": "1",
                "comment": "Comment #1",
                "username": "admin",
                "name": null
            },
            ...
        ]
    }

updateComment
-------------

-  用途: **コメントの更新**
-  パラメーター:

   -  **id** (integer, 必須)
   -  **content** 本文をMarkdown で記述 (string, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "updateComment",
        "id": 496470023,
        "params": {
            "id": 1,
            "content": "Comment #1 updated"
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1493368950,
        "result": true
    }

removeComment
-------------

-  用途: **コメントの削除**
-  パラメーター:

   -  **comment_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "removeComment",
        "id": 328836871,
        "params": {
            "comment_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 328836871,
        "result": true
    }
