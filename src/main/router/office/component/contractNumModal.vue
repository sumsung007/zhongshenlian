<template>
  <modal class="contract-number" modalWidth="800px">
    <form class="form-horizontal clearfix"
          slot="body"
          @submit.prevent
          @keyup.enter.prevent>
      <div class="form-group">
        <label class="col-sm-2">报告类型</label>
        <div class="col-sm-10">
          <template v-for="(TYPE, index) in type">
            <p>{{TYPE.name}}</p>
            <label class="checkbox-inline"
                   v-for="(WORD, index) in TYPE.words"
                   :key="index">
              <input type="checkbox"
                     v-model="WORD.state"
                     @change="reportTypeChan(TYPE, WORD)"
                     :disabled="WORD.dis"> {{WORD.name}}
            </label>
            <hr>
          </template>
        </div>
      </div>
      <div class="form-group">
        <label class="col-sm-2">编号样式</label>
        <div class="col-sm-10">
          <p class="form-control-static">
            {{number}}
          </p>
        </div>
      </div>
    </form>
    <div slot="footer">
      <button class="btn my-btn submit-btn modal-default-button"
              @click="sub()"
              :disabled="subBtn.dis">
        {{subBtn.cont}}
      </button>
      <button class="btn my-btn draft-btn modal-default-button"
              @click="cancel()">
        取消
      </button>
    </div>
  </modal>
</template>

<script>
import axios from 'axios';
import qs from 'qs';

import modal from '../../../component/modal.vue';

export default {
  name: 'contractNumModal',
  data() {
    return {
      type: this.initBusiness.report.type,
      subBtn: {
        dis: false,
        cont: '确定'
      },
      number: ''
    };
  },
  props: ['initBusiness'],
  mounted() {
    this.reportTypeChan();

    for (let i = 0; i < this.type.length; i++) {
      for (let j = 0; j < this.type[i].words.length; j++) {
        this.type[i].words[j].dis = !this.type[i].words[j].state;
      }
    }
  },
  methods: {
    reportTypeChan(TYPE, WORD) {
      let flag = false;
      let type = '';
      let word = '';
      let t = new Date();
      let year = t.getFullYear();
      outermost2:
      for (let i = 0; i < this.type.length; i++) {
        for (let j = 0; j < this.type[i].words.length; j++) {
          if (this.type[i].words[j].state) {
            flag = true;
            type = this.type[i].code;
            word = this.type[i].words[j].code;
            break outermost2;
          }
        }
      }

      this.number = flag ? `${type}-${word}-${year}-XXXX` : '';
    },
    sub() {
      this.subBtn.dis = true;
      this.subBtn.cont = '提交...';
      axios({
        headers: { 'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8' },
        method: 'post',
        url: '/service',
        data: qs.stringify({
          data: (() => {
            var obj = {
              command: 'releaseContactNumber',
              platform: 'web',
              id: this.initBusiness.id,
              reportType: (() => {
                let out = [];
                for (let i = 0; i < this.type.length; i++) {
                  let flag = false;
                  let typeArray = [];
                  for (let j = 0; j < this.type[i].words.length; j++) {
                    if (this.type[i].words[j].state) {
                      flag = true;
                      typeArray.push({
                        name: this.type[i].words[j].name
                      });
                    }
                  }
                  if (flag) {
                    out.push({
                      department: this.type[i].name,
                      typeArray
                    });
                  }
                }
                return out;
              })()
            };
            return JSON.stringify(obj);
          })()
        })
      }).then((rep) => {
        if (rep.data.statusCode === '10001') {
          let contNum = rep.data.data.contractNo;
          this.subBtn.cont = '已提交';
          this.$emit('submited', contNum);
        } else if (rep.data.statusCode === '10012') {
          window.location.href = 'signIn.html';
        }
      }, (rep) => { });
    },
    cancel() {
      this.$emit('canceled');
    }
  },
  components: {
    modal
  }
};
</script>

<style lang="sass" scoped>

</style>
