<template>
  <section ref="section" class="scroll-section">
    <div ref="content" class="scroll-content">
      <img
        v-for="i in 6"
        :key="i"
        alt="image"
        :src="`https://picsum.photos/600/400?random=${i}`"
      >
    </div>
  </section>
  <!-- <div style="height: 20vh;background:Red" /> -->
</template>

<script setup>
  import gsap from 'gsap'
  import ScrollTrigger from 'gsap/ScrollTrigger'
  import { nextTick, onMounted, onUnmounted, ref } from 'vue'

  gsap.registerPlugin(ScrollTrigger)

  const section = ref(null)
  const content = ref(null)
  let resizeObserver = null

  // 等待圖片全部載入
  function waitForImagesLoaded (containerEl) {
    const images = containerEl.querySelectorAll('img')
    const promises = [...images].map(img =>
      new Promise(resolve => {
        if (img.complete) return resolve()
        img.addEventListener('load', img.onerror = resolve)
      }),
    )
    return Promise.all(promises)
  }

  onMounted(async () => {
    await nextTick()
    await waitForImagesLoaded(content.value)

    const el = content.value
    const scrollDistance = el.scrollWidth - window.innerWidth
    if (scrollDistance <= 0) return

    gsap.set(el, {
      x: window.innerWidth,
    })

    // markers: true, 測試用
    gsap.to(el, {
      x: -scrollDistance,
      ease: 'none',
      scrollTrigger: {
        trigger: section.value,
        start: 'center 50%',
        end: `+=${scrollDistance}`,
        scrub: 0.5,
        pin: true,
        pinSpacing: true, // 防止 pin 造成 layout 抽掉
        invalidateOnRefresh: true,
      },
    })

    // 自動監測高度變化
    resizeObserver = new ResizeObserver(() => {
      ScrollTrigger.refresh()
    })
    resizeObserver.observe(section.value)

    ScrollTrigger.refresh()
  })

  onUnmounted(() => {
    for (const t of ScrollTrigger.getAll()) t.kill()
    if (resizeObserver) resizeObserver.disconnect()
  })
</script>

<style scoped>
.scroll-section {
  position: relative;
  overflow: hidden;

  height: 100vh;
}

.scroll-content {
  display: flex;
  gap: 60px;
  padding: 40px 0;
  /* width: max-content; */
  height: 100vh;
  /* box-sizing: border-box; */
  align-items: center;
  /* will-change: transform; */
}

.scroll-content img {
  width: 600px;
  height: 400px;
  border-radius: 20px;
  /* object-fit: cover; */
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.15);
  transition: transform 0.3s ease;
}

.scroll-content img:hover {
  transform: scale(1.07);
}
</style>
