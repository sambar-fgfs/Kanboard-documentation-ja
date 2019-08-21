プロジェクトの権限のAPIプロシージャ
=================================

getProjectUsers
---------------

-  用途: **プロジェクトのメンバー全てを取得する**
-  パラメーター:

   -  **project_id** (integer, 必須)

-  成功時の返り値: **Dictionary of user_id => user name**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getProjectUsers",
        "id": 1601016721,
        "params": [
            "1"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1601016721,
        "result": {
            "1": "admin"
        }
    }

getAssignableUsers
------------------

-  用途: **プロジェクトのタスクに割当可能なユーザーを取得する**
   (閲覧者を除く全てのメンバー)
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **prepend_unassigned** (boolean, 任意。 デフォルトでは false)

-  成功時の返り値: **Dictionary of user_id => user name**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getAssignableUsers",
        "id": 658294870,
        "params": [
            "1"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 658294870,
        "result": {
            "1": "admin"
        }
    }

addProjectUser
--------------

-  用途: **ユーザーにプロジェクトへのアクセス権を与える**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **user_id** (integer, 必須)
   -  **role** (string, 任意)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "addProjectUser",
        "id": 1294688355,
        "params": [
            "1",
            "1",
            "project-viewer"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1294688355,
        "result": true
    }

addProjectGroup
---------------

-  用途: **グループにプロジェクトへのアクセス権を与える**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **group_id** (integer, 必須)
   -  **role** (string, 任意)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "addProjectGroup",
        "id": 1694959089,
        "params": [
            "1",
            "1"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1694959089,
        "result": true
    }

removeProjectUser
-----------------

-  用途: **ユーザーからプロジェクトへのアクセス権を剥奪する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **user_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "removeProjectUser",
        "id": 645233805,
        "params": [
            1,
            1
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 645233805,
        "result": true
    }

removeProjectGroup
------------------

-  用途: **グループからプロジェクトへのアクセス権を剥奪する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **group_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "removeProjectGroup",
        "id": 557146966,
        "params": [
            1,
            1
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 557146966,
        "result": true
    }

changeProjectUserRole
---------------------

-  用途: **プロジェクトでのユーザーの役割を変更する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **user_id** (integer, 必須)
   -  **role** (string, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "changeProjectUserRole",
        "id": 193473170,
        "params": [
            "1",
            "1",
            "project-viewer"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 193473170,
        "result": true
    }

changeProjectGroupRole
----------------------

-  用途: **プロジェクトでのグループの役割を変更する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **group_id** (integer, 必須)
   -  **role** (string, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "changeProjectGroupRole",
        "id": 2114673298,
        "params": [
            "1",
            "1",
            "project-viewer"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 2114673298,
        "result": true
    }

getProjectUserRole
------------------

-  用途: **プロジェクトでのユーザーの役割を取得する**
-  パラメーター:

   -  **project_id** (integer, 必須)
   -  **user_id** (integer, 必須)

-  成功時の返り値: **role name**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getProjectUserRole",
        "id": 2114673298,
        "params": [
            "2",
            "3"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 2114673298,
        "result": "project-viewer"
    }
