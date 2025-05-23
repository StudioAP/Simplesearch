# Google Maps埋め込み実装ガイド

## 成功した方法の概要

Webサイトに正確な場所を示すGoogleマップを埋め込む際の効果的な方法をまとめました。

### 成功した実装アプローチ

```html
<iframe 
  src="https://www.google.com/maps?q=京都ローンテニスクラブ+〒601-1121+京都市左京区静市静原町554&output=embed&hl=ja&z=16"
  width="100%" 
  height="100%" 
  style="border: 0;" 
  allowFullScreen={false} 
  loading="lazy" 
  referrerPolicy="no-referrer-when-downgrade"
  title="京都ローンテニスクラブの地図"
  className="rounded-sm"
/>
```

## 教訓とポイント

1. **通常のGoogle Maps検索URLを使用する**
   - Google Maps Embed APIの複雑なパラメータ（pb=など）ではなく、シンプルな検索URLを使う
   - 基本形式: `https://www.google.com/maps?q=検索クエリ&output=embed`

2. **検索クエリの精度向上のためのパラメータ**
   - 施設名を含める（より具体的な検索結果につながる）
   - 郵便番号を含める（〒xxx-xxxx形式）
   - 完全な住所を含める
   - 検索クエリ例: `京都ローンテニスクラブ+〒601-1121+京都市左京区静市静原町554`
   - プラス記号（+）でクエリの各部分を連結する

3. **表示オプションの設定**
   - `output=embed` - 埋め込みモードで表示（必須）
   - `z=16` - ズームレベル（値が大きいほど拡大：14-16が建物レベルで適切）
   - `hl=ja` - 言語を日本語に設定

4. **iframeの適切な設定**
   - `width="100%"`, `height="100%"` - レスポンシブ表示の確保
   - `style="border: 0;"` - 枠線の削除
   - `loading="lazy"` - パフォーマンス向上
   - `referrerPolicy="no-referrer-when-downgrade"` - セキュリティ対策
   - 意味のある`title`属性 - アクセシビリティ向上

## 失敗したアプローチから学んだこと

1. **Google Maps Embed APIの複雑さ**
   - `pb=`で始まる長いパラメータ文字列は編集が難しく、思った通りに動作しないことが多い
   - マーカーパラメータ（`&markers=`）は常に反映されるとは限らない

2. **過度に技術的な実装の避け方**
   - JavaScript APIの使用は柔軟性が高いが、単純な表示には複雑すぎる
   - 静的マップAPIはキーが必要で、インタラクティブ性に欠ける

3. **検索クエリの重要性**
   - 検索クエリが具体的であるほど、正確な場所にピンが表示される
   - 施設名と住所の両方を含めることで精度が向上

## 応用テクニック

- **カスタムマーカー**: 現在のアプローチでは標準的な赤いピンが表示されるが、デザインをカスタマイズするにはJavaScript APIが必要
- **複数の場所**: 複数の場所を表示したい場合は、それぞれに別々のiframeを使用するか、JavaScript APIへの移行を検討
- **スタイルのカスタマイズ**: 親コンテナにCSSスタイルを適用して外観を調整可能

## まとめ

シンプルで直接的なGoogle Maps検索URLを使用することで、APIキーなしでも正確な位置表示が可能です。検索クエリに施設名と完全な住所情報を含めることで、地図上のピン表示の精度が大幅に向上します。