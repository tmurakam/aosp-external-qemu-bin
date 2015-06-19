Android Emulator HTTP Proxy 不具合修正版
========================================

概要
----

Android SDK に含まれる Android Emulator には、現時点では
特定の種類の HTTP Proxy を正常に越えられない問題があります。
(特に HTTPS を使用する場合)

具体的には、HTTP CONNECT メソッドに対し、1行以上ヘッダを返す
ような Proxy サーバの場合です。

本バグは
[Issue 75221](https://code.google.com/p/android/issues/detail?id=75221)
として AOSP に報告済みです。
パッチは AOSP の master に取り込まれていますが、リリースブランチ
側にはまだマージされていません。

本 Emulator は、この不具合を修正し、ビルドしたものです。

使い方
------

Windows / Linux / Mac OS X 版があります。

それぞれのディレクトリの内容を Android SDK の tools ディレクトリ
内に上書きコピーしてください。この際、オリジナルの内容は必ず
バックアップを取って下さい。

Android Tools をバージョンアップした場合、ファイルが上書きされ
ますので、その場合は再度コピーが必要です。

Proxy の設定
-------------

Proxy 設定は、環境変数 http_proxy で行うか、emulator 起動時の
オプションで指定してください。

    $ # 環境変数で設定する場合
    $ export http_proxy=http://<server>:<port>

    $ # emulator起動オプションで指定する場合
    $ emulator -http-proxy http://<server>:<port>

ライセンス
----------

ライセンスは GPL です。COPYING を参照してください。


ソースコード/ビルド手順
------------------------

ソースコードは以下 URL にあります。
(AOSP の external/qemu の実質ミラー)

https://github.com/tmurakam/aosp-external-qemu

自分でビルドする場合は以下のようにしてください。

1. Android Open Source Project から repo を使ってソースを取得。
   この際、'master' ブランチを取得してください。
   (現時点で、本修正は master ブランチに入っているため)
   詳細は http://tools.android.com/build を参照。

2. external/qemu に移動して ./android-rebuild.sh を実行。
   詳細は docs/BUILDING.txt を参照。

Mac OS X でビルドする場合は、Xcode 5 が必要です。
Xcode 6 ではビルドできませんので、iOS Dev Center から Xcode 5 を
個別にダウンロードしてください。Xcode5/6 は共存可能です。
ビルド時は Xcode5 側のツールを使用するよう、Xcode の設定変更が
必要です。
