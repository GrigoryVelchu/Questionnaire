<template>
    <div class="quest">
        <p class="quest__question">{{quest.question}}</p>
        <p class="quest__clarification">(пожалуйста, выберите один или несколько вариантов ответа в соответствующей ячейке)</p>
        <div class="quest__input_container" v-for="option in quest.options" :key="option">

            <input type="checkbox"
                   :id="option"
                   :required="required"
                   :name="currentQuest"
                   @input="checkboxHandler($event,currentQuest)">
            <label class="label" :for="currentQuest">{{option}}</label>

        </div>
    </div>
</template>

<script>
  export default {
    name: "q-checkbox",
    props: ['quest', 'currentQuest'],
    data(){
      return{
        selectedOptions:[],
        required:true
      }
    },
    methods:{
      checkboxHandler(e){
        if(e.target.checked && !this.selectedOptions.includes(e.target.id)){
          this.selectedOptions.push(e.target.id)
        }
        else if(this.selectedOptions.includes(e.target.id)){
          this.selectedOptions = this.selectedOptions.filter((option)=>option!==e.target.id)
        }
        this.required = !this.selectedOptions.length;
        this.$emit('checkboxHandler',this.selectedOptions, this.currentQuest)
      }
    },
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
            border-radius: 25%;
            margin-right: 1rem;
            transition: all 0.3s;
            flex-shrink: 0;
            border: 1px solid gray;
        }
    }
    input:checked+label:before{
        background-color: #5A9DE9;
    }
    input:not(:checked):hover+label:before{
        background-color: lightgray;
    }
</style>