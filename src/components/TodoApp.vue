<template lang="">
    <div>
        <h1 class="title">Todo App</h1>
        <h2 class="sub-title">Desarrollado por: <span class="nombre"> Jhord Cristian Huaccho Huaman </span></h2>
        <img src="../assets/logo.png">
        <div class="container" style="width:650px;">
            <div class="d-flex mt-4">
                <input type="text" v-model="tarea" placeholder="Ingrese la tarea" class="form-control text-center">
                <button @click="createOrUpdate" class="btn btn-warning text-buttom">{{ tareaUpdate ? "Actualizar" : "Crear" }}</button>
             </div>
             <div class="table-responsive">
                <table class="table table-dark table-hover align-middle mt-2">
                    <thead>
                        <tr class="headers">
                            <th>Tarea</th>
                            <th>Estado</th>
                            <th>Editar</th>
                            <th>Eliminar</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr class="" v-for="tarea in tareas" :key="tarea.id">
                            <td><span :class="{
                                'text-decoration-line-through text-secondary': tarea.estado === 'Culminado',
                            }">{{ tarea.nombre }}</span></td>
                            <td><span class="estado" @click="cambiarEstado(tarea)" :class="{
                                    'text-danger': tarea.estado === 'Por realizar',
                                    'text-success': tarea.estado === 'En proceso',
                                    'text-secondary': tarea.estado === 'Culminado'
                                    }">
                                {{ tarea.estado }}
                                </span> </td>
                            <td><button @click="actualizarTarea(tarea)" class="btn btn-success text-buttom">Editar</button></td>
                            <td><button @click="eliminarTarea(tarea)" class="btn btn-danger text-buttom">Eliminar</button></td>
                        </tr>
                    </tbody>
                </table>
             </div>
             
        </div>
    </div>
</template>
<script>
let count = 1;
export default {

    data(){
        return{
            tarea: '',
            tareaUpdate: null,
            tareas: [
                { id: count++, nombre: "Aprender Vue", estado: "Por realizar"},
                { id: count++, nombre: "Aprender PHP", estado: "En proceso"},
                { id: count++, nombre: "Aprender Laravel", estado: "Culminado"}
            ]
        }
    },
    methods: {
        agregarTarea(){
            if(this.tarea.trim() === ''){
            alert('Ingrese una tarea');
            }else{
                let nuevaTarea = { id: count++, nombre: this.tarea, estado: "Por realizar" }
                this.tareas.push(nuevaTarea);
                this.tarea = ''
            }
        },
        eliminarTarea(tarea){
            const result = this.tareas.filter((iteracion) => iteracion !== tarea);
            this.tareas = result;
        },
        actualizarTarea(tarea){
            this.tareaUpdate = tarea;
            this.tarea = this.tareaUpdate.nombre;
        },
        createOrUpdate(){
            if (this.tareaUpdate) {
                if(this.tarea.trim() === ''){
                alert('Ingrese una tarea');
                }else{
                    this.tareaUpdate.nombre = this.tarea;
                    this.tarea = ''
                    this.tareaUpdate = null;
                }
            } else {
                this.agregarTarea()
            }
        },
        cambiarEstado(tarea){
            if (tarea.estado === "Por realizar") {
                tarea.estado = "En proceso";
            }else if(tarea.estado === "En proceso"){
                tarea.estado = "Culminado";
            }else{
                tarea.estado = "Por realizar";
            }
        }
    }
}
</script>
<style scoped>

</style>