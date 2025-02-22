# Introduction

大規模システム開発において polyrepo アーキテクチャを採用する場合、関連リポジトリの依存関係管理が重要な課題となる。本報告では GitHub Organization(仮)管理下にある複数リポジトリを効率的に扱うための自動化手法を、サブモジュール構成の観点から実装する。

# What is submodule

Git サブモジュールは、親リポジトリ内に子リポジトリの参照情報を保持するメタデータ管理システムである。.gitmodules ファイルにリポジトリ URL とローカルパス、コミットハッシュを記録することで、バージョン固定を実現する。

# How to use

ここでは Git サブモジュールの使い方について例を用いて説明する。

まず、親のレポジトリをクローンする。

```bash
git clone https://github.com/yukihito-jokyu/submodule_main.git
```

## add submodule

`cd`コマンドで`submodule_main`ディレクトリに移動し、以下のコマンドでサブモジュールを追加する。

```bash
git submodule add https://github.com/yukihito-jokyu/submodule_a.git submodule/submodule_a
```

```bash
git submodule add https://github.com/yukihito-jokyu/submodule_b.git submodule/submodule_b
```

## pull

サブモジュールのレポジトリの main ブランチに変更があり、同期したいときは以下のコマンドを実行する。

```bash
git submodule update --remote --merge
```

`--remote` → サブモジュールのリモートリポジトリを見に行き、最新の main ブランチを取得
`--merge` → 既存の変更と統合（fast-forward できる場合は fast-forward）

## clone

他のユーザーがクローンする場合、単純にクローンするだけではサブモジュールの情報は取得できないため、以下のような工夫を設ける。

```bash
git clone --recurse-submodules https://github.com/yukihito-jokyu/submodule_main.git
```
