<template>
  <form id="app" @submit.prevent="submit">
    <div class="client-info">
      <p class="personal-title">Личные данные</p>
      <p class="description">* Поле обязательное для заполнения</p>
      
      <div class="input-text-wrapper">
        <input
          type="text" 
          class="input-text" 
          :class="$v.surname.$dirty && $v.surname.$error ? 'input-with-error' : ''"
          name="surname-input"
          v-model.trim="$v.surname.$model"
          @blur="$v.surname.$touch()"
        />

        <label
          :class="surname == '' ? '' : 'changed-label'" 
          class="input-text-label"
        >Фамилия*</label>

        <div class="error" v-if="$v.surname.$error">
          <template v-if="!$v.surname.alpha">
            Поле "Фамилия" должно содержать только буквы, пробел или дефис
          </template>
          <template v-else>
            Поле "Фамилия" обязательно для заполнения
          </template>
        </div>
      </div>

      <div class="input-text-wrapper">
        <input
          type="text" 
          class="input-text" 
          :class="$v.name.$dirty && $v.name.$error ? 'input-with-error' : ''"
          name="name-input"
          v-model.trim="$v.name.$model"
          @blur="$v.name.$touch()"
        />

        <label
          :class="name == '' ? '' : 'changed-label'" 
          class="input-text-label"
        >Имя*</label>

        <div class="error" v-if="$v.name.$error">
          <template v-if="!$v.name.alpha">
            Поле "Имя" должно содержать только буквы, пробел или дефис
          </template>
          <template v-else>
            Поле "Имя" обязательно для заполнения
          </template>
        </div>
      </div>

      <div class="input-text-wrapper">
        <input
          type="text" 
          class="input-text" 
          :class="$v.fatname.$error ? 'input-with-error' : ''"
          name="fatname-input"
          v-model.trim="$v.fatname.$model"
        />
        <label
          :class="fatname == '' ? '' : 'changed-label'"
          class="input-text-label"
        >Отчество</label>

        <div class="error" v-if="$v.fatname.$error">
            Поле "Отчество" должно содержать только буквы
        </div>
      </div>
      
      <InputDateField 
        title="Дата рождения*"
        v-on:checked-form="dateBirth = true"
      />
      <div class="select-error" v-if="!dateBirth && submitStatus === 'ERROR'">
          Поле "Дата рождения" обязательно
      </div>
      

      <div class="input-text-wrapper">
        <input
          type="text" 
          class="input-text"
          :class="$v.phone.$dirty && $v.phone.$error ? 'input-with-error' : ''" 
          name="phone-input"
          v-model.trim="$v.phone.$model"
          @blur="$v.phone.$touch()"
        />
        <label
          :class="phone == '' ? '' : 'changed-label'" 
          class="input-text-label"
        >Номер телефона*</label>

        <div class="error" v-if="$v.phone.$error">
          <template v-if="!$v.phone.alpha">
            Поле "Номер телефона" должно содержать только цифры
          </template>
          <template v-else-if="!$v.phone.between">
            Поле "Номер телефона" должно быть в формате 79993456789
          </template>
          <template v-else>
            Поле "Номер телефона" обязательно для заполнения
          </template>
        </div>
      </div>


      <div class="input-text-wrapper">
        <input
          type="text" 
          class="input-text" 
          :class="$v.male.$dirty && $v.male.$error ? 'input-with-error' : ''" 
          name="male-input"
          v-model.trim="$v.male.$model"
        />

        <label
          :class="male == '' ? '' : 'changed-label'" 
          class="input-text-label"
        >Пол</label>

        <div class="error" v-if="$v.male.$error">
          Поле "Пол" должно содержать только буквы
        </div>
      </div>

      <InputSelectorField
        title="Группа клиентов*"
        type="checkbox"
        name="client-group"
        :items="[{name:'vip', value:'VIP'},
                {name:'withTroubles', value:'Проблемные'},
                {name: 'oms', value:'ОМС'}
              ]"
        v-on:checked-form="clientGroup = true"
      />

      <div class="select-error" v-if="!clientGroup && submitStatus === 'ERROR'">
          Поле "Группа клиентов" обязательно
      </div>

      <InputSelectorField
        title="Лечащий врач"
        type="radio"
        name="doctor"
        :items="[{name:'ivanov', value:'Иванов'},
                {name:'zaharov', value:'Захаров'},
                {name: 'chernisheva', value:'Чернышева'}
              ]"
      />

      <InputSelectorField
        title="SMS"
        type="checkbox"
        name="smsSend"
        :items="[{name:'smsSend', value:'Не отправлять СМС'},
              ]"
      />
    </div>

    <div class="client-adress">
      <p class="adress-title">Адрес</p>

      <div class="input-text-wrapper">
        <input
          type="text" 
          class="input-text" 
          :class="$v.postcode.$dirty && $v.postcode.$error ? 'input-with-error' : ''" 
          name="postcode-input"
          v-model.trim="$v.postcode.$model"
        />
        <label
          :class="postcode == '' ? '' : 'changed-label'" 
          class="input-text-label"
        >Почтовый индекс</label>

        <div class="error" v-if="$v.postcode.$error">
          <template v-if="!$v.postcode.alpha">
            Поле "Почтовый индекс" должно содержать только цифры
          </template>
          <template v-else-if="!$v.postcode.minLength || !$v.postcode.maxLength">
            Поле "Почтовый индекс" должно содержать 6 цифр
          </template>
        </div>
      </div>

      <div class="input-text-wrapper">
        <input
          type="text" 
          class="input-text" 
          :class="$v.country.$dirty && $v.country.$error ? 'input-with-error' : ''" 
          name="country-input"
          v-model.trim="$v.country.$model"
        />
        <label
          :class="country == '' ? '' : 'changed-label'" 
          class="input-text-label"
        >Страна</label>

        <div class="error" v-if="$v.country.$error">
            Поле "Страна" должно содержать только буквы, пробел или дефис
        </div>
      </div>

      <div class="input-text-wrapper">
        <input
          type="text" 
          class="input-text" 
          :class="$v.region.$dirty && $v.region.$error ? 'input-with-error' : ''" 
          name="region-input"
          v-model.trim="$v.region.$model"
        />
        <label
          :class="region == '' ? '' : 'changed-label'" 
          class="input-text-label"
        >Область</label>

        <div class="error" v-if="$v.region.$error">
            Поле "Область" должно содержать только буквы
        </div>
      </div>

      <div class="input-text-wrapper">
        <input
          type="text" 
          class="input-text" 
          :class="$v.town.$dirty && $v.town.$error ? 'input-with-error' : ''" 
          name="town-input"
          v-model.trim="$v.town.$model"
        />
        <label
          :class="town == '' ? '' : 'changed-label'" 
          class="input-text-label"
        >Город*</label>

        <div class="error" v-if="$v.town.$error">
          <template v-if="!$v.town.alpha">
            Поле "Город" должно содержать только буквы, пробел или дефис
          </template>
          <template v-else>
            Поле "Город" обязательно для заполнения
          </template>
        </div>
      </div>

      <div class="input-text-wrapper">
        <input
          type="text" 
          class="input-text" 
          :class="$v.street.$dirty && $v.street.$error ? 'input-with-error' : ''" 
          name="street-input"
          v-model.trim="$v.street.$model"
        />
        <label
          :class="street == '' ? '' : 'changed-label'" 
          class="input-text-label"
        >Улица</label>

        <div class="error" v-if="$v.street.$error">
            Поле "Улица" должно содержать только буквы, пробел или дефис
        </div>
      </div>

      <div class="input-text-wrapper">
        <input
          type="text" 
          class="input-text" 
          :class="$v.house.$dirty && $v.house.$error ? 'input-with-error' : ''" 
          name="house-input"
          v-model.trim="$v.house.$model"
        />
        <label
          :class="house == '' ? '' : 'changed-label'" 
          class="input-text-label"
        >Дом</label>

        <div class="error" v-if="$v.house.$error">
            Поле "Дом" должно содержать только цифры
        </div>
      </div>

    </div>

    <div class="client-documents">
      <p class="document-title">Паспорт</p>
      
      <InputSelectorField
        title="Тип документа*"
        type="radio"
        name="typeofd"
        :items="[{name:'pasport', value:'Паспорт'},
                {name:'svidofb', value:'Свидетельство о рождении'},
                {name: 'drivecard', value:'Водительское удостоверение'}
              ]"
        v-on:checked-form="typeDocumentForm = true"
      />
      <div class="select-error" v-if="!typeDocumentForm && submitStatus === 'ERROR'">
          Поле "Тип документа" обязательно
      </div>


      <div class="input-text-wrapper">
        <input
          type="text" 
          class="input-text" 
          :class="$v.seriesofd.$dirty && $v.seriesofd.$error ? 'input-with-error' : ''" 
          name="seriesofd-input"
          v-model.trim="$v.seriesofd.$model"
        />
        <label
          :class="seriesofd == '' ? '' : 'changed-label'" 
          class="input-text-label"
        >Серия</label>

        <div class="error" v-if="$v.seriesofd.$error">
            Поле "Серия" должно содержать только цифры
        </div>
      </div>

      <div class="input-text-wrapper">
        <input
          type="text" 
          class="input-text" 
          :class="$v.numberofd.$dirty && $v.numberofd.$error ? 'input-with-error' : ''" 
          name="numberofd-input"
          v-model.trim="$v.numberofd.$model"
        />
        <label
          :class="numberofd == '' ? '' : 'changed-label'" 
          class="input-text-label"
        >Номер</label>

        <div class="error" v-if="$v.numberofd.$error">
            Поле "Номер" должно содержать только цифры
        </div>
      </div>

      <div class="input-text-wrapper">
        <input
          type="text" 
          class="input-text" 
          name="whogive-input"
          v-model.trim="$v.whogive.$model"
        />
        <label
          :class="whogive == '' ? '' : 'changed-label'" 
          class="input-text-label"
        >Кем выдан</label>
      </div>

      <InputDateField  
        title="Дата выдачи*"
        v-on:checked-form="documentDate = true"
      />

      <div class="select-error" v-if="!documentDate && submitStatus === 'ERROR'">
          Поле "Дата выдачи" обязательно
      </div>

    </div>

    <button type="submit" class="button" :disabled="submitStatus === 'PENDING'">Зарегистрироваться</button>
    <p class="submit-ok" v-if="submitStatus === 'OK'">Клиент успешно создан</p>
    <p class="select-error" v-if="submitStatus === 'ERROR'">Пожалуйста, заполните поля верно</p>
    <p class="submit-pend" v-if="submitStatus === 'PENDING'">Оправка</p>
  </form>
