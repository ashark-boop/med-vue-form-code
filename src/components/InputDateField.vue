<template>
  <div class="selectors-date-wrapper">
    <p v-if="title" class="selector-date-title">{{ title }}</p>

    <div class="dates-block">
      <select v-model="selectedDays" class="select-date">
        <option disabled value="">Месяц</option>
        <option class="selector-date-wrapper" 
          v-for="(month, index) in months" 
          :value="month.days" 
          :key="index"
        >
          {{ month.name }}
        </option>
      </select>

      <select class="select-date">
        <option disabled value="">День</option>
        <option class="selector-date-wrapper" 
          v-for="n in selectedDays" 
          :key="n"
          :value="n"
        >
          {{ n }}
        </option>
        <option v-if="selectedDays == 28 && selectedYear % 4 == 0" value="29">29</option>
      </select>

      <select v-model="selectedYear" class="select-date">
        <option disabled value="">Год</option>
        <option class="selector-date-wrapper" v-for="n in 121" :key="n">
          {{ 2022 - n }}
        </option>
      </select>
    </div>
    
  </div>
</template>

<script>

export default {
  name: 'InputSelectorField',
  props: {
    title: String,
    name: String,
    items: Array,
    type: String,
  },
  data(){
    return{
      months: [
        {name: 'Январь', days: 31},
        {name: 'Февраль', days: 28},
        {name: 'Март', days: 31},
        {name: 'Апрель', days: 30},
        {name: 'Май', days: 31},
        {name: 'Июнь', days: 30},
        {name: 'Июль', days: 31},
        {name: 'Август', days: 31},
        {name: 'Сентябрь', days: 30},
        {name: 'Октябрь', days: 31},
        {name: 'Ноябрь', days: 30},
        {name: 'Декабрь', days: 31},
      ],
      selectedDays: 30,
      selectedYear: 2021,
    }
  }
}
</script>


<style scoped>
  .selectors-date-wrapper{
    margin: 10px 11px 0;
    max-width: 450px;
    width: 80%;
  }

  .selector-date-title{
    color:rgb(121, 121, 121);
  }

  .dates-block{
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;

    width: 100%;
  }

  .select-date{
    border: 1px solid rgb(121, 121, 121);
    background: white;
    border-radius: 10px;

    min-height: 54px;
    font-size: 18px;
    text-align: center;

    box-sizing: border-box;
    padding: 1px 16px;

    margin: 5px 0;
  }

  .select-date:nth-child(1){
    flex-basis: 40%;
  }
  .select-date:nth-child(2){
    flex-basis: 20%;
  }
  .select-date:nth-child(3){
    flex-basis: 30%;
  }

  select:focus{
    outline:none;

    border: 2px solid rgb(130, 130, 255);
    padding: 0 15px;
  }
</style>