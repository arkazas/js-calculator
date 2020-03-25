<template>
  <div class="hello">
    <h1 v-if="isActive()">{{ msg }}</h1>
    <h1 v-else>Buy buy! Thank you for using</h1>
    <div v-html="output" v-if="isActive()" class="output"></div>

    <input type="text" v-model.trim="inputData" v-if="isActive()"
           @keypress="isValid($event)" @keyup="calcNumber($event)" autofocus placeholder="Please, start type numbers"/>

  </div>
</template>

<script>
export default {
  data() {
    return {
      data:[],
      output: '',
      inputData: '',
      isExit: false,
      operationCodes: [32, 42, 43, 45, 47],
      result: null
    };
  },
  name: 'CalculateCli',
  props: {
    msg: String
  },
  methods: {
    isActive() {
      return !this.isExit
    },

    setDefaults() {
      this.data = []
      this.inputData = ''
      this.output = ''
      this.result = null
    },

    calcNumber(e){
      let charCode = this.getCharCode(e)

      if (charCode === 13 && this.inputData !== '') {
        let data = this.inputData.split(' ');

        data.forEach((value) => {
          if (parseInt(value)) {
            this.data.push(value)
            return
          }

          let count = this.data.length

          this.result = eval (this.data[count - 2] + value + this.data[count - 1])
          this.data[count - 2] = this.result
          this.data.pop()
        })

        this.output += '>' + this.inputData + '<br />'
        this.output += ((this.result != null) ? this.result : this.inputData) + '<br />'

        this.inputData = ''
      }
    },

    isValid(e) {
      let charCode = this.getCharCode(e)

      if (charCode === 99) {
        this.setDefaults()
      }

      if (charCode === 113) {
        return this.isExit = true
      }

      if (charCode > 31 && (charCode < 48 || charCode > 57)
            && !this.operationCodes.includes(charCode)) {
        e.preventDefault()
      } else {
        return true
      }
    },

    getCharCode(e) {
      return (e.which) ? e.which : e.keyCode
    }
  }
}
</script>


<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.output {
  text-align: left;
  margin: 0px auto;
  width: 400px;
  max-height: 400px;
  min-height: 150px;
  overflow-y: auto;
  color: #b7ffb7;
  font-size: 13px;
  padding: 10px;
  line-height: 2;
  background-color: #000;
}
input {
  width: 300px;
  margin: 30px 0px 0px;
}
</style>