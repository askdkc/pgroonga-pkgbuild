# Arch Linux用 PKGBUILDファイル
Arch LinuxにはAURとかがあり便利なのですが、個人ユーザのボランティアベースな更新がメインのため最新化が遅れることが結構あります

ここではPGroongaに必要なPKGBUILDファイルの最新版を作成時に追加していく予定です

## PKGBUILDファイルについて
PKGBUILDは次のように格納されています
- groonga/version/PKGBUILD
- groogga/version/groonga-httpd.service
- pgroonga/version/PKGBUILD

## 使い方
1. 必要なバージョンのPKGBUILDファイルをダウンロード(Groongaは`groonga-httpd.service`も必要)
```bash
mkdir -p temp/groonga
cd temp/groonga
wget PKGBUILD_URL(Groonga)
wget groonga-httpd.service_URL(Groonga)

cd ..
mkdir pgroonga
wget PKGBUILD_URL(PGroonga)
```

2. それぞれのディレクトリで下記コマンドでインストール実行
```bash
makepkg -si
```

### 初回：`mecab-ipadic`の依存関係について

Groongaの`mecab`サポートのために`mecab`と`mecab-ipadic`が必要なのですが、`mecab-ipadic`が`mecab`のライブラリを探しに行く場所が`/usr/lib/mecab`ではなく`/usr/libexec/mecab`なので`mecab-ipadic`をAURから入れるには一手間必要です

1. 最初に`mecab-git`をインストール
```bash
yay -S mecab-git
```
2. この後
```bash
sudo mkdir -p /usr/libexec/mecab
cd /usr/libexec/mecab
ln -s /usr/lib/mecab/（ここのファイル全部）
```
3. `mecab-ipadic`のインストール
```bash
yay -S mecab-ipadic
```

これでGroongaに必要なmecabの準備が出来ました🎉
