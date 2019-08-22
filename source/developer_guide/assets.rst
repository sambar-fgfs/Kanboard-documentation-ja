ビルドのためのアセット (Javascript と CSS ファイル)
==========================================

スタイルシートと Javascript ファイルは両方をマージした縮小版です。

- オリジナルのCSSファイルは ``assets/css/src/*.css`` です。
- オリジナルのJavascriptファイルは ``assets/js/src/*.js`` です。

必要要件
------------

- PHP
- ローカルにチェックアウトしたGitリポジトリ

インストラクション
------------

Javascriptのビルド:

.. code:: bash

    ./cli js

スタイルシートのビルド:

.. code:: bash

    ./cli css

.. 注意::
	
	- Kanboardのアーカイブからアセットをビルドする事は出来ないので、リポジトリからクローンする必要があります。
	- Kanboard v1.2.11以降では、依存関係からnodejs, Sass, Gulpが削除されました。