</template>

<script>
import Vue from 'vue'
import Vuelidate from 'vuelidate'
Vue.use(Vuelidate)

import InputSelectorField from './components/InputSelectorField.vue'
import InputDateField from './components/InputDateField.vue'
import { required, alpha, between, minLength, maxLength } from 'vuelidate/lib/validators'


export default {
  components: {
    InputSelectorField,
    InputDateField 
  },
  name: 'App',
   data() {
    return {
      surname: '',
      name: '',
      fatname: '',
      phone: '',
      male: '',
      postcode: '',
      country: '',
      region: '',
      town: '',
      street: '',
      house: '',
      numberofd: '',
      seriesofd: '',
      whogive: '',

      submitStatus: null,

      dateForm: false,
      typeDocumentForm: false,
      clientGroup: false,
      dateBirth: false,
      documentDate: false,
    }
  },
  validations: {
    surname:{
      required,
      alpha: val => /^[а-яёa-zA-Z \-]*$/i.test(val)
    },
    name: {
      required,
      alpha: val => /^[а-яёa-zA-Z \-]*$/i.test(val)
    },
    fatname: {
      alpha: val => /^[а-яёa-zA-Z]*$/i.test(val)
    },
    phone: {
      required,
      alpha: val => /^[0-9]*$/i.test(val),
      between: between(70000000000,79999999999)
    },
    male: {
      alpha: val => /^[а-яёa-zA-Z]*$/i.test(val),
    },
    postcode:{
      alpha: val => /^[0-9]*$/i.test(val),
      minLength: minLength(6),
      maxLength: maxLength(6),
    },
    country:{
      alpha: val => /^[а-яёa-zA-Z \-]*$/i.test(val),
    },
    region:{
      alpha: val => /^[а-яёa-zA-Z \-]*$/i.test(val),
    },
    town:{
      required,
      alpha: val => /^[а-яёa-zA-Z \-]*$/i.test(val),
    },
    street:{
      alpha: val => /^[а-яёa-zA-Z \-]*$/i.test(val),
    },
    house:{
      alpha: val => /^[0-9]*$/i.test(val),
    },
    numberofd:{
      alpha: val => /^[0-9]*$/i.test(val),
    },
    seriesofd:{
      alpha: val => /^[0-9]*$/i.test(val),
    },
    whogive:{}
  },
  methods: {
    submit() {
      console.log('submit!')
      this.$v.$touch()
      if (this.$v.$invalid) {
        this.submitStatus = 'ERROR'
      } else {
        this.submitStatus = 'PENDING'
        setTimeout(() => {
          this.submitStatus = 'OK'
        }, 500)
      }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Roboto', sans-serif;
  padding: 30px 10px;
}

.description{
  font-style: italic;
  margin: 10px;
}

.personal-title, .adress-title, .document-title{
  margin: 50px 11px 20px;
  font-size: 18px;
  font-weight: 500;
}

.personal-title{
  margin: 10px 11px 0;
}

.input-text-wrapper{
  position: relative;

  max-width: 450px;
  width: 80%;

  margin: 10px 10px 0;
}

.input-text{
  font-size: 18px;
  background-color: rgba(0, 0, 0, 0);

  margin: 1px;

  width: calc(100% - 32px);
  height: 36px;
  padding: 18px 16px 0;

  border: 1px solid rgb(121, 121, 121);
  border-radius: 10px;
}

input:focus{
  outline:none;

  border: 2px solid rgb(130, 130, 255);
  margin: 0;
}

.input-text-label{
  color: rgb(121, 121, 121);
  position: absolute;
  z-index: -1;

  height: 20px;
  top: 18px;
  left: 18px;
  margin: 0;
}

input:focus+label, .changed-label{
  top: 8px;
  font-size: 14px;
  color:rgb(130, 130, 255);
}

.input-with-error{
  border: 1px solid rgb(255, 130, 130);
}

.input-with-error:focus{
  border: 2px solid rgb(255, 130, 130);
}

.error, .select-error{
  color:rgb(255, 130, 130);
  margin: 10px 0;
}

.submit-ok, .submit-pend, .select-error{
  margin: 10px;
}

.submit-ok{
  color:rgb(27, 110, 27);
}

.submit-pend{
  color: rgb(130, 130, 255);
}

.button, .button:active{
  display: inline-block;

  border: 2px solid rgb(130, 130, 255);
  background-color: rgb(130, 130, 255);
  
  height: 56px;
  width: 100%;
  padding: 9px 19px;
  border-radius: 10px;

  max-width: 450px;

  margin: 10px;

  font-size: 18px;
  color: white;
  cursor: pointer;
}

.button:hover{
  background-color: white;
  color: rgb(130, 130, 255);
}
</style>
