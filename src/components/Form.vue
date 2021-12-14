<template>
  <div>
    <b-form-group label="Valor a ser convertido" class="mb-3">
      <b-input-group :prepend="currency + ' - $'" class="mt-3">
        <b-form-input v-model="valor" :state="isNaN(Number(valor)) ? false: null"/>
        <b-input-group-append>
          <b-button variant="primary" @click="convertCurrency">Converter</b-button>
        </b-input-group-append>
      </b-input-group>
    </b-form-group>
    <b-form-group label="Valor em reais" class="mb-3">
      <b-input-group prepend="BR - R$ " class="mt-3">
        <b-form-input v-model="valor_final" disabled/>
      </b-input-group>
    </b-form-group>
  </div>
</template>
<script>
export default {
  name: "Form",
  data: function(){
    return {
      valor: null,
      valor_final: 0
    }
  },
  props: {
      valueCurrency : String,
      currency : String
  },
  methods : {
      convertCurrency: function(){
        if(!isNaN(Number(this.valor))){
          const result = Number(this.valor) * Number(this.valueCurrency);
          this.valor_final = this.fomratCurrency(result)
        }
      },
      fomratCurrency : function(val) {
      return Number(val).toFixed(2).toString().replace(".",",")
    }
  }
};
</script>
<style></style>
