<template>
  <v-footer
    class="text-center d-flex flex-column ga-2 py-4 mt-16"
    color="light-green-darken-4"
  >
    <!-- 顏色調整 => light-green-darken-3 -->
    <div class="d-flex ga-3">
      <v-btn
        v-for="icon in icons"
        :key="icon"
        class="d-flex ga-3"
        density="comfortable"
        :icon="icon"
        variant="tonal"
      />
    </div>

    <v-divider class="my-2" thickness="2" width="50" />
    <h1 style="color: white;">讓每一餐，都成為照顧自己的開始 🍱💖</h1>

    <div class="text-white opacity-70">

      <br>

      <h2>🌿 專題簡介：</h2>

      <h4>《JiaNice》 是一個融合 營養提醒、餐廳推薦、隨機抽選與情感記錄 的健康飲食平台，旨在陪伴使用者在忙碌生活中，也能透過簡單的操作，輕鬆維持健康、享受美食，並記錄日常心情 🌈。</h4>

      <br>

      <p>
        讓——

        「健康」不只是數據，而是一種溫柔的自我對話；<br>
        「吃飯」也不只是填飽肚子，更是照顧身心的儀式感 🍽️💕<br>
      </p>
    </div>

    <v-divider />

    <div>
      版權所有 &copy; {{ new Date().getFullYear() }} Yuna —
      <strong>Vuetify</strong>
    </div>
  </v-footer>
</template>

<script setup>
  const icons = [
    'mdi-github',
    'mdi-facebook-messenger',
    'mdi-linkedin',
    'mdi-google-plus',
    'mdi-instagram',
  ]

  const links = [
    'https://github.com/yunahsuya?tab=repositories',
    'https://www.linkedin.com/in/hsu-yuna-380062361 ',
  ]
</script>
