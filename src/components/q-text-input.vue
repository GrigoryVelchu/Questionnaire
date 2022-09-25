<template>
    <div class="quest">
        <p class="quest__question">{{quest.question}}</p>
        <p class="quest__clarification">(Пожалуйста, укажите кратко)</p>
        <input type="text" :required="reqiured" maxlength="75" :value="modelValue" @input="$emit('update:modelValue', $event.target.value)">
    </div>
</template>

<script>
  export default {
    name: "q-text-input",
    props: ['quest', 'modelValue'],
    data(){
      return{
        reqiured:true
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