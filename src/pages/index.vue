<!--
    ★ 檔案順序

       1.輪播圖 (swiper)](https://swiperjs.com/get-started#use-swiper-from-cdn)

       2.分類
       ◆ 最上面 (大項分類)
       => 全部(放熱門，常點的)、中式、義式、美式、泰式、等等

       ◆ 下面 (細項分類)
       => 中式 -> 麵、飯、熱炒、夜市等等
       => 美式 -> 披薩、漢堡...
       => 點心 -> 鬆餅、炸物、蛋糕...
       => 飲料 -> 青茶、鮮奶茶、奶茶、芒果...

       3. 側邊欄(選小項) + 評分 (評價)

       4. 頁尾
    ________________________________________________________________

    ★ 文件

    1. 顏色
    https://vuetifyjs.com/en/styles/colors/#material-colors

    2. 尺寸 (flex)
    https://vuetifyjs.com/en/styles/flex/#flex

    3. 位置 (position)
    https://vuetifyjs.com/en/styles/position/#position

    4. 大小 (sizing)
    https://vuetifyjs.com/en/styles/sizing/#sizing

    5. 間距 (spacing)
    https://vuetifyjs.com/en/styles/spacing/#spacing

    6. 字體粗度 (h1、h2....)
    https://vuetifyjs.com/en/styles/text-and-typography/#text-and-typography

-->

<template>
  <div>
    <!-- 🧁 上方內容：輪播圖 + 卡片 -->
    <v-container>
      <v-row justify="center">
        <v-col cols="12">

          <!-- 輪播圖 -->
          <SwiperCarousel />

          <hr class="mt-10">

          <!-- 卡片區 -->
          <h1 class="mt-10">餐廳</h1>
          <ProductCard />
          <ProductCard />

          <!-- 留空讓可以滑到 Gsap 出現 -->
          <!-- <div style="height: 60vh;" /> -->
        </v-col>
      </v-row>
    </v-container>

    <PeopleState />

    <!-- 🌀 橫向滾動效果區塊（不要放在 v-container 裡！） -->
    <GsapPhoto />

    <!-- 📦 Footer -->
    <IndigoFooter />
  </div>
</template>

<script setup>

// Gsap
  import GsapPhoto from '@/components/GsapPhoto.vue'

  // Footer
  import IndigoFooter from '@/components/IndigoFooter.vue'

  // 卡片
  import ProductCard from '@/components/ProductCard.vue'

  // 輪播圖
  import SwiperCarousel from '@/components/SwiperCarousel.vue'

  import PeopleState from '../components/PeopleState.vue'

</script>
