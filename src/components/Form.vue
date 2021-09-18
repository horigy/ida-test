<template>
    <div class="form-wrapper">
        <h1>Добавление товара</h1>
        <form @submit.prevent="onSubmit">
            <label for="name" class="required">Наименование товара</label>
            <input
                type="text"
                id="name"
                class="form-input"
                placeholder="Введите наименование товара"
                required
                v-model="name"
                :class="{ error: $v.name.$error }"
                @change="$v.name.$touch()"
            >
            <p class="errorText" v-if="!$v.name.required && $v.name.$error"> Поле является обязательным </p>
            <p class="errorText" v-if="!$v.name.minLength && $v.name.$error"> Введите верное название </p>
            <label for="desc">Описание товара</label>
            <textarea
                rows="6"
                id="desc"
                class="form-input"
                placeholder="Введите описание товара"
                v-model="desc"
            ></textarea>
            <label for="link" class="required">Ссылка на изображение товара</label>
            <input
                type="text"
                id="link"
                class="form-input"
                placeholder="Введите ссылку"
                required
                v-model="url"
                :class="{ error: $v.url.$error }"
                @change="$v.url.$touch()"
            >
            <p class="errorText" v-if="!$v.url.required && $v.url.$error"> Поле является обязательным </p>
            <label for="price" class="required">Цена товара</label>
            <input
                type="text"
                id="price"
                class="form-input"
                placeholder="Введите цену"
                required
                v-model="price"
                :class="{ error: $v.price.$error }"
                @change="$v.price.$touch()"
            >
            <p class="errorText" v-if="!$v.price.required && $v.price.$error"> Поле является обязательным </p>
            <p class="errorText" v-if="!$v.price.numeric && $v.price.$error"> Введите число </p>
            <button>Добавить товар</button>
        </form>
    </div>
</template>

<script>
import { required, minLength, numeric } from 'vuelidate/lib/validators'
export default {
    data() {
        return {
            name: null,
            desc: "",
            url: null,
            price: null
        }
    },
    validations: {
        name: {
            required,
            minLength: minLength(3)
        },
        url: {
            required
        },
        price: {
            required,
            numeric
        }
    },
    methods: {
        onSubmit() {
            this.$v.$touch()
            if (!this.$v.$invalid) {
                const data = {
                    name: this.name,
                    desc: this.desc,
                    img_link: this.url,
                    price: this.price
                }
                //console.log('valid', data)
                this.$store.dispatch('addItem', data)
                this.name = null
                this.desc = ""
                this.url = null
                this.price = null
                this.$v.$reset()
            }
        }
    },
}
</script>

<style lang="scss" scoped>
.form-wrapper {
    width: 332px;
    margin-right: 16px;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
}

h1 {
  font-size: 28px;
  font-weight: 600;
  margin-bottom: 16px;
}

form {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    color: #49485E;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    padding: 24px;
}

label {
    font-size: 10px;
    margin-bottom: 5px;
    width: 100%;
    text-align: left;
    position: relative;
}

.required::after {
    position: absolute;
    content: '';
    width: 4px;
    height: 4px;
    border-radius: 50%;
    background: #FF8484;
    margin-left: 3px;
    margin-top: 2px;
}

.form-input {
    font-size: 12px;
    padding: 10px 16px;
    margin-bottom: 17px;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    border: none;
    width: 100%;
    box-sizing: border-box;
    &::placeholder {
        color: #B4B4B4;
    }
    &:last-child {
        margin-bottom: 0;
    }
    .error {
        border: 1px solid #FF8484;
    }
}

input.error {
    border: 1px solid #FF8484;
}

.errorText {
    color: #FF8484;
    font-size: 8px;
    margin-top: 4px;
}

button {
    display: inline-block;
    width: 100%;
    padding: 10px;
    text-align: center;
    border-radius: 10px;
    border: none;
    letter-spacing: -0.02em;
    background-color: #7BAE73;
    color: #FFFEFB;
    margin-top: 11px;
}
</style>