プロジェクトのファイルのAPIプロシージャ
===========================

createProjectFile
-----------------

-  用途: **新しくプロジェクトに添付ファイルをアップロード・作成する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **filename** (integer, 必須)
   -  **blob** ファイルの内容を base64 でエンコードした物(string, 必須)

-  成功時の返り値: **file_id**
-  失敗時の返り値: **false**
-  注意: **添付可能な最大ファイルサイズはPHPの設定によるため、この方法では大きなファイルをアップロードすることができません**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "createProjectFile",
        "id": 94500810,
        "params": [
            1,
            "My file",
            "cGxhaW4gdGV4dCBmaWxl"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 94500810,
        "result": 1
    }

getAllProjectFiles
------------------

-  用途: **プロジェクトに添付された全てのファイルを取得する**
-  パラメーター:

   -  **project_id** (integer, 必須)

-  成功時の返り値: **list of files**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getAllProjectFiles",
        "id": 1880662820,
        "params": {
            "project_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1880662820,
        "result": [
            {
                "id": "1",
                "name": "My file",
                "path": "1\/1\/0db4d0a897a4c852f6e12f0239d4805f7b4ab596",
                "is_image": "0",
                "project_id": "1",
                "date": "1432509941",
                "user_id": "0",
                "size": "15",
                "username": null,
                "user_name": null
            }
        ]
    }

getProjectFile
--------------

-  用途: **ファイルの情報を取得する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **file_id** (integer, 必須)

-  成功時の返り値: **ファイルのプロパティ**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getProjectFile",
        "id": 318676852,
        "params": [
            "42",
            "1"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 318676852,
        "result": {
            "id": "1",
            "name": "My file",
            "path": "1\/1\/0db4d0a897a4c852f6e12f0239d4805f7b4ab596",
            "is_image": "0",
            "project_id": "1",
            "date": "1432509941",
            "user_id": "0",
            "size": "15"
        }
    }

downloadProjectFile
-------------------

-  用途: **(base64でエンコードされた)プロジェクトファイルの内容を取得する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **file_id** (integer, 必須)

-  成功時の返り値: **base64でエンコードされた文字列**
-  失敗時の返り値: **空の文字列**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "downloadProjectFile",
        "id": 235943344,
        "params": [
            "1",
            "1"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 235943344,
        "result": "cGxhaW4gdGV4dCBmaWxl"
    }

removeProjectFile
-----------------

-  用途: **プロジェクトに関連するファイルを削除する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **file_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "removeProjectFile",
        "id": 447036524,
        "params": [
            "1",
            "1"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 447036524,
        "result": true
    }

removeAllProjectFiles
---------------------

-  用途: **プロジェクトに関連する全てのファイルを削除する**
-  パラメーター:

   -  **project_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "removeAllProjectFiles",
        "id": 593312993,
        "params": {
            "project_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 593312993,
        "result": true
    }
