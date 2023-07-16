<template>
  <div>
    <Navbar :showSearch="false" />
    <h1 class="text-2xl font-semibold my-4 text-center">New Cat Data</h1>
    <form @submit.prevent="saveCat" class="max-w-md m-4 md:mx-auto">
      <input-field
        name="name"
        label="Name"
        :value.sync="cat.name"
        :submitted="submitted"
        required-message="Name is required"
      />
      <input-field
        name="age"
        type="number"
        label="Age"
        :value.sync="cat.age"
        :submitted="submitted"
        required-message="Age is required"
      />
      <input-field
        name="breed"
        label="Breed"
        :value.sync="cat.breed"
        :submitted="submitted"
        required-message="Breed is required"
      />
      <input-field
        name="color"
        label="Color"
        :value.sync="cat.color"
        :submitted="submitted"
        required-message="Color is required"
      />
      <InputFile
        name="image1"
        label="Image 1"
        :value.sync="cat.images[0]"
        :submitted="submitted"
        required-message="Image 1 is required"
        :index="0"
      />
      <InputFile
        name="image2"
        label="Image 2"
        :value.sync="cat.images[1]"
        :submitted="submitted"
        required-message="Image 2 is required"
        :index="1"
      />
      <button type="submit" class="px-6 py-2 w-full bg-green-500 text-white rounded hover:bg-green-600 focus:outline-none">Save</button>
    </form>
  </div>
</template>

<script>
import Navbar from '@/components/Navbar.vue';
import InputField from '@/components/InputField.vue';
import InputFile from '@/components/InputFile.vue';

export default {
  name: 'CreateCatPage',
  components: {
    Navbar,
    InputField,
    InputFile,
  },
  data() {
    return {
      cat: {
        name: '',
        age: null,
        breed: '',
        color: '',
        images: [null, null],
      },
      submitted: false,
      formErrors: [],
    };
  },
  methods: {
    saveCat() {
      if (!this.validateForm()) {
        this.submitted = true;
        return;
      }

      const formData = new FormData();
      formData.append('name', this.cat.name);
      formData.append('age', this.cat.age);
      formData.append('breed', this.cat.breed);
      formData.append('color', this.cat.color);
      this.cat.images.forEach((image, index) => {
        if (image) {
          formData.append(`images[${index}]`, image);
        }
      });

      this.$axios
        .$post('https://developer.redcomm.co.id/test/fe/test-api/api/cats/create', formData, {
          headers: {
            'Content-Type': 'multipart/form-data',
          },
        })
        .then((response) => {
          console.log('Cat saved:', response.data);
          this.$router.push('/');
        })
        .catch((error) => {
          console.error('Failed to save cat:', error);
        });
    },
    validateForm() {
      const errors = [];

      if (!this.cat.name) {
        errors.push('Name is required');
      }

      if (!this.cat.age) {
        errors.push('Age is required');
      }

      if (!this.cat.breed) {
        errors.push('Breed is required');
      }

      if (!this.cat.color) {
        errors.push('Color is required');
      }

      if (!this.cat.images[0]) {
        errors.push('Image 1 is required');
      }

      if (!this.cat.images[1]) {
        errors.push('Image 2 is required');
      }

      this.cat.images.forEach((image, index) => {
        if (image) {
          const fileSizeInMB = image.size / (1024 * 1024);
          if (fileSizeInMB > 2) {
            errors.push(`Image ${index + 1} size should be maximum 2MB`);
          }
        }
      });

      if (errors.length > 0) {
        this.formErrors = errors;
        return false;
      }

      this.formErrors = [];
      return true;
    },
    handleImageChange(event, index) {
      const file = event.target.files[0];
      if (file) {
        this.cat.images[index] = file.name;
      }
    },
  },
};
</script>

<style scoped>
</style>
