<template>
   <main class="main">
        <div class="main__container container"> 
            <AsidePanel @productItem="addedItem" />
            <ProductList 
                :products="products"
                @deleteProduct="deleteInArray"
            />
            <transition name="fade">
                <AlertMessage
                    v-if="showAlert"
                />
            </transition>
        </div>
    </main>
</template>

<script>
import AsidePanel from '@/components/AsidePanel'
import ProductList from '@/components/ProductList'
import AlertMessage from '@/components/AlertMessage'

export default {
    components: { AsidePanel, ProductList, AlertMessage },
    props: {
        products: {
            type: Array,
            required: true
        }
    },
    data() {
        return {
            showAlert: false
        }
    },
    methods: {
        // Удаляем элемент из массива
        deleteInArray(id) {    
            // Ищем товар с нужным ID и убираем из массива 
            const index = this.products.findIndex(arr => arr.id == id)
            if( index !== -1) {  this.products.splice(index, 1); }
        },
        // Добавляем новый item в массив
        addedItem(item, success) {
            this.products.push(item);
            if(success) {          
                this.showAlert = true;
                setTimeout(() => {
                    this.showAlert = false;
                }, 2000)
            }
        }
    }
}
</script>

<style>
.main {
    margin-top: 16px;
    padding-bottom: 50px;
}

.main__container {
    display: grid;
    grid-template-columns: 1fr 3fr;
    column-gap: 16px;
}

@media screen and (max-width: 768px) {
    .main__container  { grid-template-columns: 1fr; gap: 16px; }
}

</style>