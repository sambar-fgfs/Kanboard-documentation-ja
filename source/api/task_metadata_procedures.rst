タスクのメタデータのAPIのプロシージャ
===============================

getTaskMetadata
---------------

-  用途: **タスクのユニークなIDからタスクに関連するメタデータを取得する**
-  パラメーター:

   -  **task_id** (integer, 必須)

-  成功時の返り値: **メタデータのリスト**
-  失敗時の返り値: **空の配列**

タスクの全てのメタデータを取得するリクエストの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getTaskMetadata",
        "id": 133280317,
        "params": [
            1
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 133280317,
        "result": [
            {
                "metaKey1": "metaValue1",
                "metaKey2": "metaValue2"
            }
        ]
    }

getTaskMetadataByName
---------------------

-  用途: **タスクのユニークなIDとメタキー(名前)から関連するメタデータを取得する**
-  パラメーター:

   -  **task_id** (integer, 必須)
   -  **name** (string, 必須)

-  成功時の返り値: **メタデータの値**
-  失敗時の返り値: **空の文字列**

名前からタスクのメタデータを取得するリクエストの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getTaskMetadataByName",
        "id": 133280317,
        "params": [
            1,
            "metaKey1"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 133280317,
        "result": "metaValue1"
    }

saveTaskMetadata
----------------

-  用途: **タスクのメタデータの保存/更新**
-  パラメーター:

   -  **task_id** (integer, 必須)
   -  **array(“name” => “value”)** (配列, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

タスクのメタデータを追加/更新するリクエストの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "saveTaskMetadata",
        "id": 133280317,
        "params": [
            1,
            {
                "metaName" : "metaValue"
            }
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 133280317,
        "result": true
    }

removeTaskMetadata
------------------

-  用途: **名前でタスクのメタデータを削除する**
-  パラメーター:

   -  **task_id** (integer, 必須)
   -  **name** (string, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

名前でタスクのメタデータを削除するリクエストの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "removeTaskMetadata",
        "id": 133280317,
        "params": [
            1,
            "metaKey1"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 133280317,
        "result": true
    }
