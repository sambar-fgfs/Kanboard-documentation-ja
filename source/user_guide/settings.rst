設定
========

設定ページからいくつかのアプリケーションのパラメーターを変更できます。
これらの設定はシステム管理者のみが可能です。

アプリケーション設定
--------------------

メニューの **設定** を開いてから、左側の **アプリケーション設定** を選択してください。

.. figure:: /_static/application-settings.png
   :alt: アプリケーションの設定

アプリケーションのURL
~~~~~~~~~~~~~~~

このパラメーターはEmail通知で使用されます。Emailのフッターには、Kanboardのタスクへのリンクが記載されます。

言語
~~~~~~~~

アプリケーションの言語はいつでも変更できます。この言語設定は全てのユーザーに適用されます。

タイムゾーン
~~~~~~~~~

デフォルトではKanboard は UTC を使用しますが、自身のタイムゾーンに合わせることができます。このリストは使用しているwebサーバーがサポートしているタイムゾーン全てを含みます。

日付の書式
~~~~~~~~~~~

例えばタスクの期限などの、日付フィールドの入力の書式を設定します。

Kanboard は4つの書式が利用できます:

-  DD/MM/YYYY
-  MM/DD/YYYY (デフォルト)
-  YYYY/MM/DD
-  MM.DD.YYYY

また、 `ISO 8601 <http://ja.wikipedia.org/wiki/ISO_8601>`__ の、YYYY-MM-DD か、 YYYY_MM_DD形式はいつでも使用可能です。

カスタムスタイルシート
~~~~~~~~~~~~~~~~~

Kanboardのデフォルトのスタイルを拡張、またはオーバーライドするために、自分でCSSを書くことができます。

これは、カテゴリのラベルの色を変更する例です:

カテゴリコンテナでは:

.. code:: css

    .task-board-category-container-color span {
      border: solid 0.5px grey;
      color: black;
    }

一つのカテゴリに対してカスタムCSSの値を設定 - この例では、表示されるテキストに適用されます:

.. code:: css

    [class*="category-MyLabel"] {
      background-color: rgba(255, 0, 0, 0.50);
      border: none!important;
      font-weight: bold;
      font-style: italic;
      box-shadow: 0 1px 1px rgba(186, 186, 186, 0.55);
      color: white!important;
      font-size:11px;
    }

プロジェクト設定
----------------

メニューの **設定** を開いてから、 左側の **プロジェクト設定** を選択してください。

.. figure:: /_static/project-settings.png
   :alt: プロジェクト設定

新規プロジェクトのためのデフォルトのカラム
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

ここで、デフォルトのカラム名を変更できます。これは、いつも同じカラムでプロジェクトを作る場合に便利です。

各々のカラムはカンマで区切らなければなりません。

デフォルトでは、Kanboardは以下のカラム名を使用します: Backlog, Ready, Work in progress, Done

新しいプロジェクトのデフォルトのカテゴリ
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

カテゴリはアプリケーション全体には適用されず、プロジェクトに付属します。
各々のプロジェクトに異なるカテゴリを持たせることができます。

しかしながら、どのプロジェクトでもいつも同じカテゴリを作成しているならば、ここで自動的に作成するカテゴリのリストを定義できます。

一人のユーザーが一度に一つのサブタスクのみを進行させるようにする
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

このオプションを有効にすると、一人のユーザーは一度の一つのサブタスクのみ作業できるようになります。

もし別のサブタスクを "進行中"にしようとすると、下記のダイヤログボックスが表示されるでしょう:

.. figure:: /_static/subtask-user-restriction.png
   :alt: サブタスクの制限

サブタスクを自動で時間追跡するトリガ
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  有効にすると、サブタスクの状態が"進行中"に変わった時、タイマーが自動的にスタートします。
-  時間追跡を利用しない場合、このオプションを無効にしてください。

累積フロー図に完了したタスクを含める
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  有効にした場合、完了したタスクも累積フロー図に含められます。
-  無効の場合は、累積フロー図に含まれるのは未完了のタスクのみです。
-  このオプションは"プロジェクトの毎日の統計"の表中の"合計"列に影響します。

基本設定
--------------

メニューの **設定** を開いてから、左側の **基本設定** を選択してください。

.. figure:: /_static/board-settings.png
   :alt: 基本設定

タスクのハイライト
~~~~~~~~~~~~~~~~~

この機能は、最近移動したタスクの周りに影を表示します。

デフォルトでは2日(172800秒)ですが、値を0にすると無効になります。

一昨日以降に動いた全てのタスクの周りに影が付きます。

公開ボードの更新頻度
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

ボードを共有していると、ページはデフォルトで60秒ごとに自動更新されます。

非公開ボードの更新頻度
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

ブラウザでボードを表示しているときは、Kanboardは10秒ごとに誰かが何かを変更していないかチェックします。

技術的には Ajax polling でこのプロセスを行います。

カレンダー設定
-----------------

メニューの **設定** を開いてから、左側の **カレンダー設定** を選択してください。

.. figure:: /_static/calendar-settings.png
   :alt: カレンダー設定

Kanboardには2つの異なるカレンダーがあります:

-  プロジェクトのカレンダー
-  ユーザーのカレンダー (ダッシュボードから利用可能)

プロジェクトのカレンダー
~~~~~~~~~~~~~~~~

このカレンダーは定められた期限日とタスクの作成日か開始日を基にしてタスクをカレンダーに表示します。

作成日に基づいてタスクを表示:

-  カレンダー上のイベントの開始日はタスクの作成日になります。
-  イベントの終了日は完了日になります。

開始日に基いてタスクを表示:

-  カレンダー上のイベントの開始日はタスクの開始日になります。
-  この日付は手動で定義できます。
-  イベントの終了日は完了日になります。
-  開始日が無いタスクはカレンダー上に表示されません。

ユーザーのカレンダー
~~~~~~~~~~~~~

このカレンダーはユーザーに割当てられたタスクと、追加的なサブタスクの情報のみを表示します。

サブタスクを時間の追跡に基いて表示する:

-  時間追跡テーブルの記録情報から、サブタスクをカレンダーに表示します。
-  また、セクション内でユーザーのタイムテーブルも計算されます。

サブタスクの見積 (今後の作業の見通し)を表示する:

-  "作業予定"の状態のサブタスクは定義された"見積時間"の値から、今後の作業の終了予測時間を表示します。

リンクの設定
-------------

タスクの関連性はアプリケーション設定から変更できます ( **設定
> リンクラベル** )

.. figure:: /_static/link-labels.png
   :alt: リンクラベル

各々のラベルには対になるラベルを定義できます。対になるラベルが無い場合、そのラベルは双方向になります。

.. figure:: /_static/link-label-creation.png
   :alt: リンクラベルの作成
