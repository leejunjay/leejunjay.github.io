<template>
  <div>
    <input type="text" placeholder="请输入需要添加的姓名" v-model="addName"/>
    <button @click="submitData">add</button>
    <div v-for="(p,index) in list" :key="index">
      <input type="text" :disabled='p.disabled' v-model="p.name"/>
      <button @click="deleteName">del</button>
      <button v-if="p.disabled" @click="p.disabled = !p.disabled">更改姓名</button>
      <button v-else @click="updateOk(p)">确认</button>
    </div>
    <br/>
    <br/>
    <div>
      <label>搜索名称：</label><input v-model="searchName" type="text"/>
      <div v-for="(p,index) in searchf" :key="index">
        {{p.name}}
      </div>
      <br/>
      <br/>
      <Tc/>
    </div>
  </div>
</template>

<script>
    import Tc from './tc'
    export default {
        components: {Tc},
        data() {
            return {
                addName: '',
                searchName: '',
                defaultOk: true,
                isOk: false,
                disabled: true,
                isShow: true,
                list: [{name: 'fg', disabled: true}, {name: 'sfx', disabled: true}]
            }
        },
        methods: {
            submitData() {
                const {list, addName} = this
                let chroess = list.find((p) => p.name == addName)
                if (chroess) {
                    alert('不能添加重复值')
                } else {
                    list.push({name: this.addName})
                }
            },
            deleteName($event) {
                this.list.splice($event.index, 1)
            },
            updateOk(p) {
                let chroess = confirm('确认修改为：' + p.name + " 吗？")
                if (chroess == true) {
                    p.disabled = true
                }
            }
        }, computed: {
            searchf() {
                const {list, searchName} = this
                let filterList = list.filter(p => p.name.indexOf(searchName) !== -1)
                return filterList
            }
        }
    }
</script>

<style scoped>
  input:focus,button:focus {
    outline: none;
  }
</style>
