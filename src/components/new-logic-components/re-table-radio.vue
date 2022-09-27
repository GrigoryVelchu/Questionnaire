<template>
    <div class="quest">
        <p class="quest__question">{{quest.title}}</p>
        <p class="quest__clarification">(пожалуйста, выберите один вариант ответа в соответствующей ячейке</p>
        <div class="values_header">
            <div v-for="option in quest.polls[0].options" :key="option.name">{{option.name}}</div>
        </div>
        <div class="quest__input_container" v-for="poll in quest.polls" :key="poll.title">
            <label class="label" :for="poll.title">{{poll.title}}</label>
            <div class = 'inputs-arrow'>
                <input type="radio"
                       :required="required"
                       v-for="option in poll.options"
                       :key="option"
                       :id="poll.title"
                       :data-name = "option.name"
                       :name="poll.title"
                       @click="dataHandler($event, poll.title, option.name)">
            </div>

        </div>
    </div>
</template>

<script>
  export default {
    props:['quest','currentQuest','valueKey'],
    name: "re-table-radio",
    data(){
      return{
        answers: {},
        required:false
      }
    },
    methods:{
      dataHandler(e, type, value){
        this.answers.forEach(elem=>{
          if(elem.type === type){
            elem.value=value
          }
        })
        this.$emit('dataValueHandler', this.valueKey, this.answers)
      }
    },
    mounted() {
      this.answers = this.quest.polls.map(el=>{
        return {type:el.title,value:''}
      })
    }
  }
</script>

<style lang="scss" scoped>
    .quest__input_container{
        margin-bottom: 0!important;
        padding: 10px 20px!important;
        align-items: center!important;
        &:nth-child(even){
            background-color: lightgrey;
        }
    }
    label{
        width: 30%;
        padding-right:2rem;
        line-height: 1rem;
    }
    .inputs-arrow{
        width: 70%;
        display: flex;
        justify-content: space-between;
        padding: 0 3%;
    }
    .values_header{
        padding-left: 30%;
        display: flex;
        justify-content: space-between;
        div{
            text-align: center;
            width: 14%;
            font-size:0.8rem
        }
    }
    input[type=radio]{
        position: relative;
        &::before{
            position: absolute;
            top:-1px;
            left:-1px;
            opacity: 1;
            content:'';
            display: inline-block;
            width: 15px;
            height: 15px;
            background-color: #fbfbfb;
            border-radius: 50%;
            margin-right: 1rem;
            transition: all 0.3s;
            flex-shrink: 0;
            border: 1px solid gray;
            &:hover{
                cursor:pointer;
            }
        }
    }
    input:checked:before{
        background-color: #5A9DE9;
    }
    input:not(:checked):hover:before{
        background-color: lightgray;
        cursor: pointer;
    }
    input:not(:checked):hover:before{
        background-color: lightgray;
    }
    .quest__input_container{
        &:nth-child(even){
            input:not(:checked):hover:before{
                background-color: gray;
            }
        }
    }
    input:hover:after {
        content: attr(data-name);
        position: absolute;
        bottom: 1rem;
        right: -2.4rem;
        color: white;
        text-align: center;
        font-size: 0.7rem;
        padding: 5px;
        background-color: grey;
        opacity: 1;
    }
</style>