<template>
    <div class="addEdit-block">
        <el-form
                class="detail-form-content"
                ref="ruleForm"
                :model="ruleForm"
                :rules="rules"
                label-width="auto"
                >
            <el-row>
                <el-col :span="12"  v-if="sessionTable !='shuji'">
                    <el-form-item class="select" v-if="type!='info'"  label="书籍" prop="shujiId">
                        <el-select v-model="ruleForm.shujiId" :disabled="ro.shujiId" filterable placeholder="请选择书籍" @change="shujiChange">
                            <el-option
                                    v-for="(item,index) in shujiOptions"
                                    v-bind:key="item.id"
                                    :label="item.shujiName"
                                    :value="item.id">
                            </el-option>
                        </el-select>
                    </el-form-item>
                </el-col>

                <el-col :span="12"  v-if="sessionTable !='shuji' ">
                    <el-form-item class="input" v-if="type!='info'"  label="书籍编号" prop="shujiUuidNumber">
                        <el-input v-model="shujiForm.shujiUuidNumber"
                                  placeholder="书籍编号" clearable readonly></el-input>
                    </el-form-item>
                    <div v-else-if="type=='info'">
                        <el-form-item class="input" label="书籍编号" prop="shujiUuidNumber">
                            <el-input v-model="ruleForm.shujiUuidNumber"
                                      placeholder="书籍编号" readonly></el-input>
                        </el-form-item>
                    </div>
                </el-col>
                <el-col :span="12"  v-if="sessionTable !='shuji' ">
                    <el-form-item class="input" v-if="type!='info'"  label="书籍名称" prop="shujiName">
                        <el-input v-model="shujiForm.shujiName"
                                  placeholder="书籍名称" clearable readonly></el-input>
                    </el-form-item>
                    <div v-else-if="type=='info'">
                        <el-form-item class="input" label="书籍名称" prop="shujiName">
                            <el-input v-model="ruleForm.shujiName"
                                      placeholder="书籍名称" readonly></el-input>
                        </el-form-item>
                    </div>
                </el-col>
                <el-col :span="12"  v-if="sessionTable !='shuji' ">
                    <el-form-item class="input" v-if="type!='info'"  label="书籍作者" prop="shujiZuozhe">
                        <el-input v-model="shujiForm.shujiZuozhe"
                                  placeholder="书籍作者" clearable readonly></el-input>
                    </el-form-item>
                    <div v-else-if="type=='info'">
                        <el-form-item class="input" label="书籍作者" prop="shujiZuozhe">
                            <el-input v-model="ruleForm.shujiZuozhe"
                                      placeholder="书籍作者" readonly></el-input>
                        </el-form-item>
                    </div>
                </el-col>
                <el-col :span="12"  v-if="sessionTable !='shuji' ">
                    <el-form-item class="input" v-if="type!='info'"  label="出版社" prop="shujiChubanshe">
                        <el-input v-model="shujiForm.shujiChubanshe"
                                  placeholder="出版社" clearable readonly></el-input>
                    </el-form-item>
                    <div v-else-if="type=='info'">
                        <el-form-item class="input" label="出版社" prop="shujiChubanshe">
                            <el-input v-model="ruleForm.shujiChubanshe"
                                      placeholder="出版社" readonly></el-input>
                        </el-form-item>
                    </div>
                </el-col>
                <el-col :span="12" v-if="sessionTable !='shuji' ">
                    <el-form-item class="upload" v-if="type!='info' && !ro.shujiPhoto" label="书籍照片" prop="shujiPhoto">
                        <img style="margin-right:20px;" v-bind:key="index" v-for="(item,index) in (shujiForm.shujiPhoto || '').split(',')" :src="$base.url+item" width="100" height="100">
                    </el-form-item>
                    <div v-else-if="type=='info'">
                        <el-form-item v-if="ruleForm.shujiPhoto" label="书籍照片" prop="shujiPhoto">
                            <img style="margin-right:20px;" v-bind:key="index" v-for="(item,index) in (ruleForm.shujiPhoto || '').split(',')" :src="$base.url+item" width="100" height="100">
                        </el-form-item>
                    </div>
                </el-col>
                <el-col :span="12"  v-if="sessionTable !='shuji' ">
                    <el-form-item class="input" v-if="type!='info'"  label="书籍类型" prop="shujiValue">
                        <el-input v-model="shujiForm.shujiValue"
                                  placeholder="书籍类型" clearable readonly></el-input>
                    </el-form-item>
                    <div v-else-if="type=='info'">
                        <el-form-item class="input" label="书籍类型" prop="shujiValue">
                            <el-input v-model="ruleForm.shujiValue"
                                      placeholder="书籍类型" readonly></el-input>
                        </el-form-item>
                    </div>
                </el-col>
                <el-col :span="12"  v-if="sessionTable !='shuji' ">
                    <el-form-item class="input" v-if="type!='info'"  label="所在书架" prop="shujiaValue">
                        <el-input v-model="shujiForm.shujiaValue"
                                  placeholder="所在书架" clearable readonly></el-input>
                    </el-form-item>
                    <div v-else-if="type=='info'">
                        <el-form-item class="input" label="所在书架" prop="shujiaValue">
                            <el-input v-model="ruleForm.shujiaValue"
                                      placeholder="所在书架" readonly></el-input>
                        </el-form-item>
                    </div>
                </el-col>
                <el-col :span="12"  v-if="sessionTable !='shuji' ">
                    <el-form-item class="input" v-if="type!='info'"  label="详细地址" prop="shujiaAddress">
                        <el-input v-model="shujiForm.shujiaAddress"
                                  placeholder="详细地址" clearable readonly></el-input>
                    </el-form-item>
                    <div v-else-if="type=='info'">
                        <el-form-item class="input" label="详细地址" prop="shujiaAddress">
                            <el-input v-model="ruleForm.shujiaAddress"
                                      placeholder="详细地址" readonly></el-input>
                        </el-form-item>
                    </div>
                </el-col>
                <el-col :span="12"  v-if="sessionTable !='shuji' ">
                    <el-form-item class="input" v-if="type!='info'"  label="书籍库存" prop="shujiKucunNumber">
                        <el-input v-model="shujiForm.shujiKucunNumber"
                                  placeholder="书籍库存" clearable readonly></el-input>
                    </el-form-item>
                    <div v-else-if="type=='info'">
                        <el-form-item class="input" label="书籍库存" prop="shujiKucunNumber">
                            <el-input v-model="ruleForm.shujiKucunNumber"
                                      placeholder="书籍库存" readonly></el-input>
                        </el-form-item>
                    </div>
                </el-col>
                <el-col :span="12"  v-if="sessionTable !='shuji' ">
                    <el-form-item class="input" v-if="type!='info'"  label="热度" prop="shujiClicknum">
                        <el-input v-model="shujiForm.shujiClicknum"
                                  placeholder="热度" clearable readonly></el-input>
                    </el-form-item>
                    <div v-else-if="type=='info'">
                        <el-form-item class="input" label="热度" prop="shujiClicknum">
                            <el-input v-model="ruleForm.shujiClicknum"
                                      placeholder="热度" readonly></el-input>
                        </el-form-item>
                    </div>
                </el-col>
                <el-col :span="12"  v-if="sessionTable !='shujiChuruInout'">
                    <el-form-item class="select" v-if="type!='info'"  label="出入库" prop="shujiChuruInoutId">
                        <el-select v-model="ruleForm.shujiChuruInoutId" :disabled="ro.shujiChuruInoutId" filterable placeholder="请选择出入库" @change="shujiChuruInoutChange">
                            <el-option
                                    v-for="(item,index) in shujiChuruInoutOptions"
                                    v-bind:key="item.id"
                                    :label="item.shujiChuruInoutName"
                                    :value="item.id">
                            </el-option>
                        </el-select>
                    </el-form-item>
                </el-col>

                <el-col :span="12"  v-if="sessionTable !='shujiChuruInout' ">
                    <el-form-item class="input" v-if="type!='info'"  label="出入库流水号" prop="shujiChuruInoutUuidNumber">
                        <el-input v-model="shujiChuruInoutForm.shujiChuruInoutUuidNumber"
                                  placeholder="出入库流水号" clearable readonly></el-input>
                    </el-form-item>
                    <div v-else-if="type=='info'">
                        <el-form-item class="input" label="出入库流水号" prop="shujiChuruInoutUuidNumber">
                            <el-input v-model="ruleForm.shujiChuruInoutUuidNumber"
                                      placeholder="出入库流水号" readonly></el-input>
                        </el-form-item>
                    </div>
                </el-col>
                <el-col :span="12"  v-if="sessionTable !='shujiChuruInout' ">
                    <el-form-item class="input" v-if="type!='info'"  label="出入库名称" prop="shujiChuruInoutName">
                        <el-input v-model="shujiChuruInoutForm.shujiChuruInoutName"
                                  placeholder="出入库名称" clearable readonly></el-input>
                    </el-form-item>
                    <div v-else-if="type=='info'">
                        <el-form-item class="input" label="出入库名称" prop="shujiChuruInoutName">
                            <el-input v-model="ruleForm.shujiChuruInoutName"
                                      placeholder="出入库名称" readonly></el-input>
                        </el-form-item>
                    </div>
                </el-col>
                <el-col :span="12"  v-if="sessionTable !='shujiChuruInout' ">
                    <el-form-item class="input" v-if="type!='info'"  label="出入库类型" prop="shujiChuruInoutValue">
                        <el-input v-model="shujiChuruInoutForm.shujiChuruInoutValue"
                                  placeholder="出入库类型" clearable readonly></el-input>
                    </el-form-item>
                    <div v-else-if="type=='info'">
                        <el-form-item class="input" label="出入库类型" prop="shujiChuruInoutValue">
                            <el-input v-model="ruleForm.shujiChuruInoutValue"
                                      placeholder="出入库类型" readonly></el-input>
                        </el-form-item>
                    </div>
                </el-col>
                <input id="updateId" name="id" type="hidden">
            <input id="shujiChuruInoutId" name="shujiChuruInoutId" type="hidden">
            <input id="shujiId" name="shujiId" type="hidden">
               <el-col :span="12">
                   <el-form-item class="input" v-if="type!='info'"  label="操作数量" prop="shujiChuruInoutListNumber">
                       <el-input v-model="ruleForm.shujiChuruInoutListNumber"
                                 placeholder="操作数量" clearable  :readonly="ro.shujiChuruInoutListNumber"></el-input>
                   </el-form-item>
                   <div v-else-if="type=='info'">
                       <el-form-item class="input" label="操作数量" prop="shujiChuruInoutListNumber">
                           <el-input v-model="ruleForm.shujiChuruInoutListNumber"
                                     placeholder="操作数量" readonly></el-input>
                       </el-form-item>
                   </div>
               </el-col>
            </el-row>
            <el-form-item class="btn">
                <el-button v-if="type!='info'" type="primary" class="btn-success" @click="onSubmit">提交</el-button>
                <el-button v-if="type!='info'" class="btn-close" @click="back()">取消</el-button>
                <el-button v-if="type=='info'" class="btn-close" @click="back()">返回</el-button>
            </el-form-item>
        </el-form>
    </div>
