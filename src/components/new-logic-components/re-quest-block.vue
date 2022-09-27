<template>
    <form @submit.prevent="printAllAnswers">
        <re-select :quest="data[0]" :valueKey="'selectValue'" @dataValueHandler="dataValueHandler"/>
        <div v-for="quest in data.slice(1,4)" :key="quest.title">
            <component :is="getTypeOfInput(quest)"
                       :quest="quest"
                       :valueKey="getValueKey(quest)"
                       @dataValueHandler="dataValueHandler">
            </component>
        </div>
        <re-table-radio :quest="children[0]" @dataValueHandler="dataValueHandler" :valueKey="'radioTableValue'"/>
        <input type="submit" value="Отправить" class="paginateButton"/>
    </form>
</template>

<script>
  import ReCheckbox from "@/components/new-logic-components/re-checkbox";
  import ReSelect from "@/components/new-logic-components/re-select";
  import ReRadio from "@/components/new-logic-components/re-radio";
  import ReTableRadio from "@/components/new-logic-components/re-table-radio";
  import ReTextInput from "@/components/new-logic-components/re-text-input";

  export default {
    name: "re-quest-block",
    components: {ReTextInput, ReTableRadio, ReRadio, ReCheckbox, ReSelect},
    props: ['blockTitle', 'data', 'children',],
    data() {
      return {
        values: {
          checkboxValue: [],
          selectValue: "",
          radioValue: "",
          radioTableValue: {},
          inputTextValue: "",
        },
      }
    },
    methods: {
      dataValueHandler(valueKey, dataValue) {
        this.values[valueKey] = dataValue;
      },
      printAllAnswers() {
        console.log(this.values)
      }
    },
    computed:{
      getTypeOfInput(){
        return (quest)=>{
          if (quest.allow_any){
            return 're-text-input'
          }
          else if(quest.max_check>1){
            return 're-checkbox'
          }
          else if(quest.max_check===1){
            return 're-radio'
          }
        }
      },
      getValueKey(){
        return (quest)=>{
          if (quest.allow_any){
            return 'inputTextValue'
          }
          else if(quest.max_check>1){
            return 'checkboxValue'
          }
          else if(quest.max_check===1){
            return 'radioValue'
          }
        }
      }
    }
  }
</script>

<style scoped>

</style>