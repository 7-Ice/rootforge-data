# rootforge-data

RootForge 的机型 / 内核对照数据。纯静态 JSON，App 直接拉，不需要后端。

## 一条记录长什么样

`devices/<代号>.json`

```json
{
  "device": "amethyst",
  "brand": "Redmi",
  "series": "Redmi Note",
  "model": "Redmi Note 14 Pro+",
  "soc": "Qualcomm Snapdragon 7s Gen 3 (SM7635)",
  "variants": [
    {
      "rom": "OS3.0.306.0.WOPCNXM",
      "android": "14",
      "kernel": "6.1.138-android14-11-g0c3d559bcd85-ab14529422",
      "source": "device"
    }
  ]
}
```

同一个机型可以有多个 `variants`——不同地区、不同 OTA 的内核版本本来就不同，这是数组不是笔误。

## 怎么加一条

1. App 里解析一个 OTA，它会自动读到 `post-build` 和内核版本
2. 点"分享这条记录"，会打开一个预填好的 Issue
3. 或者直接提 PR，改 `devices/<代号>.json` 并同步 `index.json`

字段定义见 `schema.json`。

## 规则

- **`source` 必须是真实来源**：`device`（机器上读的）、`ota`（从包里解出来的）、`manual`（人工填的，最容易错）
- `fingerprint` 要和 `device` 对得上，CI 会查
- 没把握就别提交。错的数据比没有数据更糟——照着错的机型打，轻则失败，重则 panic

## 许可

数据部分 CC0，随便用。
