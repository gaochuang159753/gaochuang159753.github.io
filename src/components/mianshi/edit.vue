<template>
  <div class="mainWrap">
      <div class="mainMask" v-if="picker.pickerShow" @click="picker.pickerShow = false"></div>
      <ul>
          <li>
              <span>姓 &nbsp;&nbsp;名</span>
              <input type="text" v-model="registrationFormInfo.name">
          </li>
          <li>
              <span>性 &nbsp;&nbsp;别</span>
              <!-- <input type="text" readonly="true" @blur="blur('sex')" v-model="sex[registrationFormInfo.sex]" @click="openSelect('sex')"> -->
              <span @click="openSelect('sex')">{{sex[registrationFormInfo.sex]}}</span>
          </li>
                <mt-radio
                transition="slide-edit-box"
                   @change="radioChange()"
                    v-show="picker.type == 'sex' && picker.pickerShow"
                    v-model="registrationFormInfo.sex"
                    :options="options.sexOptions">
                </mt-radio>
          <li>
              <span>民 &nbsp;&nbsp;族</span>
              <input type="text" v-model="registrationFormInfo.national">
          </li>
          <li>
              <span>出生年月</span>
              <span @click="openPicker('birthday')">{{ registrationFormInfo.birthday }}</span>
          </li>
          <li>
              <span>政治面貌</span>
              <!-- <input type="text" v-model="politicalStatus[registrationFormInfo.politicalStatus]">  -->
              <span @click="openSelect('political')">{{politicalStatus[registrationFormInfo.politicalStatus]}}</span>
          </li>
          <mt-radio
                @change="radioChange('political')"
                v-show="picker.type == 'political' && picker.pickerShow"
                v-model="registrationFormInfo.politicalStatus"
                :options="options.politicalOptions">
          </mt-radio>
          <li>
              <span>婚姻状况 </span>
              <!-- <input type="text" v-model="marryStatus[registrationFormInfo.marryStatus]"> -->
               <span @click="openSelect('marryStatus')">{{marryStatus[registrationFormInfo.marryStatus]}}</span>
          </li>
           <mt-radio
                @change="radioChange('marryStatus')"
                v-show="picker.type == 'marryStatus' && picker.pickerShow"
                v-model="registrationFormInfo.marryStatus"
                :options="options.marryOptions">
          </mt-radio>
          <li>
              <span>最高学历 </span>
              <!-- <input type="text" v-model="education[registrationFormInfo.educationLev]"> -->
                <span @click="openSelect('education')">{{education[registrationFormInfo.educationLev]}}</span>
          </li>
            <mt-radio
                @change="radioChange('education')"
                v-show="picker.type == 'education' && picker.pickerShow"
                v-model="registrationFormInfo.educationLev"
                :options="options.educationOptions">
            </mt-radio>
          <li>
              <span>毕业院校 </span>
              <input type="text" v-model="registrationFormInfo.graduateSchool">
          </li>
          <li>
              <span>所学专业 </span>
              <input type="text" v-model="registrationFormInfo.speciality">
          </li>
          <li>
              <span>毕业时间 </span>
              <span @click="openPicker('graduateTime')">{{ registrationFormInfo.graduateTime }}</span>
          </li>
          <li>
              <span>户口所在地 </span>
              <input type="text" v-model="registrationFormInfo.hukouAddress">
          </li>
          <li>
              <span>户口性质 </span>
               <span @click="openSelect('hukou')">{{hukouType[registrationFormInfo.hukouType]}}</span>
          </li>
          <mt-radio
                @change="radioChange('hukou')"
                v-show="picker.type == 'hukou' && picker.pickerShow"
                v-model="registrationFormInfo.hukouType"
                :options="options.hukouTypeOptions">
            </mt-radio>
          <li>
              <span>身份证号 </span>
              <input type="text" v-model="registrationFormInfo.idCardNo">
          </li>
          <li>
              <span>手机号 </span>
              <input type="text" v-model="registrationFormInfo.interviewerPhone">
          </li>
          <li>
              <span>邮 &nbsp;&nbsp;箱 </span>
              <input type="text" v-model="registrationFormInfo.email">
          </li>
          <li>
              <span>现住址 </span>
              <input type="text" v-model="registrationFormInfo.nowLiveAddress">
          </li>
          <li>
              <span>在本公司有无认识的人： </span>
              <mt-switch v-model="switchValue.open" @change="switchChange"></mt-switch>
          </li>
          <li v-show="switchValue.open">
              <span>在本公司认识的人： </span>
              <input type="text" style="width: auto;" v-model="switchValue.person">
          </li>
            <li v-show="switchValue.open">
              <span>与你的关系: </span>
              <input type="text" v-model="switchValue.relation">
          </li>
           <li>
              <span>期望薪资（税前）</span>
              <input type="text"  v-model="registrationFormInfo.expectSalary">
          </li>
      </ul>
      <div class="button" @click="save()">确定</div>
       <mt-datetime-picker
            ref="picker"
            type="date"
            :startDate = "startDate"
            :endDate = "endDate"
            v-model= "timePicker.value"
            @confirm= "handleConfirm">
        </mt-datetime-picker>
  </div>
