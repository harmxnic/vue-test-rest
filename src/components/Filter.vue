<template>
  <div class="filter">
    <select
        v-model="modelValue"
        @change="changedSort"
        class="filter__select"
    >
      <option disabled value="">Choose filter</option>
      <option
          v-for="option in sortOptions"
          :key="option.value"
          :value="option.value"
      >
        {{ option.name }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "Filter",
  props: {
    modelValue: {
      type: String
    },
    sortOptions: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    changedSort(event) {
      this.$emit('update:modelValue', event.target.value)
    }
  }
}
</script>

<style lang="scss" scoped>
  .filter {
    &__select {
      width: 15rem;
      padding: 10px;
      box-sizing: border-box;
    }
  }
</style>