自動アクション
=================

ユーザーの操作を最少化するため、Kanboardは自動アクションをサポートしています。

各々の自動アクションはこれらのプロパティで定義されます:

- イベントを監視
- イベントとリンクされたアクション
- 追加のパラメータ

各々のプロジェクトには、異なる自動アクションを持たせられます。この設定パネルの場所は、「このプロジェクトの設定」→「**自動アクションの管理**」です。

新しいアクションを追加
----------------

**新しいアクションを追加** のリンクをクリックしてください。

.. figure:: /_static/automatic-action-creation.png
   :alt: 自動アクション

1. アクションを選択する
2. イベントを選択する
3. パラメータを定義する

利用可能なアクション
-----------------

-  外部サービスからコメントを作成
-  カラム間でタスクを移動するときにコメントログを追加
-  色に基いてカテゴリを変える
-  カテゴリを外部サービスに基いて変更
-  リンクに基づいてカテゴリを変える
-  カテゴリに基いて色を変える
-  タスクが特定のカラムに移動した時の色を設定
-  特定のタスクリンクを使用するとタスクの色を変更
-  色をユーザーに割当てる
-  アクションを起こしたユーザーを担当者にする
-  カラムが変更されたときにアクションを実行する人にタスクを割当てる
-  タスクの担当者を割当てる
-  担当者を外部サービスに基いて変更
-  タスクを完了する
-  特定のカラムのタスクを完了させる
-  タスクを外部サービスから作成
-  別のプロジェクトにタスクを複製
-  タスクをメールで送信
-  タスクを別プロジェクトに移動
-  ユーザーの割当てをしたらタスクを他のカラムに移動
-  カテゴリが変更されたときにタスクを別のカラムに移動
-  ユーザーの割当てがなくなったらタスクを他のカラムに移動
-  タスクを開く
-  開始日を自動的に更新

例
--------

ここに実際の使用例を記します:

カラム “Done”にタスクを移動したら、自動的にタスクを完了する
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  アクション: **特定のカラムのタスクを完了させる** を選択
-  イベント **タスクを別のカラムに移動** を選択
-  アクションのパラメータ: **カラム = Done** (送り先となるカラム) を定義

カラム “To be validated” にタスクを移動したら、タスクの担当者を割り当てる
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  アクション: **タスクの担当者を割り当てる** を選択
-  イベント **タスクを別のカラムに移動** を選択
-  アクションのパラメータ: **カラム = To be validated** と、 **ユーザー = Bob** を定義 (Bobはテスト担当)

カラム “Work in Progress” にタスクを移動したら、その人にタスクの担当者を割り当てる
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


-  アクション: **アクションを起こしたユーザーを担当者にする** を選択
-  イベント **タスクを別のカラムに移動** を選択
-  アクションのパラメータ: **カラム = Work in progress** を定義

タスクが完了したときに、別のプロジェクトにタスクを複製する
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

“受注対応” と “生産” の2つのプロジェクトが存在するケースで説明します。一旦受注を確認してから、"生産" プロジェクトに移します。

-  アクション: **別のプロジェクトにタスクを複製** を選択
-  イベント: **タスクを完了する** を選択
-  アクションのパラメータ: **カラム = 確認済** と、 **プロジェクト = 生産** を定義

タスクを最後のカラムに移動したときに、そのタスクを別のプロジェクトに移動する
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

“構想” と “開発”の2つのプロジェクトが存在するケースで説明します。一旦アイデアを検証してから、"開発"プロジェクトに移します。

-  アクション: **-  タスクを別プロジェクトに移動** を選択
-  イベント **タスクを別のカラムに移動** を選択
-  アクションのパラメータ: **カラム = 検証済** と、 **プロジェクト = 開発** を定義

ユーザー "Bob" に自動的に色を割り当てたい
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  アクション: **色をユーザーに割当てる** を選択
-  イベント: **担当者の変更** を選択
-  アクションのパラメータ: **色 = グリーン** と **担当 = Bob** を定義

定義済みカテゴリ “Feature Request” に、自動的に色を割り当てたい
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  アクション: **カテゴリに基いて色を変える** を選択
-  イベント: **タスクの作成または変更** を選択
-  アクションを定義: **色 = ブルー** と、 **カテゴリ = Feature
   Request**

タスクがカラム"Work in progress"に移動された時、自動的に開始日をセットしたい
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  アクション: **開始日を自動的に更新** を選択
-  イベント **タスクを別のカラムに移動** を選択
-  アクションのパラメータ: **カラム = Work in progress** を定義
