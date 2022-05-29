<template>
 <div class="order">
    <form>
        <div class="user-data">
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
        </div>

        <div class="adress">
            <p class="section-title">Endereço</p>
        
            <div class="delivery-type">
                <div class="radio-options">
                    <input type="radio" name="delivery-type" id="store" value="store" v-model="deliveryType"/>
                    <label for="store">Retirar na loja</label>
                </div>


                <div class="delivery-type">
                <div class="radio-options">
                    <input type="radio" name="delivery-type" id="delivery" value="delivery" v-model="deliveryType"/>
                    <label for="delivery">Delivery</label>
                </div>
            </div>
        </div>
             <div class="adress-card" v-if="isDeliveryType && hasAdressInfo && savedAdress">
                <p>{{formData.city.value}} - {{formData.cep.value}}</p>
                <p> {{formData.street.value}} , {{formData.number.value}} </p>
               
            </div>
         <a @click="onShowAdressModal" v-if="isDeliveryType">{{addressButtonLabel}}</a>
        </div>
    </form>
     <button class="primary-button" @click="orderItens">Concluir pedido</button>

     <Modal :show="showAdressModal" @on-modal-close="hideAdressModal">
        <div class="modal-content">
            <h1>Adicionar endereço</h1>
            <div class="input-field">
            <label for="">{{formData.cep.label}}</label>
            <input type="text"
            :placeholder="formData.cep.placeholder" 
            v-model="formData.cep.value"
            @blur="formData.cep.isValid()" 
            :class="{'error' : !formData.valid}">
            <p class="error-message" v-if="!formData.cep.valid">{{formData.cep.errorMessage}}</p>
         </div>

         <div class="input-field">
            <label for="">{{formData.city.label}}</label>
            <input type="text"
            :placeholder="formData.city.placeholder" 
            v-model="formData.city.value"
            @blur="formData.city.isValid()" 
            :class="{'error' : !formData.valid}">
            <p class="error-message" v-if="!formData.city.valid">{{formData.city.errorMessage}}</p>
         </div>

         <div class="adress-container">
             <div class="input-field">
            <label for="">{{formData.street.label}}</label>
            <input type="text"
            :placeholder="formData.street.placeholder" 
            v-model="formData.street.value"
            @blur="formData.street.isValid()" 
            :class="{'error' : !formData.valid}">
            <p class="error-message" v-if="!formData.street.valid">{{formData.street.errorMessage}}</p>
            </div>

            <div class="input-field">
            <label for="">{{formData.number.label}}</label>
            <input type="text"
            :placeholder="formData.number.placeholder" 
            v-model="formData.number.value"
            @blur="formData.number.isValid()" 
            :class="{'error' : !formData.valid}">
            <p class="error-message" v-if="!formData.number.valid">{{formData.number.errorMessage}}</p>
            </div>
         </div>   
         
         <button class="primary-button" @click="validateAdressForm">Adicionar</button>
         <button class="secondary-button" @click="hideAdressModal">Cancelar</button>

        </div>
     </Modal>
 </div>
</template>

<script>
import Modal from '@/components/Modal';

