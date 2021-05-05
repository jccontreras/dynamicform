<template>
  <div class="home">
    <h1 style="color: #169c47;">My CV</h1>
    <my-form/>
  </div>
</template>

<script>
// @ is an alias to /src
import MyForm from '@/components/MyForm.vue';

export default {
  name: 'Home',
  components: {
    MyForm,
  },
};
</script>

<style>
.home {
  margin-top: 3em;
}
</style>
