プラグインで通知のタイプを追加する
===================================

新しく通知のタイプを追加することで、だいたいどんなシステムにも通知を送ることができます。
通知には2種類あります: プロジェクトとユーザーです。

-  プロジェクト: プロジェクトレベルでの通知設定
- ユーザー: ユーザープロフィールで、通知を送るよう個別に設定

新しい通知の形を追加
--------------------------------

プラグインとして登録したファイルの中で ``setType()`` メソッドを呼び出す:

.. code:: php

    $this->userNotificationTypeModel->setType('irc', t('IRC'), '\Kanboard\Plugin\IRC\Notification\IrcHandler');
    $this->projectNotificationTypeModel->setType('irc', t('IRC'), '\Kanboard\Plugin\IRC\Notification\IrcHandler');

ユーザー or プロジェクトの通知のために、ハンドラが登録されます。両方をサポートすることは必須ではありません。

ハンドラが登録された時、エンドユーザーは新しいタイプでの通知を受け取るか否か選択できます。

通知のハンドラ
--------------------

通知のハンドラは ``Kanboard\Core\Notification\NotificationInterface`` インターフェースを実装しなければなりません:

.. code:: php

    interface NotificationInterface
    {
        /**
         * ユーザーに通知を送る
         *
         * @access public
         * @param  array     $user
         * @param  string    $event_name
         * @param  array     $event_data
         */
        public function notifyUser(array $user, $event_name, array $event_data);

        /**
         * プロジェクトに通知を送る
         *
         * @access public
         * @param  array     $project
         * @param  string    $event_name
         * @param  array     $event_data
         */
        public function notifyProject(array $project, $event_name, array $event_data);
    }

通知プラグインの例
-------------------------------

-  `Slack <https://github.com/kanboard/plugin-slack>`__
-  `Hipchat <https://github.com/kanboard/plugin-hipchat>`__
-  `Jabber <https://github.com/kanboard/plugin-jabber>`__
