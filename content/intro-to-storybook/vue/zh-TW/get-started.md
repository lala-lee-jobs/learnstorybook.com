---
title: 'Vue Storybook 學習指南'
tocTitle: '開始吧'
description: '在你的開發環境下，設置 Vue Storybook'
---

Storybook 可在開發模式下與您的應用程式一起執行。它可以幫助您構建 UI 元件，並與 應用程式的 業務邏輯和上下文 隔離開來。**Vue Storybook 學習指南** 適用於 **Vue**；其他可運行版本還包括 [React](/react/en/get-started)、[React Native](/react-native/en/get-started/)、[Angular](/angular/en/get-started) 及 [Svelte](/svelte/en/get-started).

![Storybook and your app](/intro-to-storybook/storybook-relationship.jpg)

## 建置 Vue Storybook

我們需要遵循一些步驟用以在您的環境中設定建置程序。首先，我們要使用 [Vue CLI](https://cli.vuejs.org) 建置系統，並在待建立的應用程式中啟用 [Storybook](https://storybook.js.org/) 和 [Jest](https://facebook.github.io/jest/)。讓我們運行以下命令：

```bash
# 使用含有 Jest 的 Preset 來初始化建立我們的專案
npx -p @vue/cli vue create taskbox --preset chromaui/vue-preset-learnstorybook

cd taskbox

# 在專案裡加上Storybook的功能
npx -p @storybook/cli sb init
```

<div class="aside">
在這個學習指南，我們會使用<code>yarn</code>做為主要的運行指令。如果你安裝了yarn，但更喜歡使用 <code>npm</code> ，請放心，您仍然可以順利的使用 <code>npm</code> 運行整個學習指南。只需將 <code>--packageManager=npm</code> 參數添加到上面的第一個指令，Vue CLI 和 Storybook 就會基於 <code>npm</code> 開始初始化。在學習本學習指南的過程中，也記得要調整指令為對應 <code>npm</code> 的指令。
</div>

我們可以快速地檢查應用程式的各種環境是否正常運行：

```bash
# 在 terminal 運行 Test Runner (Jest)
yarn test:unit

# 啟動 component explorer 在 port 6006:
yarn storybook

# 啟動前端應用程式在 port 8080:
yarn serve
```

以上是前端應用程式的三個開發模式：自動化測試 (Jest)、元件開發 (Storybook) 以及應用程式本身。

![3 modalities](/intro-to-storybook/app-three-modalities-vue.png)

根據您開發應用程式時正在處理的部分，您可能需要同時運行一個或多個方式。由於目前的重點是建立單一的 UI 元件，因此接下來會繼續運行 Storybook。

## Reuse CSS

Taskbox 重用了 [GraphQL and React Tutorial 範例應用](https://www.chromatic.com/blog/graphql-react-tutorial-part-1-6) 中的設計元素，因此我們無需在本學習指南中撰寫 CSS。複製 [這個已編譯完成的 CSS](https://github.com/chromaui/learnstorybook-code/blob/master/src/index.css) 為 `src/index.css`，然後在 `src/App.vue` 的 style 區塊中 import 這個 css，如下所示：

```html
<style>
  @import './index.css';
</style>
```

![Taskbox UI](/intro-to-storybook/ss-browserchrome-taskbox-learnstorybook.png)

<div class="aside">
如果想要修改樣式，可以使用 <a href="https://github.com/chromaui/learnstorybook-code/tree/master/src/style">所提供的 LESS 原始檔案</a> 做修改。
</div>

## 增加 assets

為了符合預期的設計，你還需要下載二個 font 及 icon 的目錄，並且把它們放到你的 `public` 檔案夾。可以在 terminal 中，使用以下的指令完成：

```bash
npx degit chromaui/learnstorybook-code/public/font public/font
npx degit chromaui/learnstorybook-code/public/icon public/icon
```

<div class="aside">
我們使用 <a href="https://github.com/Rich-Harris/degit">degit</a> 去下載放在 GitHub 上的 檔案夾。如果你想要手動下載，你也可以在使用<a href="https://github.com/chromaui/learnstorybook-code/tree/master/public">此連結</a>下載這些檔案夾。
</div>

我們也必須要在 `package.json` 中加入 Storybook script，運行 Storybook 並指定放置靜態檔案的目錄位置為 `public`：

```json
{
  "scripts": {
    "storybook": "start-storybook -p 6006 -s public"
  }
}
```

添加完樣式檔案和 assets 後，應用程式將呈現得有一些奇怪。但先別在意。我們目前還沒要使用應用程式。接下來，我們將從構建第一個元件開始！
