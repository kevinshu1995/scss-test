# Live Sass Compiler

This is Weird I know.

-   使用 CSS 框架為 [Bootstrap 4.6](https://getbootstrap.com/docs/4.6/getting-started/introduction/)
-   所有的 scss & css 檔案都會被加入版控 QQ，但這也是沒辦法的
-   使用 VS code 的 Live Sass Compiler 編譯 SCSS

## SCSS 前置作業說明

1. 安裝 VS code 插件 [Live Sass Compiler](https://marketplace.visualstudio.com/items?itemName=ritwickdey.live-sass)
2. 安裝後，VS code 裡面點擊 `Watch Sass` 即會開始編譯，檔案有變更會及時編譯
3. Live Sass Compiler 的設定檔在 `.vscode/settings.json`

-   Live Sass Compiler 只要開啟之後，使用其他編輯器也可以，因為是檔案的變動來驅動編譯的。

## SCSS 編譯結果

-   最後會編譯成兩個檔案在隔壁資料夾 (`/style/css/`)，分別是 `all.css`、`vendors.css`
-   `/style/css` 裡面請保持皆為透過 Live Sass Compiler 產生之 CSS 檔，"不要" 自行加入任何檔案，亦即使用插件編譯之後會直接產生檔案，而不需要手動加入，即使刪掉了 `/style/css` 資料夾，依舊可以透過 Live Sass Compiler 來產生
-   Bootstrap 放在 `/style/all.css` 裡面，因為考量到可以使用 Bootstrap 提供的 mixin 功能，所以將之歸類在 `/style/scss/all.css` 裡面。
-   其他插件 (例如: owl Carousel) 可以直接放 `vendors.css`，客製化的樣式寫在 `all.css` 裡面，但請注意引入 css 順序必須 "優先引入" `vendors.css`

## 資料夾結構說明

-   樣式權重 `/style/scss/utilities` > `/style/scss/components` > `/style/scss/layout` > `/style/scss/ImportDependencies`
-   每個子資料夾 (子資料夾的子資料夾也一樣) 都一定要有一個 `_index.scss`，用來引入該資料夾內部所有檔案。以此可以識別 `_index.scss` 為該資料夾的引入檔

-   `/style/scss/dependencies`

    -   此資料夾裡面的檔案都會是從官方下載下來，請保持如此
    -   裡面的檔案 "不要做任何更改"
    -   目前設定 (`.vscode/settings.json`) 為不尋找裡面的檔案來編譯，所以裡面有任何沒有底線 (`_`) 開頭的檔案一樣不會被編譯，請放心放入插件的檔案。
    -   若要引入請透過 `ImportDependencies` 來引入插件較容易理解

-   `/style/scss/ImportDependencies`

    -   這裡才是真正會引入插件的檔案
    -   用來引入 & 整理要拿來引入的插件

-   `/style/scss/vendor`

    -   用來引入不依賴 Bootstrap 而且不常更改的樣式們
    -   由於 Bootstrap 會需要調整樣式，所以就包成一包 (all.scss)
    -   一樣是從 `/style/scss/dependencies` 引入過來

-   `/style/scss/components`、`/style/scss/layout`、`/style/scss/utilities`

    -   這三個檔案都是拿來製作客製化檔案的地方
    -   因為目前(2021/07)都是在 Bootstrap 後面引入，所以一樣可以使用 bs4 提供的 mixin 功能! [mixin 功能使用範例](https://gist.github.com/anschaef/d7552885c0e1f127cf8830d3bbf6e4b1)
    -   `/style/scss/components`
        -   共用元件之樣式，例如有多種樣子的 card 元件要客製化，不一定是哪種頁面才會用到
    -   `/style/scss/layout`
        -   共用版型或者特定頁面之樣式，例如測驗相關的才會用到的版型
    -   `/style/scss/utilities`
        -   共用功能之樣式，例如 Bootstrap 不提供某些樣式則可以自行新增於此

-   `/style/scss/all.scss`

    -   用來引入包含 Bootstrap & 客製化樣式

-   `/style/scss/vendors.scss`
    -   用來引入插件 (Bootstrap 不會在這裡引入)

```
// 資料夾結構 參考
- views
    -- add_point_record.php
    -- change_password.php

- ...前面忽略
    -- scss
        -- dependencies (不會直接被編譯)
            -- plugin_1
            -- plugin_2
        -- ImportDependencies (用來引入需要被編譯的插件)
            -- bootstrap
                -- _index.scss
            _index.scss
        -- layout
            -- add_point_record
                -- _index.scss
            -- change_password
                -- _index.scss
            _index.scss
        -- components
            -- cards
                _vertical.scss
                _horizon.scss
            _index.scss
        -- utilities
            -- userSelect
                _index.scss
            _index.scss
```
