<template>
  <div>
    <div :class="{showTc:isShow}">
      <div class="box">
        <div class="small-box">
          <div class="header overflow-h">
            <div class="header-title">
              师傅弹窗这里我尽力了的
            </div>
            <div class="header-close">
              <button class="closeBtn" @click="hideTC">
                关闭
              </button>
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
        props:['isShow'],
        data() {
            return {
            }
        },
        methods: {
            hideTC() {
                this.$emit('showTC',false)
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

  .showTc {
    display: none;
  }

  .overflow-h {
    overflow: hidden;
  }

  /* Tc */
  .box {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    background: rgba(0, 0, 0, 0.5);
  }

  .small-box {
    border: 2px solid #ccc;
    background: white;
    width: 50vw;
    height: 50vh;
    padding: 1%;
  }

  .closeBtn {
    background: none;
    border: 2px solid #ccc;
    float: right;
    padding: 10px;
    border-radius: 10px;
    color: red;
    font-weight: bold;
  }

  /* End Tc */
</style>
