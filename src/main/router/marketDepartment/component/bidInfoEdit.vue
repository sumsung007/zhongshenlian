<template>
	<div>
		<div class="page-header">
			<h4 class="main-title">
				招投标信息{{ inputType }}
        <button type="button" class="btn f-r my-btn cancel-btn btn-mb" @click="cancel()">撤销</button>
        <button type="button" class="btn f-r my-btn draft-btn btn-mr btn-mb" @click="saveDraft(project)">存为草稿</button>
        <button type="button" class="btn f-r my-btn submit-btn btn-mr btn-mb" @click="submit(project)">提交</button>
			</h4>
		</div>
		<form class="form-horizontal" @submit.prevent @keyup.enter.prevent>
			<div class="form-group">
			  <label for="projectName" class="col-sm-2 control-label">项目名称：</label>
			  <div class="col-sm-10">
			    <input type="text" class="form-control half-width" id="projectName" v-model="project.projectName" name="projectName" placeholder="请输入项目名称">
			  </div>
			</div>
			<div class="form-group">
				<label for="tenderPerson" class="col-sm-2 control-label">招标人：</label>
				<div class="col-sm-10">
				  <input type="text" class="form-control half-width" id="tenderPerson" v-model="project.tenderPerson" name="tenderPerson" placeholder="请输入招标人">
				</div>
			</div>
			<div class="form-group">
				<label for="agency" class="col-sm-2 control-label">招标代理机构：</label>
				<div class="col-sm-10">
				  <input type="text" class="form-control half-width" id="agency" v-model="project.agency" name="agency" placeholder="请输入招标代理机构">
				</div>
			</div>
			<div class="form-group">
				<label class="col-sm-2 control-label">项目类型：</label>
				<div class="col-sm-10 check-wrap">
          <input class="magic-checkbox" type="checkbox" value="kjs" v-model="project.departmentType" id="5">
          <label for="5">
            会计所
          </label>
          <input class="magic-checkbox" type="checkbox" value="pgs" v-model="project.departmentType" id="6">
          <label for="6">
            评估所
          </label>
          <input class="magic-checkbox" type="checkbox" value="sws" v-model="project.departmentType" id="7">
          <label for="7">
            税务所
          </label>
          <input class="magic-checkbox" type="checkbox" value="zjs" v-model="project.departmentType" id="8">
          <label for="8">
            造价所
          </label>
				</div>
			</div>
			<hr>
			<!--会计所单独内容-->
			<div v-if="kjsContentShow">
				<div class="form-group">
					<label class="col-sm-2 control-label">会计所：</label>
				</div>
				<div class="form-group">
					<label class="col-sm-2 control-label">招标内容：</label>
					<div class="col-sm-10 check-wrap">
            <input class="magic-checkbox" type="checkbox" value="年审" v-model="project.kjsBiddingContent" id="年审">
            <label for="年审">
              年审
            </label>
            <input class="magic-checkbox" type="checkbox" value="专项" v-model="project.kjsBiddingContent" id="专项">
            <label for="专项">
              专项
            </label>
            <input class="magic-checkbox" type="checkbox" value="咨询" v-model="project.kjsBiddingContent" id="咨询">
            <label for="咨询">
              咨询
            </label>
            <input class="magic-checkbox" type="checkbox" value="决算" v-model="project.kjsBiddingContent" id="决算">
            <label for="决算">
              决算
            </label>
            <input class="magic-checkbox" type="checkbox" value="外汇年检" v-model="project.kjsBiddingContent" id="外汇年检">
            <label for="外汇年检">
              外汇年检
            </label>
					  <input class="magic-checkbox" type="checkbox" value="验资" v-model="project.kjsBiddingContent" id="验资">
            <label for="验资">
              验资
            </label>
            <input class="magic-checkbox" type="checkbox" value="外资审计" v-model="project.kjsBiddingContent" id="外资审计">
            <label for="外资审计">
              外资审计
            </label>
					</div>
				</div>
				<div class="form-group">
					<label for="ownershipStructure" class="col-sm-2 control-label">股权结构：</label>
					<div class="col-sm-10 check-wrap">
            <input class="magic-radio" type="radio" name="kjsOwnerStructure" v-model="project.kjsOwnershipStructure" value="国有" id="kjs国有">
						<label for="kjs国有">
							 国有
						</label>
            <input class="magic-radio" type="radio" name="kjsOwnerStructure" v-model="project.kjsOwnershipStructure" value="民营" id="kjs民营">
            <label for="kjs民营">
               民营
            </label>
            <input class="magic-radio" type="radio" name="kjsOwnerStructure" v-model="project.kjsOwnershipStructure" value="外资" id="kjs外资">
            <label for="kjs外资">
               外资
            </label>
            <input class="magic-radio" type="radio" name="kjsOwnerStructure" v-model="project.kjsOwnershipStructure" value="混合" id="kjs混合">
            <label for="kjs混合">
               混合
            </label>
					</div>
				</div>
				<div class="form-group">
					<label class="col-sm-2 control-label">资产总额：</label>
					<div class="col-sm-10">
						<div class="input-group half-width">
              <masked-input type="text" class="form-control" placeholder="请输入资产总额" v-model="project.totalAssets" :mask="currencyMask" :guide="false" placeholderChar="#">
              </masked-input>
							<div class="input-group-addon">元</div>
						</div>
					</div>
				</div>
				<div class="form-group">
					<label for="location" class="col-sm-2 control-label">坐落地点：</label>
					<div class="col-sm-10">
					  <input type="text" class="form-control half-width" id="location" v-model="project.location" name="location" placeholder="请输入坐落地点">
					</div>
				</div>
				<hr>
			</div>
			<!--评估所单独内容-->
			<div v-if="pgsContentShow">
				<div class="form-group">
					<label class="col-sm-2 control-label">评估所：</label>
				</div>
				<div class="form-group">
					<label class="col-sm-2 control-label">招标内容：</label>
					<div class="col-sm-10 check-wrap">
            <input class="magic-checkbox" type="checkbox" value="股改" v-model="project.pgsBiddingContent" id="股改">
            <label for="股改">
              股改
            </label>
            <input class="magic-checkbox" type="checkbox" value="专项" v-model="project.pgsBiddingContent" id="专项2">
            <label for="专项2">
              专项
            </label>
            <input class="magic-checkbox" type="checkbox" value="咨询" v-model="project.pgsBiddingContent" id="咨询2">
            <label for="咨询2">
              咨询
            </label>
            <input class="magic-checkbox" type="checkbox" value="清产核资" v-model="project.pgsBiddingContent" id="清产核资">
            <label for="清产核资">
              清产核资
            </label>
					</div>
				</div>
				<div class="form-group">
					<label for="ownershipStructure" class="col-sm-2 control-label">股权结构：</label>
					<div class="col-sm-10 check-wrap">
            <input class="magic-radio" type="radio" name="pgsOwnerStructure" v-model="project.pgsOwnershipStructure" value="国有" id="pgs国有">
            <label for="pgs国有">
               国有
            </label>
            <input class="magic-radio" type="radio" name="pgsOwnerStructure" v-model="project.pgsOwnershipStructure" value="民营" id="pgs民营">
            <label for="pgs民营">
               民营
            </label>
            <input class="magic-radio" type="radio" name="pgsOwnerStructure" v-model="project.pgsOwnershipStructure" value="外资" id="pgs外资">
            <label for="pgs外资">
               外资
            </label>
            <input class="magic-radio" type="radio" name="pgsOwnerStructure" v-model="project.pgsOwnershipStructure" value="混合" id="pgs混合">
            <label for="pgs混合">
               混合
            </label>
					</div>
				</div>
				<hr>
			</div>
			<!--税务所单独内容-->
			<div v-if="swsContentShow">
				<div class="form-group">
					<label class="col-sm-2 control-label">税务所：</label>
				</div>
				<div class="form-group">
					<label class="col-sm-2 control-label">招标内容：</label>
					<div class="col-sm-10 check-wrap">
            <input class="magic-checkbox" type="checkbox" value="税鉴" v-model="project.swsBiddingContent" id="税鉴">
            <label for="税鉴">
              税鉴
            </label>
					</div>
				</div>
				<div class="form-group">
					<label for="ownershipStructure" class="col-sm-2 control-label">股权结构：</label>
					<div class="col-sm-10 check-wrap">
            <input class="magic-radio" type="radio" name="swsOwnershipStructure" v-model="project.swsOwnershipStructure" value="国有" id="sws国有">
            <label for="sws国有">
               国有
            </label>
            <input class="magic-radio" type="radio" name="swsOwnershipStructure" v-model="project.swsOwnershipStructure" value="民营" id="sws民营">
            <label for="sws民营">
               民营
            </label>
            <input class="magic-radio" type="radio" name="swsOwnershipStructure" v-model="project.swsOwnershipStructure" value="外资" id="sws外资">
            <label for="sws外资">
               外资
            </label>
            <input class="magic-radio" type="radio" name="swsOwnershipStructure" v-model="project.swsOwnershipStructure" value="混合" id="sws混合">
            <label for="sws混合">
               混合
            </label>
					</div>
				</div>
				<hr>
			</div>
			<!--造价所单独内容-->
			<div v-if="zjsContentShow">
				<div class="form-group">
					<label class="col-sm-2 control-label">造价所：</label>
				</div>
				<div class="form-group">
					<label class="col-sm-2 control-label">招标内容：</label>
					<div class="col-sm-10 check-wrap">
            <input class="magic-checkbox" type="checkbox" value="概算" v-model="project.zjsBiddingContent" id="概算">
            <label for="概算">
              概算
            </label>
            <input class="magic-checkbox" type="checkbox" value="预算" v-model="project.zjsBiddingContent" id="预算">
            <label for="预算">
              预算
            </label>
            <input class="magic-checkbox" type="checkbox" value="结算" v-model="project.zjsBiddingContent" id="结算">
            <label for="结算">
              结算
            </label>
            <input class="magic-checkbox" type="checkbox" value="全过程造价控制" v-model="project.zjsBiddingContent" id="全过程造价控制">
            <label for="全过程造价控制">
              全过程造价控制
            </label>
            <input class="magic-checkbox" type="checkbox" value="入围" v-model="project.zjsBiddingContent" id="入围4">
            <label for="入围4">
              入围
            </label>
            <input class="magic-checkbox" type="checkbox" value="一审" v-model="project.zjsBiddingContent" id="一审">
            <label for="一审">
              一审
            </label>
            <input class="magic-checkbox" type="checkbox" value="二审" v-model="project.zjsBiddingContent" id="二审">
            <label for="二审">
              二审
            </label>
            <!--其他 还不会做-->
						<!-- <div class="checkbox">
						  <label for="other">
						    <input type="checkbox" name="biddingContent" v-model="project.zjsBiddingContent" value="其他">
						    其他：
						  </label>
						  <input type="text" v-model="project.zjsBiddingContent" id="other" class="form-control" placeholder="限15字">
						</div> -->
					</div>
				</div>
				<div class="form-group">
					<label for="zjsFundSource" class="col-sm-2 control-label">资金来源及比例：</label>
					<div class="col-sm-10 check-wrap">
            <input class="magic-checkbox" type="checkbox" value="财政" v-model="project.zjsFundSource" id="财政">
            <label for="财政">
              财政
            </label>
						<input class="magic-checkbox" type="checkbox" value="自筹" v-model="project.zjsFundSource" id="自筹">
            <label for="自筹">
              自筹
            </label>
            <input class="magic-checkbox" type="checkbox" value="贷款" v-model="project.zjsFundSource" id="贷款">
            <label for="贷款">
              贷款
            </label>
            <input class="magic-checkbox" type="checkbox" value="BT等" v-model="project.zjsFundSource" id="BT等">
            <label for="BT等">
              BT等
            </label>
					</div>
				</div>
				<div class="form-group">
					<label for="scale" class="col-sm-2 control-label">建设规模：</label>
					<div class="col-sm-10">
						<div class="row adjust-half-width">
							<div class="col-sm-4">
								<input type="text" class="form-control" id="scale" v-model="project.zjsArea" name="zjsArea" placeholder="请输入建设面积">
							</div>
							<div class="col-sm-4">
								<input type="text" class="form-control" id="scale" v-model="project.zjsLength" name="zjsLength" placeholder="请输入长度">
							</div>
							<div class="col-sm-4">
								<input type="text" class="form-control" id="scale" v-model="project.zjsTotalInvestment" name="zjsTotalInvestment" placeholder="请输入总投资额">
							</div>
						</div>
					</div>
				</div>
				<div class="form-group">
					<label for="zjsLocation" class="col-sm-2 control-label">建设地点：</label>
					<div class="col-sm-10">
					  <input type="text" class="form-control half-width" id="zjsLocation" v-model="project.zjsLocation" name="zjsLocation" placeholder="请输入建设地点">
					</div>
				</div>
				<div class="form-group">
					<label for="serviceTerm" class="col-sm-2 control-label">服务期限：</label>
					<div class="col-sm-10">
					  <input type="text" class="form-control half-width" id="serviceTerm" v-model="project.serviceTerm" name="serviceTerm" placeholder="请输入服务期限">
					</div>
				</div>
				<hr>
			</div>
			<!--共有内容-->
			<div class="form-group">
				<label for="serviceTerm" class="col-sm-2 control-label">审计期限：</label>
				<div class="col-sm-10">
					<input type="text" class="form-control half-width" id="serviceTerm" v-model="project.serviceTerm" name="serviceTerm" placeholder="请输入审计期限">
				</div>
			</div>
			<div class="form-group">
				<label for="investmentConditions" class="col-sm-2 control-label">投资人资质条件、能力：</label>
				<div class="col-sm-10">
				  <input type="text" class="form-control half-width" id="investmentConditions" v-model="project.investmentConditions" name="investmentConditions" placeholder="请输入投资人资质条件及能力">
				</div>
			</div>
			<div class="form-group">
				<label class="col-sm-2 control-label">合同体制：</label>
				<div class="col-sm-10 check-wrap">
          <input class="magic-radio" type="radio" name="commonwealth" v-model="project.contractType.type" value="联合体" id="common">
					<label class="radio-inline" @click="isCommonwealth()" for="common">
						联合体
					</label>
          <input class="magic-radio" type="radio" name="commonwealth" v-model="project.contractType.type" value="非联合体" id="nocommon">
					<label class="radio-inline" @click="notCommonwealth()" for="nocommon">
						非联合体
					</label>
				</div>
			</div>
			<div v-show="commonwealthShow">
				<div class="form-group">
					<label class="col-sm-2 control-label">基本取费：</label>
					<div class="col-sm-10">
						<div class="row half-width">
              <div class="col-sm-11">
                <div class="row">
                  <div class="col-sm-5">
                    <div class="input-group">
                      <div class="input-group-addon">主办方</div>
                      <input type="text" class="form-control" v-model="project.contractType.mainBasicName" placeholder="请输入主办方">
                    </div>
                  </div>
                  <div class="col-sm-1"></div>
                  <div class="col-sm-5">
                    <div class="input-group">
                      <div class="input-group-addon">比例</div>
                      <input type="text" class="form-control" v-model="project.contractType.mainBasicRate">
                      <div class="input-group-addon">%</div>
                    </div>
                  </div>
                  <div class="col-sm-1">

                  </div>
                </div>
              </div>
							<div class="col-sm-1"></div>
						</div>
					</div>
				</div>
				<div class="form-group">
          <label class="col-sm-2 control-label"></label>
          <div class="col-sm-10">
            <div class="row half-width">
            <template v-for="(item, index) in project.contractType.subBasicArray">
              <div class="col-sm-11">
                <div class="row">
                  <div class="col-sm-5">
                    <div class="input-group">
                      <div class="input-group-addon">协办方</div>
                      <input type="text" class="form-control" v-model="item.name" placeholder="请输入协办方">
                    </div>
                  </div>
                  <div class="col-sm-1"></div>
                  <div class="col-sm-5">
                    <div class="input-group">
                      <div class="input-group-addon">比例</div>
                      <input type="text" class="form-control" v-model="item.rate">
                      <div class="input-group-addon">%</div>
                    </div>
                  </div>
                  <div class="col-sm-1">
                    <h4>
                      <a class="text-danger" @click="delBasicFee(index)">
                        <img src="../../../../img/delete_icon.svg">
                      </a>
                    </h4>
                  </div>
                </div>
              </div>
            </template>
            <h4 class="col-sm-1">
              <a class="text-danger" @click="addBasicFee()">
                <img src="../../../../img/add_icon.svg">
              </a>
            </h4>
            </div>
          </div>
				</div>
				<div class="form-group">
					<label class="col-sm-2 control-label">效益取费：</label>
					<div class="col-sm-10">
						<div class="row half-width">
              <div class="col-sm-11">
                <div class="row">
                  <div class="col-sm-5">
                    <div class="input-group">
                      <div class="input-group-addon">主办方</div>
                      <input type="text" class="form-control" v-model="project.contractType.mainEfficiencyName" placeholder="请输入主办方">
                    </div>
                  </div>
                  <div class="col-sm-1"></div>
                  <div class="col-sm-5">
                    <div class="input-group">
                      <div class="input-group-addon">比例</div>
                      <input type="text" class="form-control" v-model="project.contractType.mainEfficiencyRate">
                      <div class="input-group-addon">%</div>
                    </div>
                  </div>
                  <div class="col-sm-1">

                  </div>
                </div>
              </div>
              <div class="col-sm-1"></div>
						</div>
					</div>
				</div>
				<div class="form-group">
					<label class="col-sm-2 control-label"></label>
					<div class="col-sm-10">
						<div class="row half-width">
              <template v-for="(item, index) in project.contractType.subEfficiencyArray">
                <div class="col-sm-11">
                  <div class="row">
                    <div class="col-sm-5">
                      <div class="input-group">
                        <div class="input-group-addon">协办方</div>
                        <input type="text" class="form-control" v-model="item.name" placeholder="请输入协办方">
                      </div>
                    </div>
                    <div class="col-sm-1"></div>
                    <div class="col-sm-5">
                      <div class="input-group">
                        <div class="input-group-addon">比例</div>
                        <input type="text" class="form-control" v-model="item.rate">
                        <div class="input-group-addon">%</div>
                      </div>
                    </div>
                    <div class="col-sm-1">
                      <h4>
                        <a class="text-danger" @click="delEfficiencyFee(index)">
                          <img src="../../../../img/delete_icon.svg">
                        </a>
                      </h4>
                    </div>
                  </div>
                </div>
              </template>
              <h4 class="col-sm-1">
                <a class="text-danger" @click="addEfficiencyFee()">
                  <img src="../../../../img/add_icon.svg">
                </a>
              </h4>
						</div>
					</div>
				</div>
			</div>
			<div class="form-group">
				<label for="biddingNumber" class="col-sm-2 control-label">中标单位数量：</label>
				<div class="col-sm-10">
					<input type="text" class="form-control half-width" id="biddingNumber" v-model="project.biddingNumber" name="biddingNumber" placeholder="请输入中标单位数量">
				</div>
			</div>
			<div class="form-group">
				<label class="col-sm-2 control-label">招标控制价：</label>
				<div class="col-sm-10">
					<div class="input-group half-width">
            <masked-input type="text" class="form-control" placeholder="请输入招标控制价" v-model="project.controlPrice" :mask="currencyMask" :guide="false" placeholderChar="#">
            </masked-input>
						<div class="input-group-addon">元</div>
					</div>
				</div>
			</div>
			<div class="form-group">
				<label for="bidStartTime" class="col-sm-2 control-label">招标报名时间：</label>
				<div class="col-sm-10">
				  <input type="date" class="form-control half-width" id="bidStartTime" v-model="project.bidStartTime" name="bidStartTime">
				</div>
			</div>
			<div class="form-group">
				<label class="col-sm-2 control-label">招标文件价格：</label>
				<div class="col-sm-10">
					<div class="input-group half-width">
            <masked-input type="text" class="form-control" placeholder="请输入招标文件价格" v-model="project.bidDocumentPrice" :mask="currencyMask" :guide="false" placeholderChar="#">
            </masked-input>
						<div class="input-group-addon">元</div>
					</div>
				</div>
			</div>
			<div class="form-group">
				<label for="quotations" class="col-sm-2 control-label">报价方式：</label>
				<div class="col-sm-10">
				  <input type="text" class="form-control half-width" id="quotations" v-model="project.quotations" name="quotations" placeholder="请输入报价方式">
				</div>
			</div>
			<div class="form-group">
				<label for="tenderValidityPeriod" class="col-sm-2 control-label">投标有效期：</label>
				<div class="col-sm-10">
					<div class="input-group half-width">
						<input type="text" class="form-control" id="tenderValidityPeriod" v-model="project.tenderValidityPeriod" name="tenderValidityPeriod" placeholder="请输入投标有限期">
						<div class="input-group-addon">天</div>
					</div>

				</div>
			</div>
			<div class="form-group">
				<label class="col-sm-2 control-label">投标保证金：</label>
				<div class="col-sm-10">
					<div class="input-group half-width">
            <masked-input type="text" class="form-control" placeholder="请输入投标保证金" v-model="project.bidBond" :mask="currencyMask" :guide="false" placeholderChar="#">
            </masked-input>
						<div class="input-group-addon">元</div>
					</div>
				</div>
			</div>
			<!--标书费-->
			<div class="form-group">
				<label for="tenderFee" class="col-sm-2 control-label">标书费：</label>
				<div class="col-sm-10">
					<div class="input-group half-width">
            <masked-input type="text" class="form-control" placeholder="请输入标书费" v-model="project.tenderFee" :mask="currencyMask" :guide="false" placeholderChar="#">
            </masked-input>
						<div class="input-group-addon">元</div>
					</div>
				</div>
			</div>
			<!--中标服务费-->
			<div class="form-group">
				<label for="winningServiceFee" class="col-sm-2 control-label">中标服务费：</label>
				<div class="col-sm-10">
					<div class="input-group half-width">
            <masked-input type="text" class="form-control" placeholder="请输入中标服务费" v-model="project.winningServiceFee" :mask="currencyMask" :guide="false" placeholderChar="#">
            </masked-input>
						<div class="input-group-addon">元</div>
					</div>
				</div>
			</div>
			<div class="form-group">
				<label for="openBidDate" class="col-sm-2 control-label">开标时间：</label>
				<div class="col-sm-10">
				  <input type="datetime-local" class="form-control half-width" id="openBidDate" v-model="project.openBidDate"  name="openBidDate" placeholder="请输入开标时间">
				</div>
			</div>
			<div class="form-group">
				<label for="openBidPlace" class="col-sm-2 control-label">开标地点：</label>
				<div class="col-sm-10">
				  <input type="text" class="form-control half-width" id="openBidPlace" v-model="project.openBidPlace" name="openBidPlace" placeholder="请输入开标地点">
				</div>
			</div>
			<hr>
			<!--备注-->
			<div class="form-group">
				<label for="remark" class="col-sm-2 control-label">备注：</label>
				<div class="col-sm-10">
				  <input type="text" class="form-control half-width" id="remark" v-model="project.remark" name="remark" placeholder="请输入备注">
				</div>
			</div>
		</form>
		<modal v-show="cancelModal">
			<p slot="body" class="ta-c cancel-word">
				<i class="fa fa-exclamation-triangle fa-3x icon" aria-hidden="true"></i>
				撤销后项目将不存在，是否确定撤销？
			</p>
			<p slot="footer">
				<button class="btn my-btn submit-btn" @click="queding()">确定</button>
				<button class="btn my-btn draft-btn" @click="quxiao()">取消</button>
			</p>
		</modal>
	</div>
