<script setup>
import { CheckCircleIcon } from "@heroicons/vue/solid"
import VAlert from "./components/Alert.vue"

const props = defineProps({
  title: String,
  text: String,
})
</script>
<template>
  <VAlert
    :data="{
      title: props.title,
      text: props.text,
      bgColor: 'bg-green-500/10',
      ringColor: 'ring-green-500/20',
      iconColor: 'text-green-400',
      titleColor: 'text-green-400',
      textColor: 'text-green-400',
      icon: CheckCircleIcon,
    }"
  />
</template>