</template>
<script>
    import styleJs from "../../../utils/style.js";
    // 数字，邮件，手机，url，身份证校验
    import { isNumber,isIntNumer,isEmail,isPhone, isMobile,isURL,checkIdCard } from "@/utils/validate";
    import utilsJs, {getYearFormat,getMonthFormat,getDateFormat,getDatetimeFormat} from "../../../utils/utils.js";
    export default {
        data() {
            return {
                addEditForm:null,
                id: '',
                type: '',
                sessionTable : "",//登录账户所在表名
                role : "",//权限
                userId:"",//当前登录人的id
                shujiForm: {},
                shujiChuruInoutForm: {},
                ro:{
                    shujiChuruInoutId: false,
                    shujiId: false,
                    shujiChuruInoutListNumber: false,
                    insertTime: false,
                },
                ruleForm: {
                    shujiChuruInoutId: '',
                    shujiId: '',
                    shujiChuruInoutListNumber: '',
                    insertTime: '',
                },
                shujiOptions : [],
                shujiChuruInoutOptions : [],
                rules: {
                   shujiChuruInoutId: [
                              { required: true, message: '出入库不能为空', trigger: 'blur' },
                              {  pattern: /^[0-9]*$/,
                                  message: '只允许输入整数',
                                  trigger: 'blur'
                              }
                          ],
                   shujiId: [
                              { required: true, message: '书籍不能为空', trigger: 'blur' },
                              {  pattern: /^[0-9]*$/,
                                  message: '只允许输入整数',
                                  trigger: 'blur'
                              }
                          ],
                   shujiChuruInoutListNumber: [
                              { required: true, message: '操作数量不能为空', trigger: 'blur' },
                              {  pattern: /^[0-9]*$/,
                                  message: '只允许输入整数',
                                  trigger: 'blur'
                              }
                          ],
                   insertTime: [
                              { required: true, message: '操作时间不能为空', trigger: 'blur' },
                          ],
                }
            };
        },
        props: ["parent"],
        computed: {
        },
        created() {
            //获取当前登录用户的信息
            this.sessionTable = this.$storage.get("sessionTable");
            this.role = this.$storage.get("role");
            this.userId = this.$storage.get("userId");


            if (this.role != "管理员"){
            }else{
            }
            this.addEditForm = styleJs.addStyle();
            this.addEditStyleChange()
            this.addEditUploadStyleChange()
            //获取下拉框信息

         this.$http({
             url: `shuji/page?page=1&limit=100`,
             method: "get"
         }).then(({ data }) => {
             if (data && data.code === 0) {
                this.shujiOptions = data.data.list;
            }
         });
         this.$http({
             url: `shujiChuruInout/page?page=1&limit=100`,
             method: "get"
         }).then(({ data }) => {
             if (data && data.code === 0) {
                this.shujiChuruInoutOptions = data.data.list;
            }
         });

        },
        mounted() {
        },
        methods: {
            // 下载
            download(file){
                window.open(`${file}`)
            },
            // 初始化
            init(id,type) {
                if (id) {
                    this.id = id;
                    this.type = type;
                }
                if(this.type=='info'||this.type=='else'){
                    this.info(id);
                }
                // 获取用户信息
                this.$http({
                    url:`${this.$storage.get("sessionTable")}/session`,
                    method: "get"
                }).then(({ data }) => {
                    if (data && data.code === 0) {
                        var json = data.data;
                    } else {
                        this.$message.error(data.msg);
                    }
                });
            },
            shujiChange(id){
                this.$http({
                    url: `shuji/info/`+id,
                    method: "get"
                }).then(({ data }) => {
                    if (data && data.code === 0) {
                        this.shujiForm = data.data;
                    }
                });
            },
            shujiChuruInoutChange(id){
                this.$http({
                    url: `shujiChuruInout/info/`+id,
                    method: "get"
                }).then(({ data }) => {
                    if (data && data.code === 0) {
                        this.shujiChuruInoutForm = data.data;
                    }
                });
            },
            // 多级联动参数
            info(id) {
                let _this =this;
                _this.$http({
                    url: `shujiChuruInoutList/info/${id}`,
                    method: 'get'
                }).then(({ data }) => {
                    if (data && data.code === 0) {
                        _this.ruleForm = data.data;
                        _this.shujiChange(data.data.shujiId)
                        _this.shujiChuruInoutChange(data.data.shujiChuruInoutId)
                    } else {
                        _this.$message.error(data.msg);
                    }
                });
            },
            // 提交
            onSubmit() {
                this.$refs["ruleForm"].validate(valid => {
                    if (valid) {
                        this.$http({
                            url:`shujiChuruInoutList/${!this.ruleForm.id ? "save" : "update"}`,
                            method: "post",
                            data: this.ruleForm
                        }).then(({ data }) => {
                            if (data && data.code === 0) {
                                this.$message({
                                    message: "操作成功",
                                    type: "success",
                                    duration: 1500,
                                    onClose: () => {
                                        this.parent.showFlag = true;
                                        this.parent.addOrUpdateFlag = false;
                                        this.parent.shujiChuruInoutListCrossAddOrUpdateFlag = false;
                                        this.parent.search();
                                        this.parent.contentStyleChange();
                                    }
                                });
                            } else {
                                this.$message.error(data.msg);
                            }
                        });
                    }
                });
            },
            // 获取uuid
            getUUID () {
                return new Date().getTime();
            },
            // 返回
            back() {
                this.parent.showFlag = true;
                this.parent.addOrUpdateFlag = false;
                this.parent.shujiChuruInoutListCrossAddOrUpdateFlag = false;
                this.parent.contentStyleChange();
            },
            //图片

            addEditStyleChange() {
                this.$nextTick(()=>{
                    // input
                    document.querySelectorAll('.addEdit-block .input .el-input__inner').forEach(el=>{
                        el.style.height = this.addEditForm.inputHeight
                        el.style.color = this.addEditForm.inputFontColor
                        el.style.fontSize = this.addEditForm.inputFontSize
                        el.style.borderWidth = this.addEditForm.inputBorderWidth
                        el.style.borderStyle = this.addEditForm.inputBorderStyle
                        el.style.borderColor = this.addEditForm.inputBorderColor
                        el.style.borderRadius = this.addEditForm.inputBorderRadius
                        el.style.backgroundColor = this.addEditForm.inputBgColor
                    })
                    document.querySelectorAll('.addEdit-block .input .el-form-item__label').forEach(el=>{
                        el.style.lineHeight = this.addEditForm.inputHeight
                        el.style.color = this.addEditForm.inputLableColor
                        el.style.fontSize = this.addEditForm.inputLableFontSize
                    })
                    // select
                    document.querySelectorAll('.addEdit-block .select .el-input__inner').forEach(el=>{
                        el.style.height = this.addEditForm.selectHeight
                        el.style.color = this.addEditForm.selectFontColor
                        el.style.fontSize = this.addEditForm.selectFontSize
                        el.style.borderWidth = this.addEditForm.selectBorderWidth
                        el.style.borderStyle = this.addEditForm.selectBorderStyle
                        el.style.borderColor = this.addEditForm.selectBorderColor
                        el.style.borderRadius = this.addEditForm.selectBorderRadius
                        el.style.backgroundColor = this.addEditForm.selectBgColor
                    })
                    document.querySelectorAll('.addEdit-block .select .el-form-item__label').forEach(el=>{
                        el.style.lineHeight = this.addEditForm.selectHeight
                        el.style.color = this.addEditForm.selectLableColor
                        el.style.fontSize = this.addEditForm.selectLableFontSize
                    })
                    document.querySelectorAll('.addEdit-block .select .el-select__caret').forEach(el=>{
                        el.style.color = this.addEditForm.selectIconFontColor
                        el.style.fontSize = this.addEditForm.selectIconFontSize
                    })
                    // date
                    document.querySelectorAll('.addEdit-block .date .el-input__inner').forEach(el=>{
                        el.style.height = this.addEditForm.dateHeight
                        el.style.color = this.addEditForm.dateFontColor
                        el.style.fontSize = this.addEditForm.dateFontSize
                        el.style.borderWidth = this.addEditForm.dateBorderWidth
                        el.style.borderStyle = this.addEditForm.dateBorderStyle
                        el.style.borderColor = this.addEditForm.dateBorderColor
                        el.style.borderRadius = this.addEditForm.dateBorderRadius
                        el.style.backgroundColor = this.addEditForm.dateBgColor
                    })
                    document.querySelectorAll('.addEdit-block .date .el-form-item__label').forEach(el=>{
                        el.style.lineHeight = this.addEditForm.dateHeight
                        el.style.color = this.addEditForm.dateLableColor
                        el.style.fontSize = this.addEditForm.dateLableFontSize
                    })
                    document.querySelectorAll('.addEdit-block .date .el-input__icon').forEach(el=>{
                        el.style.color = this.addEditForm.dateIconFontColor
                        el.style.fontSize = this.addEditForm.dateIconFontSize
                        el.style.lineHeight = this.addEditForm.dateHeight
                    })
                    // upload
                    let iconLineHeight = parseInt(this.addEditForm.uploadHeight) - parseInt(this.addEditForm.uploadBorderWidth) * 2 + 'px'
                    document.querySelectorAll('.addEdit-block .upload .el-upload--picture-card').forEach(el=>{
                        el.style.width = this.addEditForm.uploadHeight
                        el.style.height = this.addEditForm.uploadHeight
                        el.style.borderWidth = this.addEditForm.uploadBorderWidth
                        el.style.borderStyle = this.addEditForm.uploadBorderStyle
                        el.style.borderColor = this.addEditForm.uploadBorderColor
                        el.style.borderRadius = this.addEditForm.uploadBorderRadius
                        el.style.backgroundColor = this.addEditForm.uploadBgColor
                    })
                    document.querySelectorAll('.addEdit-block .upload .el-form-item__label').forEach(el=>{
                        el.style.lineHeight = this.addEditForm.uploadHeight
                        el.style.color = this.addEditForm.uploadLableColor
                        el.style.fontSize = this.addEditForm.uploadLableFontSize
                    })
                    document.querySelectorAll('.addEdit-block .upload .el-icon-plus').forEach(el=>{
                        el.style.color = this.addEditForm.uploadIconFontColor
                        el.style.fontSize = this.addEditForm.uploadIconFontSize
                        el.style.lineHeight = iconLineHeight
                        el.style.display = 'block'
                    })
                    // 多文本输入框
                    document.querySelectorAll('.addEdit-block .textarea .el-textarea__inner').forEach(el=>{
                        el.style.height = this.addEditForm.textareaHeight
                        el.style.color = this.addEditForm.textareaFontColor
                        el.style.fontSize = this.addEditForm.textareaFontSize
                        el.style.borderWidth = this.addEditForm.textareaBorderWidth
                        el.style.borderStyle = this.addEditForm.textareaBorderStyle
                        el.style.borderColor = this.addEditForm.textareaBorderColor
                        el.style.borderRadius = this.addEditForm.textareaBorderRadius
                        el.style.backgroundColor = this.addEditForm.textareaBgColor
                    })
                    document.querySelectorAll('.addEdit-block .textarea .el-form-item__label').forEach(el=>{
                        // el.style.lineHeight = this.addEditForm.textareaHeight
                        el.style.color = this.addEditForm.textareaLableColor
                        el.style.fontSize = this.addEditForm.textareaLableFontSize
                    })
                    // 保存
                    document.querySelectorAll('.addEdit-block .btn .btn-success').forEach(el=>{
                        el.style.width = this.addEditForm.btnSaveWidth
                        el.style.height = this.addEditForm.btnSaveHeight
                        el.style.color = this.addEditForm.btnSaveFontColor
                        el.style.fontSize = this.addEditForm.btnSaveFontSize
                        el.style.borderWidth = this.addEditForm.btnSaveBorderWidth
                        el.style.borderStyle = this.addEditForm.btnSaveBorderStyle
                        el.style.borderColor = this.addEditForm.btnSaveBorderColor
                        el.style.borderRadius = this.addEditForm.btnSaveBorderRadius
                        el.style.backgroundColor = this.addEditForm.btnSaveBgColor
                    })
                    // 返回
                    document.querySelectorAll('.addEdit-block .btn .btn-close').forEach(el=>{
                        el.style.width = this.addEditForm.btnCancelWidth
                        el.style.height = this.addEditForm.btnCancelHeight
                        el.style.color = this.addEditForm.btnCancelFontColor
                        el.style.fontSize = this.addEditForm.btnCancelFontSize
                        el.style.borderWidth = this.addEditForm.btnCancelBorderWidth
                        el.style.borderStyle = this.addEditForm.btnCancelBorderStyle
                        el.style.borderColor = this.addEditForm.btnCancelBorderColor
                        el.style.borderRadius = this.addEditForm.btnCancelBorderRadius
                        el.style.backgroundColor = this.addEditForm.btnCancelBgColor
                    })
                })
            },
            addEditUploadStyleChange() {
                this.$nextTick(()=>{
                    document.querySelectorAll('.addEdit-block .upload .el-upload-list--picture-card .el-upload-list__item').forEach(el=>{
                        el.style.width = this.addEditForm.uploadHeight
                        el.style.height = this.addEditForm.uploadHeight
                        el.style.borderWidth = this.addEditForm.uploadBorderWidth
                        el.style.borderStyle = this.addEditForm.uploadBorderStyle
                        el.style.borderColor = this.addEditForm.uploadBorderColor
                        el.style.borderRadius = this.addEditForm.uploadBorderRadius
                        el.style.backgroundColor = this.addEditForm.uploadBgColor
                    })
                })
            },
        }
    };
</script>
<style lang="scss">
.editor{
	  height: 500px;

	  & /deep/ .ql-container {
		  height: 310px;
	  }
	}
	.amap-wrapper {
	  width: 100%;.editor{
	  height: 500px;

	  & /deep/ .ql-container {
		  height: 310px;
	  }
	}
	.amap-wrapper {
	  width: 100%;
	  height: 500px;
	}
	.search-box {
	  position: absolute;
	}
	.addEdit-block {
		margin: -10px;
	}
	.detail-form-content {
		padding: 12px;
		background-color: transparent;
	}
	.btn .el-button {
	  padding: 0;
	}
}</style>

