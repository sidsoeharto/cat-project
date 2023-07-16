<template>
  <div class="form-control mb-4">
    <label :for="name" class="text-gray-700">{{ label }}:</label>
    <input
      :class="{
        'border-red-500': submitted && !value,
        'border-gray-300': !submitted || value
      }"
      :type="type"
      accept="image/png, image/jpeg"
      :value="file?.name"
      :id="name"
      @change="handleFileChange($event)"
      :required="isRequired"
      class="w-full px-4 py-2 border border-gray-300 rounded focus:outline-none focus:border-green-500"
    />
    <span v-if="submitted && !value" class="text-red-500 text-sm">
      {{ requiredMessage }}
    </span>
    <span v-if="fileSizeError" class="text-red-500 text-sm">
      {{ fileSizeErrorMessage }}
    </span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      file: null,
      fileSizeError: false,
      fileSizeErrorMessage: 'File size should be maximum 2MB',
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
      default: null,
      required: true,
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
      default: 'file',
    },
    isRequired: {
      type: Boolean,
      default: false,
    },
    index: {
      type: Number,
      required: true,
    },
  },
  methods: {
    handleFileChange(event) {
      const file = event.target.files[0];
      if (file) {
        const fileSizeInMB = file.size / (1024 * 1024);
        if (fileSizeInMB > 2) {
          this.fileSizeError = true;
        } else {
          this.fileSizeError = false;
          this.$emit('update:value', file, this.index);
        }
      }
    },
  },
};
</script>
