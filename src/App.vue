<template>
  <v-app>
    <!-- router-view

    # 定義
    根據目前網址（例如 /home 或 /login）去顯示對應的「頁面元件」

    router-view 是 Vue Router 的動態顯示容器，根據目前的網址，自動顯示對應的頁面元件內容。它的存在是讓「單頁應用程式（SPA）」看起來像多頁面網站，但其實是同一頁上切換不同元件內容。

    # 出現在哪裡?
    通常放在 App.vue 或 layout.vue（像是 default.vue）中，代表這個位置是頁面內容「被替換」的地方。它不需要 import，Vue Router 會自動識別並顯示對應內容。

    # 參考
    https://vuetifyjs.com/zh-Hans/concepts/routing/#section-63075357

    # 使用
    <v-btn to="/home" text="Home"></v-btn>

    # 首頁
    當網址是 /router-view => 會顯示「首頁.vue」

    # 餐廳頁
    當網址是 /restaurant => 顯示「餐廳頁.vue」

    # 登入頁
    當網址是 /login => 顯示「登入頁.vue」
-->
    <!-- 會顯示 layout -->
    <router-view />
  </v-app>
</template>

<script setup>
//
// 最基本的樣式
import "swiper/css";

// 模組樣式（你用哪些功能就要引入哪些）
import "swiper/css/navigation";
import "swiper/css/pagination";
import "swiper/css/scrollbar";
</script>
