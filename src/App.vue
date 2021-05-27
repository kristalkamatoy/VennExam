<template>
  <div id="app">
    <p class="field">BMI Calculator</p>

    <table class="table">
      <thead center border="1">
        <tr>
          <th>Gender</th>
          <th>Weigth</th>
          <th>Heigth</th>
          <th>BMI</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(arrayTests) in arrayTest"  :key="arrayTests.height" >
          <td>{{ arrayTests.gender }}</td>
          <td>{{ arrayTests.weight }}</td>
          <td>{{ arrayTests.height }}</td>
          <td :style=" `color:${bmiColor[arrayTests.bmiKeyword]}`">{{ arrayTests.bmi }}</td>
        </tr>
      </tbody>
    </table>
    
    <div class="field">   
      
        <label>Gender: </label>
        <input v-model="gender" type="radio" value="Male"/>
        <label> Male </label> 
        <input v-model="gender" type="radio" value="Female"/>
        <label> Female</label> <br/>
        <label >weight </label>
        <input v-model="weight" type="number"/>
        <label> kg</label> <br/>
        <label>height </label>
        <input v-model="height" type="number"/>
        <label> cm</label><br>
        
        
    </div>
    <div class="field">
        <button @click="submit">Submit</button>
      <div v-if="this.localbmi > 0">
        <h4>Your BMI is </h4>
        <h2 :style=" `color:${bmiColor[bmi]}`">{{ this.localbmi }}</h2>
        <img :src="bmiimage"> 
        <!-- <img src="./images/Female_Normal.png"> -->
        <h4>You are {{ this.bmi }}</h4>
    </div>
    </div>

  </div>
</template>
<script>

export default {
  name: "App",
  data() {
    return {
      bmiColor : {"Underweight": "blue", "Normal weight": "Green", "Overweight": "Orange", "Obese": "Red"},
      activeColor: {
        color: '',
        fontSize: '15px'
      },
      randomNum: "",
      weight:"",
      height:"",
      gender: "",
      localbmi: "",
      arrayTest: [{gender: "", weight: "", height: "", bmi: "", bmiKeyword: ""}]
    };
  },
  computed: {
    bmiimage () {
       if (parseInt(this.localbmi) < 18.9) {
        return this.gender === "Male"? require("./images/Male_Under.png") : require("./images/Female_Under.png");
      } else if (
        parseInt(this.localbmi) >= 18.9 &&
        parseInt(this.localbmi) < 25
      ) {
        return this.gender === "Male"? require("./images/Male_Normal.png") : require("./images/Female_Normal.png");
      } else if (
        parseInt(this.localbmi) >= 25 &&
        parseInt(this.localbmi) < 30
      ) {
        return this.gender === "Male"? require("./images/Male_Over.png") : require("./images/Female_Over.png");
      } else  {
        return this.gender === "Male"? require("./images/Male_Obese.png") : require("./images/Female_Obese.png");
      } 
    },
    bmi () {
       if (parseInt(this.localbmi) < 18.9) {
        return "Underweight";
      } else if (
        parseInt(this.localbmi) >= 18.9 &&
        parseInt(this.localbmi) < 25
      ) {
        return "Normal weight";
      } else if (
        
        parseInt(this.localbmi) >= 25 &&
        parseInt(this.localbmi) < 30
      ) {
        return "Overweight";
      } else {
        return "Obese";
      } 
    }
  },
  methods: {
    submit() {
      let weight = parseFloat(this.weight)
      let height = parseFloat(this.height) / 100
      this.localbmi = weight / (height * height)
      

      this.arrayTest.push({'gender': this.gender, 'weight': this.weight, 'height': this.height, 'bmi': this.localbmi, 'bmiKeyword': this.bmi});
      if (this.arrayTest.length > 11) {
        this.arrayTest.splice(1, 1)
      }
    }
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.field {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 10px;
  margin-left: 10px;
}


input {
  width: 5%;
  margin-top: 10px;
}

.test{
  display: block;
  position: relative;
  padding-left: 45px;
}

table {
  border-collapse: collapse;
  border: 1px solid black;
  align-content: center;
  width: 50%;
  float: right;
} 
table.table {
    margin-right: 0px;
    margin-left: auto;
}

th,td {
  border: 1px solid black;
  text-align: center;
  
}
tr:nth-child(even) {background-color: #f2f2f2;}
</style>
