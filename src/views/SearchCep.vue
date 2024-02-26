<template>
<v-container fluid class="background-container">

    <router-link to="/">
        <img src="/assets/images/PesquisaCEP.png" alt="Logo" style="height: 150px">
    </router-link>

    <BackgroundImage />

    <v-alert v-if="error" type="error" :message="error.message" @input="clearError">{{ error.message }}</v-alert>
    
    <v-sheet max-width="300" class="mt-5 mx-auto">
        <v-form ref="form" @submit.prevent="onSubmit">
            <v-text-field v-model="cep" type="string" @input="handleInput" label="Digite o CEP" append-icon="mdi-magnify"></v-text-field>
            <v-btn :loading="loading" :disabled="cep.length !== 9" prevent type="submit" block text="Buscar CEP"></v-btn>
        </v-form>
    </v-sheet>

</v-container>

<v-div v-if="response && !error" class="mt-6">
    <v-row justify="center">
        <v-col cols="12" sm="10" md="8" lg="6">
            <v-card ref="form">
                <v-card-text>
                    <v-text-field v-model="response.logradouro" label="Endereço" readonly></v-text-field>
                    <v-text-field v-model="response.bairro" label="Bairro" readonly></v-text-field>
                    <v-text-field v-model="response.localidade" label="Cidade" readonly></v-text-field>
                    <v-text-field v-model="response.uf" label="Estado" readonly></v-text-field>
                    <v-text-field v-model="response.cep" label="CEP" readonly></v-text-field>
                    <v-text-field v-if="response.complemento" v-model="response.complemento" label="Complemento" readonly></v-text-field>
                </v-card-text>
                <v-divider class="mt-6"></v-divider>
            </v-card>
        </v-col>
    </v-row>
</v-div>
</template>

<script setup>
import {ref} from 'vue';
import axios from 'axios';
import BackgroundImage from '@/components/BackgroundImage.vue';

const cep = ref('');
const loading = ref(false);
const response = ref(null);
const error = ref(null);

const onSubmit = async () => {
    try {
        error.value = null
        loading.value = true;
        const result = await axios.get(`http://localhost:8000/api/consultar-api/${cep.value.replace(/\D/g, '')}`);
        response.value = result.data;
        loading.value = false;

    } catch (err) {
        loading.value = false;
        error.value = err.response ? err.response.data : {
            message: 'Erro desconhecido ao buscar dados do CEP.'
        };
        
        // Define um temporizador para esconder o v-alert após 5 segundos
        setTimeout(() => {
            error.value = null;
        }, 5000);
    }
};

const handleInput = () => {
    // Remove caracteres não numéricos do valor do CEP
    let formattedCep = cep.value.replace(/\D/g, '');

    formattedCep = formattedCep.substring(0, 8);

    if (formattedCep.length > 5) {
        formattedCep = formattedCep.substring(0, 5) + '-' + formattedCep.substring(5);
    }

    cep.value = formattedCep;
};
</script>

<style>
.background-container {
    position: relative;
    z-index: 0;
}
</style>
