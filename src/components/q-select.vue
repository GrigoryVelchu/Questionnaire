<template>
    <div class="quest">
        <p class="quest__question">{{quest.question}}</p>
        <p class="quest__clarification">(пожалуйста, укажите один вариант ответа)</p>
        <select required :value="modelValue" @change="$emit('update:modelValue', $event.target.value)">
            <option value="" selected disabled>-Выберете-</option>
            <option v-for="option in quest.options" :value="option" :key="option">{{option}}</option>
        </select>
    </div>
</template>

<script>
  export default {
    name: "q-select",
    props: ['quest', 'modelValue']
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