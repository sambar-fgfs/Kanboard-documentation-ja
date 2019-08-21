タグのAPIプロシージャ
===================

getAllTags
----------

-  用途: **全てのタグを取得する**
-  パラメータ: 無し
-  成功時の返り値: **タグのリスト**
-  失敗時の返り値: **false | null**

リクエスト例:

.. code:: json

    {"jsonrpc":"2.0","method":"getAllTags","id":45253426}

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "result": [
            {
                "id": "1",
                "name": "another tag",
                "project_id": "33"
            }
        ],
        "id": 45253426
    }

getTagsByProject
----------------

-  用途: **プロジェクトに与えられた全てのタグを取得する**
-  パラメーター:

   -  **project_id** (integer)

-  成功時の返り値: **タグのリスト**
-  失敗時の返り値: **false | null**

リクエスト例:

.. code:: json

    {"jsonrpc":"2.0","method":"getTagsByProject","id":1217591720,"params":[33]}

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "result": [
            {
                "id": "1",
                "name": "some tag",
                "project_id": "33"
            }
        ],
        "id": 1217591720
    }

createTag
---------

-  用途: **新しいタグを作成**
-  パラメーター:

   -  **project_id** (integer)
   -  **tag** (string)

-  成功時の返り値: **tag_id**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {"jsonrpc":"2.0","method":"createTag","id":1775436017,"params":[33,"some tag"]}

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "result": 1,
        "id": 1775436017
    }

updateTag
---------

-  用途: **タグの名前を変更する**
-  パラメーター:

   -  **tag_id** (integer)
   -  **tag** (string)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {"jsonrpc":"2.0","method":"updateTag","id":2037516512,"params":["1","another tag"]}

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "result": true,
        "id": 2037516512
    }

removeTag
---------

-  用途: **タグを削除する**
-  パラメーター:

   -  **tag_id** (integer)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {"jsonrpc":"2.0","method":"removeTag","id":907581298,"params":["1"]}

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "result": true,
        "id": 907581298
    }

setTaskTags
-----------

-  用途: **タグをタスクに割当て/作成/更新する**
-  パラメーター:

   -  **project_id** (integer)
   -  **task_id** (integer)
   -  **tags** タグのリスト ([]string)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {"jsonrpc":"2.0","method":"setTaskTags","id":1524522873,"params":[39,17,["tag1","tag2"]]}

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "result": true,
        "id": 1524522873
    }

getTaskTags
-----------

-  用途: **タスクに割り当てられたタグを取得する**
-  パラメーター:

   -  **task_id** (integer)

-  成功時の返り値: **タグの連想配列**
-  失敗時の返り値: **false | null**

リクエスト例:

.. code:: json

    {"jsonrpc":"2.0","method":"getTaskTags","id":1667157705,"params":[17]}

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "result": {
            "1": "tag1",
            "2": "tag2"
        },
        "id": 1667157705
    }
