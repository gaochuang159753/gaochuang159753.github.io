<template>
    <div class="mainWrap" v-show="wrapHide == true">
        <div class="wrapContent clearfix">
            <div class="title">
                <h3>HI: &nbsp;{{interviewInfo.name}}</h3>
                <h3>{{interviewInfo.markedWordsInfo}}</h3>
            </div>
            <div class="interviewContent">
                <ul>
                    <li><span>面试类型:</span>  {{interviewTypeArr[interviewInfo.interviewType]}}</li>
                    <li><span>面试职位:</span> {{interviewInfo.positionName}}</li>
                    <li><span>面试时间:</span> {{interviewInfo.interviewTime}}</li>
                    <li><span>面试地点:</span> {{interviewInfo.interviewAddress}}</li>
                    <li><span>联系人:</span> {{interviewInfo.contractName}}</li>
                    <li><span>联系电话:</span> {{interviewInfo.contractPhone}}</li>
                </ul>
            </div>
            <footer id="footer">
                <div>{{interviewInfo.companyName}}</div>
            </footer>
        </div>   
    </div>
</template>
<script>

// var interviewerId = localStorage.getItem('interviewerId') || '12',
// isAccept = '-1'; //面试邀请详情

export default {
    name: 'init',
    data() {
        return{
            interviewerId: '',
            wrapHide: true,
            companyId:null,
            interviewTypeArr: {
                1: '现场面试',
                2: '电话面试'
            },
           interviewInfo: {
                contractPhone: '',
                interviewTime: "",
                markedWordsInfo: "",
                interviewType: 1,
                companyName: "",
                name: "",
                contractName: "",
                positionName: "",
                interviewAddress: "",
                markedWords: "接受面试邀请"
            }
        }
    },
 methods: {
    acceptInvitation(e){
      var isAccept = e;
      var self=this;
      var method="interviewer/getInterviewInfo",
            param=JSON.stringify({
                interviewerId: localStorage.getItem('interviewerid'),
                isAccept: isAccept,
                companyId:localStorage.getItem('companyid')
               
            }),
            successd=function(res){
                if(res.data.data.interviewInfo.markedWords == '接受面试邀请'){
                    self.wrapHide = true;
                    self.interviewInfo = res.data.data.interviewInfo;
                }else if(res.data.data.interviewInfo.markedWords == '链接已失效'){
                     self.$router.push({name:'loseefficacy'});
                }else if(res.data.markedWordsInfo){
                    self.$router.push({name:'refusesuccess'});
                }else if(res.data.markedWordsInfo){
                    self.$router.push({name:'declineInvitation'});
                }
            };
        self.$http(method,param,successd);
    }
  },
  beforeMount(){
      this.interviewerId = localStorage.getItem('interviewerid');
      this.companyId = localStorage.getItem('companyid');
  },
  mounted(){
      this.acceptInvitation('-1');
  }
}
</script>
<style scoped>
@media only screen and (min-width: 750px){
    .btn{
        margin-left: 10%;
        margin-bottom: 40px;
    }
    .btn .button{
        width: 40%!important;
        float: left;
        margin-top: 0!important;
        margin:  0 2.5%!important;
    }
    footer{
        position: relative!important;
        top: 40px;
        margin-bottom: 10px;
    }
}
.mainWrap{
    min-height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
}
.wrapContent{
    width: 100%;
    margin-bottom: 20px;
}
.title{
    margin: 0.5rem 0 1.2rem;
}
.imgBG{
    width: 44%;
    margin: 0.2rem auto 0;
    z-index: 2;
    display: block;
}
.interviewContent{
    width: 90%;
    background-color: #fff;
    font-size: 14px;
    height: 3.4rem;
    margin: -0.5rem auto;
    padding: 0.6rem 0 0 0.3rem;
    line-height: 0.5rem;
}
.btn{
    margin-top: 1rem;
}
.btn .button{
    width:80%;
    height:1rem; 
    background:rgba(90,162,231,1);
    border-radius: 0.5rem; 
    border: none;
    display: block;
    cursor: pointer;
     color: #fff;
     font-size: 17px;
     margin: 0 auto;
     text-align: center;
     line-height: 1rem;
} 
</style>