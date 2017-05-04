<template>  
    Resuorce Content

    <button @click="onButtonClick">get foo.json</button> 
    \{{fooMessage}}

</template>  
<script>  
    export default{
        data () {
            return {
                fooMessage: ''
            }
        },
        methods :{
            onButtonClick() {
                var foo = this;
                this.$http.get('/foo.json').then(
                (response) => {
                    //console.log('TESTE: '+response.data.msg);
                    //Usando JSON não funcionou, li direto do DATA.
                    //foo.fooMessage = JSON.parse(response.data).msg
                    foo.fooMessage = response.data.msg
                },
                (error) => {
                     console.error(error.statusText)
                })
            }
        }
    }    
</script>