<template>
  <div>

      <form @submit.prevent >
        <label>Species</label>
        <input v-model="newAnimal.species" type="text" placeholder="species" > <br>
        <label>Name</label>
        <input v-model="newAnimal.name" type="text" placeholder="name"> <br>
        <label>Date of birth</label>
        <input v-model="newAnimal.dateOfBirth" type="text" placeholder="dateOfBirth"> <br>
        <label>Status</label>
        <select v-model="newAnimal.sector">
            <option v-for="(sector,index) in sectors" :key="index" :value="sector"> {{ sector.name}} </option>
        </select><br>
        <button @click="addAnimal">Add animal</button> <br> <br>
      </form>

      <table border=1 align="center">
        <thead>
          <th>Species</th>
          <th>Name</th>
          <th>Date of Birth</th>
          <th>Status</th>
          <th></th>
          <th></th>
        </thead>
        <tbody>
          <tr v-for="(animal,index) in animals" :key="index" >            
            <td> {{animal.species}} </td>
            <td> {{animal.name}} </td>
            <!-- <td v-if= "animal.dateOfBirth"> {{animal.dateOfBirth}} </td>
            <td v-else> {{ nonexistent }} </td>  //// radi ali moze i u jednom redu-->
            <td>{{ animal.dateOfBirth ? animal.dateOfBirth : nonexistent }}</td>
            <td> {{ animal.sector.name }} </td>
            <td> <button @click="removeAnimal(animal)"> Remove</button> </td>
            <td v-if="animals.indexOf(animal) !== 0"> 
              <button @click="moveToTopAnimal(animal)"> Move to top</button> 
            </td>
            <td v-else></td>
          </tr>
        </tbody>
      </table>

      <table border=1>
        <thead>
          <th>Status</th>
          <th></th>
        </thead>
        <tbody>
          <tr v-for="(sector, index) in sectors" :key="index">
            <td>{{ sector.name }}</td>
            <td>
              <button @click="showAlert(sector.name)">Show Animal list</button>
            </td>
          </tr>
        </tbody>
      </table>
   
  </div>
</template>

<script>
const unknown = "Unknown";

const sectors =[
  {name: "Domestic"},
  {name: "Wild"}, 
  {name: unknown}  
]

export default {
  name: 'AnimalList',

  data() {
    return {
      nonexistent: unknown,
      animals: [
        {species: "Horse", name: "Zelenko", dateOfBirth: "09/01/1995", sector:sectors[0]},
        {species: "Pig", name: "Gile", dateOfBirth: "20/10/2004", sector:sectors[0]},
        {species: "Ruster", name: "Zvonko", dateOfBirth: "20/07/2011", sector:sectors[0]},
        {species: "Mouse", name: "Gricko", dateOfBirth: "30/04/2015", sector:sectors[1]},
        {species: "Zebra", name: "Zaza", dateOfBirth: "22/11/2008", sector:sectors[1]},
        {species: "Test", name: "Zivotinja", dateOfBirth: "", sector:sectors[2]}
      ],
      newAnimal: {}   ,
      sectors: sectors,
      belongsToSector: []   
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
      console.log(this.newAnimal);
      this.animals.push(this.newAnimal);
      this.newAnimal = {};
    },

    showAlert(sectorBelonging){      
      this.animals.forEach(animal => {
        let sectorOfAnimal = animal.sector.name;
        if(sectorOfAnimal === sectorBelonging){
          let nameOfAnimal = animal.name;
          this.belongsToSector.push(nameOfAnimal);
        } 
      });      
      if (this.belongsToSector == "") {
        alert("There is no animal with this status");
      } else {
        alert(this.belongsToSector);
      }
      
      this.belongsToSector = [];
    },
  },
}
</script>

