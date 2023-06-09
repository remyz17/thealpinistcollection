<script setup>
import { Menu, MenuButton, MenuItem, MenuItems } from "@headlessui/vue"
import { ChevronDownIcon } from "@heroicons/vue/solid"

const props = defineProps({
  label: {
    type: String,
    default: "Sort",
  },
  options: Array,
  current: Object,
})
const emit = defineEmits(["onChange"])

const onClick = (option) => {
  emit("onChange", option)
}
</script>

<template>
  <Menu as="div" class="relative inline-block text-left">
    <div>
      <MenuButton
        class="group inline-flex justify-center text-sm font-medium text-white hover:text-neutral-300"
      >
        {{ props.label }}
        <ChevronDownIcon
          class="-mr-1 ml-1 h-5 w-5 flex-shrink-0 text-white group-hover:text-neutral-300"
          aria-hidden="true"
        />
      </MenuButton>
    </div>

    <transition
      enter-active-class="transition ease-out duration-100"
      enter-from-class="transform opacity-0 scale-95"
      enter-to-class="transform opacity-100 scale-100"
      leave-active-class="transition ease-in duration-75"
      leave-from-class="transform opacity-100 scale-100"
      leave-to-class="transform opacity-0 scale-95"
    >
      <MenuItems
        class="absolute right-0 z-10 mt-2 w-40 origin-top-right rounded-md bg-neutral-800 shadow-2xl ring-1 ring-black ring-opacity-5 focus:outline-none"
      >
        <div class="py-1">
          <MenuItem
            v-for="option in props.options"
            :key="option.id"
            v-slot="{ active }"
          >
            <a
              :class="[
                option.id == props.current.id
                  ? 'font-medium text-primary'
                  : 'text-white',
                active ? 'bg-neutral-700' : '',
                'block px-4 py-2 text-sm hover:cursor-pointer',
              ]"
              @click="onClick(option)"
              >{{ option.name }}</a
            >
          </MenuItem>
        </div>
      </MenuItems>
    </transition>
  </Menu>
</template>
