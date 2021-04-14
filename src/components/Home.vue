<template>
<v-container>
  <v-layout row wrap>
  <v-flex xs12 text-xs-center>
    <h1>TODO LIST</h1>
    <p>Today: {{todoList.length}} / 
      Complete: {{countDone}} / remain: {{todoList.length-countDone}}</p>
  </v-flex>
    <v-flex xs6 pa-2>
      <List
        :todoList="todoList"
        @statusControl="statusControl"
        @listDelete="listDelete"
      />
    </v-flex>
    <v-flex xs6 pa-2>
      <ListAdd
        @listAdd="listAdd"
        @listEdit="listEdit"
      />
    </v-flex>
  </v-layout>
</v-container>
</template>

<script>
import List from './List'
import ListAdd from './ListAdd'

export default{
  components: {
    List,
    ListAdd
  },
  data(){
    return {
      todoList: []
    }
  },
  computed:{
    countDone(){
      let count = 0
      this.todoList.forEach(list => {
        if (list.status === 'done') count ++
      })
      return count
    }
  },
  methods:{
    listAdd(memo){
      this.todoList.push({memo: memo, status: 'created'})
    },
    statusControl(index, status){
      this.todoList[index].status = status
    },
    listDelete(index){
      this.todoList.splice(index, 1) // index 요소부터 1개 제거
    },
    listEdit(memo, index){
      this.todoList[index].memo = memo
    }
  }
}
</script>