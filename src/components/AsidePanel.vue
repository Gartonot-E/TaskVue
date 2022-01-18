<template>
    <aside class="main__aside cs-aside">
        <div class="cs-aside__wrapper">
            <label>
                <span class="required">Наименование товара</span>
                <input 
                    v-model="product.title"
                    type="text" 
                    placeholder="Введите наименование товара"
                    :class="isInvalidTitle ? 'invalid' : false"
                />
                <small>Поле является обязательным</small>
            </label>
            <label>
                <span>Описание товара</span>
                <textarea 
                    v-model="product.body"
                    cols="30" 
                    rows="8" 
                    placeholder="Введите описание товара"
                ></textarea>
            </label>
            <label>
                <span class="required">Ссылка на изображение товара</span>
                <input 
                    v-model="product.imgUrl"
                    type="text"  
                    placeholder="Введите ссылку"
                    :class="isInvalidUrlImg ? 'invalid' : false"
                />
                <small>Поле является обязательным</small>
            </label>
            <label>
                <span class="required">Цена товара</span>
                <input 
                    v-model="product.price"
                    type="text" 
                    placeholder="Введите цену"
                    @input="validPrice"
                    maxlength="7"
                    :class="isInvalidPrice ? 'invalid' : false"
                />
                <small>Поле является обязательным</small>
            </label>
            <input 
                class="btn"
                type="submit" 
                value="Добавить товар"
                :disabled="isInvalid"
                @click="validate"
                :class="successForm ? 'success' : false"
            >
        </div>
    </aside>
</template>

<script>
export default {
    data() {
        return {
            product: {
                title: '',
                body: '',
                imgUrl: '',
                price: ''
            },
            isInvalid: true,
            isInvalidTitle: false,
            isInvalidUrlImg: false,
            isInvalidPrice: false,
            successForm: false
        }
    },
    watch: {
        product: {
            handler() {
                this.isInvalid = false
            },
            deep: true
        }
    },
    methods: {
        // Валидируем Price чтоб подставлять пробелы между тысичами
        validPrice () {
            let str = this.product.price.replace(' ', '');

            // Отделяем пробелами
            if (str.length == 6) { str = str[0] + str[1] + str[2] + " " + str.substr(3); }
            if (str.length == 5) { str = str[0] + str[1] + " " + str.substr(2); }
            if (str.length == 4) { str = str[0] + " " + str.substr(1); }
            this.product.price = str;
        },
        // Валидация полей из формы
        validate() {
            // Проверяем не пустые ли поля
            if(this.product.title.length == 0) { this.isInvalidTitle = true }
            if(this.product.imgUrl.length == 0) { this.isInvalidUrlImg = true }
            if(this.product.price.length == 0) { this.isInvalidPrice = true }
            
            if(this.product.title.length != 0) { this.isInvalidTitle = false }
            if(this.product.imgUrl.length != 0) { this.isInvalidUrlImg = false }
            if(this.product.price.length != 0) { this.isInvalidPrice = false }

            // Если поля заполненны, то отправлям данные 
            if(this.product.price.length != 0 && this.product.imgUrl.length != 0 && this.product.title.length != 0) {
                this.isInvalidTitle = false;
                this.isInvalidUrlImg = false;
                this.isInvalidPrice = false;
                this.successForm = true;
                this.product.id = Date.now();
                this.$emit('productItem', this.product, this.successForm)
                this.product = {
                    title: '',
                    body: '',
                    imgUrl: '',
                    price: ''
                }
            }
        }
    }
}
</script>

<style>
.cs-aside {
    position: sticky;
    top: 24px;
    height: fit-content;
    z-index: 2;
}

.cs-aside__wrapper {
    background: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    padding: 24px;
    display: flex;
    flex-direction: column;
    gap: 16px;
}

.cs-aside__wrapper label {
    display: flex;
    flex-direction: column;
    row-gap: 4px;
}

.cs-aside__wrapper label span {
    font-weight: 400;
    font-size: 12px;
    letter-spacing: -0.02em;
    line-height: 13px;
}

.cs-aside__wrapper label span.required {
    position: relative;
}

.cs-aside__wrapper label span.required::after {
    content: "";
    position: absolute;
    width: 4px;
    height: 4px;
    border-radius: 4px;
    background: #FF8484;
    transform: translate(2px, 2px);
}

.cs-aside__wrapper label input,
.cs-aside__wrapper label textarea {
    background: #FFFEFB;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    padding: 10px 16px;
    border: none;
    font-size: 12px;
    resize: none;
}

.cs-aside__wrapper label input:focus,
.cs-aside__wrapper label input:active,
.cs-aside__wrapper label textarea:focus,
.cs-aside__wrapper label textarea:active {
    outline: 2px solid teal;
}

.cs-aside__wrapper input.btn {
    margin-top: 24px;
    background: #EEEEEE;
    color: #B4B4B4;
    border-radius: 10px;
    border: none;
    font-size: 12px;
    line-height: 15px;
    letter-spacing: -0.02em;
    padding: 10px 0;
    text-align: center;
    font-weight: 600;
    transition: .3s;
}

.cs-aside__wrapper input.btn.success {
    background: #7BAE73;
    color: #fff;
}

.cs-aside__wrapper input.btn:hover {
    background: teal;
    cursor: pointer;
    color: #fff;
}

.cs-aside__wrapper input.btn[disabled] {
    cursor: not-allowed;
    background: #EEEEEE;
    color: #B4B4B4;
}

.cs-aside__wrapper label input.invalid {
    border: 1px solid #FF8484;
}

.cs-aside__wrapper label small {
    display: none;
}

.cs-aside__wrapper label input.invalid + small {
    color: #FF8484;
    font-size: 12px;
    display: block;
}
</style>