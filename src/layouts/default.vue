<!-- 前台的 layout => 使用者可以看到的 畫面 的 layout -->

<!-- layouts/default.vue
     是給所有頁面共用的佈局結構。你可以把它想成網站的「外框」、「模板」，像是頁首、頁尾、主畫面容器都會在這裡設定，然後所有頁面會被插入進來

     # 為什麼要用 layout？
     為了避免每一頁都重複寫頁首、頁尾或統一的版型。用 layout 就像「設定一個模板」，之後的所有頁面都照這個模板去呈現，只要填中間的內容即可，讓開發更有效率、更整齊
-->

<template>
  <!-- v-app-bar => 導覽列 -->
  <!-- color="#61773c" -->
  <v-app-bar color="light-green-darken-4">
    <!-- 用 container，flex 會不見，要自己加回來 -->
    <v-container class="d-flex align-center">
      <!-- v-app-bar-title => 標題 -->
      <v-app-bar-title>JiaNice</v-app-bar-title>

      <!-- 搜尋框 -->
      <!-- v-model="search" => 綁定是搜尋 -->
      <!-- hide-details => 讓他不要飄上去 -->
      <!-- label="搜尋商品" => 會飛上去 -->
      <!-- placeholder => 搜尋框裡面，顯示的字 -->
      <!-- prepend-inner-icon="mdi-magnify" => 在前面加上 搜尋框 的圖示 -->
      <v-text-field
        v-model="search"
        flat
        hide-details
        placeholder="搜尋餐廳"
        prepend-inner-icon="mdi-magnify"
        variant="outlined"
      />

      <!-- 導覽連結
           用 v-for 方法，一次印出來 (navItems)
      -->
      <!-- show: true => 要不要顯示 導覽 的路徑 (像是 登入 跟 註冊頁，在 登入 的情況下不應該顯示，所以用 show 來判斷，要不要顯示這個項目)
                         * 要根據 使用者 有沒有登入 的狀態，去顯示的話，不能用 一般的陣列 => 要變成 動態的陣列(computed)
      -->
      <!-- 使用者功能  -->
      <!-- 使用 v-for 迴圈，把 navItems 裡的每一個項目（像是「首頁」「註冊」等）一個一個產生對應的按鈕 -->
      <!-- :key => 綁 key (綁 每一頁的 to => 因為 路徑 都不一樣)  -->
      <template v-for="item of navItems" :key="item.to">
        <!-- 換頁按鈕 => v-btn -->
        <!-- v-btn => 顯示一顆按鈕（v-btn 是 Vuetify 的按鈕） -->
        <!-- v-if="item.show" => 只有當 item.show 是 true 的時候才顯示！（例如: 已登入才看得到「購物車」） -->
        <!-- :prepend-icon => 按鈕上會加上 icon（用 item.icon 指定） -->
        <!-- :to => 點按鈕會跳轉到 item.to 指定的網址 (當作 換頁 的按鈕) => 放項目的 title => {{ item.title }} -->
        <v-btn :prepend-icon="item.icon" :to="item.to">{{ item.title }}</v-btn>
        <!-- 顯示的判斷，用 v-if (跟 v-for 不能一起寫) -->
      </template>
    </v-container>
  </v-app-bar>

  <!-- 顯示「當前頁面的內容」

       # 定義
       router-view 會根據你目前點到的網址，顯示對應的頁面（例如點到 /login 就顯示登入畫面）
  -->

  <!-- v-main (每頁都有)
       Vuetify 的元件，用來包住主要畫面內容，會自動套用主題色彩、排版空間，幫你解決很多畫面上的問題。類似畫面「主舞台」
  -->
  <v-main>
    <!-- 使用 vue-router 的話，官方建議把<router-view> 寫在 <v-main> 裡 -->
    <!-- router-view -->
    <router-view />
  </v-main>
</template>

<!-- 寫邏輯的地方（JavaScript：判斷登入、登出、資料邏輯） -->
<script setup>
//

// 導覽列的項目
// 除了 管理員 之外，其他畫面都使用 latout
  const navItems = [
    // 首頁
    { title: '首頁', to: '/home', icon: 'mdi-home' },

    // 愛心
    { title: '收藏', to: '/collection', icon: 'mdi-heart' },

    // 更多
    { title: '更多', to: '/more', icon: 'mdi-dots-vertical', variant: 'tonal' },

    // 帳戶
    { title: '帳戶', to: '/account', icon: 'mdi-account' },

    // 登入
    { title: '登入', to: '/login', icon: 'mdi-login' },
  ]
</script>

<!-- 登出，按了之後，去發請求 給 登出的 api，所以沒有 登出的頁面 -->
