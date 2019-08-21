タスクのAPIプロシージャ
===========================

createTask
----------

-  Purpose: **新しくタスクを作成する**
-  パラメーター:

   -  **title** (string, 必須)
   -  **project_id** (integer, 必須)
   -  **color_id** (string, 任意)
   -  **column_id** (integer, 任意)
   -  **owner_id** (integer, 任意)
   -  **creator_id** (integer, 任意)
   -  **date_due**: ISO8601 書式 (string, 任意)
   -  **description** Markdown 形式 (string, 任意)
   -  **category_id** (integer, 任意)
   -  **score** (integer, 任意)
   -  **swimlane_id** (integer, 任意)
   -  **priority** (integer, 任意)
   -  **recurrence_status** (integer, 任意)
   -  **recurrence_trigger** (integer, 任意)
   -  **recurrence_factor** (integer, 任意)
   -  **recurrence_timeframe** (integer, 任意)
   -  **recurrence_basedate** (integer, 任意)
   -  **reference** (string, 任意)
   -  **tags** ([]string, 任意)
   -  **date_started**: ISO8601 書式 (string, 任意)

-  成功時の返り値: **task_id**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "createTask",
        "id": 1176509098,
        "params": {
            "owner_id": 1,
            "creator_id": 0,
            "date_due": "",
            "description": "",
            "category_id": 0,
            "score": 0,
            "title": "Test",
            "project_id": 1,
            "color_id": "green",
            "column_id": 2,
            "recurrence_status": 0,
            "recurrence_trigger": 0,
            "recurrence_factor": 0,
            "recurrence_timeframe": 0,
            "recurrence_basedate": 0
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1176509098,
        "result": 3
    }

getTask
-------

-  Purpose: **タスクをユニークなIDから取得する**
-  パラメーター:

   -  **task_id** (integer, 必須)

-  成功時の返り値: **タスクのプロパティ**
-  失敗時の返り値: **null**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getTask",
        "id": 700738119,
        "params": {
            "task_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 700738119,
        "result": {
            "id": "1",
            "title": "Task #1",
            "description": "",
            "date_creation": "1409963206",
            "color_id": "blue",
            "project_id": "1",
            "column_id": "2",
            "owner_id": "1",
            "position": "1",
            "is_active": "1",
            "date_completed": null,
            "score": "0",
            "date_due": "0",
            "category_id": "0",
            "creator_id": "0",
            "date_modification": "1409963206",
            "reference": "",
            "date_started": null,
            "time_spent": "0",
            "time_estimated": "0",
            "swimlane_id": "0",
            "date_moved": "1430875287",
            "recurrence_status": "0",
            "recurrence_trigger": "0",
            "recurrence_factor": "0",
            "recurrence_timeframe": "0",
            "recurrence_basedate": "0",
            "recurrence_parent": null,
            "recurrence_child": null,
            "url": "http:\/\/127.0.0.1:8000\/?controller=task&action=show&task_id=1&project_id=1",
            "color": {
                "name": "Yellow",
                "background": "rgb(245, 247, 196)",
                "border": "rgb(223, 227, 45)"
            }
        }
    }

getTaskByReference
------------------

-  Purpose: **タスクを外部参照から取得する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **reference** (string, 必須)

-  成功時の返り値: **タスクのプロパティ**
-  失敗時の返り値: **null**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getTaskByReference",
        "id": 1992081213,
        "params": {
            "project_id": 1,
            "reference": "TICKET-1234"
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1992081213,
        "result": {
            "id": "5",
            "title": "Task with external ticket number",
            "description": "[Link to my ticket](http:\/\/my-ticketing-system\/1234)",
            "date_creation": "1434227446",
            "color_id": "yellow",
            "project_id": "1",
            "column_id": "1",
            "owner_id": "0",
            "position": "4",
            "is_active": "1",
            "date_completed": null,
            "score": "0",
            "date_due": "0",
            "category_id": "0",
            "creator_id": "0",
            "date_modification": "1434227446",
            "reference": "TICKET-1234",
            "date_started": null,
            "time_spent": "0",
            "time_estimated": "0",
            "swimlane_id": "0",
            "date_moved": "1434227446",
            "recurrence_status": "0",
            "recurrence_trigger": "0",
            "recurrence_factor": "0",
            "recurrence_timeframe": "0",
            "recurrence_basedate": "0",
            "recurrence_parent": null,
            "recurrence_child": null,
            "url": "http:\/\/127.0.0.1:8000\/?controller=task&action=show&task_id=5&project_id=1"
        }
    }

