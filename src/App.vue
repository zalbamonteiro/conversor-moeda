<template>
  <div id="app">
    <Header />
    <b-container>
      <b-row align-h="center">
        <b-col md="3" class="mt-5">
          <Card :changeCurrency="changeCurrency"/>
        </b-col>
      </b-row>
      <b-row align-h="center">
        <b-col md="5" class="mt-5">
          <h4 class="mt-5 mb-4">Faça a conversão de valores</h4>
          <Form :currency="currency" :valueCurrency="valueCurrency"/>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Card from "./components/Card.vue";
import Form from "./components/Form.vue";

export default {
  name: "App",
  components: {
    Header,
    Card,
    Form
  },
  data: function(){
    return {
      currency : 'USD',
      valueCurrency: "0",
    }
  },
  methods : {
    changeCurrency : function(currency, value){
      this.currency = currency;
      this.valueCurrency = value;
    }
  }
};
</script>

<style></style>
