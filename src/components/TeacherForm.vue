<template>
    <section class="container mt-3">
        <h3>Añadir profesor</h3>
        <section class="m-5">
            <div>
                <label class="form-label" for="name">Nombre</label>
                <input class="form-control" type="text" name="name" id="name" v-model="teacher.teacherName">
            </div>
            <div>
                <label class="form-label" for="surname">Apellidos</label>
            <input class="form-control" type="text" name="surname" id="surname" v-model="teacher.surname">
            </div>
            <div>
                <label class="form-label" for="dni">Dni</label>
                <input class="form-control" type="text" name="dni" id="dni" v-model="teacher.dni">
            </div>
            <div>
                <label class="form-label" for="materias">Materias</label> 
                <input class="form-control mb-3" type="text" name="materias" id="materias" v-model="materia"> <button @click="handleMaterias" class="btn btn-info mb-3">Agregar Materia</button>
            </div>
            <h4 v-if="teacher.materias.length > 0">materias agregadas:</h4>
            <ul class="list-group">
                <li class="list-group-item" v-for="(item, index) in teacher.materias" :key="index">{{ item }} <button @click="deleteMateria(index)" class="btn btn-secondary">Elminar</button></li>
            </ul>
            <div class="form-check">
                <input class="form-check-input" type="checkbox" v-model="teacher.Documentacion" id="doc">
                <label class="form-check-label" for="doc">Documentacion Entregada</label>
            </div>
            <button @click="handleTeachers" class="btn btn-success mt-3">Agregar Profesor</button>
        </section>
    </section>
    <section class="container mt-5">
        <h3 class="mb-5">Listado de Profesores</h3>
        <table v-if="teachers" class="table text-center">
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
                                <li class="list-group-item">{{ materia }}</li>
                            </template>   
                        </ul>
                    </td>
                    <td v-if="item.Documentacion">Entregado</td>
                    <td v-else >No entregado</td>
                    <td><button @click="editTeacher(index)" class="btn btn-warning">Editar</button></td>
                    <td><button @click="deleteTeacher(index)" class="btn btn-danger">Eliminar</button></td>
                </tr>
            </tbody>
        </table>
    </section>
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
</script>

<style scope>

</style>