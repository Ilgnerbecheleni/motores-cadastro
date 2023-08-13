<template>
    <div class="container">
      <div class="row justify-content-center">
        <div class="col-md-12">
          <b-card title="Motores Cadastrados" class="mt-3">
            <b-table :items="motores" :fields="tableFields" responsive="sm">
              <template #cell(marca)="data">
                {{ data.value }}
              </template>
              <template #cell(potencia)="data">
                {{ data.value }}
              </template>
              <template #cell(polos)="data">
                {{ data.value }}
              </template>
              <template #cell(carcaca)="data">
                {{ data.value }}
              </template>
              <template #cell(tensao)="data">
                {{ data.value }}
              </template>
              <template #cell(corrente)="data">
                {{ data.value }}
              </template>
              <template #cell(flange)="data">
                {{ data.value }}
              </template>
              <template #cell(rolamentod)="data">
                {{ data.value }}
              </template>
              <template #cell(rolamentot)="data">
                {{ data.value }}
              </template>
              <template #cell(codigosistema)="data">
                {{ data.value }}
              </template>
            </b-table>
          </b-card>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    
    data() {
      return {
        motores: [],
        tableFields: [
          { key: 'marca', label: 'Marca' },
          { key: 'potencia', label: 'Potência' },
          { key: 'polos', label: 'Polos' },
          { key: 'carcaca', label: 'Carcaça' },
          { key: 'tensao', label: 'Tensão' },
          { key: 'corrente', label: 'Corrente' },
          { key: 'flange', label: 'Flange' },
          { key: 'rolamentod', label: 'Rolamento Dianteiro' },
          { key: 'rolamentot', label: 'Rolamento Traseiro' },
          { key: 'codigosistema', label: 'Código Sistema' },
        ],
      };
    },
    created() {
      this.fetchMotores();
    },
    methods: {
      fetchMotores() {
        axios.get('http://localhost:3333/api/motors')
          .then(response => {
            this.motores = response.data;
            console.log(response.data)
          })
          .catch(error => {
            console.error('Erro ao buscar motores:', error);
          });
      },
    },
  };
  </script>
  