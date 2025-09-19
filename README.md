# maze-note
まぜねこの個人的なTIPSや雑記です。

## WindowsにSSHで接続するなどしてCUIのテキストエディタがなくて困ったときのやつ

Gitがインストールされていれば`git/usr/bin/`にvimとかnanoとかが入ってる可能性が高いのでそれを使うとよいです。

## VSCodeでPowerShell使うときに文字コードをUTF-8にしたいときのやつ

`.vscode/settings.json`でこれを設定するとよいです。

```json
"terminal.integrated.profiles.windows": {
  "PowerShell": {
    "source": "PowerShell",
    "args": [
      "-NoExit",
      "-Command",
      "chcp 65001; $env:JAVA_TOOL_OPTIONS=\"-Dfile.encoding=UTF-8\""
    ]
  }
}
```

Gradleなどでアプリを開発してるとき、アプリはUTF-8でログ出力してるけどPowerShellがSJISで表示してしまって化けることがあります。
これはそれを解決するためにVSCodeでPowerShell立ち上げる時に文字コードをUTF-8に変えるようにするやつです。

※アプリがSJISで出力してPowerShellがUTF-8で表示してしまうのを防止するために、JAVA_TOOL_OPTIONSの文字コードもUTF-8にしています。

## Spring BootのbuildBootImageを使う時の注意

プロパティファイルの拡張子をyamlにしているとコンテナで実行した時に適用されないようです。
ymlにすれば適用されるので普段からymlにするとよさそうです。

## 開発時のSpring Bootのプロパティファイルに秘匿情報を書かない

devプロファイルのプロパティを作って開発中に使うことがありますが、
resourcesにあるファイルはビルド成果物のjarファイルに含まれるので漏洩する危険性があります。

## イベントソーシングをするときのリプレイ処理では極力エラーとならないようにする

不整合などの防止で例外を投げたりしたくなりますが、
リプレイで止まると、システムが稼働不能になってしまったり、修正イベントの適用まで辿り着けなかったり、
不都合が多いので致命的な内容でない限りエラーで止めないようにした方がよいです。