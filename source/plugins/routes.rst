カスタムルート
=============

URL rewriting を有効にされている時は、プラグインからカスタムルートを定義できます。

新しいルートを定義する
-----------------

``Kanboard\Core\Http\Route`` クラスによってルートはハンドルされています。

新しいルートは ``addRoute($path, $controller, $action, $plugin)`` メソッドを使うことで追加できるので、ここに例示します:

.. code:: php

    $this->route->addRoute('/my/custom/route', 'myController', 'myAction', 'myplugin');

エンドユーザーが ``/my/custom/route`` のURLにアクセスした時、``Kanboard\Plugin\Myplugin\Controller\MyController::myAction()`` メソッドが実行されます。

コントローラーとプラグイン名の頭文字は ``ucfirst()`` 関数で大文字に変換されます。

ルートの定義には変数を併用することもできます:

.. code:: php

    $this->route->addRoute('/my/route/:my_variable', 'myController', 'myAction', 'myplugin');

接頭辞のコロン ``:`` が、変数の定義です。例えば、 ``:my_variable`` は新しい変数``my_variable`` の宣言です。

変数の値を取得するには、 ``Kanboard\Core\Http\Request`` クラスの ``getStringParam()`` か、 ``getIntegerParam()`` クラスを使用できます:

URLが ``/my/route/foobar`` の場合、変数 ``my_variable`` の値は``foobar` です`:

.. code:: php

    $this->request->getStringParam('my_variable'); // foobar を返す

ルーティングテーブルに基づいたリンクの生成
-----------------------------------------

テンプレートより、ヘルパー ``Kanboard\Helper\Url`` を使う必要があります.

HTML のリンクを生成する
~~~~~~~~~~~~~~~~~~~~

.. code:: php

    <?= $this->url->link('My link', 'mycontroller', 'myaction', array('plugin' => 'myplugin')) ?>

生成される HTML:

.. code:: html

    <a href="/my/custom/route">My link</a>

``href`` 属性のみを生成する:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: php

    <?= $this->url->href('My link', 'mycontroller', 'myaction', array('plugin' => 'myplugin')) ?>

HTML での出力:

.. code:: html

    /my/custom/route

URL rewriting が有効になっていない場合の HTML 出力:

.. code:: html

    ?controller=mycontroller&amp;action=myaction&amp;plugin=myplugin

リダイレクトのリンクを生成する:
~~~~~~~~~~~~~~~~~~~~~~~

リダイレクトする必要がある場合、コントローラーから:

.. code:: php

    $this->url->to('mycontroller', 'myaction', array('plugin' => 'myplugin'));

生成されたもの:

::

    ?controller=mycontroller&action=myaction&plugin=myplugin