getAllTasks
-----------

-  用途: **全ての活動中のタスクを取得する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **status_id**: この値を1にすると活動中のタスクを、0にすると活動中でないタスクを取得します (integer, 必須)

-  成功時の返り値: **タスクのリスト**
-  失敗時の返り値: **false**

ボード上の全てのタスクを取得するリクエストの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getAllTasks",
        "id": 133280317,
        "params": {
            "project_id": 1,
            "status_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 133280317,
        "result": [
            {
                "id": "1",
                "title": "Task #1",
                "description": "",
                "date_creation": "1409961789",
                "color_id": "blue",
                "project_id": "1",
                "column_id": "2",
                "owner_id": "1",
                "position": "1",
                "is_active": "1",
                "date_completed": null,
                "score": "0",
                "date_due": "0",
                "category_id": "0",
                "creator_id": "0",
                "date_modification": "1409961789",
                "reference": "",
                "date_started": null,
                "time_spent": "0",
                "time_estimated": "0",
                "swimlane_id": "0",
                "date_moved": "1430783191",
                "recurrence_status": "0",
                "recurrence_trigger": "0",
                "recurrence_factor": "0",
                "recurrence_timeframe": "0",
                "recurrence_basedate": "0",
                "recurrence_parent": null,
                "recurrence_child": null,
                "priority": "0",
                "external_provider": null,
                "external_uri": null,
                "url": "http:\/\/127.0.0.1:8000\/?controller=task&action=show&task_id=1&project_id=1",
                "color": {
                    "name": "Blue",
                    "background": "rgb(219, 235, 255)",
                    "border": "rgb(168, 207, 255)"
                }
            },
            {
                "id": "2",
                "title": "Test",
                "description": "",
                "date_creation": "1409962115",
                "color_id": "green",
                "project_id": "1",
                "column_id": "2",
                "owner_id": "1",
                "position": "2",
                "is_active": "1",
                "date_completed": null,
                "score": "0",
                "date_due": "0",
                "category_id": "0",
                "creator_id": "0",
                "date_modification": "1409962115",
                "reference": "",
                "date_started": null,
                "time_spent": "0",
                "time_estimated": "0",
                "swimlane_id": "0",
                "date_moved": "1430783191",
                "recurrence_status": "0",
                "recurrence_trigger": "0",
                "recurrence_factor": "0",
                "recurrence_timeframe": "0",
                "recurrence_basedate": "0",
                "recurrence_parent": null,
                "recurrence_child": null,
                "priority": "0",
                "external_provider": null,
                "external_uri": null,
                "url": "http:\/\/127.0.0.1:8000\/?controller=task&action=show&task_id=2&project_id=1",
                "color": {
                    "name": "Green",
                    "background": "rgb(189, 244, 203)",
                    "border": "rgb(74, 227, 113)"
                }
            },
            ...
        ]
    }

getOverdueTasks
---------------

-  用途: **全ての期限切れタスクを取得する**
-  成功時の返り値: **タスクのリスト**
-  失敗時の返り値: **false**

ボード上の全てのタスクを取得するリクエストの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getOverdueTasks",
        "id": 133280317
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 133280317,
        "result": [
            {
                "id": "1",
                "title": "Task #1",
                "date_due": "1409961789",
                "project_id": "1",
                "project_name": "Test",
                "assignee_username":"admin",
                "assignee_name": null
            },
            {
                "id": "2",
                "title": "Test",
                "date_due": "1409962115",
                "project_id": "1",
                "project_name": "Test",
                "assignee_username":"admin",
                "assignee_name": null
            },
            ...
        ]
    }

getOverdueTasksByProject
------------------------

-  用途: **プロジェクトの期限切れタスクを取得する**
-  成功時の返り値: **タスクのリスト**
-  失敗時の返り値: **false**

ボード上の全てのタスクを取得するリクエストの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getOverdueTasksByProject",
        "id": 133280317,
        "params": {
            "project_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 133280317,
        "result": [
            {
                "id": "1",
                "title": "Task #1",
                "date_due": "1409961789",
                "project_id": "1",
                "project_name": "Test",
                "assignee_username":"admin",
                "assignee_name": null
            },
            {
                "id": "2",
                "title": "Test",
                "date_due": "1409962115",
                "project_id": "1",
                "project_name": "Test",
                "assignee_username":"admin",
                "assignee_name": null
            },
            ...
        ]
    }

