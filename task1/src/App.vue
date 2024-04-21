<template>
  <div id="app">
    <h1>Форма создания клиента</h1>
    <div class="content">
      <RegisterForm />
    </div>
  </div>
</template>

<script>
import RegisterForm from "@/components/RegisterForm.vue";
export default {
  name: "app",
  components: {
    RegisterForm,
  }
};
</script>

<style>
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  background: #B9ACA2;
  margin-top: 60px;
}

.content {
  padding: 5px 25% 0;
}

h1 {
  text-align: center;
  padding-bottom: 25px;
  margin-left: 90px;
  margin-right: 90px;
}
</style>
