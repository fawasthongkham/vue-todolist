<template>
  <button class="px-4 py-2 text-white rounded-md" :class="btnColor()">
    {{ props.buttonName }}
  </button>
</template>

<script setup>
const props = defineProps({
  buttonName: {
    type: String,
    default: 'button'
  },
  buttonClass: {
    type: String,
    default: 'bg-red-100'
  },
  btnColor: {
    type: String
  }
})

const btnColor = () => {
  if (props.btnColor === 'primary') {
    return 'bg-blue-500 hover:bg-blue-600'
  } else if (props.btnColor === 'warning') {
    return 'bg-yellow-500 hover:bg-yellow-600'
  } else if (props.btnColor === 'success') {
    return 'bg-green-500 hover:bg-green-600'
  }
}
</script>

<style lang="scss" scoped></style>
