<template>
    <header class="header">
        <div class="header__container container">
            <h1>Добавление товара</h1>
            <MySelect 
                v-model="SelectedSort"
                :options="sortOptions"
            />
        </div>
    </header>
</template>

<script>
import MySelect from '@/components/MySelect'

export default {
    components: { MySelect },
    data() {
        return {
            SelectedSort: '',
            sortOptions: [
                { value: 'title', name: 'По названию' },
                { value: 'min',   name: 'Сначала подешевле' },
                { value: 'max',   name: 'Сначала подороже' },
            ]
        }
    },
    watch: {
        SelectedSort(newValue) {
            this.$emit('sortName', newValue);
        }
    }
}
</script>

<style>
header.header {
    margin-top: 31px;
}

.header__container {
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.cs-filter { 
    display: inline-block;
    color: #B4B4B4;
    background: #FFFEFB;
    box-shadow:  0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    padding: 10px 16px; 
    box-sizing: border-box; 
    border: none;
    margin: 0; 
    -moz-appearance: none;
    -webkit-appearance: none;
    appearance: none;
    background-image: url('../assets/arrow.svg'), linear-gradient(to bottom, #FFFEFB 0%,#FFFEFB 100%); 
    background-repeat: no-repeat;
    background-position: right .7em top 50%, 0 0;
} 

.cs-filter:focus,
.cs-filter:active {
    outline: none;
}

@media screen and (max-width: 768px) {
    .header__container {
        flex-wrap: wrap;
        gap: 16px;
    }
}
</style>