サブタスクの時間追跡のプロシージャ
====================================

hasSubtaskTimer
---------------

-  用途: **指定したサブタスクとユーザーがタイマーをスタートしたかチェックする**
-  パラメーター:

   -  **subtask_id** (integer, 必須)
   -  **user_id** (integer, 任意)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {"jsonrpc":"2.0","method":"hasSubtaskTimer","id":1786995697,"params":[2,4]}

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "result": true,
        "id": 1786995697
    }

setSubtaskStartTime
-------------------

-  用途: **サブタスクのタイマーをスタートする**
-  パラメーター:

   -  **subtask_id** (integer, 必須)
   -  **user_id** (integer, 任意)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {"jsonrpc":"2.0","method":"setSubtaskStartTime","id":1168991769,"params":[2,4]}

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "result": true,
        "id": 1168991769
    }

setSubtaskEndTime
-----------------

-  用途: **サブタスクのタイマーを止める**
-  パラメーター:

   -  **subtask_id** (integer, 必須)
   -  **user_id** (integer, 任意)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {"jsonrpc":"2.0","method":"setSubtaskEndTime","id":1026607603,"params":[2,4]}

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "result": true,
        "id": 1026607603
    }

getSubtaskTimeSpent
-------------------

-  用途: **ユーザーがサブタスクに費やした時間を取得する**
-  パラメーター:

   -  **subtask_id** (integer, 必須)
   -  **user_id** (integer, 任意)

-  成功時の返り値: **消費した時間**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {"jsonrpc":"2.0","method":"getSubtaskTimeSpent","id":738527378,"params":[2,4]}

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "result": 1.5,
        "id": 738527378
    }
