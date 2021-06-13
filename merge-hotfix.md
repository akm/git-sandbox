# hotfixのマージ

## 概要

hotfixは、リリースしたブランチで深刻な不具合が見つかり、とにかく急いで修正しなければならないような場合に作ります。
その際、開発作業が進められている場合、リリースしたブランチとは別の開発用のブランチにはまだリリースするべきでない機能が入っていることが多々あります。
そのような場合ホットフィックスをリリースしたブランチにマージして、サイドリリースした後、ホットフィックスを開発用のブランチに反映させますが、
いくつかの方法があるので検討します。

## 使用するブランチ名

ブランチ名 | 説明  | git-flowのでの名前 | 作成元 | マージ先
--------|-----------------|--------|---------|---------
develop  | 開発のためのブランチ | develop | - | -
main | 製品をビルドするためのブランチ | master | develop | -
topic | リリースに含めるための機能追加・バグ修正のためのブランチ | feature | develop | develop |
release | リリースするためのブランチ。developの内容をmainに反映させるためのブランチ | release | develop | main
hotfix | リリース後に判明した緊急度の高い不具合を修正するブランチ | hotfix | main | main
backport-main | mainブランチの変更をdevelopに反映するためのブランチ | - | main | develop
backport-hotfix | hotfixブランチの変更をdevelopに反映するためのブランチ | - | hotfix | develop

- [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/) (git-flowがサポートするモデル)
    - [日本語訳](http://keijinsonyaban.blogspot.com/2010/10/a-successful-git-branching-model.html)
- [GitHub Flow](http://scottchacon.com/2011/08/31/github-flow.html)
    - [日本語訳](https://gist.github.com/Gab-km/3705015)

## このリポジトリでの接頭辞

このリポジトリでは同じ状況を、複数の方法で解決させる例を表すために、ブランチに接頭辞にをつけて表現します。

接頭辞 | 場合
------|-------------
merge-hotfix1/ | backport-mainを使う場合
merge-hotfix2/ | backport-hotfixを使う場合
merge-hotfix3/ | 同じ修正を異なるブランチで行う場合