export default {
    components: {
        Modal 
    },
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
                        this.formData.cellphone.valid = !!this.formData.cellphone.value.length === 16;
                    }
                },

                cep: {
                    value: '',
                    placeholder: 'Digite o seu cep',
                    errorMessage: 'O cep é obrigatório',
                    label: 'CEP*', 
                    valid: true,
                    isValid: () => {
                        this.formData.cep.valid = !!this.formData.cep.value.length;
                    }
                },

                city: {
                    value: '',
                    placeholder: 'Digite o sua cidade',
                    errorMessage: 'A cidade é obrigatória',
                    label: 'Cidade*', 
                    valid: true,
                    isValid: () => {
                        this.formData.city.valid = !!this.formData.city.value.length;
                    }
                },

                street: {
                    value: '',
                    placeholder: 'Digite sua rua',
                    errorMessage: 'A rua é obrigatória',
                    label: 'Rua*', 
                    valid: true,
                    isValid: () => {
                        this.formData.street.valid = !!this.formData.street.value.length;
                    }
                }, 

                 number: {
                    value: '',
                    placeholder: 'Digite o número',
                    errorMessage: 'O número é obrigatório',
                    label: 'Número*', 
                    valid: true,
                    isValid: () => {
                        this.formData.number.valid = !!this.formData.number.value.length;
                    }
                },
            }, 
            showAdressModal: false,
            deliveryType: '',
            savedAdress: false
        };
    },
    computed: {
        isAddressFormValid() {
            let isValid = true;
            isValid &= this.formData.cep.valid;
            isValid &= this.formData.city.valid;
            isValid &= this.formData.street.valid;
            isValid &= this.formData.number.valid;
            return isValid;
        },
        isDeliveryType() {
            return this.deliveryType === 'delivery';
        },
        hasAdressInfo () {
            return (
            this.formData.cep.value|| 
            this.formData.city.value||
            this.formData.street.value||
            this.formData.number.value
            );
        },
        addressButtonLabel() {
            return this.hasAdressInfo ? 'Editar Endereço' : 'Adicionar endereço '
        },
    },

    methods: {
        triggerValidations() {
            this.formData.name.isValid();
            this.formData.cellphone.isValid();
        },
        triggerAdressFormValidations() {
            this.formData.cep.isValid();
            this.formData.city.isValid();
            this.formData.street.isValid();
            this.formData.number.isValid();
        },
        orderItens() {
            this.triggerValidations(); 
        }, 
        onShowAdressModal() {
            this.showAdressModal = true;
        },
        hideAdressModal() {
            this.showAdressModal = false; 
        }, 
        validateAdressForm() {
            this.triggerAdressFormValidations();
            if(!this.isAddressFormValid) return;
            this.savedAdress = true;
            this.showAdressModal = false;
        }
    }
};
</script>

<style lang="less" scoped>
.order {
    width: 720px;
    margin: 30px auto;
    background: #292929;
    border-radius: 8px;
    padding: 30px 50px;

    .input-field {
            display: flex;
            flex-direction: column;


            .error-message{
                font-size: 12px;
                color: @error-color;

                }

            label {
            color: @write;
            font-weight: 500;
            font-size: 16px;
            margin-bottom: 5px;
        }

            & + .input-field {
                margin-top: 15px;
            }
        }

        .adress-container {
            display: flex;
            margin-top: 15px;

            .input-field {
                margin: 0;
                width: 100%;



                & + .input-field {
                    width: 30%;
                    margin-left: 15px;
                }
            }


        }

    form {
        display: flex;
        flex-direction: column;


        .section-title {
            color: @write;
            font-weight: 600;
            font-size: 27px;
            margin-bottom: 20px;
        }

        

        .adress{
            .delivery-type{
            color: @write;
            display: flex;

        }

        a {
            color: @blue;
            font-weight: normal;
            font-size: 12px;
            text-decoration: underline;
            cursor: pointer;
            margin: 15px 0;
            display: block;
            width: fit-content;
        }
        
        .adress-card {
            border-radius: 8px;
            border: 1px solid @write;
            padding: 10px 20px;
            margin: 15px 0; 
            width: fit-content;


            p{
                font-weight: normal;
                font-size: 16px;
                color: @write;
                margin: 5px 0;
            }
        }

        }
        

        .radio-options{
            display: flex;
            align-items: center;

            & + .radio-options {
                margin-left: 25px;
            }


            label {
                padding-left: 10px;
                margin: 0;
            }
        }
    }

    button {
        margin: 30px auto;
    }

    .modal-content {
        button{
            text-align: center;

            & + button { 
                margin-left: 15px;
            }
        }
    }
}

</style>