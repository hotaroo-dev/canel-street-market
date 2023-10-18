<script setup lang="ts">
import { animate, spring } from 'motion'

const isVisible = ref(false)

function handleScroll() {
  console.log('run')
  if (window.scrollY > 100) {
    isVisible.value = true
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

const unwatch = watch(isVisible, (isVisible) => {
  if (isVisible) {
    animate(
      '.hero-bg',
      { opacity: 1 },
      { duration: 1, delay: 0.25, easing: spring() }
    )
    unwatch()
  }
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <div class="mt-[22vh] pb-20">
    <div class="container lg:w-9/12">
      <div class="lg:h-screen">
        <h1 class="text-4xl font-thin leading-tight">
          Canal Street Market is a carefully curated retail market, food hall &
          community space open year-round at 265 Canal Street.
          <a
            href="#"
            class="bg-repeat-x"
            style="
              background-image: repeating-linear-gradient(
                  -45deg,
                  #ffb400,
                  #ffb400 1px,
                  transparent 0,
                  transparent 13px
                ),
                repeating-linear-gradient(
                  45deg,
                  #ffb400,
                  #ffb400 1px,
                  transparent 0,
                  transparent 11px
                );
              background-size: 17px 10px;
              background-position:
                0 103%,
                2px 103%;
            "
          >
            Support Small Business
          </a>
          this weekend!
        </h1>
      </div>
    </div>
    <div
      class="hero-bg mt-10 h-[98vh] w-full bg-cover bg-center opacity-0"
      style="background-image: url(./hero.jpg)"
    ></div>
  </div>
</template>
