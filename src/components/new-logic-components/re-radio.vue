<template>
    <div class="quest">
        <p class="quest__question">{{quest.title}}</p>
        <p class="quest__clarification">(пожалуйста, укажите один вариант ответа)</p>
        <div v-if="htmlFormat">
            <div  class="quest__input_container" v-for="option in quest.options" :key="option.name">
                <input type="radio" :id="option.name" :required="required"
                       :name="quest.title" @click="$emit('dataValueHandler',valueKey, option.name)">
                <label v-html="option.name" class="label" :for="quest.title"></label>
            </div>
        </div>
        <div v-else>
            <div  class="quest__input_container" v-for="option in quest.options" :key="option.name">
                <input type="radio" :id="option.name" :required="required"
                       :name="quest.title" @click="$emit('dataValueHandler',valueKey, option.name)">
                <label class="label" :for="quest.title">{{option.name}}</label>
            </div>
        </div>

    </div>
</template>

<script>
  export default {
    name: "re-radio",
    props: ['quest', 'valueKey','htmlFormat'],
    data(){
      return{
        required:false
      }
    }
  }
</script>

<style lang="scss" scoped>
    .quest__input_container{
        position: relative;
        input{
            position: absolute;
            width: 100%;
            height: 100%;
            opacity: 0;
            &:hover{
                cursor:pointer
            }
        }
    }
    .label{
        display: flex;
        align-items: flex-start;
        &::before{
            display: inline-block;
            opacity: 1;
            width: 15px;
            height: 15px;
            content: '';
            background-color: #fbfbfb;
            border-radius: 50%;
            margin-right: 1rem;
            transition: all 0.3s;
            flex-shrink: 0;
            border: 1px solid lightgrey;
        }
    }
    input:checked+label:before{
        background-color: #5A9DE9;
    }
    input:not(:checked):hover+label:before{
        background-color: lightgray;
    }
</style>