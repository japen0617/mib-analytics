# MIB Analytics

MIB Analytics 是一個可離線使用的單頁前端工具，用來讀取 MIB 檔案並解析出每筆 `OBJECT IDENTIFIER` 的名稱、定義與完整 numeric OID。

## 功能

- 直接在瀏覽器中選取 `.mib` 或 `.txt` 檔案
- 自動解析 MIB 內的 OID 階層
- 顯示名稱、定義與完整 OID
- 依名稱即時搜尋，大小寫不敏感
- 不需要後端服務，檔案內容只在本機瀏覽器中處理

## 使用方式

1. 開啟網站或直接開啟 `outputs/mib-oid-viewer.html`。
2. 點選「MIB 檔案」並選擇要分析的 `.mib` 或 `.txt` 檔。
3. 等待解析完成後，在表格中查看結果。
4. 使用搜尋框輸入名稱關鍵字，例如 `x440g2`、`x460` 或 `summitX350`。

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
