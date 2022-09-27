<template>
    <div class="quest">
        <p class="quest__question">{{quest.title}}</p>
        <p class="quest__clarification">(Пожалуйста, укажите кратко)</p>
        <input type="text" :required="reqiured" maxlength="75" value="" @input="$emit('dataValueHandler',valueKey, $event.target.value)">
    </div>
</template>

<script>
  export default {
    name: "re-text-input",
    props: ['quest', 'currentValue','valueKey'],
    data(){
      return{
        reqiured:false
      }
    }
  }
</script>
<style lang="scss" scoped>
    input{
        padding: 1rem;
        width: 100%;
        max-width: 45rem;
        border: 1px solid salmon;
        border-radius: 5px;
    }
</style>