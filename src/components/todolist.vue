<template>
  <div>
    <input type="text" placeholder="请输入需要添加的姓名" v-model="addName" />
    <button @click="submitData">add</button>
    <div v-for="(p,index) in list" :key="index">
      {{index}} -- {{p.name}} <button @click="deleteName">del</button>
    </div>
  </div>
</template>

<script>
    export default {
        name: "todolist",
        data() {
            return {
                addName:'',
                list:[{name: 'fg'},{name:'sfx'}]
            }
        },methods: {
            submitData() {
                this.list.push({name:this.addName})
            },
            deleteName($event) {
                this.list.splice($event.index,1)
            }
        }
    }
</script>

<style scoped>

</style>
