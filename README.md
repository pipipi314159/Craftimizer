# Craftimizer (TW)

FFXIV 台服（繁中）版 Craftimizer 移植，可在台服 Dalamud（API13）上使用。

在遊戲內模擬製作、自動產生製作巨集，並在製作過程中提供下一步建議。

- 原版：https://github.com/WorkingRobot/Craftimizer
- 基於版本：`2.8.0.0`（commit `3359748d1382dab09f76aaed98ea7c2b07e36888`，2025-08-19）
- Dalamud API：13（`Dalamud.NET.Sdk/13.0.0`）
- 分支：`tw-api13`

> 問題請回報到本 repo，不要回報給原作者。

## 程式修改

| 檔案 | 修改 | 原因 |
|---|---|---|
| `Craftimizer/LuminaSheets.cs` | 讀取英文 Item 表時加上 try/catch，失敗則為 `null` | 台服資料可能沒有英文表，原寫法會讓整個插件載入失敗 |
| `Craftimizer/Utils/Gearsets.cs` | 「輝煌工具」偵測：沒有英文表時改用目前語言的說明文字是否含「1.75」判斷 | 同上 |
| `Craftimizer/Craftimizer.json` | `Name` 加上 ` (TW)`、`RepoUrl` 改為本 repo | 區分版本；`InternalName` 不變，保留原設定 |

## 台服測試狀況

2026-10-23 於台服測試，以下功能正常：

- 插件載入（無錯誤）
- 製作筆記旁的 Crafting Log Helper：配方、職業、屬性正確讀取，中文配方名稱正常顯示
- 巨集求解（Suggested Macro / Generate，Raphael 求解器）
- 社群巨集搜尋（Search Online）
- 巨集編輯器（`/crafteditor`）
- 製作輔助（Synthesis Helper）：製作中顯示下一步建議，模擬結果與遊戲一致

台服資料內含英文物品表，因此上述「輝煌工具」的替代判斷目前不會用到，僅作為保險。

## 注意事項

- 「社群巨集」功能會連到 FFXIV Teamcraft、craftingway 讀取巨集，那些網站的資料以國際服為準，部分配方在台服可能還沒有。
- 求解器使用 [Raphael](https://github.com/KonaeAkira/raphael-rs)（`Raphael.Net` 套件，內含預編譯原生程式庫）。

## 編譯

需要 .NET SDK 9 以及台服 Dalamud（XIVLauncher / FFXIVSimpleLauncher）。

```bat
set DALAMUD_HOME=<你的 Dalamud Injector 資料夾>
dotnet build Craftimizer\Craftimizer.csproj -c Release
```

輸出：`Craftimizer\bin\Release\Craftimizer.dll`

## 作者與授權

原作者：Asriel Camora（[WorkingRobot](https://github.com/WorkingRobot)）。依原專案 MIT 授權，見 [LICENSE](LICENSE)。
