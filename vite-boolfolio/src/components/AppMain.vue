<template>
    <div>
        <h1 class="main-title">
            Products:
        </h1>
        <div class="products">
            <div class="single-product" v-for="product in products">
                <h2>
                    {{ products.name }}
                </h2>
                <h3>
                    Infos: {{ products.description }}
                </h3>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'AppMain',

    data() {
        return {
            products : [],
            apiUrl : 'http://127.0.0.1:8000/api/products'
        }
    },

    methods: {
        getProducts(){
            axios.get(this.apiUrl, {
                params: {}
            })
            .then((response) => {
                console.log(response.data.results.data)
                this.products = response.data.results.data;
            })
            .catch(function (error) {
                console.log(error);
            })
        }
    },

    created(){
        this.getProducts();
    }
}

</script>

<style lang="scss">

    h1.main-title{
        margin-bottom: 3rem;
    }

    div.products{
        display: flex;
        justify-content: center;
        align-items: center;
        flex-wrap: wrap;

        div.single-product{
            width: calc((100% / 2) - 1rem);
            border-radius: 1rem;
            padding: 1rem;
            margin-right: 1rem;
            background-color: rgb(221, 221, 221);
            color: black;
            margin-bottom: 2rem;

            *{
                margin-bottom: 1rem;
            }

            h6 span{
                margin-right: 1rem;
            }

            &:hover{
                background-color: white;
            }
        }
    }
</style>