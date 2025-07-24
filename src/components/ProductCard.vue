<template>
  <v-row justify="center">
    <v-col
      v-for="(variant, i) in variants"
      :key="i"
      cols="12"
      lg="3"
      md="4"
    >
      <v-card
        class="mx-auto mt-3 mt-sm-1"
        color="light-green-darken-4"
        :variant="variant"
      >
        <img
          class="w-100"
          :src="`https://picsum.photos/1920/1080/?random=${i}`"
          style="object-fit: cover; "
        >
        <v-card-item>
          <div>
            <div class="text-overline mb-1">
              {{ variant }}
            </div>
            <div class="text-h6 mb-1">Headline</div>
            <div class="text-caption">
              Greyhound divisely hello coldly fonwderfully
            </div>
          </div>
        </v-card-item>
        <v-card-actions>
          <v-btn variant="tonal"> Button </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>
<script setup>

  const variants = ['elevated', 'elevated', 'flat', 'flat']
</script>
