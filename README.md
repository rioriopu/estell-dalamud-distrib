# estell-dalamud-distrib

estell の自前 Dalamud 配布パッケージ置き場(`goatcorp/dalamud-distrib` 相当)。
改変版 XIVLauncher(`rioriopu/FFXIVQuickLauncher`)が静的に参照する。

## 構成

```
meta.json            … ブランチ一覧(ベータキー切替UI用、camelCase)
estell/version       … トラック estell の DalamudVersionInfo(PascalCase)
estell/             …(zip は GitHub Release アセットとして配布)
```

## 参照 URL(launcher の DistributionConfig と対応)

- Meta:     `https://raw.githubusercontent.com/rioriopu/estell-dalamud-distrib/main/meta.json`
- Version:  `https://raw.githubusercontent.com/rioriopu/estell-dalamud-distrib/main/estell/version`
- Zip:      `https://github.com/rioriopu/estell-dalamud-distrib/releases/download/estell/latest.zip`

## 更新方法

`rioriopu/estell-dalamud-declarative` の GitHub Actions
(`build-and-publish.yml`)が自動で:

1. `rioriopu/Dalamud` をビルド
2. `latest.zip` を本リポジトリの Release(タグ `estell`)へアップロード
3. `estell/version` と `meta.json` を再生成してコミット

を行う。手動編集も可。

## 注意

- `Key`(ベータキー)は `meta.json` と `estell/version` で一致必須。利用者はこのキーを XIVLauncher の
  「Have a beta key?」で入力する。
- `AssemblyVersion` は公式と必ず別値にする(launcher は `Hooks/{AssemblyVersion}` にインストールするため、
  同一だと公式ビルドとフォルダ衝突する)。
- `SupportedGameVer` は対応ゲームバージョンと一致させる(不一致だと起動不可)。
- `RuntimeVersion` を公式と同じ値にすれば、.NET ランタイムは公式 kamori からそのまま取得される
  (自前でランタイムをホストする必要はない)。
