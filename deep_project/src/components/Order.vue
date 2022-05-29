<template>
 <div class="order">
     <form>
         <p class="section-title">Seus dados</p>
         <div class="input-field">
        <label for="">{{formData.name.label}}</label>
         <input type="text"
          :placeholder="formData.name.placeholder" 
         v-model="formData.name.value"
          @blur="formData.name.isValid()" 
         :class="{'error' : !formData.valid}">
         <p class="error-message" v-if="!formData.name.valid">{{formData.name.errorMessage}}</p>
         </div>

         <div class="input-field">
        <label for="">{{formData.cellphone.label}}</label>
         <input
                        type="text"
                        :placeholder="formData.cellphone.placeholder"
                        v-mask="'(##) # ####-####'"
                        v-model="formData.cellphone.value"
                        @blur="formData.cellphone.isValid()"
                        :class="{ error: !formData.cellphone.valid }"
                    />
                    <p class="error-message" v-if="!formData.cellphone.valid">{{ formData.cellphone.errorMessage }}</p>
         </div>
     </form>
     <button class="primary-button" @click="orderItens">Concluir pedido</button>
 </div>
</template>

<script>
export default {
    data() {
        return {
            formData: {
                name: {
                    value: '',
                    placeholder: 'Digite o seu nome',
                    errorMessage: 'O nome é obrigatório',
                    label: 'Nome*', 
                    valid: true,
                    isValid: () => {
                        this.formData.name.valid = !!this.formData.name.value.length;
                    }
                },

                cellphone: {
                    value: '',
                    placeholder: 'Digite o seu celular',
                    errorMessage: 'O celular é obrigatório',
                    label: 'Celular*', 
                    valid: true,
                    isValid: () => {
                        this.formData.cellphone.valid = this.formData.cellphone.value.length === 16;
                    }
                }
            }
        }
    },
    methods: {
        triggerValidations() {
            this.formData.name.isValid();
            this.formData.cellphone.isValid();
        },
        orderItens() {
            this.triggerValidations();
        }
    }
}
</script>

<style lang="less" scoped>
.order {
    width: 720px;
    margin: 30px auto;
    background: #292929;
    border-radius: 8px;
    padding: 30px 50px;

    form {
        display: flex;
        flex-direction: column;

        .input-field {
            display: flex;
            flex-direction: column;

            & + .input-field {
                margin-top: 15px;
            }
        }

        .section-title {
            color: @write;
            font-weight: 600;
            font-size: 27px;
            margin-bottom: 20px;
        }

        label {
            color: @write;
            font-weight: 500;
            font-size: 16px;
            margin-bottom: 5px;
        }

        .error-message{
            font-size: 12px;
            color: @error-color;

        }
    }

    button {
        margin: 30px auto;
    }
}

</style>