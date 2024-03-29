# インプットメソッドについて

## 調査の背景

- ibus、uim など現在のLinux環境で利用されているインプットメソッドがある。
- ただ、それらが現在どのような仕組みで動作しているのかを知るには、ドキュメントは断片的であったり、ソースコードを読んだ人のみ知っているなどまとまった情報がないように思う。
- 本記事は、Linuxで日本語入力を行う場合に使うインプットメソッドの仕組みと実装について調査してまとめものである。

## 参考情報

- [https://wiki.archlinux.jp/index.php/インプットメソッド](https://wiki.archlinux.jp/index.php/インプットメソッド)
- [京都発！ オープンソースなかな漢字変換の変遷 (2016)](https://www.ospn.jp/osc2016-kyoto/pdf/OSC2016_Kyoto_openmanyo.pdf)
- [プログラミングでLinuxの日本語入力の流れを知る (2022)](https://qiita.com/ai56go/items/2b033d014d34a602e219)
- [予測入力システムの開発 (2011)](https://www.jstage.jst.go.jp/article/jssst/28/4/28_4_4_17/_pdf)
- [共起性を考慮したかな漢字変換 (2016)](https://staff.aist.go.jp/yoriyuki.yamagata/slide/kanakan-20160610.pdf)

## インプットメソッドとは
   
- xxx

## 日本語入力とインプットメソッドの関係

- 日本語入力を行うソフトウェアは主に「モノリシック方式」と「クライアント・サーバ方式」がある。
    - モノリシック方式の実装例
        - Anthy
    - クライアント・サーバ方式の実装例
        - Cannna、Wnn、PRIME、Mozc

- [京都発！ オープンソースなかな漢字変換の変遷](https://www.ospn.jp/osc2016-kyoto/pdf/OSC2016_Kyoto_openmanyo.pdf) によると、現在のLinux環境における日本語入力は以下のパターンが多いとのこと。

    入力 | キー入力 -> input method -> ひらがな、ローマ字等 -> かな漢字
    
    出力 | 画面出力 <- input method <- 変換した日本語       -> 変換システム

## インプットメソッドとデスクトップ環境の連携方法

### 環境変数

- 解説記事
  - [Input method related environment variables](https://fcitx-im.org/wiki/Input_method_related_environment_variables)
- 環境変数
    - GTK\_IM\_MODULE
      - GTKが使う IMモジュールを指定する設定値
      - debian の場合 (uim用のim-uim.so は uim-gtk3-immodule パッケージに含まれている)

        $ ls /usr/lib/x86_64-linux-gnu/gtk-3.0/3.0.0/immodules
        im-am-et.so              im-thai.so
        im-broadway.so           im-ti-er.so
        im-cedilla.so            im-ti-et.so
        im-cyrillic-translit.so  im-uim.so
        im-ibus.so               im-viqr.so
        im-inuktitut.so          im-wayland.so
        im-ipa.so                im-xim.so
        im-multipress.so
    
    - QT\_IM\_MODULE
      - QTが使う IM モジュールを指定する設定値
      - debian の場合 (uim用はuim-qt5-immodule パッケージに含まれている)
        - /usr/lib/x86_64-linux-gnu/qt5/plugins/platforminputcontexts/libuimplatforminputcontextplugin.so
      - 「Qt の im モジュールは Gtk と似ていますが、認識するために余分なファイルは必要ありません。QT\_IM\_MODULE が指定されていない場合、qtconfig (Ubuntu/Debian/ArchLinux qtconfig-qt4) を使用してデフォルトのものを構成できます。それ以外の場合は、QT_IM_MODULE によってオーバーライドされます。」
    - XMODIFIERS
        - XIM を使うアプリケーション向けのキー入力の送信先
        - 書式は「XMODIFIERS=@im=<xim server name>」。(例)「XMODIFIERS=@im=ibus」

### コンソール環境

- 自分は過去にDebianのコンソール上で、フレームバッファーコンソール(昔はkon、今はjfbterm)と uim-fep を利用して日本語入力をしたことがある。
- （どういう仕組みで動いているのかは後で調べる）

### GTKを使ったデスクトップ環境

### KDE環境を使ったデスクトップ環境

## インプットメソッドの実装

### uim

- xxx

### ibus

- xxx

### fiticx

- xxx
