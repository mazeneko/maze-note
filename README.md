# maze-note
まぜねこの個人的なTIPSや雑記です。

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
