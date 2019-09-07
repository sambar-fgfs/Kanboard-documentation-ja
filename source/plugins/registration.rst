プラグインの登録
===================

プロジェクトの骨組みのジェネレーター
--------------------------

プラグインで自動的にプロジェクトの構造を作成するには　``cookiecutter`` が利用できます。

Cookiecutter をインストールする:

.. code:: bash

    pip install -U cookiecutter

Run Kanboard cookiecutter:

.. code:: bash

    cookiecutter gh:kanboard/cookiecutter-plugin
    plugin_name [My Plugin]: Some Plugin
    plugin_namespace [MyPlugin]: SomePlugin
    plugin_author [Plugin Author]: Me
    plugin_description [My plugin is awesome]:
    plugin_homepage [https://github.com/kanboard/plugin-myplugin]:

ディレクトリの構造
-------------------

プラグインは ``plugins`` サブディレクトリの中に保存されています。プラグインディレクトリの構造の例:

.. code:: bash

    plugins
    └── Budget            <= Plugin name
        ├── Asset         <= Javascript/CSS files
        ├── Controller
        ├── LICENSE       <= Plugin license
        ├── Locale
        │   ├── fr_FR
        │   ├── it_IT
        │   ├── ja_JP
        │   └── zh_CN
        ├── Model
        ├── Plugin.php    <= Plugin registration file
        ├── README.md
        ├── Schema        <= Database migrations
        ├── Template
        └── Test          <= Unit tests

プラグインの登録ファイルの ``Plugin.php`` のみが必要です。それ以外のフォルダーは任意です。

プラグイン名の頭文字は大文字にする必要があります。

プラグインの登録ファイル
------------------------

Kanboardは ``plugins`` ディレクトリをスキャンし、ディレクトリ以下にある物を自動的にロードします。``Plugin.php`` ファイルはプラグインのロードと登録に使用されます。

``Plugin.php`` (``plugins/Foobar/Plugin.php``) ファイルの例:

.. code:: php

    <?php

    namespace Kanboard\Plugin\Foobar;

    use Kanboard\Core\Plugin\Base;

    class Plugin extends Base
    {
        public function initialize()
        {
            $this->template->hook->attach('template:layout:head', 'theme:layout/head');
        }

        public function getCompatibleVersion()
        {
            // Examples:
            // >=1.0.37
            // <1.0.37
            // <=1.0.37
            return '1.0.37';
        }
    }

このファイルは ``Kanboard\Plugin\Yourplugin`` 名前空間の下に ``Plugin`` クラスの定義を含んでいて、``Kanboard\Core\Plugin\Base`` を拡張しなければなりません。

必要なメソッドは ``initialize()`` だけです。このメソッドはプラグインがロードされる時の要求の都度呼ばれます。

プラグインのメソッド
--------------

``Kanboard\Core\Plugin\Base`` から利用可能なメソッド:

-  ``initialize()``: プラグインがロードされた時に実行される
-  ``getClasses()``: Return all classes that should be stored in the dependency injection container
-  ``on($event, $callback)``: Listen on internal events
-  ``getPluginName()``: Should return plugin name (must match plugins.json ``"title":`` entry for "Plugin Directory" version update notifications to work)
-  ``getPluginAuthor()``: Should return plugin author
-  ``getPluginVersion()``: Should return plugin version
-  ``getPluginDescription()``: Should return plugin description
-  ``getPluginHomepage()``: Should return plugin Homepage (link)
-  ``setContentSecurityPolicy(array $rules)``: Override default HTTP CSP rules
-  ``onStartup()``: If present, this method is executed automatically when the event “app.bootstrap” is triggered
-  ``getCompatibleVersion()``: You may want to specify the Kanboard version compatible with the plugin

Your plugin registration class can also inherit from
``Kanboard\Core\Base``, that way you can access
all classes and methods of Kanboard easily.

ユーザー #123 を取得する例:

.. code:: php

    $this->user->getById(123);

プラグインの翻訳
-------------------

プラグインはアプリケーションと同じ方法で翻訳できます。
セッションが生成された時に、自身で翻訳をロードしなければなりません:

.. code:: php

    public function onStartup()
    {
        Translator::load($this->languageModel->getCurrentLanguage(), __DIR__.'/Locale');
    }

翻訳ファイルは ``plugins/Myplugin/Locale/xx_XX/translations.php`` (xx_XX は、fr_FR, en_US…のように言語コードに置き換え) に保存されていなければなりません。

翻訳は連想配列として保存されていて、既知の文をオーバーライドしたいならば、翻訳ファイル中で同じキーを使用するだけで済みます。

DIコンテナ
------------------------------

Kanboard は、シンプルなPHPのDIの pimpleを使用します。
しかしながら、Kanboard はコンテナ内のクラスの登録を簡単に行えます。

これらのクラスはインスタンスを一つ作るだけで、アプリケーションのどこからでも利用可能です。

ここにコンテナ内のモデルを登録する例を示します:

.. code:: php

    public function getClasses()
    {
        return array(
            'Plugin\Budget\Model' => array(
                'HourlyRateModel',
                'BudgetModel',
            )
        );
    }

すでに、  ``Core\Base`` から拡張したクラスで、これらのインスタンスに直接アクセスできます。

.. code:: php

    $this->hourlyRateModel->remove(123);
    $this->budgetModel->getDailyBudgetBreakdown(456);

    // コンテナを使用するのと同じ事が起きます:
    $this->container['hourlyRateModel']->getAll();

コンテナのキーはアプリケーションにわたってユニークです。既存のクラスをオーバーライドすれば、デフォルトの挙動を変更できます。
