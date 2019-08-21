リンクのAPIプロシージャ
===================

getAllLinks
-----------

-  用途: **全てのタスク間の関係を取得する**
-  パラメータ: 無し
-  成功時の返り値: **リンクのリスト**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getAllLinks",
        "id": 113057196
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 113057196,
        "result": [
            {
                "id": "1",
                "label": "relates to",
                "opposite_id": "0"
            },
            {
                "id": "2",
                "label": "blocks",
                "opposite_id": "3"
            },
            {
                "id": "3",
                "label": "is blocked by",
                "opposite_id": "2"
            },
            {
                "id": "4",
                "label": "duplicates",
                "opposite_id": "5"
            },
            {
                "id": "5",
                "label": "is duplicated by",
                "opposite_id": "4"
            },
            {
                "id": "6",
                "label": "is a child of",
                "opposite_id": "7"
            },
            {
                "id": "7",
                "label": "is a parent of",
                "opposite_id": "6"
            },
            {
                "id": "8",
                "label": "targets milestone",
                "opposite_id": "9"
            },
            {
                "id": "9",
                "label": "is a milestone of",
                "opposite_id": "8"
            },
            {
                "id": "10",
                "label": "fixes",
                "opposite_id": "11"
            },
            {
                "id": "11",
                "label": "is fixed by",
                "opposite_id": "10"
            }
        ]
    }

getOppositeLinkId
-----------------

-  用途: **タスク間リンクのリンク先を取得する**
-  パラメーター:

   -  **link_id** (integer, 必須)

-  成功時の返り値: **link_id**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getOppositeLinkId",
        "id": 407062448,
        "params": [
            2
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 407062448,
        "result": "3"
    }

getLinkByLabel
--------------

-  Purpose: **リンクをラベルから取得する**
-  パラメーター:

   -  **label** (integer, 必須)

-  成功時の返り値: **リンクのプロパティ**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getLinkByLabel",
        "id": 1796123316,
        "params": [
            "blocks"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1796123316,
        "result": {
            "id": "2",
            "label": "blocks",
            "opposite_id": "3"
        }
    }

getLinkById
-----------

-  Purpose: **リンクをIDから取得する**
-  パラメーター:

   -  **link_id** (integer, 必須)

-  成功時の返り値: **リンクのプロパティ**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "getLinkById",
        "id": 1190238402,
        "params": [
            4
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1190238402,
        "result": {
            "id": "4",
            "label": "duplicates",
            "opposite_id": "5"
        }
    }

createLink
----------

-  Purpose: **新しくタスク同士の関連性を作成する**
-  パラメーター:

   -  **label** (integer, 必須)
   -  **opposite_label** (integer, 任意)

-  成功時の返り値: **link_id**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "createLink",
        "id": 1040237496,
        "params": [
            "foo",
            "bar"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 1040237496,
        "result": 13
    }

updateLink
----------

-  Purpose: **リンクをアップデートする**
-  パラメーター:

   -  **link_id** (integer, 必須)
   -  **opposite_link_id** (integer, 必須)
   -  **label** (string, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "updateLink",
        "id": 2110446926,
        "params": [
            "14",
            "12",
            "boo"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 2110446926,
        "result": true
    }

removeLink
----------

-  用途: **リンクを削除する**
-  パラメーター:

   -  **link_id** (integer, 必須)

-  成功時の返り値: **true**
-  失敗時の返り値: **false**

リクエスト例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "method": "removeLink",
        "id": 2136522739,
        "params": [
            "14"
        ]
    }

レスポンスの例:

.. code:: json

    {
        "jsonrpc": "2.0",
        "id": 2136522739,
        "result": true
    }
