<template>
    <div id="burger-table">
        <Message :msg="msg" v-show="msg" />
        <div>
            <div id="burger-table-head">
                <div class="order-id">#</div>
                <div>Cliente: </div>
                <div>Pão: </div>
                <div>Carne: </div>
                <div>Opicionais: </div>
                <div>Ação: </div>
            </div>
        </div>
        <div id="burger-table-rows">
            <div id="burger-table-row" v-for="burger in burgers" :key="burger.id">
                <div class="order-number">{{ burger.id }} </div>
                <div>{{ burger.nome }}</div>
                <div>{{ burger.pao }}</div>
                <div>{{ burger.carne }}</div>
                <div> 
                    <ul>
                        <li v-for="(opcional, index) in burger.opicionais" :key="index"> 
                            {{ opcional }}
                        </li>
                    </ul> 
                </div>
                <div>
                    <select name="status" id="status" @change="updatedBurger($event, burger.id)">
                        <option :value="s.tipo" v-for="s in status" :key="s.id"  :selected="burger.status == s.tipo">
                            {{s.tipo}}
                        </option>
                    </select>
                    <button class="delete-btn" @click="deleteBurger(burger.id)">Cancelar</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Message from './Message.vue';

    export default{
        // eslint-disable-next-line vue/multi-word-component-names
        name: 'Dashboard',
        components: {
            Message
        },
        data() {
            return {
                burgers: null,
                burger_id: null,
                status: [],
                msg: null
            }
        },
        methods: {
            async getPedidos(){

                const rep = await fetch("http://localhost:3000/burgers");
                
                const data = await rep.json();

                this.burgers = data
                
                // Resgatar os status
                this.getStatus()

            },
            async getStatus() {
                const rep = await fetch("http://localhost:3000/status")
                const data = await rep.json();

                this.status = data

            }, 
            async deleteBurger(id) {
                
                const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                    method: "DELETE"
                });

                const res = await req.json();

                this.getPedidos();

                // mgs

                this.msg = `Pedido N° ${res.id} Cancelado com sucesso`

                setTimeout(() => this.msg = "", 3000)
            },
            async updatedBurger(event, id) {

                const option = event.target.value;

                const dataJson = JSON.stringify({ status: option});

                const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                    method: "PATCH",
                    headers: {"Content-Type": "application/json"},
                    body: dataJson
                });

                const res = await req.json();

                // mgs

                this.msg = `O pedido N° ${res.id} foi atualizado para ${res.status}`

                setTimeout(() => this.msg = "", 3000)

                console.log(res)

            }
        }, 
        mounted() {
            this.getPedidos()
        }
    }
</script>

<style scoped>
    * {
        margin: 0;
        padding: 0;
        color: white;
    }

    #burger-table{
        /* max-width: 1200px; */
        margin: 0 auto;
         
    }

    #burger-table-head,
    #burger-table-rows,
    #burger-table-row {
        display: flex;
        flex-wrap: wrap;
    }
    
    #burger-table-head {
        font-weight: bold;
        padding: 12px;
        border-bottom: 3px solid black;
    }
    
    #burger-table-head div,
    #burger-table-row div{
        width: 19%;
    }
    
    #burger-table-row{
       width: 100%;
       padding: 12px;
       border-bottom: 1px solid black;
    }

    #burger-table-head .order-id,
    #burger-table-row .order-number {
         width: 5%;
    }

    select {
        padding: 12px 6px;
        margin-right: 12px;
        color: black;   
    }

    option {
        color: black;
    }

    .delete-btn {
        background-color: black;
        color: white;
        border: 2px solid black;
        padding: 10px;
        font-size: 16px;
        cursor: pointer;
    }

    .delete-btn:hover {
        background-color: white;
        color: #ffcc00;
        font-weight: bold;
    }
</style>