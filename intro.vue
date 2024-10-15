<template>
    <div id="app">
        <h1>Bonjour</h1>

        <input v-model="name" type="text" :class="{'input_error': name_error}" placeholder="votre nom">
        <input v-model="age" type="text" placeholder="age">
        <button @click="add_person" >add</button>

        <p v-if="name === 'bob'"> Saisie : {{ name }} </p>

        <p v-for="i in tab">
            {{ i }}
        </p>

        <div class="person" v-for="(person, ind) in persons">
            <span class="title">Le nom est : </span> {{ person.name }} {{ ind }}
            <button @click="del_person(ind)"><span>&#10006;</span></button>
        </div>
        <button @click="test">Test</button>

        <h2>Adults</h2>
        <div class="person" v-for="(person, ind) in adults">
            <span class="title">Le nom est : </span> {{ person.name }} {{ ind }}
            <button @click="del_person(ind)"><span>&#10006;</span></button>
        </div>

    </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const txt = ref("Default");
const tab = ref([1, 2, 3, 4, 5]);

const name_error = ref(false)

const del_person = (ind) => {
    console.log(ind)
    persons.value.splice(ind,1);
}

const persons = ref([
    { name: "John", age: 12 },
    { name: "Marta", age: 20 }
])

const compt_test = computed( () => {
    return name + "test" + age;
})

const adults = computed( () => {
    console.log("adult computed");
    window.per = persons;
    return persons.value.filter( (p) => p.age >= 18);
})

const add_person = () => {
    console.log(`name : {name.value}`)
    if( name.value === "" || age.value === ""){
        name_error.value = name.value === ""
        return
    }

    persons.value.push({name:name.value, age:age.value})
    name.value = "";
    age.value = "";
}

const name = ref("");
const age = ref("")

const test = () => { txt.value = "Nouveau texte" };



</script>

<style scoped>
.title{
    color: blue;
}

.person{
    height: 40px;
    padding: 5px;
}

.input_error{
    border: 2px solid red;
}
</style>
