<template>
  <div class="list-item">
    <div class="list-item-label">
      {{ label }}
    </div>
    <button class="button minus-button" :class="{'button--disabled': minusDisabled }" @click="minus">
      <PhMinusCircle :size="32" :color="minusDisabled ? '#888888' : '#000'" weight="fill" />
    </button>
    <div class="count">
      {{ count }}
    </div>
    <button class="button add-button" @click="add" :class="{'button--disabled': addDisabled }">
      <PhPlusCircle :size="32" :color="addDisabled ? '#888888' : '#000'" weight="fill" />
    </button>
  </div>
</template>
<script setup>
import { ref, computed } from 'vue'
import { PhPlusCircle, PhMinusCircle } from "@phosphor-icons/vue"
const props = defineProps({
  label: {
    type: String,
    default: ''
  },
  addDisabled: {
    type: Boolean,
    default: false
  }
})

const count = defineModel({ default: 0 })

const add = () => {
  if (!props.addDisabled)
    count.value++
}

const minus = () => {
  if (count.value > 0)
    count.value-- 
}

const minusDisabled = computed(() => count.value === 0)

</script>
<style lang="scss" scoped>
.list-item {
  display: flex;
  margin-bottom: 6px;
  justify-content: center;
  align-items: center;
  &:last-child {
    margin-bottom: 0;
  }
  &-label {
    padding: 2px 16px;
  }
  .count {
    font-size: 18px;
    padding: 0 4px;
  }
  .button {
    background-color: transparent;
    padding: 0;
    width: 32px;
    height: 32px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    box-sizing: border-box;
    border: none;
    &--disabled {
      cursor: not-allowed;
    }
  }
}
</style>