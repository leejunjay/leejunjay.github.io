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
      <div v-for="(p,index) in searchf" :key="index">
        {{p.name}}
      </div>
      编辑姓名：<input type="text" ref="add" disabled='disabled' v-model="updateName"/>
      <button v-if="defaultOk" @click="updatef">更改姓名</button>
      <button v-if="isOk" @click="updateOk">确认</button>
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
                updateName:'哈哈哈',
                defaultOk:true,
                isOk:false,
                list:[{name: 'fg'},{name:'sfx'}]
            }
        },methods: {
            submitData() {
                const {list,addName} = this
                    let chroess = list.find((p) => p.name.trim() == addName.trim())
                    if(chroess) {
                        alert('不能添加重复值')
                    } else {
                        list.push({name:this.addName})
                    }
            },
            unique(arr) {
                const res = new Map()
                return arr.filter((arr) => !res.has(arr.name))
            },
            deleteName($event) {
                this.list.splice($event.index,1)
            },
            updatef() {
                this.$refs.add.removeAttribute('disabled')
                this.defaultOk = false
                this.isOk = true

            },
            updateOk() {
                let chroess = confirm('确认修改为：'+ this.updateName+" 吗？")
                if(chroess == true) {
                    this.isOk = false
                    this.defaultOk = true
                    this.$refs.add.setAttribute('disabled','disabled')
                } else {

                }
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
