<!-- <template> -->
  <!-- <modal class="add-width" alignSelf="flex-start" modalWidth="800px">
    <form class="form-horizontal clearfix"
          slot="body"
          @submit.prevent
          @keyup.enter.prevent>
      <div class="row">
        <div class="form-group col-md-6"
             :class="{'has-error': !customer.customerName.ver}">
          <label class="control-label">客户名称</label>
          <div>
            <input type="text"
                   class="form-control"
                   placeholder="请输入客户名称"
                   v-model="customer.customerName.val">
          </div>
        </div>
        <div class="col-md-1"></div>
        <div class="form-group col-md-6"
             :class="{'has-error': !customer.name.ver}">
          <label class="control-label">客户联系人</label>
          <div>
            <input type="text"
                   class="form-control"
                   placeholder="请输入客户联系人"
                   v-model="customer.name.val">
          </div>
        </div>
      </div>
      <div class="row">
        <div class="form-group col-md-6"
             :class="{'has-error': !customer.duty.ver}">
          <label class="control-label">联系人职位</label>
          <div>
            <input type="text"
                   class="form-control"
                   placeholder="请输入联系人职位"
                   v-model="customer.duty.val">
          </div>
        </div>
        <div class="col-md-1"></div>
        <div class="form-group col-md-6"
             :class="{'has-error': !customer.telephone.ver}">
          <label class="control-label">联系人电话</label>
          <div>
            <input type="tel"
                   class="form-control"
                   placeholder="请输入联系人电话"
                   v-model="customer.telephone.val">
          </div>
        </div>
      </div>
      <div class="row">
        <div class="form-group col-md-6"
             :class="{'has-error': !customer.department.ver}">
          <label class="control-label">联系人部门</label>
          <div>
            <input type="text"
                   class="form-control"
                   placeholder="请输入联系人部门"
                   v-model="customer.department.val">
          </div>
        </div>
        <div class="col-md-1"></div>
        <div class="form-group col-md-6"
             :class="{'has-error': !customer.businessLicenseNumber.ver}">
          <label class="control-label">营业执照号码</label>
          <div>
            <input type="text"
                   class="form-control"
                   placeholder="请输入营业执照号码"
                   v-model="customer.businessLicenseNumber.val">
          </div>
        </div>
      </div>
      <div class="form-group row"
           :class="{'has-error': !customer.registeredAddress.ver}">
        <label class="control-label">注册地址</label>
        <div>
          <input type="text"
                 class="form-control"
                 placeholder="请输入注册地址"
                 v-model="customer.registeredAddress.val">
        </div>
      </div>
      <div class="row">
        <div class="form-group col-md-6"
             :class="{'has-error': !customer.assetSize.ver}">
          <label class="control-label">资产规模</label>
          <div>
            <div class="input-group">
              <masked-input type="text"
                            class="form-control"
                            placeholder="请输入资产规模"
                            v-model="customer.assetSize.val"
                            :mask="currencyMask"
                            :guide="false"
                            placeholderChar="#">
              </masked-input>
              <div class="input-group-addon">万元</div>
            </div>
          </div>
        </div>
        <div class="col-md-1"></div>
        <div class="form-group col-md-6"
             :class="{'has-error': !customer.registeredCapital.ver}">
          <label class="control-label">注册资本</label>
          <div>
            <div class="input-group">
              <masked-input type="text"
                            class="form-control"
                            placeholder="请输入注册资本"
                            v-model="customer.registeredCapital.val"
                            :mask="currencyMask"
                            :guide="false"
                            placeholderChar="#">
              </masked-input>
              <div class="input-group-addon">万元</div>
            </div>
          </div>
        </div>
      </div>
      <div class="form-group">
        <label class="control-label">客户性质</label>
        <div class="check-wrap" v-for="(NAT, index) in customer.customerNature" :key="index">
          <input class="magic-checkbox"
                 type="checkbox"
                 v-model="NAT.state"
                 :id="index">
          <label class="checkbox-inline"
                 :key="index"
                 :for="index">
                 {{NAT.val}}
          </label>
        </div>
      </div>
      <div class="row">
        <div class="form-group col-md-6"
             :class="{'has-error': !customer.setUpTime.ver}">
          <label class="control-label">成立日期</label>
          <div>
            <input type="date"
                   class="form-control"
                   placeholder="请输入成立日期"
                   v-model="customer.setUpTime.val">
          </div>
        </div>
        <div class="col-md-1"></div>
        <div class="form-group col-md-6"
             :class="{'has-error': !customer.industry.ver}">
          <label class="control-label">所属行业</label>
          <div>
            <input type="text"
                   class="form-control"
                   placeholder="请输入所属行业"
                   v-model="customer.industry.val">
          </div>
        </div>
      </div>
      <div class="form-group row"
           :class="{'has-error': !customer.mailingAddress.ver}">
        <label class="control-label">邮寄地址</label>
        <div>
          <input type="text"
                 class="form-control"
                 placeholder="请输入邮寄地址"
                 v-model="customer.mailingAddress.val">
        </div>
      </div>
      <div class="row">
        <div class="form-group col-md-6">
          <label class="control-label">
            创建部门&nbsp;
            <span>
              {{customer.founderDepartment.val}}
            </span>
          </label>
        </div>
        <div class="form-group col-md-6">
          <label class="control-label">
            创建人&nbsp;
            <span>
              {{customer.founderName.val}}
            </span>
          </label>
        </div>
      </div>
      <div class="alert alert-danger well-sm"
           v-show="alert.show">
        {{alert.cont}}
      </div>
    </form>
    <div class="ta-c" slot="footer">
      <button class="btn my-btn submit-btn"
              @click="save()"
              :disabled="subBtn.dis">
        {{subBtn.cont}}
      </button>
      <button class="btn my-btn draft-btn"
              @click="cancel()">
        取消
      </button>
    </div>
  </modal> -->
  <!-- <modal class="add-width" modalWidth="800px">
    
  </modal>
