iCalendar 配信
=======================

KanboardはプロジェクトとユーザーについてのiCalender配信をサポートしています。この特徴により、主要なカレンダープログラム(Microsoft OutLook, Apple Calender, Mozilla Thunderbird, Googleカレンダー)はKanboardのタスクをインポートできます。

カレンダー配信は **read-only** アクセスで、外部のカレンダーソフトウェアからタスクをつくる事は出来ません。カレンダー配信のエクスポートの流れはiCalendarの標準によります。(訳注:多分RFC5545。)

注意:iCalenderで配信されるタスクは、2ヵ月前から6ヵ月先の範囲だけです。

プロジェクトのカレンダー
-----------------

-  各々のプロジェクトは自身のカレンダーを持ちます
-  配信リンクはプロジェクト毎にユニークで、**プロジェクト設定 > 公開アクセス** で公開アクセスを有効化したときにリンクがアクティブになります。
-  このカレンダーは選択したプロジェクトのタスクのみを表示します。

ユーザーのカレンダー
--------------

-  ユーザー毎に自身のためのカレンダーもあります。
-  配信リンクはユーザー毎にユニークで、**ユーザープロフィール > 公開アクセス** で公開アクセスを有効化したときにリンクがアクティブになります。
-  このカレンダーはユーザーに割当てられた全てのプロジェクトのタスクを表示します。

KanboardのカレンダーをApple Calenderに追加する
-----------------------------------------------

-  カレンダーを開く
-  **File > New Calendar Subscription** を選択
-  KanboardのiCal Feed URLをコピー・ペーストする

.. figure:: /_static/apple-calendar-add-subscription.png
   :alt: iCalサブスクリプションを追加

-  利用可能な全てのデバイスをiCloudでカレンダーを同期するか選択できます。
-  頻繁に更新するよう選択するのを忘れないでください。

.. figure:: /_static/apple-calendar-edit-subscription.png
   :alt: iCal サブスクリプションを編集

Kanboard のカレンダーをMozilla Thunderbirdに追加する
----------------------------------------------------

-  Thunderbirdでカレンダーをサポートするために、**Lightning** アドオンをインストールする。
-  **File > New Calendar** をクリックする
-  ダイアログボックス内で、**On the Network**を選択する

.. figure:: /_static/thunderbird-new-calendar-step1.png
   :alt: Thunderbird (ステップ1)

-  iCalenderフォーマットを選択する
-  KanboardのiCal Feed URLをコピー・ペーストする

.. figure:: /_static/thunderbird-new-calendar-step2.png
   :alt: Thunderbird (ステップ 2)

-  色を選択して、その他の設定をしてから、最後に保存する

KanboardカレンダーをGoogleカレンダーに追加する
------------------------------------------------

-  「↓」の次にある、*その他のカレンダー**をクリックする
-  メニューから**URLで追加**を選択する
-  KanboardのiCal Feed URLをコピー・ペーストする

.. figure:: /_static/google-calendar-add-subscription.png
   :alt: Googleカレンダー

また、同期を有効にしているならばKanboardカレンダーはAndroidデバイスからも利用可能です。

注意:Googleサポートによると、外部カレンダーは頻繁には更新されません。`この文書を参照願います。 <https://support.google.com/calendar/answer/37100?hl=en&ref_topic=1672445>`__
