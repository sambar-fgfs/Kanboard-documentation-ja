プロジェクトのメタデータのAPIのプロシージャ
===============================

getProjectMetadata
------------------

-  用途: **プロジェクトのメタデータを取得**
-  パラメーター:

   -  **project_id** (integer, 必須)

-  成功時の返り値: **メタデータの連想配列**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getProjectMetadata",
        "id": 1797076613,
        "params": {
            "project_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1797076613,
        "result": {
            "key1": "value1"
        }
    }

getProjectMetadataByName
------------------------

-  用途: **単一のメタデータの値を取得する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **name** (string, 必須)

-  成功時の返り値: **混合**
-  失敗時の返り値: **空の文字列**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getProjectMetadataByName",
        "id": 1797076613,
        "params": {
            "project_id": 1,
            "name": "key1"
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1797076613,
        "result": "value1"
    }

saveProjectMetadata
-------------------

-  用途: **メタデータを追加または更新する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **値** (連想配列, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "saveProjectMetadata",
        "id": 1797076613,
        "params": {
            "project_id": 1,
            "values": {
                "key1": "value1"
            }
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1797076613,
        "result": true
    }

removeProjectMetadata
---------------------

-  用途: **プロジェクトのメタデータを削除する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **name** (string, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "removeProjectMetadata",
        "id": 1797076613,
        "params": {
            "project_id": 1,
            "name": "my key"
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1797076613,
        "result": true
    }
