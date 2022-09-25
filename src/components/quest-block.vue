<template>
  <div>
    <h2>{{blockTitle}}</h2>
    <div v-for="quest in partOfQuest" :key="quest.question">
      <component
          :is="`q-${quest.type}`"
          :quest="quest"
          @checkboxHandler="checkboxHandler"
          v-model="quest.currentValue"
          :htmlFormat="quest.htmlFormat"
          :currentQuest="quest.currentQuest"></component>
    </div>
  </div>

</template>

<script>
import QTextInput from "@/components/q-text-input";
import QTableRadio from "@/components/q-table-radio";
import QCheckbox from "@/components/q-checkbox";
import QRadio from "@/components/q-radio";
import QSelect from "@/components/q-select";

export default {
  name: "quest-block",
  components: {
    QTextInput,
    QTableRadio,
    QCheckbox,
    QRadio,
    QSelect
  },
  props:['partOfQuest', 'blockTitle'],
  methods:{
    checkboxHandler(options, currentQuest){
      this.$emit('checkboxHandler', options, currentQuest)
    }
  },
  computed:{
    getTypeofQuestComponent(){
      return () =>{

      }
    }
  },
}
</script>

<style scoped>

</style>