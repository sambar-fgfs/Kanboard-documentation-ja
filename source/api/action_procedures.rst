自動アクションAPIのプロシージャ
================================

getAvailableActions
-------------------

-  用途: **利用可能な自動アクションの一覧を取得する**
-  パラメータ: 無し
-  成功時の返り値: **自動アクションの一覧**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getAvailableActions",
        "id": 1217735483
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1217735483,
        "result": {
            "\Kanboard\Action\TaskLogMoveAnotherColumn": "Add a comment logging moving the task between columns",
            "\Kanboard\Action\TaskAssignColorUser": "Assign a color to a specific user",
            "\Kanboard\Action\TaskAssignColorColumn": "Assign a color when the task is moved to a specific column",
            "\Kanboard\Action\TaskAssignCategoryColor": "Assign automatically a category based on a color",
            "\Kanboard\Action\TaskAssignColorCategory": "Assign automatically a color based on a category",
            "\Kanboard\Action\TaskAssignSpecificUser": "Assign the task to a specific user",
            "\Kanboard\Action\TaskAssignCurrentUser": "Assign the task to the person who does the action",
            "\Kanboard\Action\TaskUpdateStartDate": "Automatically update the start date",
            "\Kanboard\Action\TaskAssignUser": "Change the assignee based on an external username",
            "\Kanboard\Action\TaskAssignCategoryLabel": "Change the category based on an external label",
            "\Kanboard\Action\TaskClose": "Close a task",
            "\Kanboard\Action\CommentCreation": "Create a comment from an external provider",
            "\Kanboard\Action\TaskCreation": "Create a task from an external provider",
            "\Kanboard\Action\TaskDuplicateAnotherProject": "Duplicate the task to another project",
            "\Kanboard\Action\TaskMoveColumnAssigned": "Move the task to another column when assigned to a user",
            "\Kanboard\Action\TaskMoveColumnUnAssigned": "Move the task to another column when assignee is cleared",
            "\Kanboard\Action\TaskMoveAnotherProject": "Move the task to another project",
            "\Kanboard\Action\TaskOpen": "Open a task"
        }
    }

getAvailableActionEvents
------------------------

-  用途: **アクションに利用可能なイベントの一覧を取得する**
-  パラメータ: 無し
-  成功時の返り値: **イベントのリスト**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getAvailableActionEvents",
        "id": 2116665643
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 2116665643,
        "result": {
            "bitbucket.webhook.commit": "Bitbucket commit received",
            "task.close": "Closing a task",
            "github.webhook.commit": "Github commit received",
            "github.webhook.issue.assignee": "Github issue assignee change",
            "github.webhook.issue.closed": "Github issue closed",
            "github.webhook.issue.commented": "Github issue comment created",
            "github.webhook.issue.label": "Github issue label change",
            "github.webhook.issue.opened": "Github issue opened",
            "github.webhook.issue.reopened": "Github issue reopened",
            "gitlab.webhook.commit": "Gitlab commit received",
            "gitlab.webhook.issue.closed": "Gitlab issue closed",
            "gitlab.webhook.issue.opened": "Gitlab issue opened",
            "task.move.column": "Move a task to another column",
            "task.open": "Open a closed task",
            "task.assignee_change": "Task assignee change",
            "task.create": "Task creation",
            "task.create_update": "Task creation or modification",
            "task.update": "Task modification"
        }
    }

getCompatibleActionEvents
-------------------------

-  用途: **アクションと互換性があるイベントの一覧を取得する**
-  パラメーター:

   -  **action_name** (string, 必須)

-  成功時の返り値: **イベントのリスト**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getCompatibleActionEvents",
        "id": 899370297,
        "params": [
            "\Kanboard\Action\TaskClose"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 899370297,
        "result": {
            "bitbucket.webhook.commit": "Bitbucket commit received",
            "github.webhook.commit": "Github commit received",
            "github.webhook.issue.closed": "Github issue closed",
            "gitlab.webhook.commit": "Gitlab commit received",
            "gitlab.webhook.issue.closed": "Gitlab issue closed",
            "task.move.column": "Move a task to another column"
        }
    }

getActions
----------

-  用途: **プロジェクトで利用されているアクションの一覧を取得する**
-  パラメーター:

   -  **project_id** (integer, 必須)

-  成功時の返り値: **アクションのプロパティの一覧**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getActions",
        "id": 1433237746,
        "params": [
            "1"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1433237746,
        "result": [
            {
                "id" : "13",
                "project_id" : "2",
                "event_name" : "task.move.column",
                "action_name" : "\Kanboard\Action\TaskAssignSpecificUser",
                "params" : {
                    "column_id" : "5",
                    "user_id" : "1"
                }
            }
        ]
    }

createAction
------------

-  用途: **アクションを作成する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **event_name** (string, required)
   -  **action_name** (string, 必須)
   -  **params** (key/value parameters, required)

-  Result on success: **action_id**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "createAction",
        "id": 1433237746,
        "params": {
            "project_id" : "2",
            "event_name" : "task.move.column",
            "action_name" : "\Kanboard\Action\TaskAssignSpecificUser",
            "params" : {
                "column_id" : "3",
                "user_id" : "2"
            }
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1433237746,
        "result": 14
    }

removeAction
------------

-  用途: **アクションを削除する**
-  パラメーター:

   -  **action_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "removeAction",
        "id": 1510741671,
        "params": [
            1
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1510741671,
        "result": true
    }
