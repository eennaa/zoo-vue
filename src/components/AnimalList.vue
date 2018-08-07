<template>
  <div>
      <table border=1 align="center">
        <thead>
          <th>Species</th>
          <th>Name</th>
          <th>Date of Birth</th>
          <th></th>
          <th></th>
        </thead>
        <tbody>
          <tr v-for="(animal,index) in animals" :key="index" >            
            <td> {{animal.species}} </td>
            <td> {{animal.name}} </td>
            <td v-if= "animal.dateOfBirth"> {{animal.dateOfBirth}} </td>
            <td v-else> {{ nonexistent }} </td>
            <th> <button @click="removeAnimal(animal)"> Remove</button> </th>
            <th> <button @click="moveToTopAnimal(animal)"> Move to top</button> </th>
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
      ]      
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
      
    }
  },
}
</script>

