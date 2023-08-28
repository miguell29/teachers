<template>
    <section>
        <h3>Añadir profesor</h3>
            <label for="name">Nombre</label>
            <input type="text" name="name" id="name" v-model="teacher.teacherName">
            <label for="surname">Apellidos</label>
            <input type="text" name="surname" id="surname" v-model="teacher.surname">
            <label for="dni">Dni</label>
            <input type="text" name="dni" id="dni" v-model="teacher.dni">
            <label for="materias">Materias</label> 
            <input type="text" name="materias" id="materias" v-model="materia"> <button @click="handleMaterias">Agregar Materia</button>
            <h4>materias agregadas:</h4>
            <ul>
                <li v-for="(item, index) in teacher.materias" :key="index">{{ item }}</li>
            </ul>
            <input type="checkbox" v-model="teacher.Documentacion">Documentacion Entregada
            <button @click="handleTeachers">Agregar Profesor</button>
    </section>
    <section>
        <h3>Listado de Profesores</h3>
        <table v-if="teachers">
            <thead>
                <tr>
                    <th>Nombre</th>
                    <th>Apellidos</th>
                    <th>Dni</th>
                    <th>Materias</th>
                    <th>Documentacion</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(item, index) in teachers" :key="index">
                    <td>{{ item.teacherName }}</td>
                    <td>{{ item.surname }}</td>
                    <td>{{ item.dni }}</td>
                    <td>
                        <ul>
                            <li v-for="(materia, index) in item.materias" :key="index">{{ materia }}</li>
                        </ul>
                    </td>
                    <td v-if="item.Documentacion">Entregado</td>
                    <td v-else >No entregado</td>
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
</script>

<style scope>

</style>