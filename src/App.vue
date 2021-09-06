<template>
  <div id="app">
    <div class="client-info">
      <p class="personal-title">Личные данные</p>
      
      <InputTextField 
        name="surname" 
        title="Фамилия*"
      />

      <InputTextField 
        name="name" 
        title="Имя*"
      />

      <InputTextField 
        name="fathname" 
        title="Отчество"
      />
      
      <InputDateField 
        title="Дата рождения*"
      />
      
      <InputTextField 
        name="phone" 
        title="Номер телефона*" 
        type="number"
      />

      <InputTextField 
        name="sex" 
        title="Пол"
      />

      <InputSelectorField
        title="Группа клиентов*"
        type="checkbox"
        name="client-group"
        :items="[{name:'vip', value:'VIP'},
                {name:'withTroubles', value:'Проблемные'},
                {name: 'oms', value:'ОМС'}
              ]"
      />

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

      <InputTextField 
        name="post-code" 
        title="Индекс"
      />

      <InputTextField 
        name="country" 
        title="Страна"
      />

      <InputTextField 
        name="oblast" 
        title="Область"
      />

      <InputTextField 
        name="town" 
        title="Город*"
      />

      <InputTextField 
        name="street" 
        title="Улица"
      />

      <InputTextField 
        name="house" 
        title="Дом"
      />

    </div>

    <div class="client-documents">
      <p class="document-title">Паспорт</p>
      
      <InputSelectorField
        title="Тип документа"
        type="radio"
        name="typeofd"
        :items="[{name:'pasport', value:'Паспорт'},
                {name:'svidofb', value:'Свидетельство о рождении'},
                {name: 'drivecard', value:'Водительское удостоверение'}
              ]"
      />

      <InputTextField 
        name="seriesofd" 
        title="Серия"
      />

      <InputTextField 
        name="numberofd" 
        title="Номер"
      />
      
      <InputTextField 
        name="whofive" 
        title="Кем выдан"
      />
      <InputDateField  
        title="Дата выдачи*"
      />

    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import Vuelidate from 'vuelidate'
Vue.use(Vuelidate)

import InputTextField from './components/InputTextField.vue'
import InputSelectorField from './components/InputSelectorField.vue'
import InputDateField from './components/InputDateField.vue'

export default {
  components: { 
    InputTextField,
    InputSelectorField,
    InputDateField 
  },
  name: 'App',
  data() {
    return {
      name: '',
      age: 0
    }
  },
}
</script>

<style>
#app {
  font-family: 'Roboto', sans-serif;
}
.personal-title, .adress-title, .document-title{
  margin: 50px 11px 20px;
  font-size: 18px;
  font-weight: 500;
}

.personal-title{
  margin: 30px 11px 0;
}
</style>
