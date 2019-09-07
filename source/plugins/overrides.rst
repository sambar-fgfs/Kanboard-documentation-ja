プラグインのオーバーライド
================

HTTP コンテンツのセキュリティポリシーをオーバーライドする
-------------------------------------

デフォルトの HTTP コンテンツのセキュリティポリシーヘッダーを置き換える事を望むならば、 ``setContentSecurityPolicy()`` メソッドが利用できます:

.. code:: php

    <?php

    namespace Kanboard\Plugin\Csp;

    use Kanboard\Core\Plugin\Base;

    class Plugin extends Base
    {
        public function initialize()
        {
            $this->setContentSecurityPolicy(array('script-src' => 'something'));
        }
    }

テンプレートのオーバーライド
------------------

どんなテンプレートでもコア内で定義されていて、オーバーライドできます。例えば、デフォルトのレイアウトやEMail通知を再定義できます。

テンプレートのオーバーライドの例:

.. code:: php

    $this->template->setTemplateOverride('header', 'theme:layout/header');

最初の引数は元のテンプレート名で、2つ目の引数は置き換えに使うテンプレートです。

それでも、“kanboard:” 接頭辞を使うことで元のテンプレートを使用できます:

.. code:: php

    <?= $this->render('kanboard:header') ?>

フォーマッターのオーバーライド
-------------------

これは、Kanboardでフォーマッターオブジェクトをオーバーライドする例です:

.. code:: php

    class MyFormatter extends UserAutoCompleteFormatter
    {
        public function format()
        {
            $users = parent::format();

            foreach ($users as &$user) {
                $user['label'] = 'something'; // Do something useful here
            }

            return $users;
        }
    }

    class Plugin extends Base
    {
        public function initialize()
        {
            $this->container['userAutoCompleteFormatter'] = $this->container->factory(function ($c) {
                return new MyFormatter($c);
            });
        }
    }
