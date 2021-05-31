<template>
    <table class="table">
      <thead center border="1">
        <tr>
          <th>Gender</th>
          <th>Weight</th>
          <th>Height</th>
          <th>BMI</th>
          <th>Description</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="arrayTest in arraytests"  :key="arrayTest.id" >
          <td>{{ arrayTest.gender }}</td>
          <td>{{ arrayTest.weight }}</td>
          <td>{{ arrayTest.height }}</td>
          <td :style=" `color:${bmiColor[arrayTest.bmiKeyword]}`">{{ arrayTest.bmi }}</td>
          <td>{{ arrayTest.bmiKeyword }}</td>
         <td> <span @click="updateValue(arrayTest)">{{ arrayTest.view }}</span> </td>
        </tr>
      </tbody>
    </table>
</template>
<script>
export default {
  props: ['arraytests', 'bmiColor'],

  data: () => ({
    drawer: null,
  }),
  methods: {
    updateValue(arrayVal) {
      this.$emit("update-value", arrayVal);
    }
  },
  
}
</script>