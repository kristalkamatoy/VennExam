<template>
  <div id="app">
<div class="row">
  <div class="column">
    <form>
      
    <h3 class="field">BMI Calculator</h3>
    
    <div class="field">   
    <!-- GENDER -->
    <div class="row">
    <div class="column"><label>Gender: </label> </div><br/>
    <div class="column"> 
       <input v-model="gender" type="radio" value="Male"/>
        <label> Male </label> 
    </div>
        <div class="column"> 
        <input v-model="gender" type="radio" value="Female"/>
        <label> Female</label> <br/> 
      </div>
      </div>
    <!-- end Gender  -->
    <!-- Height -->
    <div class="row">
    <div class="column"><label>Height: </label> </div><br/>
    <div class="column"> 
       <input v-model="inch" type="number"/>
        <label> in inches </label> 
    </div>
        <div class="column"> 
        <input v-model="cm" type="number"/>
        <label> in cm</label> <br/> 
      </div>
      </div>
    <!-- end Height  -->
    <!-- Weight -->
    <div class="row">
    <div class="column"><label>Weight: </label> </div><br/>
    <div class="column"> 
       <input v-model="kg" type="number"/>
        <label> in kg </label> 
    </div>
        <div class="column"> 
        <input v-model="lbs" type="number"/>
        <label> in lbs</label> <br/> 
      </div>
      </div>
    <!-- end Weight  -->

        
        
    </div>
    <div class="field">
        <button @click="submit">Save</button>
         <button @click="clear">Clear</button>
      <div v-if="this.localbmi > 0">
        <h4>Your BMI is </h4>
        <h2 :style=" `color:${bmiColor[bmi]}`">{{ this.localbmi }}</h2>
        <h4> ({{ this.bmi }})</h4>
    </div>
    </div>
  </form>
  </div>
  <div class="column">
 <h3 class="field">History</h3>
    <array-test  :arraytests="arrayTest" :bmiColor="bmiColor"  @update-value="callUpdate"></array-test>
  </div>
</div>
  <!-- en here -->
  </div>
</template>
<script>
import UpdateTable from "./components/UpdateTable.vue"

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
      gender: "",
      arrayTest: [{gender: "", weight: "", height: "", bmi: "", bmiKeyword: "", view: ""}],
      cm: 0,
      inch: 0,
      kg: 0,
      lbs: 0
    };
  },
  components: {
    'array-test':UpdateTable
  },
  computed: {
    localbmi () {
      let weight = parseFloat(this.kg)
      let cm = parseFloat(this.cm) / 100

      return weight / (cm * cm)
    },
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
    },

  },
  methods: {
    submit() {
      this.arrayTest.push({'gender': this.gender, 'weight': this.kg, 'height': this.cm, 'bmi': this.localbmi, 'bmiKeyword': this.bmi, 'view':"view"});
    
      if (this.arrayTest.length > 11) {
        this.arrayTest.splice(1, 1)
      }
    },
  callUpdate (arrayVal) {
    this.kg = arrayVal.weight;
    this.gender = arrayVal.gender;
    this.cm = arrayVal.height;
    this.localbmi = arrayVal.bmi;
   }  ,
  clear () {
    this.kg = '';
    this.gender = '';
    this.cm = '';
    this.localbmi = '';
   }  
  },
   beforeMount() {
    alert('Hi User! Welcome to BMI Calculator')
 },
  watch: {
    inch() {
      this.cm = this.inch ? (this.inch * 2.54).toFixed(2) : 0;
    },
   cm() {
      this.inch = this.cm ? (this.cm / 2.54).toFixed(2) : 0;
    },

  kg() {
      this.lbs = this.kg ? (this.kg * 2.20462).toFixed(2) : 0;
    },
   lbs() {
      this.kg = this.lbs ? (this.lbs / 2.20462).toFixed(2) : 0;
    }
  }
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
  margin: auto;
  margin-left: 10px;
}


input {
  margin: 10px;
  width: 40%;
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
  width: 100%;

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

* {
  box-sizing: border-box;
}

/* Create two equal columns that floats next to each other */
.column {
  float: left;
  width: 50%;
 
}

/* Clear floats after the columns */
.row:after {
  content: "";
  display: table;
  clear: both;
  
}

</style>
