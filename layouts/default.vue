<script setup lang="ts">
import { Motion, Presence } from 'motion/vue'

const show = ref(false)

const items = ref([
  { title: 'about', color: '#fff', rotate: '-45deg' },
  { title: 'food', color: '#5ea3ec', rotate: '45deg' },
  { title: 'retail', color: '#f64444', rotate: '45deg' },
  { title: 'community', color: '#ffb400', rotate: '-45deg' }
])
</script>

<template>
  <Motion
    :initial="{ opacity: 0 }"
    :animate="{ opacity: 1 }"
    :transition="{ duration: 0.4, delay: 0.25 }"
  >
    <header class="fixed top-0 z-10 w-full py-8">
      <div class="container flex min-h-[60px] items-center overflow-x-hidden">
        <Presence>
          <Motion
            v-show="!show"
            :initial="{ opacity: 0 }"
            :animate="{ opacity: 1 }"
            :exit="{ opacity: 0 }"
          >
            <img src="/logo.svg" alt="canel street market logo" />
          </Motion>
        </Presence>
        <div class="flex-1"></div>
        <div class="relative h-8 w-8 lg:hidden">
          <Presence>
            <Motion
              v-if="show"
              :initial="{ x: -30, opacity: 0 }"
              :animate="{ x: 0, opacity: 1 }"
              :exit="{ x: -30, opacity: 0 }"
              :transition="{ duration: 0.25, easing: 'ease-in-out' }"
              class="absolute h-full w-full"
            >
              <button class="h-full w-full" @click="show = false">
                <span class="block h-[1px] w-full rotate-45 bg-black"></span>
                <span class="block h-[1px] w-full -rotate-45 bg-black"></span>
              </button>
            </Motion>
            <Motion
              v-else
              :initial="{ x: 30, opacity: 0 }"
              :animate="{ x: 0, opacity: 1 }"
              :exit="{ x: 30, opacity: 0 }"
              :transition="{ duration: 0.25, easing: 'ease-in-out' }"
              class="absolute h-full w-full"
            >
              <button class="h-full w-full space-y-2.5" @click="show = true">
                <span class="block h-[1px] w-full bg-black"></span>
                <span class="block h-[1px] w-full bg-black"></span>
                <span class="block h-[1px] w-full bg-black"></span>
              </button>
            </Motion>
          </Presence>
        </div>

        <Teleport to="body">
          <Transition name="list">
            <div v-show="show" class="absolute top-0 z-10 w-full">
              <ul class="grid grid-cols-2">
                <li
                  v-for="(item, i) in items"
                  :key="item.title"
                  :style="{ backgroundColor: item.color, '--i': i }"
                  class="item flex h-[43vh] items-center justify-center"
                >
                  <span
                    class="text-xl font-semibold tracking-wider"
                    :style="{ rotate: item.rotate }"
                  >
                    {{ item.title[0].toUpperCase() + item.title.slice(1) }}
                  </span>
                </li>
                <li
                  :style="{ '--i': items.length }"
                  class="item col-span-2 h-[40vh] bg-white"
                >
                  <div>
                    <p
                      class="mx-8 mt-6 border border-zinc-800 py-4 text-center font-semibold tracking-wider"
                    >
                      become a ventor
                    </p>
                  </div>
                </li>
              </ul>
            </div>
          </Transition>
        </Teleport>
      </div>
    </header>

    <Presence>
      <Motion
        v-show="!show"
        tag="main"
        :initial="false"
        :animate="{ opacity: 1 }"
        :exit="{ opacity: 0, transition: { duration: 0, delay: 1 } }"
        class="pt-32"
      >
        <slot />
      </Motion>
    </Presence>
  </Motion>
</template>

<style scoped>
.list-enter-active,
.list-leave-active,
.list-enter-active .item,
.list-leave-active .item {
  transition: all 1.6s cubic-bezier(0.4, 0, 0.2, 1);
}

.list-enter-active .item,
.list-leave-active .item {
  transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);
}

.list-enter-active .item {
  transition-delay: calc(0.15s * var(--i));
}

.list-enter-from .item,
.list-leave-to .item {
  opacity: 0;
}
</style>
