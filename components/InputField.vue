<template>
  <div class="form-control mb-4">
    <label :for="name" class="text-gray-700">{{ label }}:</label>
    <input
      :class="{
        'border-red-500': submitted && !inputValue,
        'border-gray-300': !submitted || inputValue
      }"
      :type="type"
      :id="name"
      :value="inputValue"
      @input="updateInputValue($event.target.value)"
      :required="isRequired"
      class="w-full px-4 py-2 border border-gray-300 rounded focus:outline-none focus:border-green-500"
    />
    <span
      v-if="submitted && !inputValue"
      class="text-red-500 text-sm"
    >
      {{ requiredMessage }}
    </span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputValue: this.value,
    };
  },
  props: {
    name: {
      type: String,
      required: true,
    },
    label: {
      type: String,
      required: true,
    },
    value: {
      type: [String, Number],
      default: '',
      sync: true,
    },
    submitted: {
      type: Boolean,
      default: false,
    },
    requiredMessage: {
      type: String,
      default: 'This field is required',
    },
    type: {
      type: String,
      default: 'text',
    },
    isRequired: {
      type: Boolean,
      default: false,
    },
  },
  watch: {
    value(newValue) {
      this.inputValue = newValue;
    },
  },
  methods: {
    updateInputValue(value) {
      this.inputValue = value;
      this.$emit('update:value', value);
    },
  },
};
</script>
