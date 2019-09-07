認証アーキテクチャ
===========================

Kanboardは柔軟でプラガブルな認証アーキテクチャを提供しています。

デフォルトで複数の方法でのユーザー認証をすることができます:

-  ユーザー名とパスワード (ローカルなデータベースとLDAP)
-  OAuth2 認証
- リバースプロキシ認証
-  Cookie ベースの認証 (Remember Me)

更に、認証に成功した後も、2要素認証をすることができます。Kanboard は TOTP 標準をネイティブでサポートしています。

認証インターフェース
-------------------------

プラガブルなシステムを持っているので、認証ドライバーにインターフェースを与えなければなりません:

+-----------------------------------------+-------------------------------------------+
| インターフェース                              | 役割                                      |
+=========================================+===========================================+
| AuthenticationProviderInterface         | 他の認証インターフェースの土台となる   |
|                                         | インターフェース                                |
+-----------------------------------------+-------------------------------------------+
| PreAuthenticationProviderInterface      | アプリケーションを開いた時に    |
|                                         | 既にユーザーが認証を済ませている時に     |
|                                         | いくつかの環境変数を定義するのに使用される |
+-----------------------------------------+-------------------------------------------+
| PasswordAuthenticationProviderInterface | ログインフォーム内でユーザー名と  |
|                                         | パスワードでの認証を提供するメソッド       |
+-----------------------------------------+-------------------------------------------+
| OAuthAuthenticationProviderInterface    | OAuth2 認証を提供する          |
+-----------------------------------------+-------------------------------------------+
| PostAuthenticationProviderInterface     | 2要素認証で、確認コードを |
|                                         |  問い質すドライバ                        |
+-----------------------------------------+-------------------------------------------+
| SessionCheckProviderInterface           | ユーザーのセッションが有効か   |
|                                         |  確認できるようにするプロバイダ                   |
+-----------------------------------------+-------------------------------------------+

認証プロバイダの例:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  -デフォルトのデータベースのメソッドの実装は ``PasswordAuthenticationProviderInterface`` と ``SessionCheckProviderInterface`` です。
-  リバースプロキシのメソッドの実装は ``PreAuthenticationProviderInterface`` と  ``SessionCheckProviderInterface`` です。
-  グーグルを利用するメソッドでの実装は ``OAuthAuthenticationProviderInterface`` です。
-  LDAPを利用するメソッドでの実装は ``PasswordAuthenticationProviderInterface`` です。
-  RememberMe cookieのメソッドの実装は ``PreAuthenticationProviderInterface`` です。
-  二要素認証(TOTP) メソッドの実装は ``PostAuthenticationProviderInterface`` です。

認証のワークフロー
-----------------------

HTTPのリクエストの都度:

1. ユーザーのセッションが既に開かれている場合、``SessionCheckProviderInterface`` を実行します。
2. 全ての認証プロバイダは ``PreAuthenticationProviderInterface`` を実行します。
3. エンドユーザーがログインフォームを使用するならば、``PasswordAuthenticationProviderInterface`` 認証プロバイダ が実行されます。
4. エンドユーザーがOAuth2の使用を望むならば、選択したプロバイダが実行されます。
5. 認証が成功した後は、最後に登録されている ``PostAuthenticationProviderInterface`` が使用されます。
6. 必要ならば、ユーザー情報を同期します。

このワークフローは ``Kanboard\Core\Security\AuthenticationManager`` クラスで管理されています。

トリガされるイベント:

-  ``AuthenticationManager::EVENT_SUCCESS``: 認証成功
-  ``AuthenticationManager::EVENT_FAILURE``: 認証失敗

認証失敗イベントが起こる都度、ログイン失敗カウンターが加算されます。

総当たり攻撃を回避するため、設定された上限に達した時にユーザーアカウントがロックされ、captcha認証が表示されます。

ユーザー情報提供インターフェース
-----------------------

認証が成功した時, ``AuthenticationManager``  は ``getUser()`` メソッドと呼ばれるドライバを呼び出し、ユーザー情報を問い合わせます。
このメソッドは ``Kanboard\Core\User\UserProviderInterface`` として実装されているインターフェースにオブジェクトを返す必要があります。

この抽象化されたクラスは別のシステムから情報を集めます。

例:

-  ``DatabaseUserProvider`` 内部のユーザーの情報を提供します。
-  ``LdapUserProvider`` はLDAPのユーザーの情報を提供します。
-  ``ReverseProxyUserProvider`` はリバースプロキシのユーザーの情報を提供します。
-  ``GoogleUserProvider`` はGoogleのユーザー情報を再送します。

ユーザー情報提供インターフェースのメソッド:

-  ``isUserCreationAllowed()``: 自動でのユーザー作成を許容しtrueを返す
-  ``getExternalIdColumn()``: 外部IDのカラム名を取得する (google_id, github_id, gitlab_id…)
-  ``getInternalId()``: 内部データベース上のIDを取得する
-  ``getExternalId()``: 外部ID (ユニークな id) を取得する
-  ``getRole()``: ユーザーの役割を取得する
-  ``getUsername()``: ユーザー名を取得する
-  ``getName()``: ユーザーのフルネームを取得する
-  ``getEmail()``: ユーザーのemailアドレスを取得する
-  ``getExternalGroupIds()``: 外部グループのIDを取得し、もしあれば自動でグループのメンバーシップを同期する
-  ``getExtraAttributes()``: ローカルの同期のためにセットする、追加の属性を取得する

個々のメソッドは必ずしも値を返すわけではありません。

ローカルのユーザーの同期
--------------------------

ユーザーの情報はローカルのデータベースと自動で同期可能です。

-  ``getInternalId()`` の返り値があった場合、その値は同期が実行されません。
-  ``getExternalIdColumn()`` と ``getExternalId()`` メソッドの返り値をユーザーと同期しなければなりません。
-  プロパティの返り値が空の文字列の場合、同期されないでしょう。
