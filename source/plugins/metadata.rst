メタデータ
========

個々のプロジェクト、タスク、ユーザー、あるいはアプリケーション全体にメタデータを添付できます。メタデータは、 キー/値 のテーブルのカスタムフィールドです。

例えばあなたのプラグインはタスクやプロジェクトの新しい設定を外部情報として保存できます。これは基本的に、新しいテーブルを作らずにデフォルトのフィールドを拡張することを許容します。

メタデータをタスクに添付/削除する
----------------------------------------

.. code:: php


    // $task_id :連想配列のメタデータ (キー/値)
    $this->taskMetadataModel->getAll($task_id);

    // タスクのみの値を取得する
    $this->taskMetadataModel->get($task_id, 'my_plugin_variable', 'default_value');

    // 既にmy_plugin_variable にメタデータがあれば、 true を返す
    $this->taskMetadataModel->exists($task_id, 'my_plugin_variable');

    // タスクのメタデータを作成or更新する
    $this->taskMetadataModel->save($task_id, ['my_plugin_variable' => 'something']);

    // プロジェクトからメタデータを削除する
    $this->projectMetadataModel->remove($project_id, my_plugin_variable);

メタデータのタイプ
--------------

-  タスクのメタデータ: ``$this->taskMetadataModel``
-  プロジェクトのメタデータ: ``$this->projectMetadataModel``
-  ユーザーのメタデータ: ``$this->userMetadataModel``
-  設定: ``$this->configModel``

.. 注意::  メタデータ名のプレフィックスは常にプラグイン名になります。