updateTask
----------

-  Purpose: **タスクのアップデート**
-  パラメーター:

   -  **id** (integer, 必須)
   -  **title** (string, 任意)
   -  **color_id** (string, 任意)
   -  **owner_id** (integer, 任意)
   -  **date_due**: ISO8601 書式 (string, 任意)
   -  **description** Markdown 形式 (string, 任意)
   -  **category_id** (integer, 任意)
   -  **score** (integer, 任意)
   -  **priority** (integer, 任意)
   -  **recurrence_status** (integer, 任意)
   -  **recurrence_trigger** (integer, 任意)
   -  **recurrence_factor** (integer, 任意)
   -  **recurrence_timeframe** (integer, 任意)
   -  **recurrence_basedate** (integer, 任意)
   -  **reference** (string, 任意)
   -  **tags** ([]string, 任意)
   -  **date_started**: ISO8601 書式 (string, 任意)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

タスクの色を変えるリクエストの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "updateTask",
        "id": 1406803059,
        "params": {
            "id": 1,
            "color_id": "blue"
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1406803059,
        "result": true
    }

openTask
--------

-  用途: **タスクの状態をオープンにする**
-  パラメーター:

   -  **task_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "openTask",
        "id": 1888531925,
        "params": {
            "task_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1888531925,
        "result": true
    }

closeTask
---------

-  用途: **タスクの状態を終了にする**
-  パラメーター:

   -  **task_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "closeTask",
        "id": 1654396960,
        "params": {
            "task_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1654396960,
        "result": true
    }

removeTask
----------

-  用途: **タスクを削除する**
-  パラメーター:

   -  **task_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "removeTask",
        "id": 1423501287,
        "params": {
            "task_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1423501287,
        "result": true
    }

moveTaskPosition
----------------

-  用途: **同一ボード内でタスクを別の位置/カラム/スイムレーンに移動する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **task_id** (integer, 必須)
   -  **column_id** (integer, 必須)
   -  **position** (integer, 必須)
   -  **swimlane_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "moveTaskPosition",
        "id": 117211800,
        "params": {
            "project_id": 1,
            "task_id": 1,
            "column_id": 2,
            "position": 1,
            "swimlane_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 117211800,
        "result": true
    }

moveTaskToProject
-----------------

- 用途: **タスクを別のプロジェクトに移動**
-  パラメーター:

   -  **task_id** (integer, 必須)
   -  **project_id** (integer, 必須)
   -  **swimlane_id** (integer, 任意)
   -  **column_id** (integer, 任意)
   -  **category_id** (integer, 任意)
   -  **owner_id** (integer, 任意)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "moveTaskToProject",
        "id": 15775829,
        "params": [
            4,
            5
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 15775829,
        "result": true
    }

duplicateTaskToProject
----------------------

-  用途: **タスクを別のカラムor別の場所に複製する**
-  パラメーター:

   -  **task_id** (integer, 必須)
   -  **project_id** (integer, 必須)
   -  **swimlane_id** (integer, 任意)
   -  **column_id** (integer, 任意)
   -  **category_id** (integer, 任意)
   -  **owner_id** (integer, 任意)

-  成功時の返り値: **task_id**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "duplicateTaskToProject",
        "id": 1662458687,
        "params": [
            5,
            7
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1662458687,
        "result": 6
    }

searchTasks
-----------

-  用途: **(Kanboard内部の)検索エンジンを使用してタスクを検索する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **query** (string, 必須)

-  成功時の返り値: **タスクのリスト**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "searchTasks",
        "id": 1468511716,
        "params": {
            "project_id": 2,
            "query": "assignee:nobody"
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1468511716,
        "result": [
            {
                "nb_comments": "0",
                "nb_files": "0",
                "nb_subtasks": "0",
                "nb_completed_subtasks": "0",
                "nb_links": "0",
                "nb_external_links": "0",
                "is_milestone": null,
                "id": "3",
                "reference": "",
                "title": "T3",
                "description": "",
                "date_creation": "1461365164",
                "date_modification": "1461365164",
                "date_completed": null,
                "date_started": null,
                "date_due": "0",
                "color_id": "yellow",
                "project_id": "2",
                "column_id": "5",
                "swimlane_id": "0",
                "owner_id": "0",
                "creator_id": "0"
                // ...
             }
        ]
    }
