<template>
  <div>
    <div v-for="(item, idx) in list" :key="idx">
      <h2>
        <button
          @click="openOrClose(item)"
          type="button"
          class="flex w-full items-center justify-between border border-gray-200 bg-white p-5 text-left font-medium text-gray-500 hover:bg-gray-100"
          :class="{
            'rounded-t-xl': idx === 0,
            'border-b-0': questionBorder(idx, item, items),
            'bg-gray-100': item.open,
          }"
        >
          <span>{{ item.title }}</span>
          <Icon name="mdi:chevron-down" />
        </button>
      </h2>

      <div class="bg-white" :class="{ hidden: !item.open }">
        <div
          class="border border-t-0 border-gray-200 p-5"
          :class="{
            'border-b-0': idx < list.length - 1,
          }"
        >
          <p class="text-gray-500">{{ item.text }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  items: {
    Array,
  },
});

const list = ref(
  props.items.map((item) => {
    return { ...item, open: false };
  })
);

function openOrClose(item) {
  item.open = !item.open;
}

function questionBorder(idx, item, items) {
  if (idx < items.length - 1 && !item.open) return true;
}
</script>
