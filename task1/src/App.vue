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

<style lang="sass">
body
  font-family: Avenir, Helvetica, Arial, sans-serif
  color: #2c3e50
  background: #B9ACA2
  margin-top: 60px


.content
  padding: 0 15% 0


h1
  text-align: center
  padding-bottom: 25px
  margin-left: 90px
  margin-right: 90px


@media (max-width: 1500px)
  .content
    padding: 5px 13% 0

@media (max-width: 1190px)
  .content
    padding: 5px 12% 0

@media (max-width: 900px)
  .content
    padding: 5px 8% 0

@media (max-width: 750px)
  .content
    padding: 5px 3% 0
  h1
    margin-left: 80px
    margin-right: 80px

@media (max-width: 600px)
  .content
    padding: 5px 1% 0
  h1
    margin-left: 40px
    margin-right: 40px

@media (max-width: 550px)
  h1
    margin-left: 10px
    margin-right: 10px


@media (max-width: 450px)
  .content
    padding: 5px 0.5% 0


</style>
