<template>
    <div>
        <Message :msg="msg" v-show="msg"  />

        <div>
            <form id="burge-form" @submit="createBurger">
                <div class="input-container">
                    <label for="name">Nome Cliente: </label>
                    <input type="text" id="name" name="name" v-model="nome" placeholder="Dijite seu nome" required>
                </div>
                <div class="input-container">
                    <label for="pao">Escolha o Pão: </label>
                    <select name="pao" id="pao" v-model="pao" required>
                        <option value="">Seleciona seu pão</option>
                        <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
                    </select>
                </div>
                <div class="input-container">
                    <label for="carne">Escolha a carne do seu Burge: </label>
                    <select name="carne" id="carne" v-model="carne" required>
                        <option value="">Seleciona seu tipo de carne</option>
                        <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
                    </select>
                </div>
                <div id="opcionais-container" class="input-container">
                    <label id="opicionais-title" for="opicionais">Opicionais </label>
                    <div class="checkbox-container" v-for="opcoe in opicionaisdata" :key="opcoe.id">
                        <input type="checkbox" name="opicionais" v-model="opcionais" :value="opcoe.tipo">
                        <span>{{ opcoe.tipo }}</span>
                    </div>
                </div>
                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Criar Meu Burger!">
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import Message from './Message.vue';

    export default {
        name: "BurgeForm",
        components: {
            Message
        },
        data() {
            return{
                paes: null,
                carnes: null,
                opicionaisdata: null,

                nome: null,
                pao: null,
                carne: null,
                opcionais: [

                ],
                
                status: "Solicitados",
                msg: null
            }
        },
        methods: {
            async getIngrediente() {
                
                const requestes = await fetch("https://json-burgue-hpdadj8pj-protagonistaaas-projects.vercel.app/ingredientes");
                const data = await requestes.json()

                this.paes = data.paes;
                this.carnes = data.carnes;
                this.opicionaisdata = data.opcionais

            },
            async createBurger(e) {
                e.preventDefault();

                const data = {
                    nome: this.nome,
                    pao: this.pao,
                    carne: this.carne,
                    opicionais: Array.from(this.opcionais),
                    status: "Solicitados"
                }

                const dataJson = JSON.stringify(data);

                const rep = await fetch("https://json-burgue-hpdadj8pj-protagonistaaas-projects.vercel.app/burgers", {
                    method: "POST",
                    headers: {"Content-Type": "application/json"},
                    body: dataJson
                });

                // eslint-disable-next-line no-unused-vars
                const res = await rep.json();

                // Colocar uma msg de sistema 
                this.msg = `Pedido N° ${res.id} realizado com sucesso`

                // Limpar msg
                setTimeout(() => {
                    this.msg = ""
                }, 3000)

                // limpar formulario
                this.nome = "";
                this.pao = "";
                this.carne = "";
                this.opcionais = "";
            }
        },
        mounted() {
            this.getIngrediente()
        }
    }
</script>

<style scoped>
    #burge-form {
        max-width: 400px;
        margin: 0 auto;
        color: white;
    }
    
    .input-container {
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }
    
    label {
        font-weight: bold;
        margin-bottom: 15px;
        padding: 5px 10px;
        border-left: 4px solid #ffd21d;
    }

    input, select {
        padding: 5px 10px;
        width: 300px;
    }

    #opcionais-container {
        flex-direction: row;
        flex-wrap: wrap;
    }

    #opicionais-title {
        width: 100%;
    }

    .checkbox-container {
        display: flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 20px;
    }

    .checkbox-container span,
    .checkbox-container input {
        width: auto;
    }

    .checkbox-container span {
        margin-left: 6px;
        font-weight: bold;
    }

    .submit-btn {
        background-color: black;
        color: #ffd21d;
        font-weight: bold;
        padding: 10px;
        border: 2px solid black;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5;
    }
    
    .submit-btn:hover {
        opacity: 0.5;
    }
</style>