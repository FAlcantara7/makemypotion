<template>
    <div id="potion-table">
        <div>
            <div id="potion-table-header">
                <div class="order-id">#:</div>
                <div>Cliente:</div>
                <div>Qualidade:</div>
                <div>Efeito:</div>
                <div>Opcionais:</div>
                <div>Acões:</div>
            </div>
        </div>
        <div id="potion-table-rows">
            <div class="potion-table-row" v-for="potion in potioners" :key="potion.id">
                <div class="order-number">{{potion.id}}</div>
                <div>{{potion.nome}}</div>
                <div>{{potion.qualidade}}</div>
                <div>{{potion.efeito}}</div>
                <div>
                    <ul>
                        <li v-for="(opcional,index) in potion.opcionais" :key="index">
                            {{opcional}}
                        </li>
                    </ul>
                </div>
                <div>
                    <select name="status" id="status">
                        <option value="">Selecione</option>
                        <option value="stat.tipo" v-for="stat in status" :key="stat.id" :selected="potion.status == stat.tipo">{{stat.tipo}}</option>
                    </select>
                    <button class="delete-btn" @click="deletePotion(potion.id)">Cancelar</button>
                </div>
            </div>
        </div>
    </div>
  
</template>

<script>
export default {
    name: 'DashBoard',
    data(){
        return{
            potioners: null,
            potion_id: null,
            status: []
        }
    },
    methods: {
        async getPedidos() {
            const req = await fetch("http://localhost:3000/potioners");

            const data = await req.json();

            this.potioners = data;

            this.getStatus();
        },
        async getStatus() {
            const req = await fetch("http://localhost:3000/status");

            const data = await req.json();

            this.status = data;

        },
        async deletePotion(id){
            const req = await fetch(`http://localhost:3000/potioners/${id}`, {
                method: "DELETE"
            });

            const res = await req.json();

            this.getPedidos();
        }
    },
    mounted() {
        this.getPedidos();
    }

}
</script>

<style scoped>
    #potion-table {
        max-width: 1200px;
        margin: 0 auto;
    }

    #potion-table-header,
    #potion-table-rows,
    .potion-table-row {
        display: flex;
        flex-wrap: wrap;
    }

    #potion-table-header {
        font-weight: bold;
        padding: 12px;
        border-bottom: 3px solid #333;
    }

    #potion-table-header div,
    .potion-table-row div {
        width: 18.5%;
    }

    .potion-table-row {
        width: 100%;
        padding: 12px;
        border-bottom: 1px solid #ccc;
    }

    #potion-table-header .order-id,
    .potion-table-row .order-number {
        width: 7.5%;
    }

    select {
        padding: 12px 6px;
        margin-right: 9px;
    }

    .delete-btn {
        background-color: #222;
        color: #03fc66;
        font-weight: bold;
        border: 2px solid #222;
        border-radius: 10px;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: 0.5s;
    }

    .delete-btn:hover {
        background-color: transparent;
        color: #222;
    }


</style>