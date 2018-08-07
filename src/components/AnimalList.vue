<template>
  <div>

      <form @submit.prevent >
        <label>Species</label>
        <input v-model="newAnimal.species" type="text" placeholder="species" > <br>
        <label>Name</label>
        <input v-model="newAnimal.name" type="text" placeholder="name"> <br>
        <label>Date of birth</label>
        <input v-model="newAnimal.dateOfBirth" type="text" placeholder="dateOfBirth"> <br>
        <button @click="addAnimal">Add animal</button> <br> <br>
      </form>

      <table border=1 align="center">
        <thead>
          <th>Species</th>
          <th>Name</th>
          <th>Date of Birth</th>
          <!-- <th></th>
          <th></th> -->
        </thead>
        <tbody>
          <tr v-for="(animal,index) in animals" :key="index" >            
            <td> {{animal.species}} </td>
            <td> {{animal.name}} </td>
            <td v-if= "animal.dateOfBirth"> {{animal.dateOfBirth}} </td>
            <td v-else> {{ nonexistent }} </td>
            <th> <button @click="removeAnimal(animal)"> Remove</button> </th>
            <th v-if="animals.indexOf(animal) !== 0"> 
              <button @click="moveToTopAnimal(animal)"> Move to top</button> 
            </th>
            <!-- <th v-else></th> -->
          </tr>
        </tbody>
      </table>
   
  </div>
</template>

<script>
export default {
  name: 'AnimalList',
  data() {
    return {
      nonexistent: "Unknown",
      animals: [
        {species: "Horse", name: "Zelenko", dateOfBirth: "09/01/1995"},
        {species: "Pig", name: "Gile", dateOfBirth: "20/10/2004"},
        {species: "Ruster", name: "Zvonko", dateOfBirth: "20/07/2011"},
        {species: "Mouse", name: "Gricko", dateOfBirth: "30/04/2015"},
        {species: "Zebra", name: "Zaza", dateOfBirth: "22/11/2008"},
        {species: "Test", name: "Zivotinja", dateOfBirth: ""},
      ],
      newAnimal: {}      
    };
  },
  methods: {
    removeAnimal(animal){
      // console.log(this.animals.indexOf(animal));
      let indexOfAnimal = this.animals.indexOf(animal);
      this.animals.splice(indexOfAnimal, 1);
    },

    moveToTopAnimal(animal){
      this.removeAnimal(animal);
      this.animals.unshift(animal);
      
    },

    addAnimal(){
      // console.log(this.newAnimal);
      this.animals.push(this.newAnimal);
      this.newAnimal = {};
    },

  },
}
</script>

