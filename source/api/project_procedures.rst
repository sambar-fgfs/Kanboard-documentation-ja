プロジェクトのAPIプロシージャ
===========================

createProject
-------------

-  用途: **プロジェクトの新規作成**
-  パラメーター:

   -  **name** (string, 必須)
   -  **description** (string, 任意)
   -  **owner_id** (integer, 任意)
   -  **identifier** (alphanumeric string, 任意)

-  成功時の返り値: **project_id**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "createProject",
        "id": 1797076613,
        "params": {
            "name": "PHP client"
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1797076613,
        "result": 2
    }

getProjectById
--------------

-  用途: **プロジェクトの情報を取得する**
-  パラメーター:

   -  **project_id** (integer, 必須)

-  成功時の返り値: **プロジェクトのプロパティ**
-  失敗時の返り値: **null**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getProjectById",
        "id": 226760253,
        "params": {
            "project_id": 1
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 226760253,
        "result": {
            "id": "1",
            "name": "API test",
            "is_active": "1",
            "token": "",
            "last_modified": "1436119135",
            "is_public": "0",
            "is_private": "0",
            "default_swimlane": "Default swimlane",
            "show_default_swimlane": "1",
            "description": "test",
            "identifier": "",
            "url": {
                "board": "http:\/\/127.0.0.1:8000\/?controller=board&action=show&project_id=1",
                "calendar": "http:\/\/127.0.0.1:8000\/?controller=calendar&action=show&project_id=1",
                "list": "http:\/\/127.0.0.1:8000\/?controller=listing&action=show&project_id=1"
            }
        }
    }

getProjectByName
----------------

-  用途: **プロジェクトの情報を取得する**
-  パラメーター:

   -  **name** (string, 必須)

-  成功時の返り値: **プロジェクトのプロパティ**
-  失敗時の返り値: **null**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getProjectByName",
        "id": 1620253806,
        "params": {
            "name": "Test"
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1620253806,
        "result": {
            "id": "1",
            "name": "Test",
            "is_active": "1",
            "token": "",
            "last_modified": "1436119135",
            "is_public": "0",
            "is_private": "0",
            "default_swimlane": "Default swimlane",
            "show_default_swimlane": "1",
            "description": "test",
            "identifier": "",
            "url": {
                "board": "http:\/\/127.0.0.1:8000\/?controller=board&action=show&project_id=1",
                "calendar": "http:\/\/127.0.0.1:8000\/?controller=calendar&action=show&project_id=1",
                "list": "http:\/\/127.0.0.1:8000\/?controller=listing&action=show&project_id=1"
            }
        }
    }

getProjectByIdentifier
----------------------

-  用途: **プロジェクトの情報を取得する**
-  パラメーター:

   -  **identifier** (alphanumeric string, 必須)

-  成功時の返り値: **プロジェクトのプロパティ**
-  失敗時の返り値: **null**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getProjectByIdentifier",
        "id": 1620253806,
        "params": {
            "identifier": "TEST"
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1620253806,
        "result": {
            "id": "1",
            "name": "Test",
            "is_active": "1",
            "token": "",
            "last_modified": "1436119135",
            "is_public": "0",
            "is_private": "0",
            "default_swimlane": "Default swimlane",
            "show_default_swimlane": "1",
            "description": "test",
            "identifier": "TEST",
            "url": {
                "board": "http:\/\/127.0.0.1:8000\/?controller=board&action=show&project_id=1",
                "calendar": "http:\/\/127.0.0.1:8000\/?controller=calendar&action=show&project_id=1",
                "list": "http:\/\/127.0.0.1:8000\/?controller=listing&action=show&project_id=1"
            }
        }
    }

getProjectByEmail
-----------------

-  用途: **プロジェクトの情報を取得する**
-  パラメーター:

   -  **email** (string, 必須)

