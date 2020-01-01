<template>
  <div>
    <input type="text" placeholder="请输入需要添加的姓名" v-model="addName"/>
    <button @click="submitData">add</button>
    <div v-for="(p,index) in list" :key="index">
      <input type="text" :disabled='p.disabled' v-model="p.name"/>
      <button @click="deleteName(index)">del</button>
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
      <button @click="showTC()">弹窗</button>
      <Tc :isShow="isShow" @showTC="showTC(isShow)"/>
    </div>
    <div>
      <table>
        <tr v-for="(item,idx) of list" :key="idx">
          <td :class="[{active: isActive===idx},'defaultColor']"
              @click="ColorF(idx)">{{item.name}}
          </td>
        </tr>
      </table>
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
                list: [{name: 'fg', disabled: true}, {name: 'sfx', disabled: true}],
                checkList: [],
                isActive: false,
                commit : -1
            }
        },
        methods: {
            submitData() {
                const {list, addName} = this
                let chroess = list.find((p) => p.name === addName)
                if (chroess) {
                    alert('不能添加重复值')
                } else {
                    list.push({name: this.addName})
                }
            },
            deleteName(index) {
                this.list.splice(index, 1)
            },
            updateOk(p) {
                let chroess = confirm('确认修改为：' + p.name + " 吗？")
                if (chroess === true) {
                    p.disabled = true
                }
            },
            showTC(isShow) {
                if (isShow !== false) {
                    this.isShow = false
                } else {
                    this.isShow = true
                }
            },
            ColorF(idx) {
                    /*if (this.checkList.indexOf(idx) === -1) {
                        this.checkList.push(idx);
                    } else {
                        let spliceIndex = this.checkList.indexOf(idx);
                        this.checkList.splice(spliceIndex, 1);
                    }
                    if(this.checkList.length === 2) {
                        this.checkList.splice(0,1)
                    }*/
                /*1.删除所有样式
                2.添加当前点击的样式*/
                if(this.commit === idx) {
                    this.isActive = false
                } else {
                    this.isActive = idx
                    this.commit = idx
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
  input:focus, button:focus {
    outline: none;
  }

  .defaultColor {
    border: 2px solid #ccc;
  }

  .active {
    border: 2px solid deeppink;
  }
</style>
