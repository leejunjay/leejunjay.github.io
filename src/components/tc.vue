<template>
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
              <button @click="hideTc"
                      style="background: none;border: 2px solid #ccc;float: right;padding: 10px;border-radius: 10px;color: red;font-weight: bold;">
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
</template>

<script>
    export default {
        name: "tc",
        data() {
            return {
                isShow: true
            }
        },
        methods: {
            showTC() {
                this.isShow = false
            },
            hideTc() {
                this.isShow = true
            }
        }
    }
</script>

<style scoped>
  input:focus, button:focus {
    outline: none;
  }

  button {
    cursor: pointer;
  }

  .show {
    display: none;
  }
</style>
