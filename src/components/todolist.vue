<template>
  <div>
    <input type="text" placeholder="请输入需要添加的姓名" v-model="addName"/>
    <button @click="submitData">add</button>
    <div v-for="(p,index) in list" :key="index">
      <input type="text" :disabled='p.disabled' v-model="p.name"/>
      <button @click="deleteName">del</button>
      <button v-if="p.defaultOk" @click="updatef(p)">更改姓名</button>
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
      <div>
        <button @click="showTC">弹窗</button>
        <div :class="{show:isShow}">
          <div
            style="display: flex;justify-content: center;align-items: center;width: 100%;height: 100%;position: fixed;top:0;background: rgba(0,0,0,0.5);">
            <div style="border: 2px solid #ccc;background: white;width: 50vw;height: 50vh;padding: 1%;">
              <div class="header" style="overflow:hidden;">
                <div class="header-title">
                </div>
                <div class="header-close">
                  <button @click="hideTc" style="background: none;border: 2px solid #ccc;float: right;padding: 10px;border-radius: 10px;color: red;font-weight: bold;">
                    关闭
                  </button>
                </div>
              </div>
              <div style="height: 50px;margin-top:15px;">
                <div style="width: 10%;float: left;height: 100%;display: flex;align-items: center;">
                  <label>姓名：</label>
                </div>
                <div style="width: 90%;float: left;height: 100%">
                  <input style="width: 100%;height:100%;border-radius: 10px;text-indent: 1em;"/>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
    export default {
        data() {
            return {
                addName: '',
                searchName: '',
                defaultOk: true,
                isOk: false,
                disabled: true,
                isShow: true,
                list: [{name: 'fg', disabled: true, defaultOk: true}, {name: 'sfx', disabled: true, defaultOk: true}]
            }
        }, methods: {
            submitData() {
                const {list, addName} = this
                let chroess = list.find((p) => p.name.trim() == addName.trim())
                if (chroess) {
                    alert('不能添加重复值')
                } else {
                    list.push({name: this.addName})
                }
            },
            deleteName($event) {
                this.list.splice($event.index, 1)
            },
            updatef(p) {
                p.disabled = false
                p.defaultOk = false
            },
            updateOk(p) {
                let chroess = confirm('确认修改为：' + p.name + " 吗？")
                if (chroess == true) {
                    p.defaultOk = true
                    p.disabled = true
                }
            },
            showTC() {
                this.isShow = false
            },
            hideTc() {
                this.isShow = true
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

  button {
    cursor: pointer;
  }

  .show {
    display: none;
  }
</style>
