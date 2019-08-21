サブタスクのAPIプロシージャ
======================

createSubtask
-------------

-  用途: **サブタスクの新規作成**
-  パラメーター:

   -  **task_id** (integer, 必須)
   -  **title** (integer, 必須)
   -  **user_id** (int, 任意)
   -  **time_estimated** (int, 任意)
   -  **time_spent** (int, 任意)
   -  **status** (int, 任意)

-  成功時の返り値: **subtask_id**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "createSubtask",
        "id": 2041554661,
        "params": {
            "task_id": 1,
            "title": "Subtask #1"
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 2041554661,
        "result": 45
    }

getSubtask
----------

-  用途: **サブタスクの情報を取得する**
-  パラメーター:

   -  **subtask_id** (integer)

-  成功時の返り値: **サブタスクのプロパティ**
-  失敗時の返り値: **null**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getSubtask",
        "id": 133184525,
        "params": {
            "subtask_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 133184525,
        "result": {
            "id": "1",
            "title": "Subtask #1",
            "status": "0",
            "time_estimated": "0",
            "time_spent": "0",
            "task_id": "1",
            "user_id": "0"
        }
    }

getAllSubtasks
--------------

-  用途: **全ての活動中のサブタスクを取得する**
-  パラメーター:

   -  **task_id** (integer, 必須)

-  成功時の返り値: **サブタスクのリスト**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getAllSubtasks",
        "id": 2087700490,
        "params": {
            "task_id": 1
        }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 2087700490,
        "result": [
            {
                "id": "1",
                "title": "Subtask #1",
                "status": "0",
                "time_estimated": "0",
                "time_spent": "0",
                "task_id": "1",
                "user_id": "0",
                "username": null,
                "name": null,
                "status_name": "Todo"
            },
            ...
        ]
    }

updateSubtask
-------------

-  Purpose: **サブタスクをアップデートする**
-  パラメーター:

   -  **id** (integer, 必須)
   -  **task_id** (integer, 必須)
   -  **title** (integer, 任意)
   -  **user_id** (integer, 任意)
   -  **time_estimated** (integer, 任意)
   -  **time_spent** (integer, 任意)
   -  **status** (integer, 任意)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "updateSubtask",
        "id": 191749979,
        "params": {
            "id": 1,
            "task_id": 1,
            "status": 1,
            "time_spent": 5,
            "user_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 191749979,
        "result": true
    }

removeSubtask
-------------

-  用途: **サブタスクを削除する**
-  パラメーター:

   -  **subtask_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "removeSubtask",
        "id": 1382487306,
        "params": {
            "subtask_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1382487306,
        "result": true
    }
