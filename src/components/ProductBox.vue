<template>
    <div class="column is-3">
        <div class="box">
            <figure class="image mb-4">
                <img v-bind:src="product.image">
            </figure>

            <h3 class="is-size-4">{{ product.title }}</h3>
            <p class="is-size-6 has-text-grey">${{ product.price }}</p>

            <div class="infoBtn">
                <div class="control" style="width: 50px;" >
                    <input type="number" class="input" min="1" v-model="quantity">
                </div>

                <button @click="addToCart()" class="button is-dark">Add To Cart</button>                
            </div>
            
          
        </div>
        
    </div>
</template>

<script>
import { toast } from 'bulma-toast'


export default {
    name: 'ProductBox',
    data(){
        return{
            quantity: 1
        }
    },
    props: {
        product: Object
    },
    methods:{
        addToCart() {
            if (isNaN(this.quantity) || this.quantity < 1) {
                this.quantity = 1
            }

            const item = {
                product: this.product,
                quantity: this.quantity
            }

            this.$store.commit('addToCart', item)

            toast({
                message: 'The product was added to the cart',
                type: 'is-success',
                dismissible: true,
                pauseOnHover: true,
                duration: 2000,
                position: 'bottom-right',
            })
        },
    }

 
}
</script>

<style scoped>
  .image {
    margin-top: -1.25rem;
    margin-left: -1.25rem;
    margin-right: -1.25rem;
  }
  .infoBtn{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
</style>