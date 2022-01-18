<template>
    <section class="main__goods cs-goods">
        <div class="goods__list">
            <ProductItem 
                class="goods__item"
                v-for="productOne in products"
                :key="productOne.id"
                :product="productOne"
                @deleteProduct="deleteProduct"
            />
        </div>
    </section>
</template>

<script>
import ProductItem from '@/components/ProductItem'

export default {
    components: { ProductItem },
    props: {
        products: {
            type: Array,
            required: true
        }
    },
    methods: {
        deleteProduct(data) {
            this.$emit('deleteProduct', data)
        }
    }
}
</script>

<style>

.goods__list {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(299px, 1fr));
    gap: 16px;
}

.goods__item {
    background: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    position: relative;
}

.goods__item .delete {
    position: absolute;
    right: -10px;
    top: -10px;
    background: #FF8484;
    padding: 8px 9px;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    cursor: pointer;
    opacity: 0;
    transition: .3s;
}

.goods__item:hover .delete {
    opacity: 1;
}

.goods__item img {
    width: 100%;
    height: auto;
    object-fit: cover;
}

.goods__item h3 {
    margin: 16px;
    font-weight: 600;
    font-size: 20px;
    line-height: 25px;
    color: #3F3F3F;
}

.goods__item p {
    margin: 16px;
    line-height: 20px;
    color: #3F3F3F;
}

.goods__item span {
    margin: 32px 0 24px 16px;
    display: block;
    font-weight: 600;
    font-size: 24px;
    line-height: 30px;
    color: #3F3F3F;
    align-self: flex-start;    
}
</style>