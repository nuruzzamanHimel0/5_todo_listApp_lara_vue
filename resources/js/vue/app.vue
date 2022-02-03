<template>
    <div id="todolistContainer">
        <div class="heading">
            <h2 class="title">To DO list Title</h2>
            <addItemForm
                v-on:reloadlist = "getList()"
            />
        </div>
        <list-view
        :items="items"
        v-on:reloadlist = "getList()"
         />
    </div>
</template>

<script>
import addItemForm from './addItemForm.vue'
import listView from './listView.vue'
export default {
    data(){
        return {
            items: [],
        }
    },
    created(){
        this.getList();
    },
    methods:{
        getList(){
            axios.get('api/items')
            .then(response =>{
                this.items = response.data;
            })
            .catch((error) => {
                console.log(error);
            });
        }
    },
    components:{
        addItemForm,
        listView
    }
}
</script>

<style scoped>
    #todolistContainer{
        width: 350px;
        margin: auto;
    }
    .heading{
        padding:10px;
        background:#ddd;
    }
    .title{
        text-align: center;
    }
</style>
