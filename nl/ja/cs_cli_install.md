---

copyright:
  years: 2014, 2018
lastupdated: "2018-01-29"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# CLI と API のセットアップ
{: #cs_cli_install}

{{site.data.keyword.containershort_notm}} CLI または API を使用して、Kubernetes クラスターを作成して管理できます。
{:shortdesc}

<br />


## CLI のインストール
{: #cs_cli_install_steps}

{{site.data.keyword.containershort_notm}} での Kubernetes クラスターの作成と管理、およびクラスターへのコンテナー化アプリのデプロイに必要な CLI をインストールします。
{:shortdesc}

このタスクには、次の CLI とプラグインをインストールするための情報が含まれています。

-   {{site.data.keyword.Bluemix_notm}} CLI バージョン 0.5.0 以降
-   {{site.data.keyword.containershort_notm}} プラグイン
-   Kubernetes CLI バージョン 1.8.6 以降
-   オプション: {{site.data.keyword.registryshort_notm}} プラグイン
-   オプション: Docker バージョン 1.9 以降

<br>
CLI をインストールするには、以下のことを行います。

1.  {{site.data.keyword.containershort_notm}} プラグインの前提条件として、[{{site.data.keyword.Bluemix_notm}} CLI ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://clis.ng.bluemix.net/ui/home.html) をインストールします。 {{site.data.keyword.Bluemix_notm}} CLI を使用してコマンドを実行するための接頭部は、`bx` です。

2.  {{site.data.keyword.Bluemix_notm}} CLI にログインします。 プロンプトが出されたら、{{site.data.keyword.Bluemix_notm}} 資格情報を入力します。

    ```
    bx login
    ```
    {: pre}

    **注:** フェデレーテッド ID がある場合は、`bx login --sso` を使用して、{{site.data.keyword.Bluemix_notm}} CLI にログインします。 ユーザー名を入力し、CLI 出力に示された URL を使用して、ワンタイム・パスコードを取得してください。 `--sso` なしではログインに失敗し、`--sso` オプションを指定すると成功する場合、フェデレーテッド ID があることがわかります。

3.  Kubernetes クラスターを作成し、ワーカー・ノードを管理するには、{{site.data.keyword.containershort_notm}} プラグインをインストールします。 {{site.data.keyword.containershort_notm}} プラグインを使用してコマンドを実行するための接頭部は、`bx cs` です。

    ```
    bx plugin install container-service -r Bluemix
    ```
    {: pre}

    プラグインが正常にインストールされていることを検証するには、以下のコマンドを実行します。

    ```
    bx plugin list
    ```
    {: pre}

    {{site.data.keyword.containershort_notm}} プラグインは container-service として結果に表示されます。

4.  Kubernetes ダッシュボードのローカル・バージョンを表示して、アプリをクラスター内にデプロイするには、[Kubernetes CLI をインストールします![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://kubernetes.io/docs/tasks/tools/install-kubectl/)。 Kubernetes CLI を使用してコマンドを実行するための接頭部は、`kubectl` です。

    1.  機能の完全な互換性を確保するには、使用する予定の Kubernetes クラスター・バージョンと一致する Kubernetes CLI バージョンをダウンロードします。 現在の {{site.data.keyword.containershort_notm}} のデフォルト Kubernetes バージョンは 1.8.6 です。

        OS X:   [https://storage.googleapis.com/kubernetes-release/release/v1.7.4/bin/darwin/amd64/kubectl ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://storage.googleapis.com/kubernetes-release/release/v1.7.4/bin/darwin/amd64/kubectl)

        Linux:   [https://storage.googleapis.com/kubernetes-release/release/v1.7.4/bin/linux/amd64/kubectl ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://storage.googleapis.com/kubernetes-release/release/v1.7.4/bin/linux/amd64/kubectl)

        Windows:   [https://storage.googleapis.com/kubernetes-release/release/v1.7.4/bin/windows/amd64/kubectl.exe ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://storage.googleapis.com/kubernetes-release/release/v1.7.4/bin/windows/amd64/kubectl.exe)

        **ヒント:** Windows を使用している場合、Kubernetes CLI を {{site.data.keyword.Bluemix_notm}} CLI と同じディレクトリーにインストールします。 このようにセットアップすると、後でコマンドを実行するとき、ファイル・パスの変更を行う手間がいくらか少なくなります。

    2.  OSX と Linux のユーザーは、以下の手順を実行してください。
        1.  実行可能ファイルを `/usr/local/bin` ディレクトリーに移動します。

            ```
            mv /<path_to_file>/kubectl /usr/local/bin/kubectl
            ```
            {: pre}

        2.  `/usr/local/bin` が `PATH` システム変数にリストされていることを確認します。 `PATH` 変数には、オペレーティング・システムが実行可能ファイルを見つけることのできるすべてのディレクトリーが含まれています。 `PATH` 変数にリストされた複数のディレクトリーには、それぞれ異なる目的があります。 `/usr/local/bin` は実行可能ファイルを保管するために使用されますが、保管対象となるのは、オペレーティング・システムの一部ではなく、システム管理者によって手動でインストールされたソフトウェアです。

            ```
            echo $PATH
            ```
            {: pre}

            CLI 出力例:

            ```
            /usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
            ```
            {: screen}

        3.  ファイルを実行可能にします。

            ```
            chmod +x /usr/local/bin/kubectl
            ```
            {: pre}

5.  プライベート・イメージ・リポジトリーを管理するには、{{site.data.keyword.registryshort_notm}} プラグインをインストールします。 このプラグインを使用して、IBM がホストするマルチテナントで可用性が高く拡張可能なプライベート・イメージ・レジストリー内に独自の名前空間をセットアップし、Docker イメージを保管して他のユーザーと共有します。 クラスターにコンテナーをデプロイするためには、Docker イメージが必要です。 レジストリー・コマンドを実行するための接頭部は、`bx cr` です。

    ```
    bx plugin install container-registry -r Bluemix
    ```
    {: pre}

    プラグインが正常にインストールされていることを検証するには、以下のコマンドを実行します。

    ```
    bx plugin list
    ```
    {: pre}

    プラグインは container-registry として結果に表示されます。

6.  ローカルにイメージを作成して、それらをレジストリー名前空間にプッシュするには、[Docker をインストールします![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.docker.com/community-edition#/download)。 Windows 8 以前を使用している場合、代わりに [Docker Toolbox ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.docker.com/toolbox/toolbox_install_windows/) をインストールしてください。 Docker CLI は、イメージ内にアプリを構築するために使用されます。 Docker CLI を使用してコマンドを実行するための接頭部は、`docker` です。

次に、[{{site.data.keyword.containershort_notm}} における CLI からの Kubernetes クラスターの作成](cs_clusters.html#clusters_cli)を開始します。

以下の CLI に関する参照情報については、それらのツールの資料を参照してください。

-   [`bx` コマンド](/docs/cli/reference/bluemix_cli/bx_cli.html)
-   [`bx cs` コマンド](cs_cli_reference.html#cs_cli_reference)
-   [`kubectl` コマンド ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)
-   [`bx cr` コマンド](/docs/cli/plugins/registry/index.html)

<br />


## `kubectl` を実行するように CLI を構成する
{: #cs_cli_configure}

Kubernetes CLI に用意されているコマンドを使用して、{{site.data.keyword.Bluemix_notm}} のクラスターを管理することができます。 Kubernetes 1.8.6 内で使用できるすべての `kubectl` コマンドは、{{site.data.keyword.Bluemix_notm}} 内のクラスターに対して使用することができます。 クラスターを作成したら、環境変数を使用してローカル CLI のコンテキストをそのクラスターに設定します。 その後、Kubernetes のさまざまな `kubectl` コマンドを実行して、{{site.data.keyword.Bluemix_notm}} のクラスターを操作することができます。
{:shortdesc}

`kubectl` コマンドを実行する前に、[必要な CLI をインストール](#cs_cli_install)して、[クラスターを作成](cs_clusters.html#clusters_cli)します。

1.  {{site.data.keyword.Bluemix_notm}} CLI にログインします。 プロンプトが出されたら、{{site.data.keyword.Bluemix_notm}} 資格情報を入力します。 {{site.data.keyword.Bluemix_notm}} 地域を指定するには、[API エンドポイントを含めます](cs_regions.html#bluemix_regions)。

      ```
      bx login
      ```
      {: pre}

      **注:** フェデレーテッド ID がある場合は、`bx login --sso` を使用して、{{site.data.keyword.Bluemix_notm}} CLI にログインします。 ユーザー名を入力し、CLI 出力に示された URL を使用して、ワンタイム・パスコードを取得してください。 `--sso` なしではログインに失敗し、`--sso` オプションを指定すると成功する場合、フェデレーテッド ID があることがわかります。

  2.  {{site.data.keyword.Bluemix_notm}} アカウントを選択します。 複数の {{site.data.keyword.Bluemix_notm}} の組織が割り当てられている場合は、対象クラスターが作成されている組織を選択してください。 クラスターは組織に固有のものですが、{{site.data.keyword.Bluemix_notm}} スペースからは独立しています。 そのため、スペースを選択する必要はありません。

  3.  前に選択した {{site.data.keyword.Bluemix_notm}} 地域以外の地域で Kubernetes クラスターの作成とアクセスを行う場合は、`bx cs region-set` を実行します。

  4.  クラスターの名前を取得するために、アカウントに含まれているすべてのクラスターのリストを出力します。

      ```
      bx cs clusters
      ```
      {: pre}

  5.  作成したクラスターを、このセッションのコンテキストとして設定します。 次の構成手順は、クラスターの操作時に毎回行ってください。
      1.  環境変数を設定して Kubernetes 構成ファイルをダウンロードするためのコマンドを取得します。

          ```
          bx cs cluster-config <cluster_name_or_id>
          ```
          {: pre}

          構成ファイルをダウンロードした後に、そのローカルの Kubernetes 構成ファイルのパスを環境変数として設定するために使用できるコマンドが表示されます。

          例:

          ```
          export KUBECONFIG=/Users/<user_name>/.bluemix/plugins/container-service/clusters/<cluster_name>/kube-config-prod-dal10-<cluster_name>.yml
          ```
          {: screen}

      2.  `KUBECONFIG` 環境変数を設定するためのコマンドとしてターミナルに表示されたものを、コピーして貼り付けます。
      3.  `KUBECONFIG` 環境変数が適切に設定されたことを確認します。

          例:

          ```
          echo $KUBECONFIG
          ```
          {: pre}

          出力:
          ```
          /Users/<user_name>/.bluemix/plugins/container-service/clusters/<cluster_name>/kube-config-prod-dal10-<cluster_name>.yml
          ```
          {: screen}

  6.  Kubernetes CLI サーバーのバージョンを調べて、ご使用のクラスターで `kubectl` コマンドが正常に実行することを確認します。

      ```
      kubectl version  --short
      ```
      {: pre}

      出力例:

      ```
      Client Version: v1.8.6
      Server Version: v1.8.6
      ```
      {: screen}

これで、`kubectl` のコマンドを実行して、{{site.data.keyword.Bluemix_notm}} のクラスターを管理できるようになりました。 すべてのコマンドのリストについては、[Kubernetes の資料![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) を参照してください。

**ヒント:** Windows を使用している場合、Kubernetes CLI が {{site.data.keyword.Bluemix_notm}} CLI と同じディレクトリーにインストールされていなければ、`kubectl` コマンドを正常に実行するために、Kubernetes CLI のインストール先パスにディレクトリーを変更する必要があります。


<br />


## CLI の更新
{: #cs_cli_upgrade}

新しいフィーチャーを使用するためには、CLI を定期的に更新する必要があります。
{:shortdesc}

このタスクには、これらの CLI を更新するための情報が含まれています。

-   {{site.data.keyword.Bluemix_notm}} CLI バージョン 0.5.0 以降
-   {{site.data.keyword.containershort_notm}} プラグイン
-   Kubernetes CLI バージョン 1.8.6 以降
-   {{site.data.keyword.registryshort_notm}} プラグイン
-   Docker バージョン 1.9. 以降

<br>
CLI を更新するには、以下のようにします。

1.  {{site.data.keyword.Bluemix_notm}} CLI を更新します。 [最新バージョン ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://clis.ng.bluemix.net/ui/home.html) をダウンロードし、インストーラーを実行します。

2. {{site.data.keyword.Bluemix_notm}} CLI にログインします。 プロンプトが出されたら、{{site.data.keyword.Bluemix_notm}} 資格情報を入力します。 {{site.data.keyword.Bluemix_notm}} 地域を指定するには、[API エンドポイントを含めます](cs_regions.html#bluemix_regions)。

    ```
    bx login
    ```
    {: pre}

     **注:** フェデレーテッド ID がある場合は、`bx login --sso` を使用して、{{site.data.keyword.Bluemix_notm}} CLI にログインします。 ユーザー名を入力し、CLI 出力に示された URL を使用して、ワンタイム・パスコードを取得してください。 `--sso` なしではログインに失敗し、`--sso` オプションを指定すると成功する場合、フェデレーテッド ID があることがわかります。

3.  {{site.data.keyword.containershort_notm}} プラグインを更新します。
    1.  {{site.data.keyword.Bluemix_notm}} プラグイン・リポジトリーからアップデートをインストールします。

        ```
        bx plugin update container-service -r Bluemix
        ```
        {: pre}

    2.  以下のコマンドを実行し、インストールされたプラグインのリストを確認することで、プラグインのインストールを検証します。

        ```
        bx plugin list
        ```
        {: pre}

        {{site.data.keyword.containershort_notm}} プラグインは container-service として結果に表示されます。

    3.  CLI を初期化します。

        ```
        bx cs init
        ```
        {: pre}

4.  Kubernetes CLI を更新します。
    1.  使用する予定の Kubernetes クラスター・バージョンと一致する Kubernetes CLI バージョンに更新します。 現在の {{site.data.keyword.containershort_notm}} のデフォルト Kubernetes バージョンは 1.8.6 です。

        OS X:   [https://storage.googleapis.com/kubernetes-release/release/v1.7.4/bin/darwin/amd64/kubectl ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://storage.googleapis.com/kubernetes-release/release/v1.7.4/bin/darwin/amd64/kubectl)

        Linux:   [https://storage.googleapis.com/kubernetes-release/release/v1.7.4/bin/linux/amd64/kubectl ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://storage.googleapis.com/kubernetes-release/release/v1.7.4/bin/linux/amd64/kubectl)

        Windows:   [https://storage.googleapis.com/kubernetes-release/release/v1.7.4/bin/windows/amd64/kubectl.exe ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://storage.googleapis.com/kubernetes-release/release/v1.7.4/bin/windows/amd64/kubectl.exe)

        **ヒント:** Windows を使用している場合、Kubernetes CLI を {{site.data.keyword.Bluemix_notm}} CLI と同じディレクトリーにインストールします。 このようにセットアップすると、後でコマンドを実行するとき、ファイル・パスの変更を行う手間がいくらか少なくなります。

    2.  OSX と Linux のユーザーは、以下の手順を実行してください。
        1.  実行可能ファイルを `/usr/local/bin` ディレクトリーに移動します。

            ```
            mv /<path_to_file>/kubectl /usr/local/bin/kubectl
            ```
            {: pre}

        2.  `/usr/local/bin` が `PATH` システム変数にリストされていることを確認します。 `PATH` 変数には、オペレーティング・システムが実行可能ファイルを見つけることのできるすべてのディレクトリーが含まれています。 `PATH` 変数にリストされた複数のディレクトリーには、それぞれ異なる目的があります。 `/usr/local/bin` は実行可能ファイルを保管するために使用されますが、保管対象となるのは、オペレーティング・システムの一部ではなく、システム管理者によって手動でインストールされたソフトウェアです。

            ```
            echo $PATH
            ```
            {: pre}

            CLI 出力例:

            ```
            /usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
            ```
            {: screen}

        3.  ファイルを実行可能にします。

            ```
            chmod +x /usr/local/bin/kubectl
            ```
            {: pre}

5.  {{site.data.keyword.registryshort_notm}} プラグインを更新します。
    1.  {{site.data.keyword.Bluemix_notm}} プラグイン・リポジトリーからアップデートをインストールします。

        ```
        bx plugin update container-registry -r Bluemix
        ```
        {: pre}

    2.  以下のコマンドを実行し、インストールされたプラグインのリストを確認することで、プラグインのインストールを検証します。

        ```
        bx plugin list
        ```
        {: pre}

        レジストリー・プラグインが container-registry として結果に表示されます。

6.  Docker を更新します。
    -   Docker Community Edition を使用している場合は、Docker を開始し、**Docker** アイコンをクリックし、**「Check for updatess (更新のチェック)」**をクリックします。
    -   Docker Toolbox を使用する場合は、[最新バージョン ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.docker.com/toolbox/toolbox_install_windows/) をダウンロードし、インストーラーを実行します。

<br />


## CLI のアンインストール
{: #cs_cli_uninstall}

不要になった CLI はアンインストールできます。
{:shortdesc}

このタスクには、次の CLI を削除するための情報が含まれています。


-   {{site.data.keyword.containershort_notm}} プラグイン
-   Kubernetes CLI バージョン 1.8.6 以降
-   {{site.data.keyword.registryshort_notm}} プラグイン
-   Docker バージョン 1.9. 以降

<br>
CLI をアンインストールするには、以下のようにします。

1.  {{site.data.keyword.containershort_notm}} プラグインをアンインストールします。

    ```
    bx plugin uninstall container-service
    ```
    {: pre}

2.  {{site.data.keyword.registryshort_notm}} プラグインをアンインストールします。

    ```
    bx plugin uninstall container-registry
    ```
    {: pre}

3.  次のコマンドを実行し、インストールされているプラグインのリストを確認することで、プラグインがアンインストールされたことを検証します。

    ```
    bx plugin list
    ```
    {: pre}

    container-service プラグインと container-registry プラグインは結果に表示されません。





6.  Docker をアンインストールします。 Docker をアンインストールする手順は、ご使用のオペレーティング・システムによって異なります。

    - [OSX ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.docker.com/docker-for-mac/#uninstall-or-reset)
    - [Linux ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/#uninstall-docker-ce)
    - [Windows ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.docker.com/toolbox/toolbox_install_windows/#how-to-uninstall-toolbox)

<br />


## API を使用したクラスターのデプロイメントの自動化
{: #cs_api}

{{site.data.keyword.containershort_notm}} API を使用して、Kubernetes クラスターの作成、デプロイメント、管理を自動化できます。
{:shortdesc}

{{site.data.keyword.containershort_notm}} API にはヘッダー情報が必要です。これは、API 要求に指定する必要があります。また、使用する API に応じて異なる場合があります。 使用する API に必要なヘッダー情報を調べるには、[{{site.data.keyword.containershort_notm}} API の資料 ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://us-south.containers.bluemix.net/swagger-api) を参照してください。

**注:** {{site.data.keyword.containershort_notm}} で認証するには、{{site.data.keyword.Bluemix_notm}} 資格情報を使用して生成された IAM (ID およびアクセス管理) トークンを提供する必要があります。このトークンには、クラスターの作成に使用された {{site.data.keyword.Bluemix_notm}} アカウント ID が入っています。 {{site.data.keyword.Bluemix_notm}} での認証方法に応じて、IAM トークンの作成を自動化するための次のオプションから選択できます。

<table>
<thead>
<th>{{site.data.keyword.Bluemix_notm}} ID</th>
<th>選択オプション</th>
</thead>
<tbody>
<tr>
<td>非フェデレーテッド ID</td>
<td><ul><li><strong>{{site.data.keyword.Bluemix_notm}} ユーザー名とパスワード:</strong> このトピックに記載されたステップに従って、IAM アクセス・トークンの作成を完全に自動化できます。</li>
<li><strong>{{site.data.keyword.Bluemix_notm}} API キーの生成:</strong> {{site.data.keyword.Bluemix_notm}} ユーザー名とパスワードを使用する代わりに、<a href="../iam/apikeys.html#manapikey" target="_blank">{{site.data.keyword.Bluemix_notm}} API キー</a>を使用できます。{{site.data.keyword.Bluemix_notm}} API キーは、その生成対象の {{site.data.keyword.Bluemix_notm}} アカウントに依存しています。 {{site.data.keyword.Bluemix_notm}} API キーと別のアカウント ID を同一の IAM トークンで結合することはできません。 {{site.data.keyword.Bluemix_notm}} API キーの基となっているアカウント以外のアカウントを使用して作成されたクラスターにアクセスするには、そのアカウントにログインして新しい API キーを生成する必要があります。 </li></ul></tr>
<tr>
<td>フェデレーテッド ID</td>
<td><ul><li><strong>{{site.data.keyword.Bluemix_notm}} API キーの生成:</strong> <a href="../iam/apikeys.html#manapikey" target="_blank">{{site.data.keyword.Bluemix_notm}} API キー</a>は、その生成対象の {{site.data.keyword.Bluemix_notm}} アカウントに依存しています。 {{site.data.keyword.Bluemix_notm}} API キーと別のアカウント ID を同一の IAM トークンで結合することはできません。 {{site.data.keyword.Bluemix_notm}} API キーの基となっているアカウント以外のアカウントを使用して作成されたクラスターにアクセスするには、そのアカウントにログインして新しい API キーを生成する必要があります。 </li><li><strong>ワンタイム・パスコードの使用: </strong>ワンタイム・パスコードを使用して {{site.data.keyword.Bluemix_notm}} で認証する場合、IAM トークンの作成を完全に自動化することはできません。ワンタイム・パスコードを取得するには、Web ブラウザーとの手動対話が必要になるためです。 IAM トークンの作成を完全に自動化するには、代わりに {{site.data.keyword.Bluemix_notm}} API キーを作成する必要があります。 </ul></td>
</tr>
</tbody>
</table>

1.  IAM (ID およびアクセス管理) アクセス・トークンを作成します。 要求に含まれる本文情報は、使用する {{site.data.keyword.Bluemix_notm}} 認証方式によって異なります。 以下の値を置き換えます。
  - _&lt;my_username&gt;_: {{site.data.keyword.Bluemix_notm}} ユーザー名。
  - _&lt;my_password&gt;_: {{site.data.keyword.Bluemix_notm}} パスワード。
  - _&lt;my_api_key&gt;_: {{site.data.keyword.Bluemix_notm}} API キー。
  - _&lt;my_passcode&gt;_: {{site.data.keyword.Bluemix_notm}} ワンタイム・パスコード。 `bx login --sso` を実行し、CLI 出力の説明に従って、Web ブラウザーを使用してワンタイム・パスコードを取得します。

    ```
    POST https://iam.<region>.bluemix.net/oidc/token
    ```
    {: codeblock}

    例:
    ```
    POST https://iam.ng.bluemix.net/oidc/token
    ```
    {: pre}

    {{site.data.keyword.Bluemix_notm}} 地域を指定するには、[API エンドポイントで使用される地域の略語を確認してください](cs_regions.html#bluemix_regions)。

    <table summary-"Input parameters to get tokens">
    <thead>
        <th>入力パラメーター</th>
        <th>値</th>
    </thead>
    <tbody>
    <tr>
    <td>ヘッダー</td>
    <td><ul><li>Content-Type:application/x-www-form-urlencoded</li> <li>Authorization: Basic Yng6Yng=<p><b>注</b>: この Yng6Yng= は、ユーザー名 **bx** とパスワード **bx** の URL エンコードされた許可です。</p></li></ul>
    </td>
    </tr>
    <tr>
    <td>{{site.data.keyword.Bluemix_notm}} ユーザー名とパスワードの本文</td>
    <td><ul><li>grant_type: password</li>
    <li>response_type: cloud_iam、uaa</li>
    <li>username: <em>&lt;my_username&gt;</em></li>
    <li>password: <em>&lt;my_password&gt;</em></li>
    <li>uaa_client_id: cf</li>
    <li>uaa_client_secret:</li></ul>
    <p><b>注</b>: uaa_client_secret キーは値を指定せずに追加します。</p></td>
    </tr>
    <tr>
    <td>{{site.data.keyword.Bluemix_notm}} API キーの本文</td>
    <td><ul><li>grant_type: urn:ibm:params:oauth:grant-type:apikey</li>
    <li>response_type: cloud_iam、uaa</li>
    <li>apikey: <em>&lt;my_api_key&gt;</em></li>
    <li>uaa_client_id: cf</li>
    <li>uaa_client_secret:</li></ul>
    <p><b>注</b>: uaa_client_secret キーは値を指定せずに追加します。</p></td>
    </tr>
    <tr>
    <td>{{site.data.keyword.Bluemix_notm}} ワンタイム・パスコードの本文</td>
    <td><ul><li>grant_type: urn:ibm:params:oauth:grant-type:passcode</li>
    <li>response_type: cloud_iam、uaa</li>
    <li>passcode: <em>&lt;my_passcode&gt;</em></li>
    <li>uaa_client_id: cf</li>
    <li>uaa_client_secret:</li></ul>
    <p><b>注</b>: uaa_client_secret キーは値を指定せずに追加します。</p></td>
    </tr>
    </tbody>
    </table>

    API 出力例:

    ```
    {
    "access_token": "<iam_token>",
    "refresh_token": "<iam_refresh_token>",
    "uaa_token": "<uaa_token>",
    "uaa_refresh_token": "<uaa_refresh_token>",
    "token_type": "Bearer",
    "expires_in": 3600,
    "expiration": 1493747503
    }

    ```
    {: screen}

    IAM トークンは、API 出力の **access_token** フィールドで確認できます。 次のステップでさらにヘッダー情報を取得するため、IAM トークンをメモしておきます。

2.  クラスターの作成に使用した {{site.data.keyword.Bluemix_notm}} アカウントの ID を取得します。 _&lt;iam_token&gt;_ を、前の手順で取得した IAM トークンに置き換えてください。

    ```
    GET https://accountmanagement.<region>.bluemix.net/v1/accounts
    ```
    {: codeblock}

    <table summary="{{site.data.keyword.Bluemix_notm}} アカウント ID を取得するための入力パラメーター">
    <thead>
  	<th>入力パラメーター</th>
  	<th>値</th>
    </thead>
    <tbody>
  	<tr>
  		<td>ヘッダー</td>
  		<td><ul><li>Content-Type: application/json</li>
      <li>Authorization: bearer &lt;iam_token&gt;</li>
      <li>Accept: application/json</li></ul></td>
  	</tr>
    </tbody>
    </table>

    API 出力例:

    ```
    {
      "total_results": 3,
      "total_pages": 1,
      "prev_url": null,
      "next_url": null,
      "resources":
        {
          "metadata": {
            "guid": "<my_account_id>",
            "url": "/v1/accounts/<my_account_id>",
            "created_at": "2016-01-07T18:55:09.726Z",
            "updated_at": "2017-04-28T23:46:03.739Z",
            "origin": "BSS"
    ...
    ```
    {: screen}

    API 出力の **resources/metadata/guid** フィールドに、{{site.data.keyword.Bluemix_notm}} アカウントの ID があります。

3.  {{site.data.keyword.Bluemix_notm}} 資格情報と、クラスターの作成に使用したアカウント ID の両方が含まれる新しい IAM トークンを生成します。 _&lt;my_account_id&gt;_ を、前のステップで取得した {{site.data.keyword.Bluemix_notm}} アカウントの ID に置き換えます。

    **注:** {{site.data.keyword.Bluemix_notm}} API キーを使用している場合、API キーの作成対象となった {{site.data.keyword.Bluemix_notm}} アカウント ID を使用する必要があります。 他のアカウントのクラスターにアクセスするには、そのアカウントにログインし、このアカウントに基づく {{site.data.keyword.Bluemix_notm}} API キーを作成します。

    ```
    POST https://iam.<region>.bluemix.net/oidc/token
    ```
    {: codeblock}

    例:
    ```
    POST https://iam.ng.bluemix.net/oidc/token
    ```
    {: pre}

    {{site.data.keyword.Bluemix_notm}} 地域を指定するには、[API エンドポイントで使用される地域の略語を確認してください](cs_regions.html#bluemix_regions)。

    <table summary-"Input parameters to get tokens">
    <thead>
        <th>入力パラメーター</th>
        <th>値</th>
    </thead>
    <tbody>
    <tr>
    <td>ヘッダー</td>
    <td><ul><li>Content-Type:application/x-www-form-urlencoded</li> <li>Authorization: Basic Yng6Yng=<p><b>注</b>: この Yng6Yng= は、ユーザー名 **bx** とパスワード **bx** の URL エンコードされた許可です。</p></li></ul>
    </td>
    </tr>
    <tr>
    <td>{{site.data.keyword.Bluemix_notm}} ユーザー名とパスワードの本文</td>
    <td><ul><li>grant_type: password</li>
    <li>response_type: cloud_iam、uaa</li>
    <li>username: <em>&lt;my_username&gt;</em></li>
    <li>password: <em>&lt;my_password&gt;</em></li>
    <li>uaa_client_id: cf</li>
    <li>uaa_client_secret:</li>
    <li>bss_account: <em>&lt;my_account_id&gt;</em></li></ul>
    <p><b>注</b>: uaa_client_secret キーは値を指定せずに追加します。</p></td>
    </tr>
    <tr>
    <td>{{site.data.keyword.Bluemix_notm}} API キーの本文</td>
    <td><ul><li>grant_type: urn:ibm:params:oauth:grant-type:apikey</li>
    <li>response_type: cloud_iam、uaa</li>
    <li>apikey: <em>&lt;my_api_key&gt;</em></li>
    <li>uaa_client_id: cf</li>
    <li>uaa_client_secret:</li>
    <li>bss_account: <em>&lt;my_account_id&gt;</em></li></ul>
    <p><b>注</b>: uaa_client_secret キーは値を指定せずに追加します。</p></td>
    </tr>
    <tr>
    <td>{{site.data.keyword.Bluemix_notm}} ワンタイム・パスコードの本文</td>
    <td><ul><li>grant_type: urn:ibm:params:oauth:grant-type:passcode</li>
    <li>response_type: cloud_iam、uaa</li>
    <li>passcode: <em>&lt;my_passcode&gt;</em></li>
    <li>uaa_client_id: cf</li>
    <li>uaa_client_secret:</li>
    <li>bss_account: <em>&lt;my_account_id&gt;</em></li></ul>
    <p><b>注<b>: uaa_client_secret キーは値を指定せずに追加します。</p></td>
    </tr>
    </tbody>
    </table>

    API 出力例:

    ```
    {
      "access_token": "<iam_token>",
    "refresh_token": "<iam_refresh_token>",
    "uaa_token": "<uaa_token>",
    "uaa_refresh_token": "<uaa_refresh_token>",
    "token_type": "Bearer",
    "expires_in": 3600,
    "expiration": 1493747503
    }

    ```
    {: screen}

    **access_token** に IAM トークンがあり、**refresh_token** に IAM リフレッシュ・トークンがあります。

4.  アカウント内の Kubernetes クラスターをすべてリストします。 前述のステップで取得した情報を使用して、ヘッダー情報をビルドします。

        ```
        GET https://containers.bluemix.net/v1/clusters
        ```
        {: codeblock}

        <table summary="API を使用するための入力パラメーター">
        <thead>
        <th>入力パラメーター</th>
        <th>値</th>
        </thead>
        <tbody>
        <tr>
        <td>ヘッダー</td>
        <td><ul><li>Authorization: bearer <em>&lt;iam_token&gt;</em></li>
        <li>X-Auth-Refresh-Token: <em>&lt;refresh_token&gt;</em></li></ul></td>
        </tr>
        </tbody>
        </table>

5.  [{{site.data.keyword.containershort_notm}} API の資料 ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://containers.bluemix.net/swagger-api) を参照して、サポートされている API のリストを確認します。

<br />


## IAM アクセス・トークンのリフレッシュ
{: #cs_api_refresh}

API から発行されるすべての IAM (ID およびアクセス管理) アクセス・トークンの有効期間は 1 時間です。 {{site.data.keyword.containershort_notm}} API へのアクセスを確保するには、アクセス・トークンを定期的にリフレッシュする必要があります。
{:shortdesc}

始める前に、新しいアクセス・トークンを要求するために使用できる IAM リフレッシュ・トークンを用意してください。 リフレッシュ・トークンがない場合は、[{{site.data.keyword.containershort_notm}} API によるクラスターの作成と管理のプロセスの自動化](#cs_api)を参照してアクセス・トークンを取得してください。

IAM トークンをリフレッシュするには、以下の手順を実行します。

1.  新しい IAM アクセス・トークンを生成します。 _&lt;iam_refresh_token&gt;_ を、{{site.data.keyword.Bluemix_notm}} での認証時に受け取った IAM リフレッシュ・トークンに置き換えます。

    ```
    POST https://iam.bluemix.net/identity/token
    ```
    {: codeblock}

    <table summary="新しい IAM トークンのための入力パラメーター">
    <thead>
    <th>入力パラメーター</th>
    <th>値</th>
    </thead>
    <tbody>
    <tr>
    <td>ヘッダー</td>
    <td><ul><li>Content-Type: application/x-www-form-urlencoded</li>
    <li>Authorization: Basic Yng6Yng=<p><b>注</b>: この Yng6Yng= は、ユーザー名 **bx** とパスワード **bx** の URL エンコードされた許可です。</p></li></ul></td>
    </tr>
    <tr>
    <td>本文</td>
    <td><ul><li>grant_type: refresh_token</li>
    <li>response_type: cloud_iam、uaa</li>
    <li>refresh_token: <em>&lt;iam_refresh_token&gt;</em></li>
    <li>uaa_client_id: cf</li>
    <li>uaa_client_secret:</li>
    <li>bss_account: <em>&lt;account_id&gt;</em></li></ul><p><b>注</b>: uaa_client_secret キーは値を指定せずに追加します。</p></td>
    </tr>
    </tbody>
    </table>

    API 出力例:

    ```
    {
      "access_token": "<iam_token>",
    "refresh_token": "<iam_refresh_token>",
    "uaa_token": "<uaa_token>",
    "uaa_refresh_token": "<uaa_refresh_token>",
    "token_type": "Bearer",
    "expires_in": 3600,
    "expiration": 1493747503
    }

    ```
    {: screen}

    API 出力の **access_token** フィールドに新しい IAM トークンがあり、**refresh_token** フィールドに IAM リフレッシュ・トークンがあります。

2.  前の手順のトークンを使用して、[{{site.data.keyword.containershort_notm}} API の資料 ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://us-south.containers.bluemix.net/swagger-api) の作業を進めます。
