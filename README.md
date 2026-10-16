# RMML Marp 簡報模板

用 Markdown 寫簡報，存檔後即時預覽，版面與 RMML meeting 的 PowerPoint 範本一致（右側色條、三個 logo、藍色標題）。

## 資料夾內容
```
rmml-marp-template/
├─ rmml.css               主題（版面、顏色、logo 都在這裡，logo 已內嵌）
├─ template.md            各種版面的示範，可直接複製來改
├─ AGENT.md               給 AI agent 的填寫規則（每次丟新內容時一起給它）
├─ .marprc.yml            CLI 設定（自動載入主題）
├─ .vscode/settings.json  VS Code 預覽設定（自動載入主題）
├─ examples/
│  ├─ thr-charging.md     完整範例：溫室充電站 16 頁
│  └─ fig-incline.svg     範例用的受力圖
├─ decks/                 每次 meeting 一個日期資料夾
│  └─ 2026-10-16/
│     ├─ 2026-10-16.md    當次簡報
│     └─ img/             當次用到的圖片
└─ assets/                原始 logo（備用）
```

新的 meeting：建立 `decks/YYYY-MM-DD/`，把 `template.md` 複製進去改。
匯出的 `.pptx`、`.pdf` 與影片檔（`.mp4`、`.mov`）不會進 git（見 `.gitignore`），只留在本機。

## 一次性設定：即時預覽
1. 安裝 VS Code 擴充套件 **Marp for VS Code**（marp-team.marp-vscode）。
2. 用 VS Code 打開**整個資料夾**（不是單一檔案），`.vscode/settings.json` 才會生效。
3. 打開任一 `.md`，按右上角的預覽圖示（或 `Ctrl/Cmd+K V`）。之後每次存檔，預覽就會更新。
4. 若出現「信任工作區」提示，選信任。主題要在受信任的工作區才能載入。

## 匯出
需要 Node.js。在資料夾根目錄執行：
```bash
npx @marp-team/marp-cli examples/thr-charging.md --pdf          # PDF（報告用這個）
npx @marp-team/marp-cli examples/thr-charging.md --pptx         # PPTX（每頁是圖片，不能改字）
npx @marp-team/marp-cli examples/thr-charging.md --html         # 單一 HTML
npx @marp-team/marp-cli -s .                                    # 瀏覽器即時預覽伺服器
```
- 也可以直接用 VS Code 預覽視窗右上角的「Export Slide Deck」。
- `--pptx-editable` 可以輸出能改字的 PPTX，但目前是實驗功能，需要安裝 LibreOffice，卡片和甘特圖的樣式會跑掉。如果一定要可編輯的 PPT，建議另外請 agent 直接生成。

## 跟 agent 合作的流程
1. 每次報告前，把**新的內容架構**（條列、數字、圖片路徑）連同 `AGENT.md` 一起給 agent。
2. agent 只會產出一個新的 `.md`。如果它讀了 `rmml.css`，就是在浪費 token，請它不要讀。
3. 你在 VS Code 直接改字，存檔就看到結果。
4. 定稿後匯出 PDF。

## 想改版面
顏色在 `rmml.css` 最上面的 `:root` 裡。logo 是 base64 內嵌的，換 logo 時把 `assets/` 裡的新圖轉成 base64 再貼回去即可。
