ユーザーとグループ
================

ユーザーのタイプ
----------

Kanboard には、2つのタイプのユーザーがあります:

+-----------+----------------------------------------------------------+
| タイプ    | 概要                                                     |
+===========+==========================================================+
| ローカル  | Kanboardのデータベースにパスワードが保存されるユーザー   |
| ユーザー  |                                                          |
+-----------+----------------------------------------------------------+
| リモート  | 別のシステムによって管理されるユーザー                   |
| ユーザー  | 例:LDAP サーバー)                                        |
+-----------+----------------------------------------------------------+

リモートユーザーの例:

-  LDAP のユーザー
-  リバースプロキシによるユーザー認証
-  OAuth2 のユーザー

ユーザーの役割
----------

アプリケーションでの役割
~~~~~~~~~~~~~~~~~

各々のKanboard のユーザーはこれらのうちの一つの役割を持ちます:

+--------------------------------+---------------------------------------+
| 役割                           | 概要                                  |
+================================+=======================================+
| システム管理者                 | 全てにアクセス可能                    |
+--------------------------------+---------------------------------------+
| 組織の管理者                   | チームプロジェクトの作成は可能だが、  |
|                                | アプリケーションの設定は              |
|                                | 変更不可                              |
+--------------------------------+---------------------------------------+
| ユーザー                       | プライベートプロジェクトのみ作成可能  |
+--------------------------------+---------------------------------------+

プロジェクトでの役割
~~~~~~~~~~~~~

個々のチームプロジェクト毎に各々のユーザーとグループに違う役割を割り当てることができます :

+--------------+--------------------------------------------------------+
| 役割         | 概要                                                   |
+==============+========================================================+
| プロジェクト | プロジェクト設定を変更でき、                           |
| 管理者       | ガントチャートと 分析へアクセス可能                    |
+--------------+--------------------------------------------------------+
| プロジェクト | タスクの作成と、ボードの使用が可能                     |
| メンバー     |                                                        |
+--------------+--------------------------------------------------------+
| プロジェクト | ボードとタスクの閲覧のみ可能                           |
| ビューアー   |                                                        |
+--------------+--------------------------------------------------------+

ユーザーに制限を掛けるために、プロジェクト独自の役割を作成することができます。

グループの管理
-----------------

Kanboardでは、各々のユーザーは一つ、あるいは複数のグループのメンバーになることができます。グループとは、一つのチームもしくは組織のようなものです。

システム管理者のみが新しいグループの作成とユーザーの割り当てを行えます。

**ユーザー管理 > 全てのグループを表示** から、グループの管理を行えます。ここから、グループの作成とユーザーの割り当てができます。

.. figure:: /_static/groups-management.png
   :alt: グループの管理

各々のプロジェクト管理者は プロジェクト>権限 のページから、グループに対しアクセス権を設定できます。


外部IDは主に外部グループプロバイダにより使用されます。Kanboardは 自動的にグループをLDAPサーバーと同期するために、LDAPグループプロバイダを提供します。

新規ユーザーの追加
--------------

新規ユーザーを追加するには、管理者でなければなりません。

1. 右上部角のドロップダウンメニューから **ユーザー管理** を開いてください。
2. 上部の **新規ユーザー** のリンクを開いてください。
3. フォームを埋めて、保存してください。

.. figure:: /_static/new-user.png
   :alt: 新規ユーザー

**ローカルユーザー** を作成するときには、最低でも以下を指定しなければなりません。

-  **ユーザー名**: これはユーザー(のログイン時)の識別のためにユニークな物です。
-  **パスワード**: パスワードは最低でも6文字以上必要です。

**リモートユーザー** では、必須なのはユーザー名だけです。

ユーザーの編集
----------

メニュー内の **ユーザー管理** を開くと、ユーザーの一覧が表示されるので、編集するユーザーの **編集** リンクをクリックしてください。

-  一般ユーザーは、自分のプロフィールを編集することのみできます。
-  他のユーザーを編集できるようになるには、管理者になる必要があります。

ユーザーの削除
------------

**ユーザー管理** メニューから、 **削除** のリンクをクリックしてください。このリンクはシステム管理者だけに見えます。

特定のユーザーを削除した後には、 **その人に割当てられていたタスクが未割当になります。** 

二要素認証
-------------------------

個々のユーザーは`二要素認証 <https://ja.wikipedia.org/wiki/%E5%A4%9A%E8%A6%81%E7%B4%A0%E8%AA%8D%E8%A8%BC>`__ を有効にできます。
パスワードとIDの入力に成功した後、Kanboardへユーザーのアクセスを許可するために、ワンタイムパスワード(6文字)が質問されます。

このコードはスマートフォンか別のデバイスにインストールされている、互換性のあるソフトウェアから供給されます。

Kanboard は `RFC 6238 <http://tools.ietf.org/html/rfc6238>`__ で規定される、`Time-based One-time Password Algorithm <http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm>`__ を使用します。

これは標準的なTOTPシステムの多くと互換性があります。
例えば、これらのアプリケーションがあります:

-  `Google 認証システム <https://github.com/google/google-authenticator/>`__
   (Android, iOS, Blackberry)
-  `FreeOTP <https://freeotp.github.io/>`__ (Android, iOS)
-  `OATH Toolkit <http://www.nongnu.org/oath-toolkit/>`__ (Command line utility on Unix/Linux)

このシステムはオフラインで使用でき、必ずしも携帯電話を持っている必要はありません。

設定
-------------

1. ユーザープロフィールを開く
2. 左の **二要素認証** をクリックし、「二要素認証を有効にする」ボタンをクリックする
3. あなたの秘密鍵が生成されます。

.. figure:: /_static/2fa.png
   :alt: 二要素認証

-  TOTPソフトウェアに秘密鍵を保存する必要があります。スマートフォンを使用しているならば、もっとも簡単なのはFreeOTPかGoogle認証でQRコードをスキャンする方法です。
-  新しいセッションを開始する都度、新しいコードを質問されます
-  セッションを閉じる前に、デバイスのテストを忘れないでください。

この機能の有効/無効を切り替える都度、新しい秘密鍵が生成されます。

.. 注意::  Kanboard v1.2.8以降では、二要素認証を有効にするにはAPIキーを使用しなければなりません。
