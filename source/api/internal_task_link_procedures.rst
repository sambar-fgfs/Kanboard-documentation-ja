タスクの内部リンクのプロシージャ
=================================

createTaskLink
--------------

-  用途: **2つのタスク間のリンクを作成する**
-  パラメーター:

   -  **task_id** (integer, 必須)
   -  **opposite_task_id** (integer, 必須)
   -  **link_id** (integer, 必須)

- 成功時の返り値: **task_link_id**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "createTaskLink",
        "id": 509742912,
        "params": [
            2,
            3,
            1
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 509742912,
        "result": 1
    }

updateTaskLink
--------------

-  Purpose: **タスクのリンクのアップデート**
-  パラメーター:

   -  **task_link_id** (integer, 必須)
   -  **task_id** (integer, 必須)
   -  **opposite_task_id** (integer, 必須)
   -  **link_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "updateTaskLink",
        "id": 669037109,
        "params": [
            1,
            2,
            4,
            2
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 669037109,
        "result": true
    }

getTaskLinkById
---------------

-  Purpose: **タスクのリンクを取得する**
-  パラメーター:

   -  **task_link_id** (integer, 必須)

-  成功時の返り値: **タスクのリンクのプロパティ**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getTaskLinkById",
        "id": 809885202,
        "params": [
            1
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 809885202,
        "result": {
            "id": "1",
            "link_id": "1",
            "task_id": "2",
            "opposite_task_id": "3"
        }
    }

getAllTaskLinks
---------------

-  用途: **タスクに関連する全てのリンクを取得する**
-  パラメーター:

   -  **task_id** (integer, 必須)

-  成功時の返り値: **タスクのリンクのリスト**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getAllTaskLinks",
        "id": 810848359,
        "params": [
            2
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 810848359,
        "result": [
            {
                "id": "1",
                "task_id": "3",
                "label": "relates to",
                "title": "B",
                "is_active": "1",
                "project_id": "1",
                "task_time_spent": "0",
                "task_time_estimated": "0",
                "task_assignee_id": "0",
                "task_assignee_username": null,
                "task_assignee_name": null,
                "column_title": "Backlog"
            }
        ]
    }

removeTaskLink
--------------

-  Purpose: **2つのタスク間のリンクを削除する**
-  パラメーター:

   -  **task_link_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "removeTaskLink",
        "id": 473028226,
        "params": [
            1
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 473028226,
        "result": true
    }
