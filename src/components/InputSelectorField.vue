<template>
  <div class="selector-wrapper">
    <p v-if="title" class="selector-title">{{ title }}</p>

    <div class="selector-item-wrapper" v-for="item in items" :key="item.name">
      <input 
        class="input-selector" 
        :type="type ? type : 'radio'" 
        :name="name+'-selector-input'" 
        :value="item.name"
        :id="item.name+'-selector-input'"
      />
      <label 
        class="form-label" 
        :for="item.name+'-selector-input'"
      >
        <p>{{ item.value }}</p>
      </label>
    </div>

  </div>
</template>

<script>

export default {
  name: 'InputSelectorField',
  data() {
    return{
      selected:'',
    }
  },
  props: {
    title: String,
    name: String,
    type: String,
    items: Array,
    validations: Array,
  }
}
</script>


<style>
.selector-wrapper{
  margin: 10px 10px 0;
  max-width: 450px;
  width: 80%;
}

.selector-title{
  flex-basis: 100%;
}

.input-selector{
  opacity: 0;
  position: absolute;
  z-index: -1;
}

.selector-item-wrapper{
  height: 54px;
  padding: 5px 0;
  margin: 0;

  flex-basis: 100%;

  display: flex;
  justify-content: start;
}

.form-label{
  width: 80%;
  height: 100%;
  border-radius: 10px;
  cursor: pointer;

  border: 1px solid rgb(121, 121, 121);
}

.form-label > p{
  text-align: center;
  font-size: 16px;
}

.input-selector:checked+.form-label{
  border: 1px solid rgb(130, 130, 255);
  color: rgb(130, 130, 255);
}
</style>