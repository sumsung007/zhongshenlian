<template>
  <div class="customer-info-add">
    <!-- <crumbs :paths="paths"></crumbs> -->
    <customer-info-edit :iniNewCustomerInfo="customerInfo" :iniIsEdit="isEdit"></customer-info-edit>
  </div>
</template>

<script>
import axios from 'axios';
import card from '@/main/component/card.vue';
import crumbs from '@/main/component/crumbs.vue';
import modal from '@/main/component/modal.vue';
import customerInfoEdit from './customerInfoEdit.vue';

export default {
  name: 'customerInfoDetail',
  data() {
    return {
      paths: [
        { name: '客户信息', url: '/customer-infor-list', present: false },
        { name: '客户信息详情', url: '/customer-infor-list/add', present: true }
      ],
      customerInfo: {
        id: '',
        customerName: '',
        name: '',
        telephone: '',
        duty: '',
        department: '',
        registeredAddress: '',
        mailingAddress: '',
        businessLicenseNumber: '',
        registeredCapital: '',
        customerNature: '',
        assetSize: '',
        setUpTime: '',
        industry: '',
        companyFounder: '',
        founderId: '',
        founderName: '',
        founderDepartment: '',
        code: '',
        legalPersonTelephone: '',
        mainWork: '',
        customerIndustryId: '',
        customerNatureId: '',
        removedStatus: '',
        createAt: '',
        updateAt: ''
      },
      isEdit: true,
      customerInfoId: ''
    }
  },
  methods: {
    getCustomerInfo () {
      return new Promise((resolve, reject) => {
        axios({
          headers: { 'Content-Type': 'application/x-www-form-urlencoded;charset=utf-8' },
          method: 'get',
          url: '/service',
          params: {
            data: (() => {
              let obj = {
                command: 'getCustomerInfo',
                platform: 'web',
                id: this.customerInfoId
              }
              return JSON.stringify(obj);
            })()
          }
        }).then((rep) => {
          if (rep.data.statusCode === '10001') {
            resolve(rep.data.data);
          }
        }, (rep) => { });
      })
    }
  },
  created() {
    this.customerInfoId = this.$route.params.id
    this.getCustomerInfo().then((data) => {
      this.customerInfo = data
    })
  },
  components: {
    card,
    crumbs,
    modal,
    customerInfoEdit
  }
};
</script>

<style lang="sass" scoped>
  .customer-info-add {
    .title {
      font-size: 18px;
      text-align: center;
      + p {
        font-size: 13px;
        text-align: center;
      }
    }
    .message-box {
      background-color: #f9fbfe;
      padding: 20px 50px;
      p {
        display: flex;
        line-height: 34px;
        padding: 0 20px;
        span {
          width: 88px;
        }
      }
      + p {
        margin-top: 20px;
        text-align: center;
      }
    }
    .load-modal {
      .loading {
        text-align: center;
        font-size: 15px;
      }
    }
  }
</style>