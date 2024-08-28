# UbuntuでのLLMサーバーセットアップ

このリポジトリには、Ubuntuマシンに大規模言語モデル（LLM）サーバーをセットアップするためのAnsibleプレイブックと関連タスクが含まれています。このプレイブックは、NVIDIAドライバー、Docker、およびNVIDIAコンテナツールキットを含む必要なソフトウェアをインストールし、システムを最適なパフォーマンスに構成します。

## 前提条件

- ローカルマシンにAnsibleがインストールされていること。
- SSHアクセスが可能なUbuntuサーバー。
- ターゲットサーバーでのsudo権限。

## リポジトリ構成

```
.
├── .gitignore
├── ansible.cfg
├── inventory.yaml
├── linux_llm_server_playbook.yaml
└── tasks/
    ├── install_git_lfs.yaml
    ├── setup_docker.yaml
    ├── setup_nvidia_container_toolkit.yaml
    ├── setup_nvidia_driver.yaml
    └── upgrade_ubuntu.yaml
```

## プレイブック概要

### メインプレイブック: [`linux_llm_server_playbook.yaml`](command:_github.copilot.openRelativePath?%5B%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2FUsers%2Fanek%2FPersonalProjects%2Fllm-ansible-playbook%2Flinux_llm_server_playbook.yaml%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%5D "/Users/anek/PersonalProjects/llm-ansible-playbook/linux_llm_server_playbook.yaml")

これは、LLMサーバーのセットアップを指揮するメインプレイブックです。システムの更新、Git LFSのインストール、NVIDIAドライバー、Docker、およびNVIDIAコンテナツールキットのセットアップを含むタスクが含まれています。

### タスク

- **Ubuntuの更新**: Ubuntuシステムを更新およびアップグレードします。
  - ファイル: [`tasks/upgrade_ubuntu.yaml`](command:_github.copilot.openRelativePath?%5B%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2FUsers%2Fanek%2FPersonalProjects%2Fllm-ansible-playbook%2Ftasks%2Fupgrade_ubuntu.yaml%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%5D "/Users/anek/PersonalProjects/llm-ansible-playbook/tasks/upgrade_ubuntu.yaml")
- **Git LFSのインストール**: Git Large File Storageをインストールします。
  - ファイル: [`tasks/install_git_lfs.yaml`](command:_github.copilot.openRelativePath?%5B%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2FUsers%2Fanek%2FPersonalProjects%2Fllm-ansible-playbook%2Ftasks%2Finstall_git_lfs.yaml%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%5D "/Users/anek/PersonalProjects/llm-ansible-playbook/tasks/install_git_lfs.yaml")
- **NVIDIAドライバーのセットアップ**: NVIDIAドライバーをインストールおよび構成します。
  - ファイル: [`tasks/setup_nvidia_driver.yaml`](command:_github.copilot.openRelativePath?%5B%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2FUsers%2Fanek%2FPersonalProjects%2Fllm-ansible-playbook%2Ftasks%2Fsetup_nvidia_driver.yaml%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%5D "/Users/anek/PersonalProjects/llm-ansible-playbook/tasks/setup_nvidia_driver.yaml")
- **Dockerのセットアップ**: Dockerをインストールし、構成します。
  - ファイル: [`tasks/setup_docker.yaml`](command:_github.copilot.openRelativePath?%5B%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2FUsers%2Fanek%2FPersonalProjects%2Fllm-ansible-playbook%2Ftasks%2Fsetup_docker.yaml%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%5D "/Users/anek/PersonalProjects/llm-ansible-playbook/tasks/setup_docker.yaml")
- **NVIDIAコンテナツールキットのセットアップ**: NVIDIAコンテナツールキットをインストールし、構成します。
  - ファイル: [`tasks/setup_nvidia_container_toolkit.yaml`](command:_github.copilot.openRelativePath?%5B%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2FUsers%2Fanek%2FPersonalProjects%2Fllm-ansible-playbook%2Ftasks%2Fsetup_nvidia_container_toolkit.yaml%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%5D "/Users/anek/PersonalProjects/llm-ansible-playbook/tasks/setup_nvidia_container_toolkit.yaml")

## 使用方法

1. リポジトリをクローンします:
    ```sh
    git clone <repository-url>
    cd <repository-directory>
    ```

2. [`inventory.yaml`](command:_github.copilot.openRelativePath?%5B%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2FUsers%2Fanek%2FPersonalProjects%2Fllm-ansible-playbook%2Finventory.yaml%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%5D "/Users/anek/PersonalProjects/llm-ansible-playbook/inventory.yaml")ファイルを更新し、サーバーの詳細を入力します。
    SSH接続可能なサーバーのホストを指定してください。

3. プレイブックを実行します:
    ```sh
    ansible-playbook -i inventory.yaml linux_llm_server_playbook.yaml
    ```

## 設定

### [`ansible.cfg`](command:_github.copilot.openRelativePath?%5B%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2FUsers%2Fanek%2FPersonalProjects%2Fllm-ansible-playbook%2Fansible.cfg%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%5D "/Users/anek/PersonalProjects/llm-ansible-playbook/ansible.cfg")

このファイルには、Ansibleの設定が含まれています。

### [`inventory.yaml`](command:_github.copilot.openRelativePath?%5B%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2FUsers%2Fanek%2FPersonalProjects%2Fllm-ansible-playbook%2Finventory.yaml%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%5D "/Users/anek/PersonalProjects/llm-ansible-playbook/inventory.yaml")

このファイルには、管理するサーバーのインベントリが含まれています。

### [`.vscode/settings.json`](command:_github.copilot.openRelativePath?%5B%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2FUsers%2Fanek%2FPersonalProjects%2Fllm-ansible-playbook%2F.vscode%2Fsettings.json%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%5D "/Users/anek/PersonalProjects/llm-ansible-playbook/.vscode/settings.json")

このファイルには、Visual Studio Codeの設定が含まれています。

## ライセンス

このプロジェクトはMITライセンスの下でライセンスされています。詳細はLICENSEファイルを参照してください。

## コントリビューション

コントリビューションは歓迎します！変更がある場合は、issueを開くか、プルリクエストを提出してください。
