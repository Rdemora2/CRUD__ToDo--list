<template>
    <div class="container mt-2" v-if="tasks.length != 0">
      <div v-for="(task, index) in tasks" :key="index">
        <b-card :title="task.subject" class="mb-2" id="card1">
          <b-card-text>{{ task.description }}</b-card-text>

          <b-button variant="outline-secondary" class="mr-2" @click="edit(index)"> Editar </b-button>
          <b-button variant="outline-danger" class="mr-2" @click="remove(task, index)"> Excluir </b-button>
        </b-card>
      </div>

      <b-modal ref="modalRemove" hide-footer title="Exclusão de tarefa">
        <div class="d-block text-center">
          <p>Deseja realmente excluir essa tarefa?</p>
          <p>Tarefa: {{ taskSelected.subject }}</p>
        </div>
        <div class="mt-3 d-flex justify-content-end">
          <b-button variant="outline-secondary" class="mr-2" @click="hideModal"> Cancelar </b-button>
          <b-button variant="outline-danger" class="mr-2" @click="confirmRemoveTask"> Excluir </b-button>
        </div> 
      </b-modal>
    </div>
    <div class="container mt-2 alinhar" v-else>
      <b-card class="mb-2" id="card1">
        <b-card-text>Pô, vc ainda não criou nenhuma task....</b-card-text>
        <b-card-text>Bora criar uma?</b-card-text>
        <b-button variant="outline-danger" class="mr-2" to="/form">É só clicar aqui!</b-button>
      </b-card>
    </div>
</template>
    
    <script>
    export default {
      name: "List",
    
      data() {
        return {
          tasks: [],
          taskSelected: []
        }
      },
    
      created() {
        this.tasks = (localStorage.getItem("tasks")) ? JSON.parse(localStorage.getItem("tasks")) : [];
      },
    
      methods: {
        edit(index) {
          this.$router.push({ name: "form", params: { index } });
        },
    
        remove(task, index) { 
          this.taskSelected = task;
          this.taskSelected.index = index;
          this.$refs.modalRemove.show();
        },
    
        hideModal() {
          this.$refs.modalRemove.hide();
        },
    
        confirmRemoveTask() {
          this.tasks.splice(this.taskSelected.index, 1);
          localStorage.setItem("tasks", JSON.stringify(this.tasks));
          this.hideModal();
        }
      }
    }
    </script>
    
    <style>
      #card1{
      background-color: #342432;
      border-radius: 20px;
      color: rgb(219, 209, 209);
      box-shadow: -1px 1px 11px 1px rgba(0,0,0,0.36);
      -webkit-box-shadow: -1px 1px 11px 1px rgba(0,0,0,0.36);
      }
      .alinhar{
        height: calc(100vh - 64px) !important;
        width: 100vh !important;
        display: flex !important;
        justify-content: flex-start !important;
        align-items: center !important;
      }
    </style>