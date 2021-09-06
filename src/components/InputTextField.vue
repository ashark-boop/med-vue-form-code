<template>
  <div class="input-text-wrapper">
    <input :type="type ? type : 'text'" class="input-text" :name="name+'-input' "
      @focus="inputChanged = true" 
      @blur="inputText == '' ? inputChanged = false : true"
      v-model="inputText"
    />
    <p :class="inputChanged ? 'input-text-label changed-text-label': 'input-text-label'">{{ title }}</p>
  </div>
</template>

<script>
export default {
  name: 'InputTextField',
  data() {
    return {
      inputText: '',
      inputChanged: false,
    }
  },
  props: {
    title: String,
    name: String,
    type: String,
  },
  methods: {
  }
}
</script>


<style>
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

  .changed-text-label{
    top: 8px;
    font-size: 14px;
    color:rgb(130, 130, 255);
  }
</style>
