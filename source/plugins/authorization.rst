認可アーキテクチャ
==========================

Kanboard はプロジェクトのレベルとアプリケーションのレベルによって複数の役割をサポートしています。

認可のワークフロー
----------------------

HTTPのリクエストの都度:

1. アプリケーションのアクセスリストを元に、リソースへのアクセスを承認/不承認します。
2. リソースがプロジェクト (ボード、タスク…)の場合:

   1. プロジェクト上のユーザーの役割を取得する
   2. プロジェクトのアクセスマップを元にアクセス件を付与/拒否する

アクセスマップを展開する
--------------------

アクセスリスト (ACL) はコントローラーのクラス名とメソッド名を基にしています。アクセスリストは ``Kanboard\Core\Security\AccessMap`` クラスでハンドルされています。

これらは2つのアクセスマップがあります:一つはアプリケーションの、もう一つはプロジェクトを扱います。

-  Application access map: ``$this->applicationAccessMap``
-  Project access map: ``$this->projectAccessMap``

あなたのプラグインから新しいポリシーを定義する例:

.. code:: php

    // All methods of the class MyController:
    $this->projectAccessMap->add('MyController', '*', Role::PROJECT_MANAGER);

    // Specific methods:
    $this->projectAccessMap->add('MyOtherController', array('create', 'save'), Role::PROJECT_MEMBER);

役割は ``Kanboard\Core\Security\Role`` クラスで定義されます。

認可クラス (``Kanboard\Core\Security\Authorization``) は個々のページごとにアクセスをチェックします。
