<template>
  <div class="main">
    <!-- <crumbs :paths="paths"></crumbs> -->
    <card class="detail-page">
      <!--查看招投标信息-->
      <bid-info-check
        :iniProject="project"
        inputType="编辑"
        @submit="submit"
        @saveDraft="saveDraft"
        @delBasicFee="delBasicFee"
        @addBasicFee="addBasicFee"
        @delEfficiencyFee="delEfficiencyFee"
        @addEfficiencyFee="addEfficiencyFee"
        @quedingDelete="quedingDelete"></bid-info-check>
      <!--编辑招投标信息-->
      <!-- <bid-info-edit :iniProject="project"
                     inputType="编辑"
                     @submit="submit"
                     @saveDraft="saveDraft"
                     @delBasicFee="delBasicFee"
                     @addBasicFee="addBasicFee"
                     @delEfficiencyFee="delEfficiencyFee"
                     @addEfficiencyFee="addEfficiencyFee"
                     @quedingDelete="quedingDelete"
                     v-if="editShow"></bid-info-edit> -->
    </card>
  </div>
</template>

<script>
import Vue from 'vue';
import axios from 'axios';
import qs from 'qs';
import { Message } from 'element-ui';

import crumbs from '../../component/crumbs.vue';
import card from '../../component/card.vue';
import bidInfoCheck from './component/bidInfoCheck.vue';
import bidInfoEdit from './component/bidInfoEdit.vue';
import modal from '../../component/modal.vue';

Vue.prototype.$message = Message;

export default {
  name: 'bidInfoDetail',
  data() {
    return {
      paths: [],
      project: {},
      iniProject: {},
      editShow: false, //招投标信息编辑页面显示
      checkShow: true, //招投标信息查看页面显示
      id: '',          //获取地址栏id参数
      isDraft: '' ,     //获取地址栏判断草稿还是详情参数
      inputType: '',
      editable: ''
    }
  },
  methods: {
    //获取一条招投标信息
  	getInfo() {
  		axios({
  		  headers: { 'Content-Type': 'application/x-www-form-urlencoded;charset=utf-8' },
  		  method: 'get',
  		  url: '/service',
  		  params: {
  		    data: (() => {
  		      let obj = {
  		        command: 'getBiddingInfo',
  		        platform: 'web',
  		        id: this.$route.params.id
  		      }
  		      return JSON.stringify(obj);
  		    })()
  		  }
  		}).then((rep) => {
      		if (rep.data.statusCode === '10001') {
    				this.project = rep.data.data;
    				this.iniProject = this.project;
      		}
    		}, (rep) => {});
  	},
    //判断是查看还是编辑页面
  	// isEdit() {
  	// 	this.editShow = true;
  	// 	this.checkShow = false;
  	// },
    //编辑页面提交
    submit(project) {
      // project.departmentType = this.departmentType;
      axios({
        headers: {'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8'},
        method: 'post',
        url: '/service',
        data: qs.stringify({
          data: (() => {
            var obj = {
              command: 'addOrEditBiddingInfo',
              platform: 'web',
              type: 'add',
              data: project
            };
            return JSON.stringify(obj);
          })()
        })
      }).then((rep)=>{
        if (rep.data.statusCode === '10001') {
          this.$message.success('保存信息成功');
          this.$router.push('/bid-info-list');
        }
      }, (rep)=>{});
    },
    //编辑页面存草稿
    saveDraft(project) {
      // project.departmentType = this.departmentType;
      axios({
          headers: {'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8'},
          method: 'post',
          url: '/service',
          data: qs.stringify({
            data: (() => {
              var obj = {
                command: 'addOrEditBiddingInfo',
                platform: 'web',
                type: 'temp',
                data: project
              };
              return JSON.stringify(obj);
            })()
          })
      }).then((rep)=>{
        if (rep.data.statusCode === '10001') {
          this.$message.success('保存草稿成功');
          this.$router.push('/bid-info-draft');
        }
      }, (rep)=>{});
    },
    delBasicFee(index) {
      this.project.contractType.subBasicArray.splice(index,1);
    },
    addBasicFee() {
      console.log(123);
      this.project.contractType.subBasicArray.push({"name":'',"rate": 0});
    },
    delEfficiencyFee(index) {
      this.project.contractType.subEfficiencyArray.splice(index,1);
    },
    addEfficiencyFee() {
      this.project.contractType.subEfficiencyArray.push({"name":'',"rate": 0});
    },
    //编辑页面删除
    quedingDelete(id) {
      let arr = []
      let obj = {}
      obj.name = this.id
      arr.push(obj)
      axios({
          headers: {'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8'},
          method: 'post',
          url: '/service',
          data: qs.stringify({
            data: (() => {
              var obj = {
                command: 'delBiddingInfo',
                platform: 'web',
                id: arr
              };
              return JSON.stringify(obj);
            })()
          })
      }).then((rep)=>{
        if (rep.data.statusCode === '10001') {
          this.$message.success('撤销成功，已删除项目');
          this.$router.push('/bid-info-list');
        }
      }, (rep)=>{});
    },
    //根据地址栏里的参数信息判断是列表还是草稿箱的面包屑信息
    definePath() {
      if (this.isDraft === "isDraft") {
        this.paths = [
          {name: '草稿箱', url: '/bid-info-draft', present: false},
          {name: '招投标详情', url: '/bid-info-detail', present: true}
        ]
      }
      if (this.isDraft === "notDraft") {
        this.paths = [
          {name: '招投标信息', url: '/bid-info-list', present: false},
          {name: '招投标详情', url: '/bid-info-detail', present: true}
        ]
      }
    }
  },
  created() {
    this.id = this.$route.params.id;  //获取地址栏id参数
    this.isDraft = this.$route.params.isDraft;  //获取地址栏标志位参数
    this.getInfo();
    this.editShow = false;
    this.checkShow = true;
    this.definePath();
  },
  components: {
    crumbs,
    card,
    bidInfoCheck,
    bidInfoEdit,
    modal
  }
}
</script>

<style lang="sass" scoped>
  .icon {
      vertical-align: middle;
      color: #efa844;
  }
  .ta-c {
      text-align: center;
  }
  .cancel-word {
      margin: 0;
  }
  .text-danger {
      text-decoration: none;
      cursor: pointer;
  }
</style>