-  成功時の返り値: **プロジェクトのプロパティ**
-  失敗時の返り値: **null**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getProjectByEmail",
        "id": 1620253806,
        "params": {
            "email": "my_project@my_domain.tld"
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1620253806,
        "result": {
            "id": "1",
            "name": "Test",
            "is_active": "1",
            "token": "",
            "last_modified": "1436119135",
            "is_public": "0",
            "is_private": "0",
            "default_swimlane": "Default swimlane",
            "show_default_swimlane": "1",
            "description": "test",
            "identifier": "",
            "email": "my_project@my_domain.tld",
            "url": {
                "board": "http:\/\/127.0.0.1:8000\/?controller=board&action=show&project_id=1",
                "calendar": "http:\/\/127.0.0.1:8000\/?controller=calendar&action=show&project_id=1",
                "list": "http:\/\/127.0.0.1:8000\/?controller=listing&action=show&project_id=1"
            }
        }
    }

getAllProjects
--------------

-  用途: **全ての活動中のプロジェクトを取得する**
-  パラメーター:

   -  **none**

-  成功時の返り値: **プロジェクトのリスト**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getAllProjects",
        "id": 2134420212
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 2134420212,
        "result": [
            {
                "id": "1",
                "name": "API test",
                "is_active": "1",
                "token": "",
                "last_modified": "1436119570",
                "is_public": "0",
                "is_private": "0",
                "default_swimlane": "Default swimlane",
                "show_default_swimlane": "1",
                "description": null,
                "identifier": "",
                "url": {
                    "board": "http:\/\/127.0.0.1:8000\/?controller=board&action=show&project_id=1",
                    "calendar": "http:\/\/127.0.0.1:8000\/?controller=calendar&action=show&project_id=1",
                    "list": "http:\/\/127.0.0.1:8000\/?controller=listing&action=show&project_id=1"
                }
            }
        ]
    }

updateProject
-------------

-  Purpose: **プロジェクトをアップデートする**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **name** (string, 任意)
   -  **description** (string, 任意)
   -  **owner_id** (integer, 任意)
   -  **identifier** (string, 任意)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "updateProject",
        "id": 1853996288,
        "params": {
            "project_id": 1,
            "name": "PHP client update"
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1853996288,
        "result": true
    }

removeProject
-------------

-  用途: **プロジェクトを削除する**
-  Parameters:  **project_id** (integer, 必須)
-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "removeProject",
        "id": 46285125,
        "params": {
            "project_id": "2"
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 46285125,
        "result": true
    }

enableProject
-------------

-  用途: **プロジェクトを有効化する**
-  パラメーター:

   -  **project_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "enableProject",
        "id": 1775494839,
        "params": [
            "1"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1775494839,
        "result": true
    }

disableProject
--------------

-  用途: **プロジェクトを無効化する**
-  パラメーター:

   -  **project_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "disableProject",
        "id": 1734202312,
        "params": [
            "1"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1734202312,
        "result": true
    }

enableProjectPublicAccess
-------------------------

-  用途: **プロジェクトの公開アクセスを有効化する**
-  パラメーター:

   -  **project_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "enableProjectPublicAccess",
        "id": 103792571,
        "params": [
            "1"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 103792571,
        "result": true
    }

disableProjectPublicAccess
--------------------------

-  用途: **プロジェクトの公開アクセスを無効化する**
-  パラメーター:

   -  **project_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "disableProjectPublicAccess",
        "id": 942472945,
        "params": [
            "1"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 942472945,
        "result": true
    }

getProjectActivity
------------------

-  用途: **プロジェクトのアクティビティを取得する**
-  パラメーター:

   -  **project_id** (integer, 必須)

-  成功時の返り値: **イベントのリスト**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getProjectActivity",
        "id": 942472945,
        "params": [
            "project_id": 1
        ]
    }

getProjectActivities
--------------------

-  用途: **(複数の)プロジェクトのフィードを取得する**
-  パラメーター:

   -  **project_ids** (integer array, 必須)

-  成功時の返り値: **イベントのリスト**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getProjectActivities",
        "id": 942472945,
        "params": [
            "project_ids": [1,2]
        ]
    }