</template>

<script>
// import { Picker } from 'mint-ui';
// import { DatetimePicker } from 'mint-ui';

export default {
  name: 'edit',
  data(){
      return{
          picker: {
             pickerShow: false,
             type: ''
          },
          timePicker:{
              value: '',
              type: ''
          },
          options: {
              sexOptions:[
                {
                    label: '男',
                    value: '1',
                },
                {
                    label: '女',
                    value: '2'
                },
                {
                    label: '未知',
                    value: '3'
                }
              ],
              politicalOptions:[
                {
                    label: '党员',
                    value: '8',
                },
                {
                    label: '团员',
                    value: '9'
                },
                {
                    label: '群众',
                    value: '10'
                }, 
              ],
              marryOptions: [
                   {
                        label: '未婚',
                        value: '1',
                    },
                    {
                        label: '已婚',
                        value: '2'
                    },
                    {
                        label: '离异',
                        value: '3'
                    },
                    {
                        label: '保密',
                        value: '4',
                    },
              ],
               educationOptions:[
                    {
                        label: '硕士',
                        value: '15'
                    },   
                    {
                        label: '博士',
                        value: '1',
                    },
                    {
                        label: '本科',
                        value: '4',
                    },
                    {
                        label: '大专',
                        value: '5'
                    },
                    {
                        label: '大专以下',
                        value: '14'
                    },
              ],
              hukouTypeOptions:[
                    {
                        label: '农村',
                        value: '0'
                    },   
                    {
                        label: '非农',
                        value: '1'
                    },
              ],
          },
          switchValue: {
              open: false,
              person: '',
              relation: '',
          },
          education: ['', '博士', '研究生', 'MBA', '本科', '大专', '大学', '高中', '中专', '技校', '中技', '初中', '小学',,'大专以下','硕士'],
          politicalStatus: ['', '中共党员', '中共预备党员', '共青团员', '民革党员', '民盟盟员', '民建会员', '民进会员', '党员', '团员', '群众'],
          sex: ['', '男', '女', '未知'],
          hukouType: ['农村', '非农'],
          marryStatus: ['','未婚','已婚','离异','保密'],
          interviewerId: '',
          registrationFormInfo: {
                // birthday: "1989.12.22",
                // educationLev: '1',
                // graduateSchool: "湘西民族职业技术学院",
                // politicalStatus: '5',
                // graduateTime: "2017.09",
                // sex: '2',
                // idCardNo: "121212121212121212",
                // marryStatus: '1',
                // speciality: "服装设计",
                // nowLiveAddress: "公元里",
                // interviewerPhone: 12345678901,
                // name: "张洁",
                // hukouAddress: "大理",
                // hukouType: '0',
                // national: "汉族",
                // email: "412863280@qq.com",
                // haveAcquaintance: "有(维尼+表姐妹)",
            },
                 //   slots: [
        //         {
        //             flex: 1,
        //             defaultIndex: 0,
        //             // values: [{value: '男', keys: 1},{value: '女', keys: 2}],
        //             values: ['男', '女'],
        //             className: 'slot1',
        //             textAlign: 'center',
        //         }
        //   ],
      }
  },
  methods: {
      init() {
          var detail =  localStorage.getItem('detail');
          var registrationFormInfo = JSON.parse(detail);
              for(var key in registrationFormInfo){
                  if(typeof registrationFormInfo[key] == 'number'){
                      registrationFormInfo[key] = String(registrationFormInfo[key]);
                  }
              }
              this.registrationFormInfo = registrationFormInfo;
             this.transitonHaveAcquaintanceH(this.registrationFormInfo);

        //   var self = this;
        //   let method = 'interviewer/signSuccessList',
        //   param=JSON.stringify({
        //       interviewerId: this.$route.query.interviewerId,
        //       firstSubmit: localStorage.getItem('firstsubmit') || '0'
        //   }),
        //   successd = function(res){
        //       let registrationFormInfo = res.data.data.registrationFormInfo;
        //       for(var key in registrationFormInfo){
        //           if(typeof registrationFormInfo[key] == 'number'){
        //               registrationFormInfo[key] = String(registrationFormInfo[key]);
        //           }
        //       }
        //      self.registrationFormInfo = res.data.data.registrationFormInfo;
        //      self.transitonHaveAcquaintanceH(self.registrationFormInfo.haveAcquaintance);
        //   }
        //   this.$http(method, param, successd);
      },
      save() {
          var self=this;
                this.registrationFormInfo.haveAcquaintance = Number(this.switchValue.open);
                this.registrationFormInfo.friendRemaik = this.haveAcquaintance;
                this.registrationFormInfo.interviewerId = this.$route.query.interviewerId;
                let detail = JSON.stringify(self.registrationFormInfo);
                localStorage.setItem('detail', detail);
                self.$router.push({ name: 'editfinish',query:{interviewerId: self.$route.query.interviewerId}})
                // var method = "interviewer/updateBaiscInfo",
                // param = JSON.stringify(self.registrationFormInfo),
                // successd = function(res){
                //     self.$router.push({ name: 'editfinish',query:{interviewerId: self.$route.query.interviewerId}})
                // };
                // self.$http(method,param,successd);
      },
      onValuesChange(picker, values) {
          console.log(picker.getValues())
      },
      openPicker(type) {
          this.timePicker.type = type;
          this.$refs.picker.open();
      }, 
      numberReg(){
          var obj = this.registrationFormInfo.expectSalary;
            this.registrationFormInfo.expectSalary = obj.replace(/[^\d.]/g,"");  //清除“数字”和“.”以外的字符  
            this.registrationFormInfo.expectSalary = obj.replace(/\.{2,}/g,"."); //只保留第一个. 清除多余的  
            this.registrationFormInfo.expectSalary = obj.replace(".","$#$").replace(/\./g,"").replace("$#$","."); 
            this.registrationFormInfo.expectSalary = obj.replace(/^(\-)*(\d+)\.(\d\d).*$/,'$1$2.$3');//只能输入两个小数  
            if(this.registrationFormInfo.expectSalary.indexOf(".")< 0 && obj !=""){//以上已经过滤，此处控制的是如果没有小数点，首位不能为类似于 01、02的金额 
                this.registrationFormInfo.expectSalary= parseFloat(obj); 
            } 
      },
      radioChange(){
          this.picker.pickerShow = false
      },
      handleConfirm(e) {
          if(this.timePicker.type == 'birthday'){
            this.registrationFormInfo.birthday = this.$date(e)              
          }else if(this.timePicker.type == 'graduateTime'){
            this.registrationFormInfo.graduateTime = this.$date(e)              
          } 
        //   if(this.timePicker.type.openPicker == 'sex'){
            // this.registrationFormInfo.sex = this.$date(e)  
        //   }
      },
      openSelect(type) {
          this.picker.pickerShow = true;
          this.picker.type = type;    
      },
      transitonHaveAcquaintanceH(val) {
          let arr = val.friendRemaik.split('+');
          this.switchValue.open =  val.haveAcquaintance == '1'? true: false;
          this.switchValue.person = arr[0];
          this.switchValue.relation = arr[1];
      },
      switchChange(){
          if(this.switchValue.open == false){
              this.switchValue.person = '';
              this.switchValue.relation = '';
          }
      }
   },
  computed: {
      startDate(){
        return new Date(1970,0,1); 
      },
      endDate(){
         return new Date();
      },
      haveAcquaintance() {
          var switchval = this.switchValue? '有': '无';
          if(this.switchValue.relation){
               return this.switchValue.person + '+' + this.switchValue.relation;
          }else{
              return this.switchValue.person
          }
      }
  },
  mounted() {
      this.init();
  }
}
</script>
<style scoped>
.mainMask{
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background-color: rgba(0, 0, 0, 0.4);
}
.mint-radiolist{
    z-index: 2;
}
.mint-cell-wrapper{
    background: none;
    float: left;
    width: 1px;
}
mainWrap{
    width: 100%;
    display: flex;
    flex-direction: column;
}
ul li{
    display: flex;
    justify-content: flex-start;
    font-size: 0.18rem;
    font-size: 14px;
    font-family:PingFang-SC-Medium;
    color:rgba(153,153,153,1);
    line-height: 0.4rem;
    height: 0.4rem;
    padding: 0.3rem;
}
ul{
    background: #fff;
}
ul li{
    border-top: 1px solid #D7D7D7;  
    border-width: 0.5px;
}
ul li:nth-child(1){
    border: none;
}
ul li span{
    min-width: 30%;
    word-wrap: nowrap;
    word-break: keep-all;
}
ul li input{
    font-size: 14px;
    font-weight:bold;
}
ul li span:nth-child(2){
    font-size: 14px;
    font-weight:bold;
    width: 100%;
    color: black;
}
ul li input{
    background: none;
    outline: none;
    border: none;
    width: 100%;
    color: black;
}
.pickerWrap{
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    background: #fff;
    text-align: right;
}
.maskWrap{
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background-color: rgba(0, 0, 0, 0.4);
}
.pickerWrap button{
    margin: 10px 20px;
}
</style>

