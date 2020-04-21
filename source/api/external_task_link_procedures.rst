タスクの外部リンクのAPIプロシージャ
=================================

getExternalTaskLinkTypes
------------------------

-  用途: **登録済みの全ての外部リンクの提供元を取得する**
-  パラメータ: **無し**
-  成功時の返り値: **dict**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {"jsonrpc":"2.0","method":"getExternalTaskLinkTypes","id":477370568}

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "result": {
            "auto": "Auto",
            "attachment": "Attachment",
            "file": "Local File",
            "weblink": "Web Link"
        },
        "id": 477370568
    }

getExternalTaskLinkProviderDependencies
---------------------------------------

-  用途: **提供元が使用可能な依存関係を取得する**
-  パラメーター:

   -  **providerName** (string,必須)

-  成功時の返り値: **dict**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {"jsonrpc":"2.0","method":"getExternalTaskLinkProviderDependencies","id":124790226,"params":["weblink"]}

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "result": {
            "related": "Related"
        },
        "id": 124790226
    }

createExternalTaskLink
----------------------

-  用途: **新しい外部リンクを作成**
-  パラメーター:

   -  **task_id** (integer, 必須)
   -  **url** (string, 必須)
   -  **dependency** (string, 必須)
   -  **type** (string, 任意)
   -  **title** (string, 任意)

-  成功時の返り値: **link_id**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {"jsonrpc":"2.0","method":"createExternalTaskLink","id":924217495,"params":[9,"http:\/\/localhost\/document.pdf","related","attachment"]}

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "result": 1,
        "id": 924217495
    }

updateExternalTaskLink
----------------------

-  用途: **タスクの外部リンクのアップデート**
-  パラメーター:

   -  **task_id** (integer, 必須)
   -  **link_id** (integer, 必須)
   -  **title** (string, 必須)
   -  **url** (string, 必須)
   -  **dependency** (string, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc":"2.0",
        "method":"updateExternalTaskLink",
        "id":1123562620,
        "params": {
            "task_id":9,
            "link_id":1,
            "title":"New title"
        }
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "result": true,
        "id": 1123562620
    }

getExternalTaskLinkById
-----------------------

-  用途: **タスクの外部リンクを取得する**
-  パラメーター:

   -  **task_id** (integer, 必須)
   -  **link_id** (integer, 必須)

-  成功時の返り値: **dict**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {"jsonrpc":"2.0","method":"getExternalTaskLinkById","id":2107066744,"params":[9,1]}

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "result": {
            "id": "1",
            "link_type": "attachment",
            "dependency": "related",
            "title": "document.pdf",
            "url": "http:\/\/localhost\/document.pdf",
            "date_creation": "1466965256",
            "date_modification": "1466965256",
            "task_id": "9",
            "creator_id": "0"
        },
        "id": 2107066744
    }

getAllExternalTaskLinks
-----------------------

-  用途: **タスクに添付された全ての外部リンクを取得する**
-  パラメーター:

   -  **task_id** (integer, 必須)

-  成功時の返り値: **外部リンクのリスト**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {"jsonrpc":"2.0","method":"getAllExternalTaskLinks","id":2069307223,"params":[9]}

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "result": [
            {
                "id": "1",
                "link_type": "attachment",
                "dependency": "related",
                "title": "New title",
                "url": "http:\/\/localhost\/document.pdf",
                "date_creation": "1466965256",
                "date_modification": "1466965256",
                "task_id": "9",
                "creator_id": "0",
                "creator_name": null,
                "creator_username": null,
                "dependency_label": "Related",
                "type": "Attachment"
            }
        ],
        "id": 2069307223
    }

removeExternalTaskLink
----------------------

-  用途: **外部リンクを削除する**
-  パラメーター:

   -  **task_id** (integer, 必須)
   -  **link_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {"jsonrpc":"2.0","method":"removeExternalTaskLink","id":552055660,"params":[9,1]}

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "result": true,
        "id": 552055660
    }
