<template>
    <div class="p-3" :class="{'text-bg-dark bg-gradient':darkMode}">
        <section class="container">
        <div class="mode fixed-top p-5">
            <button @click="handleMode" class="bg-transparent h4" :class="{'text-light':darkMode}">
                <i v-if="darkMode" class="bi bi-moon-stars-fill"></i>
                <i v-else class="bi bi-brightness-high-fill"></i>
            </button>
        </div>
        <h3>Añadir profesor</h3>
        <section class="m-5">
            <div>
                <label class="form-label" for="name">Nombre</label>
                <input class="form-control" type="text" required name="name" id="name" v-model="teacher.teacherName" :class="{'text-danger border-bottom border-danger bg-transparent':darkMode}">
            </div>
            <div>
                <label class="form-label" for="surname">Apellidos</label>
            <input class="form-control" type="text" required name="surname" id="surname" v-model="teacher.surname" :class="{'text-danger border-bottom border-danger bg-transparent':darkMode}">
            </div>
            <div>
                <label class="form-label" for="dni">Dni</label>
                <input class="form-control" type="text" required name="dni" id="dni" v-model="teacher.dni" :class="{'text-danger border-bottom border-danger bg-transparent':darkMode}">
            </div>
            <div>
                <label class="form-label" for="materias">Materias</label> 
                <input class="form-control mb-3" type="text" required name="materias" id="materias" v-model="materia" :class="{'text-danger border-bottom border-danger bg-transparent':darkMode}"> <button @click="handleMaterias" class="btn mb-3" :class="{'btn-outline-info':darkMode,'btn-info':!darkMode}"> <i class="bi bi-plus-circle"></i> Agregar Materia</button>
            </div>
            <h4 v-if="teacher.materias.length > 0">materias agregadas:</h4>
            <ul class="list-group">
                <li class="list-group-item" :class="{'list-group-item-action list-group-item-dark':darkMode}" v-for="(item, index) in teacher.materias" :key="index">{{ item }} <button @click="deleteMateria(index)" class="btn btn-secondary">Elminar</button></li>
            </ul>
            <div class="form-check">
                <input class="form-check-input" type="checkbox" v-model="teacher.Documentacion" id="doc">
                <label class="form-check-label" for="doc">Documentacion Entregada</label>
            </div>
            <button @click="handleTeachers" class="btn mt-3" :class="{'btn btn-outline-success':darkMode,'btn-success':!darkMode}"> <i class="bi bi-plus-circle"></i> Agregar Profesor</button>
        </section>
    </section>
    <section class="container mt-5">
        <h3 class="mb-5">Listado de Profesores</h3>
        <table v-if="teachers" class="table table-hover text-center" :class="{'table-dark':darkMode}">
            <thead>
                <tr>
                    <th scope="col">Nombre</th>
                    <th scope="col">Apellidos</th>
                    <th scope="col">Dni</th>
                    <th scope="col">Materias</th>
                    <th scope="col">Documentacion</th>
                    <th scope="col">Editar</th>
                    <th scope="col">Eliminar</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(item, index) in teachers" :key="item.dni">
                    <td>{{ item.teacherName }}</td>
                    <td>{{ item.surname }}</td>
                    <td>{{ item.dni }}</td>
                    <td>
                        <ul class="list-group">
                            <template  v-for="(materia, index) in item.materias" :key="index">
                                <li class="list-group-item" :class="{'list-group-item-action list-group-item-dark':darkMode}">{{ materia }}</li>
                            </template>   
                        </ul>
                    </td>
                    <td v-if="item.Documentacion">Entregado</td>
                    <td v-else >No entregado</td>
                    <td><button @click="editTeacher(index)" class="btn" :class="{'btn btn-outline-warning':darkMode,'btn-warning':!darkMode}"><i class="bi bi-pencil"></i></button></td>
                    <td><button @click="deleteTeacher(index)" class="btn" :class="{'btn btn-outline-danger':darkMode,'btn-danger':!darkMode}"><i class="bi bi-x-circle"></i></button></td>
                </tr>
            </tbody>
        </table>
    </section>
    </div>
    
</template>

<script lang="ts" setup>
    import {Ref,ref} from 'vue';
     
    interface Iteacher{
        teacherName : string,                       
        surname : string,
        dni : string,
        materias : Array<string>,
        Documentacion:boolean
    }
    let teacher:Ref<Iteacher> = ref({
        teacherName : '',
        surname : '',
        dni : '',
        materias : [],
        Documentacion : false
    })

    let teachers:Ref<Array<Iteacher>> = ref([]);
    let materia:Ref<string> = ref('');
    let darkMode:Ref<boolean> =ref(false);


    const handleMaterias = ():void=>{
        teacher.value.materias.push(materia.value);
        materia.value = '';
    }
    const handleTeachers = ():void=>{
        teachers.value.push(teacher.value);
        teacher.value = {
            teacherName : '',
            surname : '',
            dni : '',
            materias : [],
            Documentacion : false
        }
    }

    const deleteMateria = (indice: number): void => {
        teacher.value.materias.splice(indice, 1);
    }
    const deleteTeacher = (indice:number):void=>{
        teachers.value.splice(indice,1);
    }
    const editTeacher = (indice:number):void=>{
        teacher.value = teachers.value[indice];
        teachers.value.splice(indice,1);
    }
    const handleMode = ():void =>{
        darkMode.value = !darkMode.value
    }
</script>

<style scope>
.mode{
    display: flex;
    justify-content: flex-end;
}
div{
    margin: 0;
}
</style>