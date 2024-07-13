<template>
  <main>
    <div class="list no-select">
      <ListItem v-model="aldult" label="大人" :add-disabled="addDisabled"></ListItem>
      <ListItem v-model="child" label="小孩" :add-disabled="addDisabled || aldult === 0"></ListItem>
      <ListItem v-model="baby" label="嬰兒" :add-disabled="babyAddDisabled"></ListItem>
    </div>
  </main>
</template>
<script setup>
import { computed, ref, watch } from "vue";
import ListItem from "./components/list-item.vue";
const aldult = ref(0)
const child = ref(0)
const baby = ref(0)
const limit = 9

const addDisabled = computed(() => {
  return aldult.value + child.value + baby.value >= limit
})

const babyAddDisabled = computed(() => {
  return addDisabled.value || aldult === 0 || baby.value >= aldult.value
})

watch(aldult, (newVal, oldVal) => {
  if ((newVal < oldVal) && newVal < baby.value) {
    baby.value--
  }
  if (newVal === 0) {
    child.value = 0
    baby.value = 0
  }
})

</script>
<style lang="scss" scoped>
.list {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
</style>
