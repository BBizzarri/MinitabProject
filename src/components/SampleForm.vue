
<template>
  <div>
    <div class="grid">
        <label>Sample Size:</label>
        <input type="number" v-model="size" onkeypress="return event.charCode >= 48 && event.charCode <= 57">
        <label>Sample mean:</label>
        <input type="number" v-model="mean">
        <label>Standard deviation:</label>
        <input type="number" v-model="deviation">
    </div>  
    <div class="hypothesis-mean-checkbox">
      <input type="checkbox" id="checkbox1" @change="changeState">
      <label>Perform hypothesis test</label>
    </div>  
    <div class="grid">
        <label :class="{'disableLabel' : !hypothesisTest}" disabled="hypothesisTest">Hypothesized mean:</label>
        <input type="number" v-model="hypothesizedMean" :disabled="!hypothesisTest">  
    </div>  
    <div class="button"> 
        <button class="submit-button" @click="submit">OK</button>
        <button class="reset-button" @click="reset">Reset</button>
    </div>    
    <div v-if="errors" class="error-message">
      <label v-for="message in errorMessage" v-bind:key="message">*{{message}}<br></label>
    </div>  
    <div>
      <table v-if="addRecord">
        <tr>
          <th class="table-head">Sample size</th>
          <th class="table-head">Sample mean</th>
          <th class="table-head">Standard deviation</th>
          <th v-if="hypothesisTest">Hypothesized mean</th>
        </tr>
        <tr>
          <td class="table-head">{{ this.size }}</td>
          <td class="table-head">{{ this.mean }}</td>
          <td class="table-head">{{ this.deviation }}</td>
          <td v-if="hypothesisTest">{{ this.hypothesizedMean }}</td>
        </tr>
      </table>
    </div>      
  </div>      
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      size: null,
      mean: null,
      deviation: null,
      hypothesizedMean: null,
      errors: false,
      errorMessage: [],
      hypothesisTest: false,
      formSubmitted: false,
      addRecord: false
    }
  },
  props: {
    msg: String
  },
  methods: {
    submit() {
      if(this.size < 2 || this.deviation <= 0) {
        this.errors = true
        if(this.size < 2) {
          this.errorMessage.push("The Sample size must be a whole number that is greater than or equal to 2.")
        } 
        if (this.deviation <= 0) {
          this.errorMessage.push("The Standard deviation must be a numeric value that is greater than 0.")
        }
      } else {
        this.errors = false
        this.errorMessage = []
        this.formSubmitted = true
        this.addRecord = true
      }
    },
    reset() {
      this.addRecord = false
      this.hypothesisTest = false
      this.size = ""
      this.mean = ""
      this.deviation = ""
      this.hypothesizedMean = ""
      document.getElementById('checkbox1').checked = false
      this.errorMessage = []
    },
    changeState () {
      if(this.hypothesisTest) { this.hypothesisTest = false }
      else { this.hypothesisTest = true }
    }
  }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.disableLabel {
  color: #ccc;
}

.grid {
  display: grid;
  grid-template-columns: 200px 400px;
  grid-gap: 10px;
}

.error-message {
  color: red;
}

.button {
  padding-top: 30px;
  padding-left: 515px;
}
.submit-button {
  background-color:#2979FF;
  margin-right: 10px;
}

.reset-button {
  background-color:#CCCCCC
}

.table-head{
  padding-right: 20px;
}

</style>
