<template lang="">
  <div>
    <div class="container" style="max-width: 600px">
      <h1>Task App</h1>
      <img src="../assets/logo.png" alt="">
      <form @submit.prevent="submitForm">
        <div class="d-flex mt-5">
          <input type="text" v-model="task" class="text-center mb-3 form-control" placeholder="Ingresa la tarea" >
          <button class="btn btn-primary" style="height: 38px;">{{ editTask ? 'Actualizar' : 'Agregar' }}</button>
        </div>
      </form>
   
      <table class="table table-bordered">
        <thead>
          <tr>
            <th scope="col">Tarea</th>
            <th scope="col">Estado</th>
            <th scope="col">Editar</th>
            <th scope="col">Eliminar</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="tarea in tasks" :key="tarea.id">
            <td><span :class="tarea.status === 'finished' ? 'text-decoration-line-through' : ''">{{ tarea.name }}</span></td>
            <td><span
              @click="changeColor(tarea.id)"
             :class="{
              'text-danger': tarea.status === 'finished',
              'text-success': tarea.status === 'to-do',
              'text-primary': tarea.status === 'in-progess'
              }">{{ tarea.status }}</span></td>
            <td>
              <button class="btn btn-success" @click="editarTarea(tarea)">Editar</button>
            </td>
            <td>
              <button class="btn btn-danger" @click="eliminarTarea(tarea.id)">Eliminar</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
  
<script>
export default {
  name: 'TareaComponente',
  data() {
    return {
      task: '',
      editTask: null,
      tasks: [
        {
          id: 1,
          name: "Testing task 1",
          status: "to-do"
        },
        {
          id: 2,
          name: "Testing task 2",
          status: "in-progess"
        },
        {
          id: 3,
          name: "Testing task 3",
          status: "finished"
        },
      ]
    };
  },
  methods: {
    changeColor(index) {
      let tarea = this.tasks.find(tarea => tarea.id === index);
      if (tarea.status === "to-do") {
        tarea.status = "in-progess";
      } else if (tarea.status === "in-progess") {
        tarea.status = "finished";
      } else {
        tarea.status = "to-do";
      }
      console.log("cambio de color " + index);
    },
    agregarTarea() {
      if (this.task.trim() === '') {
        alert("No puede agregar una tarea vacía");
      } else {
        let nuevaTarea = {
          id: this.tasks.length + 1,
          name: this.task,
          status: "to-do"
        };
        this.tasks.push(nuevaTarea);
        this.task = '';
      }
    },
    eliminarTarea(tarea_id) {
      this.tasks = this.tasks.filter(tarea => tarea.id !== tarea_id);
      console.log("Tarea eliminada: " + tarea_id);
    },
    editarTarea(tarea) {
      this.task = tarea.name;
      this.editTask = tarea;
    },
    submitForm() {
      if (this.editTask) {
        this.editTask.name = this.task;
        this.editTask = null;
      } else {
        this.agregarTarea();
      }
      this.task = '';
    }
  }
}
</script>
  <style lang="">

  </style>
  