<template>
    <div class="addItem">
        <input type="text" v-model="item.name">
        <font-awesome-icon
        icon="plus-square"
        @click.prevent="addItem()"
        v-bind:class="[item.name ? 'active' : 'inactive' , 'plus' ] "
         />
    </div>
</template>

<script>
export default {
    data:function(){
        return {
            item:{
                name: ""
            }
        }
    },
    methods:{
        addItem(){
            if(this.item.name == ''){
                return false;
            }

            axios.post('api/items/store',{
                item : this.item
            })
            .then(response => {
                if(response.status == 201){
                    this.item.name = "";
                    this.$emit('reloadlist');
                    // alert('dfd');
                }
            })
            .catch(error =>{
                console.log(error);
            })
        }
    }
}
</script>
<style scoped>
.addItem{
    display: flex;
    justify-content: center;
    align-items: center;
}
input[type="text"]{
    background: #f7f7f7;
width: 100%;
border: 0px;
outline: none;
padding: 5px;
margin-right: 11px;
}
.plus{
    font-size: 24px;
}
.active{
    color: #00ce25;
}
.inactive{
    color:#999999;
}
</style>
