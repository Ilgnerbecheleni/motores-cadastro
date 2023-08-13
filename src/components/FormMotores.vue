<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-md-8">
        <b-card title="Cadastrar Motor Elétrico" class="mt-3">
          <b-form @submit.prevent="submitForm">
            <b-form-group id="marca" label="Marca:" label-for="marca">
              <b-form-input v-model="motor.marca" id="marca" required></b-form-input>
            </b-form-group>
            <b-form-group id="potencia" label="Potência:" label-for="potencia">
              <b-form-input v-model="motor.potencia" id="potencia" required></b-form-input>
            </b-form-group>
            <b-form-group id="polos" label="Polos:" label-for="polos">
              <b-form-select v-model="motor.polos" id="polos" class="form-control" required>
                <option value="2">2 Polos</option>
                <option value="4">4 Polos</option>
                <option value="6">6 Polos</option>
                <option value="8">8 Polos</option>
                <option value="10">10 Polos</option>
                <option value="12">12 Polos</option>
                <!-- Adicione outras opções conforme necessário -->
              </b-form-select>
            </b-form-group>

            <b-form-group id="carcaca" label="Carcaça:" label-for="carcaca">
              <b-form-input v-model="motor.carcaca" id="carcaca" required></b-form-input>
            </b-form-group>
            <b-form-group id="tensao" label="Tensão:" label-for="tensao">
              <b-form-select v-model="motor.tensao" id="tensao" class="form-control" required>
                <option value="220/380/440V">220/380/440V</option>
                <option value="220/380V">220/380V</option>
                <option value="380/660V">380/660V</option>
                <option value="440V">440V</option>
              </b-form-select>
            </b-form-group>

            <b-form-group id="corrente" label="Corrente:" label-for="corrente">
              <b-form-input v-model="motor.corrente" id="corrente" required></b-form-input>
            </b-form-group>
            <b-form-group id="flange" label="Flange:" label-for="flange">
              <b-form-select v-model="motor.flange" id="flange" class="form-control" required>
                <option v-for="flange in flanges" :key="flange" :value="flange">{{ flange }}</option>
              </b-form-select>
            </b-form-group>
        
            <b-form-group id="rolamentoD" label="Rolamento Dianteiro:" label-for="rolamentoD">
              <b-form-input v-model="motor.rolamentoD" id="rolamentoD" required></b-form-input>
            </b-form-group>
            <b-form-group id="rolamentoT" label="Rolamento Traseiro:" label-for="rolamentoT">
              <b-form-input v-model="motor.rolamentoT" id="rolamentoT" required></b-form-input>
            </b-form-group>
            <b-form-group id="codigoSistema" label="Código Sistema:" label-for="codigoSistema">
              <b-form-input v-model="motor.codigoSistema" id="codigoSistema" required></b-form-input>
            </b-form-group>
            <div class="mt-4">
              <b-button type="submit" variant="primary">Salvar</b-button>
            </div>
          </b-form>
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
      motor: {
        marca: '',
        potencia: '',
        polos: '',
        carcaca: '',
        tensao: '',
        corrente: '',
        flange: '',
        modeloFlange: '',
        rolamentoD: '',
        rolamentoT: '',
        codigoSistema: '',
      },
      flanges: [
        'Não Possui','C-105', 'C-120', 'C-140', 'C-160', 'C-200', 'C-250',
        'FC-95', 'FC-149', 'FC-184', 'FC-228', 'FC-279', 'FC-355', 'FC-368',
        'FF-130', 'FF-165', 'FF-215', 'FF-265', 'FF-300', 'FF-350', 'FF-400',
        'FF-500', 'FF-600', 'FF-740'
      ],
   
    };
  },
  methods: {
    submitForm() {
      axios.post('http://localhost:3333/api/motors', this.motor)
        .then(response => {
          console.log('Motor cadastrado com sucesso:', response.data);
          // Limpe o formulário após o envio bem-sucedido
          this.resetForm();
        })
        .catch(error => {
          console.error('Erro ao cadastrar motor:', error);
        });
    },
    resetForm() {
      // Limpe o formulário
      this.motor = {
        marca: '',
        potencia: '',
        polos: '',
        carcaca: '',
        tensao: '',
        corrente: '',
        flange: '',
        modeloFlange: '',
        rolamentoD: '',
        rolamentoT: '',
        codigoSistema: '',
      };
    },
  },
};
</script>