</template>

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
    img {
      width: 42px;
    }
	}
  .adjust-half-width {
    width: 630px;
  }
  .row.width-adjust {
      width: 800px;
  }
  .check-wrap {
    padding-top: 7px;
  }
</style>

<script>
import axios from 'axios';
import qs from 'qs';
import maskedInput from 'vue-text-mask';

import modal from '../../../component/modal.vue';
import currencyMask from '../../../currencyMask.js';

export default {
	name: 'bidInfoEdit',
	data() {
		return {
			project: this.iniProject,
			cancelModal: false,
			commonwealthShow: false
		}
	},
	computed: {
    //用数组的some()方法，判断数组里是否有某个元素，包含就返回true，如果是true，对应所属类型显示
		kjsContentShow() {
			let kjs = this.project.departmentType.some((item,index,array)=> {
				return item === 'kjs';
			})
			if (kjs) {
				return true;
			}
		},
		pgsContentShow() {
			let pgs = this.project.departmentType.some((item,index,array)=> {
				return item === 'pgs';
			})
			if (pgs) {
				return true;
			}
		},
		swsContentShow() {
			let sws = this.project.departmentType.some((item,index,array)=> {
				return item === 'sws';
			})
			if (sws) {
				return true;
			}
		},
		zjsContentShow() {
			let zjs = this.project.departmentType.some((item,index,array)=> {
				return item === 'zjs';
			})
			if (zjs) {
				return true;
			}
		}
	},
	props: ['iniProject','inputType'],
	methods: {
    currencyMask,
		submit(project) {
			this.$emit('submit',project);
		},
		saveDraft(project) {
			this.$emit('saveDraft',project);
		},
		cancel() {
			this.cancelModal = true;
		},
		quxiao() {
			this.cancelModal = false;
		},
		queding() {
			this.$emit('quedingDelete',this.project.id);
		},
		delBasicFee(index) {
			this.$emit('delBasicFee',index);
		},
		addBasicFee() {
			this.$emit('addBasicFee');
		},
		delEfficiencyFee(index) {
			this.$emit('delEfficiencyFee',index);
		},
		addEfficiencyFee() {
			this.$emit('addEfficiencyFee');
		},
		isCommonwealth() {
			this.commonwealthShow = true;
		},
		notCommonwealth() {
			this.commonwealthShow = false;
		}
	},
	created() {

	},
	components: {
		modal,
    maskedInput
	}
};
</script>
