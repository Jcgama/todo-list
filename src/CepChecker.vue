<template>
  <section class="cepChecker">
    <label>Digite o CEP:</label>
    <input type="text" @blur="checkCep"></input>
    <router-link class="home" to="/">Ver Tarefas</router-link>
    <div v-show="hasAddress()">
      <p>Rua:{{address.logradouro}}</p>
      <p>Bairro:{{address.bairro}}</p>
      <p>Cidade:{{address.cidade}}</p>
      <p>Estado: {{address.estado}}</p>
    </div>
  </section>
</template>

<script>
export default {
  data() {
      return {
          address:{}
      }
  },
  methods:{
    checkCep($event){
      let cep = $event.target.value
      this.$http.get('http://api.postmon.com.br/v1/cep/' + cep).then(res => {
        this.address = res.body
        console.log(this.address)
      }, err => {
        console.log(err)
      })
    },
    hasAddress(){
      return Object.keys(this.address).length > 0
    }
  }
}
</script>