</template> -->

// <script>
// import axios from 'axios';
// import qs from 'qs';
// import maskedInput from 'vue-text-mask';

// import modal from '@/main/component/modal.vue';
// import currencyMask from '../../../../currencyMask.js';

// export default {
//   name: 'customerModModal',
//   data() {
//     return {
//       customer: (() => {
//         return {
//           id: {
//             val: ''
//           },
//           customerName: {
//             val: '',
//             ver: true
//           },
//           name: {
//             val: '',
//             ver: true
//           },
//           telephone: {
//             val: '',
//             ver: true
//           },
//           duty: {
//             val: '',
//             ver: true
//           },
//           department: {
//             val: '',
//             ver: true
//           },
//           registeredAddress: {
//             val: '',
//             ver: true
//           },
//           mailingAddress: {
//             val: '',
//             ver: true
//           },
//           businessLicenseNumber: {
//             val: '',
//             ver: true
//           },
//           registeredCapital: {
//             val: '',
//             ver: true
//           },
//           customerNature: [
//             { val: '央企', state: false },
//             { val: '国企', state: false },
//             { val: '私企', state: false },
//             { val: '行政事业单位', state: false },
//             { val: '内资', state: false },
//             { val: '外资', state: false },
//             { val: '金融机构', state: false },
//             { val: '其他', state: false }
//           ],
//           assetSize: {
//             val: '',
//             ver: true
//           },
//           industry: {
//             val: '',
//             ver: true
//           },
//           setUpTime: {
//             val: (() => {
//               let t = new Date();
//               let Y = t.getFullYear();
//               let M = (t.getMonth() + 1 < 10) ? `0${t.getMonth() + 1}` : `${t.getMonth() + 1}`;
//               let D = (t.getDate() < 10) ? `0${t.getDate()}` : `${t.getDate()}`;
//               return `${Y}-${M}-${D}`;
//             })(),
//             ver: true
//           },
//           founderId: {
//             val: this.user.id
//           },
//           founderName: {
//             val: this.user.name
//           },
//           founderDepartment: {
//             val: this.user.department
//           }
//         }
//       })(),
//       alert: {
//         show: false,
//         cont: ''
//       },
//       subBtn: {
//         dis: false,
//         cont: '保存'
//       }
//     };
//   },
//   props: ['user'],
//   methods: {
//     currencyMask,
//     save() {
//       let reg = /^(1+\d{10})$/;
//       this.alert.show = false;
//       this.alert.cont = '';
//       if (this.customer.customerName.val === '') {
//         this.customer.customerName.ver = false;
//       } else {
//         this.customer.customerName.ver = true;
//       }
//       if (this.customer.name.val === '') {
//         this.customer.name.ver = false;
//       } else {
//         this.customer.name.ver = true;
//       }
//       if (this.customer.telephone.val === '') {
//         this.customer.telephone.ver = false;
//       } else if (!reg.test(this.customer.telephone.val)) {
//         this.customer.telephone.ver = false;
//       } else {
//         this.customer.telephone.ver = true;
//       }
//       if (this.customer.duty.val === '') {
//         this.customer.duty.ver = false;
//       } else {
//         this.customer.duty.ver = true;
//       }
//       if (this.customer.department.val === '') {
//         this.customer.department.ver = false;
//       } else {
//         this.customer.department.ver = true;
//       }
//       if (this.customer.registeredAddress.val === '') {
//         this.customer.registeredAddress.ver = false;
//       } else {
//         this.customer.registeredAddress.ver = true;
//       }
//       if (this.customer.mailingAddress.val === '') {
//         this.customer.mailingAddress.ver = false;
//       } else {
//         this.customer.mailingAddress.ver = true;
//       }
//       if (this.customer.businessLicenseNumber.val === '') {
//         this.customer.businessLicenseNumber.ver = false;
//       } else {
//         this.customer.businessLicenseNumber.ver = true;
//       }
//       if (this.customer.registeredCapital.val === '') {
//         this.customer.registeredCapital.ver = false;
//       } else {
//         this.customer.registeredCapital.ver = true;
//       }
//       if (this.customer.assetSize.val === '') {
//         this.customer.assetSize.ver = false;
//       } else {
//         this.customer.assetSize.ver = true;
//       }
//       if (this.customer.setUpTime.val === '') {
//         this.customer.setUpTime.ver = false;
//       } else {
//         this.customer.setUpTime.ver = true;
//       }
//       if (this.customer.industry.val === '') {
//         this.customer.industry.ver = false;
//       } else {
//         this.customer.industry.ver = true;
//       }
//       if (!(this.customer.customerName.ver && this.customer.name.ver && this.customer.telephone.ver && this.customer.duty.ver && this.customer.department.ver && this.customer.registeredAddress.ver && this.customer.mailingAddress.ver && this.customer.registeredCapital.ver && this.customer.assetSize.ver && this.customer.setUpTime.ver && this.customer.industry.ver)) {
//         this.alert.show = true;
//         this.alert.cont = '您有信息尚未输入或信息格式有误，请检查';
//       } else {
//         this.subBtn.dis = true;
//         this.subBtn.cont = '保存中...';
//         axios({
//           headers: { 'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8' },
//           method: 'post',
//           url: '/service',
//           data: qs.stringify({
//             data: (() => {
//               var obj = {
//                 command: 'addCustomerInfo',
//                 platform: 'web',
//                 data: {
//                   customerName: this.customer.customerName.val,
//                   name: this.customer.name.val,
//                   telephone: this.customer.telephone.val,
//                   duty: this.customer.duty.val,
//                   department: this.customer.department.val,
//                   registeredAddress: this.customer.registeredAddress.val,
//                   mailingAddress: this.customer.mailingAddress.val,
//                   businessLicenseNumber: this.customer.businessLicenseNumber.val,
//                   registeredCapital: this.customer.registeredCapital.val,
//                   customerNature: this.customer.customerNature,
//                   assetSize: this.customer.assetSize.val,
//                   industry: this.customer.industry.val,
//                   setUpTime: this.customer.setUpTime.val,
//                   founderId: this.customer.founderId.val,
//                   founderName: this.customer.founderName.val,
//                   founderDepartment: this.customer.founderDepartment.val
//                 }
//               };
//               return JSON.stringify(obj);
//             })()
//           })
//         }).then((rep) => {
//           if (rep.data.statusCode === '10001') {
//             this.customer.id.val = rep.data.data.id;
//             this.subBtn.cont = '已保存';
//             this.$emit('added', this.customer);
//           } else if (rep.data.statusCode === '10013') {
//             this.subBtn.dis = false;
//             this.subBtn.cont = '保存';
//             this.alert.show = true;
//             this.alert.cont = '您输入的客户已存在';
//           } else if (rep.data.statusCode === '10012') {
//             window.location.href = 'signIn.html';
//           }
//         }, (rep) => { });
//       }
//     },
//     cancel() {
//       this.$emit('canceled');
//     }
//   },
//   components: {
//     modal,
//     maskedInput
//   }
// };
// </script>

// <style lang="sass" scoped>
//   .form-horizontal .control-label {
//       text-align: right;
//       margin-bottom: 0;
//       padding-top: 7px;
//       font-weight: normal;
//       text-align: left;
//       width: 100%;
//   }

//   .check-wrap {
//     display: inline-block;
//   }

//   .form-horizontal .radio, .form-horizontal .checkbox, .form-horizontal .radio-inline, .form-horizontal .checkbox-inline {
//       margin-top: 0;
//       margin-bottom: 0;
//       padding-top: 0px;
//   }
// </style>
