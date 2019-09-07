新しいヘルパーを登録する
=======================

ヘルパーの概略:

.. code:: php

    <?php

    namespace Kanboard\Plugin\MyPlugin\Helper;

    use Kanboard\Core\Base;

    class MyHelper extends Base
    {
        public function doSomething()
        {
            return 'foobar';
        }
    }

ヘルパーのクラスを登録する:

.. code:: php

    $this->helper->register('myHelper', '\Kanboard\Plugin\MyPlugin\Helper\MyHelper');

テンプレートからヘルパーを利用する:

.. code:: php

    <p>
        <?= $this->myHelper->doSomething() ?>
    </p>

別のクラスからヘルパーを使用する:

.. code:: php

    $this->helper->myHelper->doSomething();
