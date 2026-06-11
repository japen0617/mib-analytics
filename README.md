# MIB Analytics

MIB Analytics 是一個可離線使用的單頁前端工具，用來讀取單一 MIB 檔案或整個 MIB 資料夾，並解析出每筆 MIB 定義的名稱、類型、定義、完整 numeric OID 與來源檔案。

## 功能

- 直接在瀏覽器中選取單一 `.mib` / `.txt` 檔案
- 支援選取整個 MIB 資料夾，一次載入其中所有 `.mib`、`.MIB`、`.txt`
- 跨檔案解析 MIB OID 階層，支援 `IMPORTS` 依賴常見的 base/SMI MIB
- 顯示名稱、類型、定義、完整 OID 與來源檔案
- 依名稱即時搜尋，大小寫不敏感
- 不需要後端服務，檔案內容只在本機瀏覽器中處理

## 使用方式

1. 開啟網站或直接開啟 `outputs/mib-oid-viewer.html`。
2. 點選「單一 MIB 檔案」選擇要分析的 `.mib` / `.txt`，或點選「整個 MIB 資料夾」選取完整 MIB 目錄。
3. 等待解析完成後，在表格中查看結果。
4. 使用搜尋框輸入名稱關鍵字，例如 `x440g2`、`x460`、`summitX350` 或 `zyxelAaa`。

## OID 解析規則

工具會先建立 MIB 符號表，例如：

```text
extremenetworks ::= { enterprises 1916 }
extremeProduct OBJECT IDENTIFIER ::= { extremenetworks 2 }
summitX440G2-48p-10G4 OBJECT IDENTIFIER ::= { extremeProduct 220 }
```

接著展開為完整 numeric OID：

```text
.1.3.6.1.4.1.1916.2.220
```

`定義` 欄位會使用 `OBJECT IDENTIFIER` 後方連續的 `--` 註解文字；如果沒有註解，會顯示 `-`。

對於分散在多個檔案的 MIB，例如：

```text
esMgmt FROM ZYXEL-ES-SMI
zyxelAaa ::= { esMgmt 94 }
```

請使用資料夾上傳，讓工具先讀入 `ZYXEL-ES-SMI.MIB` 等 base MIB，再展開完整 OID。

## Vercel 部署

此專案是純靜態網站，不需要 build step。部署到 Vercel 時，根路徑 `/` 會透過 `vercel.json` 導向：

```text
/outputs/mib-oid-viewer.html
```

## 本地開啟

可直接雙擊以下檔案：

```text
outputs/mib-oid-viewer.html
```

或使用任一靜態伺服器開根目錄。
