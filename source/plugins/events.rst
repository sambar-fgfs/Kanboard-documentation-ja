イベントを使用
============

Kanboard は内部で `Symfony EventDispatcher
component <https://symfony.com/doc/2.3/components/event_dispatcher/index.html>`__
を内部イベントの管理に使用しています。

イベントを監視
---------------

.. code:: php

    $this->on('app.bootstrap', function($container) {
        // Do something
    });

-  最初の引数はイベント名 (string) です。
-  2つめの引数は 呼び出し可能なPHPの関数 (closure or class method) です。

新しいイベントを追加する
------------------

新しいイベントを追加するには、 ``Kanboard\Core\Event\EventManager`` クラス内の ``register()`` メソッドを呼び出さなければなりません:

.. code:: php

    $this->eventManager->register('my.event.name', 'My new event description');

これらのイベントは自動アクションのようなKanboardの他のコンポーネントで使われる可能性があります。
