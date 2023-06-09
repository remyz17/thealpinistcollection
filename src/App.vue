<script setup>
import { computed, onBeforeMount, onMounted } from "vue"
import { useRoute } from "vue-router"
import VBanner from "./components/VBanner.vue"
import VModal from "./components/VModal.vue"
import VNoficiations from "./components/VNotifications.vue"
import VTransitionFade from "./components/VTransitionFade.vue"
import Footer from "./layouts/Footer.vue"
import Header from "./layouts/Header.vue"
import { useAuthUserStore } from "./stores/auth"
import { useSettingsStore } from "./stores/settings"

const store = useAuthUserStore()
const settings = useSettingsStore()
const route = useRoute()

const isHome = computed(() => route.path == "/")

onBeforeMount(() => {
  store.fetchUser()
})

onMounted(() => settings.fetch())
</script>

<template>
  <div class="flex flex-col h-full min-h-screen bg-neutral-900 z-20">
    <Header class="z-20" />
    <main class="flex-grow relative z-0">
      <VTransitionFade>
        <div
          v-if="!isHome"
          class="absolute inset-x-0 -top-16 -z-10 flex transform-gpu justify-center overflow-hidden blur-3xl"
          aria-hidden="true"
        >
          <div
            class="aspect-[1318/752] w-[82.375rem] flex-none bg-gradient-to-r from-[#80caff] to-primary opacity-25"
            style="
              clip-path: polygon(
                73.6% 51.7%,
                91.7% 11.8%,
                100% 46.4%,
                97.4% 82.2%,
                92.5% 84.9%,
                75.7% 64%,
                55.3% 47.5%,
                46.5% 49.4%,
                45% 62.9%,
                50.3% 87.2%,
                21.3% 64.1%,
                0.1% 100%,
                5.4% 51.1%,
                21.4% 63.9%,
                58.9% 0.2%,
                73.6% 51.7%
              );
            "
          />
        </div>
      </VTransitionFade>
      <router-view v-slot="{ Component }">
        <VTransitionFade>
          <component :is="Component" class="z-0" />
        </VTransitionFade>
      </router-view>
    </main>
    <Footer />
  </div>
  <teleport to="body">
    <VNoficiations />
    <VModal />
    <VBanner />
  </teleport>
</template>
