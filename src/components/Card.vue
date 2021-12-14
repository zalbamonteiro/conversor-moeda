<template>
  <div>
    <b-card
      style="max-width: 20rem"
      class="mb-2 text-center"
      bg-variant="light"
    >
      <h2 class="mt-3">R$ {{cotacao && fomratCurrency(cotacao.ask)}}</h2>
      <b-card-text>
        Cotação do <strong>{{ selected }}</strong> hoje
      </b-card-text>
      <b-card-text>
        <b-form-group label="Moeda: ">
          <b-form-select v-model="selected" :options="options" @change="getCurrency"></b-form-select>
        </b-form-group>
      </b-card-text>
    </b-card>
  </div>
</template>
<script>

export default {
  name: "Card",
  props : {
      changeCurrency : Function,
  },
  data() {
    return {
      selected: "USD",
      options: [
        { value: 'USD', text: "USD (Dolar Americano)" },
        { value: "EUR", text: "EUR (Euro)" },
      ],
      cotacao: null,
    };
  },
  methods: {
    getCurrency: async function() {
      const URL = `https://economia.awesomeapi.com.br/json/last/${this.selected}-BRL`;
      const result = await fetch(URL)
        .then((res) => res.json())
        .then((res) => res)
        .catch((error) => {
          return {
            error: true,
            message: error,
          };
        });

        if(!result.error){
            this.cotacao = result[`${this.selected}BRL`]
            this.changeCurrency(this.selected, this.cotacao.ask);
        }
    },
    fomratCurrency : function(val) {
      return Number(val).toFixed(2).toString().replace(".",",")
    }
  },
  created: function(){
      this.getCurrency();
  },
};
</script>
<style></style>
