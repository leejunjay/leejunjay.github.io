<template>
  <div>
    <input type="text" placeholder="请输入需要添加的姓名" v-model="addName" />
    <button @click="submitData">add</button>
    <div v-for="(p,index) in list" :key="index">
      {{index}} -- {{p.name}} <button @click="deleteName">del</button>
    </div>
    <br/>
    <div>
      搜索名称：<input v-model="searchName" type="text" />
      <div v-for="(p,index) in searchf" :key="iii">
        {{p.name}}
      </div>
    </div>
  </div>
</template>

<script>
    export default {
        name: "todolist",
        data() {
            return {
                addName:'',
                searchName:'',
                list:[{name: 'fg'},{name:'sfx'}]
            }
        },methods: {
            submitData() {
                this.list.push({name:this.addName})
            },
            deleteName($event) {
                this.list.splice($event.index,1)
            }
        },computed: {
            searchf() {
                const {list,searchName} = this
                let filterList = list.filter(p=> p.name.indexOf(searchName) !== -1)
                return filterList
            }
        }
    }
</script>

<style scoped>

</style>
