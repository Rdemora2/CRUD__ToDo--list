<template>
    <div class="container mt-2">
      <formAddTask/>
    </div>
</template>

<script>
import formAddTask from "../components/formAddTask.vue"

export default {
  name: "Form",

  components: {
    formAddTask,
  }
}
</script>

<style>
  .container{
    height: calc(100vh - 64px);
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    padding-top: 30px;
  }
</style>