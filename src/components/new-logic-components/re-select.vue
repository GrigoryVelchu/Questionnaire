<template>
    <div class="quest">
        <p class="quest__question">{{quest.title}}</p>
        <p class="quest__clarification">(пожалуйста, укажите один вариант ответа)</p>
        <select :required="required"  @change="$emit('dataValueHandler',valueKey, $event.target.value)">
            <option value="" selected disabled>-Выберете-</option>
            <option v-for="option in quest.options" :value="option.name" :key="option.name">{{option.name}}</option>
        </select>
    </div>
</template>

<script>
  export default {
    name: "re-select",
    props: ['quest','valueKey'],
    data(){
      return{
        required:true
      }
    }
  }
</script>

<style lang="scss" scoped>
    select {
        padding: 1rem;
        width: 100%;
        max-width: 40rem;
        border: 1px solid salmon;
        border-radius: 5px;
    }
</style>