<template>
	<div>
		<div class="header1">
			<div class="left">
				<img src="@/assets/imgs/home/logo/Basement Logo1.png" />
				<span>城区组团碳排放与用地布局关系模拟平台</span>
			</div>
			<div class="ulList">
				<ul>
					<li class="none" @click="clear">退出</li>
					<li>{{ username }}</li>
					<li class="none1"><img src="@/assets/imgs/details/Icon_slices/Icon.png" /></li>
				</ul>
			</div>
		</div>
		<div style="clear: both"></div>
		<el-menu :default-active="0" class="el-menu-demo" mode="horizontal" text-color="#000000" active-text-color="#3F75D4" @select="handleSelect">
			<el-menu-item index="1">
				<i class="el-icon-folder-add"></i>
				新建方案
			</el-menu-item>
			<el-menu-item index="2" @click="historyCase()">
				<i class="el-icon-d-arrow-left"></i>
				历史方案
			</el-menu-item>
			<el-submenu index="3">
				<template slot="title">
					<i class="el-icon-s-order"></i>
					计算
				</template>
				<el-menu-item index="3-1">碳排量计算</el-menu-item>
			</el-submenu>
			<el-menu-item index="5">
				<i class="el-icon-notebook-2"></i>
				报告
			</el-menu-item>
		</el-menu>
		<!-- 弹窗一 -->
		<el-dialog title="新建方案" :visible.sync="dialogFormVisible" :width="width" class="posi1" :top="top">
			<el-form class="block" :rules="rule" ref="form" :model="formData">
				<el-form-item label="方案名称" :label-width="formLabelWidth" prop="caseName">
					<el-col :span="18"><el-input placeholder="请输入内容" v-model="formData.caseName" clearable></el-input></el-col>
				</el-form-item>
				<el-form-item label="所在城市" :label-width="formLabelWidth">
					<el-col :span="18"><List @getArea="getArea" /></el-col>
				</el-form-item>
				<el-form-item label="设计类型" :label-width="formLabelWidth" prop="caseType">
					<el-col :span="18"><el-input placeholder="请输入内容" v-model="formData.caseType" clearable></el-input></el-col>
				</el-form-item>
				<el-form-item label="规划时间" :label-width="formLabelWidth" prop="planDate">
					<el-date-picker
						v-model="formData.planDate"
						type="date"
						format="yyyy-MM-dd"
						value-format="yyyy-MM-dd"
						placeholder="选择日期"
						class="widthSet"
						style="width: 275px;"
						@change="getTime()"
					></el-date-picker>
				</el-form-item>
				<el-form-item label="规划范围" :label-width="formLabelWidth">
					<el-upload
						class="upload-demo"
						action="http://localhost:8080/TransportCE/shape/upload"
						:on-preview="handlePreview"
						:on-remove="handleRemove"
						:on-success="handleSuccess1"
						multiple
						:limit="1"
						:on-exceed="handleExceed"
						:file-list="fileList"
						v-model="planLand"
						accept=".zip,.rar"
					>
						<el-button size="large" type="primary" class="btn3">点击上传</el-button>
						<div slot="tip" class="el-upload__tip">只能上传zip或rar格式的文件</div>
					</el-upload>
				</el-form-item>
				<el-form-item label="规划用地" :label-width="formLabelWidth">
					<el-upload
						class="upload-demo"
						action="http://localhost:8080/TransportCE/shape/upload"
						:on-preview="handlePreview"
						:on-remove="handleRemove"
						:on-success="handleSuccess2"
						multiple
						:limit="1"
						:on-exceed="handleExceed"
						:file-list="fileList"
						v-model="planScope"
						accept=".zip,.rar"
					>
						<el-button size="large" type="primary" class="btn3">点击上传</el-button>
						<div slot="tip" class="el-upload__tip">只能上传zip或rar格式的文件</div>
					</el-upload>
				</el-form-item>
				<el-form-item label="规划路网" :label-width="formLabelWidth">
					<el-upload
						class="upload-demo"
						action="http://localhost:8080/TransportCE/shape/upload"
						:on-preview="handlePreview"
						:on-remove="handleRemove"
						:on-success="handleSuccess3"
						multiple
						:limit="1"
						:on-exceed="handleExceed"
						:file-list="fileList"
						v-model="planRoadNetwork"
						accept=".zip,.rar"
					>
						<el-button size="large" type="primary" class="btn3">点击上传</el-button>
						<div slot="tip" class="el-upload__tip">只能上传zip或rar格式的文件</div>
					</el-upload>
				</el-form-item>
				<el-form-item label="规划慢行路网" :label-width="formLabelWidth">
					<el-upload
						class="upload-demo"
						action="http://localhost:8080/TransportCE/shape/upload"
						:on-preview="handlePreview"
						:on-remove="handleRemove"
						:on-success="handleSuccess4"
						multiple
						:limit="1"
						:on-exceed="handleExceed"
						:file-list="fileList"
						v-model="planSlowRoadNetwork"
						accept=".zip,.rar"
					>
						<el-button size="large" type="primary" class="btn3">点击上传</el-button>
						<div slot="tip" class="el-upload__tip">只能上传zip或rar格式的文件</div>
					</el-upload>
				</el-form-item>
				<el-form-item label="交叉口" :label-width="formLabelWidth">
					<el-upload
						class="upload-demo"
						action="http://localhost:8080/TransportCE/shape/upload"
						:on-preview="handlePreview"
						:on-remove="handleRemove"
						:on-success="handleSuccess5"
						multiple
						:limit="1"
						:on-exceed="handleExceed"
						:file-list="fileList"
						v-model="intersections"
						accept=".zip,.rar"
					>
						<el-button size="large" type="primary" class="btn3">点击上传</el-button>
						<div slot="tip" class="el-upload__tip">只能上传zip或rar格式的文件</div>
					</el-upload>
				</el-form-item>
				<el-form-item label="规划公交线" :label-width="formLabelWidth">
					<el-select v-model="value1" placeholder="请选择" class="select" @change="judge1(value1)">
						<el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value"></el-option>
					</el-select>
					<el-form :model="numberValidateForm" ref="numberValidateForm" v-show="ifShowInput1">
						<el-form-item prop="input1" :rules="[{ required: true, message: '请输入' }, { type: 'number', message: '请填写数字' }]" class="inputAll1">
							<el-input type="input1" v-model.number="numberValidateForm.input1" autocomplete="off" placeholder="请输入(%)"></el-input>
						</el-form-item>
					</el-form>
					<el-upload
						class="upload-demo"
						action="http://localhost:8080/TransportCE/shape/upload"
						:on-preview="handlePreview"
						:on-remove="handleRemove"
						:on-success="handleSuccess6"
						multiple
						:limit="1"
						:on-exceed="handleExceed"
						:file-list="fileList"
						v-model="file1"
						accept=".zip,.rar"
						v-show="ifShowUpload1"
					>
						<div slot="tip" class="el-upload__tip">只能上传zip或rar格式的文件</div>
						<el-button size="large" type="primary" class="btn4">点击上传</el-button>
					</el-upload>
				</el-form-item>
				<el-form-item label="规划公交站" :label-width="formLabelWidth">
					<el-select v-model="value2" placeholder="请选择" class="select" @change="judge2(value2)">
						<el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value"></el-option>
					</el-select>
					<el-form :model="numberValidateForm" ref="numberValidateForm" v-show="ifShowInput2">
						<el-form-item prop="input2" :rules="[{ required: true, message: '请输入' }, { type: 'number', message: '请填写数字' }]" class="inputAll1">
							<el-input type="input2" v-model.number="numberValidateForm.input2" autocomplete="off" placeholder="请输入(%)"></el-input>
						</el-form-item>
					</el-form>
					<el-upload
						class="upload-demo"
						action="http://localhost:8080/TransportCE/shape/upload"
						:on-preview="handlePreview"
						:on-remove="handleRemove"
						:on-success="handleSuccess7"
						multiple
						:limit="1"
						:on-exceed="handleExceed"
						:file-list="fileList"
						v-model="file2"
						accept=".zip,.rar"
						v-show="ifShowUpload2"
					>
						<div slot="tip" class="el-upload__tip">只能上传zip或rar格式的文件</div>
						<el-button size="large" type="primary" class="btn4">点击上传</el-button>
					</el-upload>
				</el-form-item>
				<el-form-item label="规划地铁站" :label-width="formLabelWidth" class="demo-ruleForm">
					<el-select v-model="value3" placeholder="请选择" class="select" @change="judge3(value3)">
						<el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value"></el-option>
					</el-select>
					<el-form :model="numberValidateForm" ref="numberValidateForm" v-show="ifShowInput3">
						<el-form-item prop="input3" :rules="[{ required: true, message: '请输入' }, { type: 'number', message: '请填写数字' }]" class="inputAll1">
							<el-input type="input3" v-model.number="numberValidateForm.input3" autocomplete="off" placeholder="请输入(%)"></el-input>
						</el-form-item>
					</el-form>
					<el-upload
						class="upload-demo"
						action="http://localhost:8080/TransportCE/shape/upload"
						:on-preview="handlePreview"
						:on-remove="handleRemove"
						:on-success="handleSuccess8"
						multiple
						:limit="1"
						:on-exceed="handleExceed"
						:file-list="fileList"
						v-model="file3"
						accept=".zip,.rar"
						v-show="ifShowUpload3"
					>
						<div slot="tip" class="el-upload__tip">只能上传zip或rar格式的文件</div>
						<el-button size="large" type="primary" class="btn4">点击上传</el-button>
					</el-upload>
				</el-form-item>
			</el-form>
			<div slot="footer" class="posi btn">
				<el-button @click="dialogFormVisible = false">取 消</el-button>
				<el-button type="primary" @click="judge()">确 定</el-button>
			</div>
		</el-dialog>
		<!-- 弹窗二 -->
		<el-dialog title="历史方案" :visible.sync="dialogTableVisible" class="posi" :width="width1">
			<el-table :data="tableData" stripe style="width: 100%" :row-class-name="tableRowClassName" :cell-style="cellStyle">
				<el-table-column property="num" width="50"></el-table-column>
				<el-table-column v-if="false" property="caseId" ></el-table-column>
				<el-table-column v-if="false" property="caseName" ></el-table-column>
				<el-table-column property="caseName" width="200"></el-table-column>
				<el-table-column property="circle" width="10"></el-table-column>
				<el-table-column property="state" width="100"></el-table-column>
				<el-table-column property="data" width="100"></el-table-column>
				<el-table-column width="50" >
					<template slot-scope="scope">
					    <a href="javascript:;" @click="appearIndex(scope.row)">查看</a>
					</template>
				</el-table-column>
			</el-table>
			<div slot="footer" class="btn1">
				<el-button @click="dialogTableVisible = false">取 消</el-button>
				<el-button type="primary" @click="dialogTableVisible = false">确 定</el-button>
			</div>
		</el-dialog>
		<!-- 弹窗三 -->
		<el-dialog title="输入参数" :visible.sync="dialogVisible1" width="35%" :show-close="false" :modal="false" class="posi">
			<el-form class="block1" :rules="rule" ref="form" :model="formData">
				<el-form-item label="城市人口" :label-width="formLabelWidth" prop="Planning_population">
					<el-col :span="18"><el-input placeholder="请输入" v-model="formData.Planning_population" clearable></el-input></el-col>
				</el-form-item>
				<el-form-item label="规划人口" :label-width="formLabelWidth" prop="city_population">
					<el-col :span="18"><el-input placeholder="请输入" v-model="formData.city_population" clearable class="width"></el-input></el-col>
				</el-form-item>
				<el-form-item label="出行比例常数" :label-width="formLabelWidth" prop="walk" class="float">
					<el-col :span="10"><el-input placeholder="慢行" v-model="formData.walk"></el-input></el-col>
				</el-form-item>
				<el-form-item label="" :label-width="formLabelWidth" prop="bus" class="float">
					<el-col :span="10"><el-input placeholder="公交" v-model="formData.bus"></el-input></el-col>
				</el-form-item>
				<el-form-item label="" :label-width="formLabelWidth" prop="subway" class="float">
					<el-col :span="10"><el-input placeholder="地铁" v-model="formData.subway"></el-input></el-col>
				</el-form-item>
				<el-form-item label="" :label-width="formLabelWidth" prop="car" class="float">
					<el-col :span="10"><el-input placeholder="小汽车" v-model="formData.car"></el-input></el-col>
				</el-form-item>
			</el-form>
			<div slot="footer" class="last">
				<el-button @click="dialogVisible1 = false">取 消</el-button>
				<el-button type="primary" @click="dialogVisible1 = false, ceComputed()">确 定</el-button>

			</div>
		</el-dialog>
	</div>
</template>
<script>
import List from '@/components/common/List.vue';
import dddd from '@/views/details/demo.json';
import login from '@/api/login.js';
import caseinfo from '@/api/case.js';
	import {jenks} from "@/utils/jenks.js";
export default {
	components: {
		List
	},
	data() {
		return {
			numberValidateForm: {
				input1: '',
				input2: '',
				input3: ''
			},
			ifShowInput1: false,
			ifShowUpload1: false,
			ifShowInput2: false,
			ifShowUpload2: false,
			ifShowInput3: false,
			ifShowUpload3: false,
			file1: '',
			file2: '',
			file3: '',
			options: [
				{
					value: 'text',
					label: '请输入参数'
				},
				{
					value: 'file',
					label: '请上传文件'
				}
			],
			value1: '',
			value2: '',
			value3: '',
			rule: {
				caseName: [{ required: true, message: '请输入方案名称', trigger: 'blur' }],
				caseType: [{ required: true, message: '请输入方案类型', trigger: 'blur' }],
				planDate: [{ required: true, message: '请选择日期', trigger: 'blur' }],
				verification: [{ required: true, message: '请输入验证码', trigger: 'blur' }],
				Planning_population: [{ required: true, message: '请输入', trigger: 'blur' }],
				city_population: [{ required: true, message: '请输入', trigger: 'blur' }],
				walk: [{ required: true, message: '请输入', trigger: 'blur' }],
				subway: [{ required: true, message: '请输入', trigger: 'blur' }],
				bus: [{ required: true, message: '请输入', trigger: 'blur' }],
				car: [{ required: true, message: '请输入', trigger: 'blur' }]
			},
			username: this.$store.getters.getUserInfo.username,
			activeIndex: '1',
			dialogTableVisible: false,
			dialogFormVisible: false,
			dialogVisible1: false,
			width: '30%',
			width1: '30%',
			caseName: '',
			province: '',
			city: '',
			area: '',
			caseType: '',
			planDate: '',
			planLand: '',
			planScope: '',
			planRoadNetwork: '',
			planSlowRoadNetwork: '',
			intersections: '',
			plannPublicTransportationLines: '',
			planBusStation: '',
			planMetroStation: '',
			Planning_population: '',
			city_population: '',
			formLabelWidth: '140px',
			fileList: [],
			tableData: [
				{
					name: '西咸新区',
					status: '完成/待完成',
					time: '2020-10-25',
					href: '查看'
				},
				{
					name: '天府新区',
					status: '完成/待完成',
					time: '2020-12-16',
					href: '查看'
				}
			],
			top: '4vh',
			formData: {
				caseName: '',
				caseType: '',
				Planning_population: '',
				city_population: '',
				walk: '',
				subway: '',
				car: '',
				bus: ''
			}
		};
	},
	methods: {
		judge1(value) {
			if (value == 'text') {
				this.ifShowUpload1 = false;
				this.ifShowInput1 = true;
				this.file1='';
			} else if (value == 'file') {
				this.ifShowInput1 = false;
				this.ifShowUpload1 = true;
				this.numberValidateForm.input1=''
			}
		},
		judge2(value) {
			if (value == 'text') {
				this.ifShowUpload2 = false;
				this.ifShowInput2 = true;
				this.file2='';
			} else if (value == 'file') {
				this.ifShowInput2 = false;
				this.ifShowUpload2 = true;
				this.numberValidateForm.input2=''
			}
		},
		judge3(value) {
			if (value == 'text') {
				this.ifShowUpload3 = false;
				this.ifShowInput3 = true;
				this.file3='';
			} else if (value == 'file') {
				this.ifShowInput3 = false;
				this.ifShowUpload3 = true;
				this.numberValidateForm.input3=''
			}
		},
		handleSelect(key, keyPath) {
			if (key == '1') {
				this.dialogFormVisible = true;
			} else if (key == '2') {
				this.dialogTableVisible = true;
			} else if (key == '3-1') {
				this.dialogVisible1 = true;
			}else if(key == '5'){
				 var a = document.createElement("a");
				 a.download = "print.doc";
				 a.href = "http://www.baierinfo.com/出行方式占比.doc";
				 a.click();
			}
		},
		cellStyle({ column, columnIndex }) {
			if (columnIndex == 2) {
				return 'color:rgba(82, 196, 26, 1);';
			} else if (columnIndex == 3) {
				return {
					cursor: 'pointer'
				};
			}
		},
		tableRowClassName({ row, rowIndex }) {
			row.index = rowIndex;
		},
		onRowClick(row, event, column) {
			const index = row.index;
		},
		appearIndex(row) {
			this.$store.commit('setCaseInfo', row);
			if (row.state == "未计算") {
				alert('请先进行计算');
			} else {
				this.ceComputed();
			}
		},
		clear() {
			this.$store.commit('setCaseInfo', null);
			this.$store.commit('setCaseBasicData', {});
			this.$router.push('/login');
		},
		handlePreview(file) {
			console.log(file);
		},
		handleRemove(file, fileList) {
			console.log(file, fileList);
		},
		beforeRemove(file, fileList) {
			return this.$confirm(`确定移除 ${file.name}？`);
		},
		handleExceed(files, fileList) {
			this.$message.warning(`当前限制选择1个文件`);
		},
		handleSuccess1(response, file, fileList) {
			this.planLand = response.jsonmap.filePath;
			console.log(this.planLand);
		},
		handleSuccess2(response, file, fileList) {
			this.planScope = response.jsonmap.filePath;
			console.log(this.planScope);
		},
		handleSuccess3(response, file, fileList) {
			this.planRoadNetwork = response.jsonmap.filePath;
			console.log(this.planRoadNetwork);
		},
		handleSuccess4(response, file, fileList) {
			this.planSlowRoadNetwork = response.jsonmap.filePath;
			console.log(this.planSlowRoadNetwork);
		},
		handleSuccess5(response, file, fileList) {
			this.intersections = response.jsonmap.filePath;
			console.log(this.intersections);
		},
		handleSuccess6(response, file, fileList) {
			this.file1 = response.jsonmap.filePath;
			console.log(this.file1);
		},
		handleSuccess7(response, file, fileList) {
			this.file2 = response.jsonmap.filePath;
			console.log(this.file2);
		},
		handleSuccess8(response, file, fileList) {
			this.file3 = response.jsonmap.filePath;
			console.log(this.file3);
		},
		getArea(lable) {
			this.province = lable[0];
			this.city = lable[1];
			this.area = lable[2];
		},
		createCase: function() {
			var params = {
				caseName: this.formData.caseName,
				province: this.province,
				city: this.city,
				area: this.area,
				caseType: this.formData.caseType,
				planDate: this.formData.planDate,
				planLand: this.planLand,
				planScope: this.planScope,
				planRoadNetwork: this.planRoadNetwork,
				planSlowRoadNetwork: this.planSlowRoadNetwork,
				intersections: this.intersections,
				plannPublicTransportationLines: this.numberValidateForm.input1 || this.file1,
				planBusStation: this.numberValidateForm.input2 || this.file2,
				planMetroStation: this.numberValidateForm.input3 || this.file3
			};
			console.log(this.numberValidateForm.input1 + this.file1);
			console.log(this.numberValidateForm.input2 + this.file2);
			console.log(this.numberValidateForm.input3 + this.file3);
			caseinfo.createCase(params).then(res => {
				if (res.data.code == 0) {
					this.$store.commit('setCaseInfo', res.data);
					alert('方案添加成功');
					this.$store.commit('setCaseInfo', res.data);
					location.reload();
				} else {
					alert(res.data.msg);
				}
			});
		},
		timestampToTime: function(timestamp) {
			var date = new Date(timestamp * 1000);
			var Y = date.getFullYear() + '-';
			var M = (date.getMonth() + 1 < 10 ? '0' + (date.getMonth() + 1) : date.getMonth() + 1) + '-';
			var D = date.getDate() + '';
			return Y + M + D;
		},
		historyCase: function() {
			var params = {
				offset: 0,
				limit: 20,
				sort: 'createTime',
				order: 'desc'
			};
			caseinfo.historyCase(params).then(res => {
				if (res.data.code == 0) {
					console.info(res.data.page.list)
					this.tableData = [];
					for(var i=0;i<res.data.page.list.length;i++){
						if(res.data.page.list[i].state == 1){
								this.tableData.push({
									num: i+1,
									caseId:res.data.page.list[i].caseId,
									caseName:res.data.page.list[i].caseName,
									city: res.data.page.list[i].province+res.data.page.list[i].city,
									circle:'·',
									data:this.timestampToTime(res.data.page.list[i].createTime),
									state: "已计算",
									href:'查看'
								});
						}else{
								this.tableData.push({
									num: i+1,
									caseId:res.data.page.list[i].caseId,
									caseName:res.data.page.list[i].caseName,
									city: res.data.page.list[i].province+res.data.page.list[i].city,
									circle:'·',
									data:this.timestampToTime(res.data.page.list[i].createTime),
									state: "未计算",
									href:'查看'
								});
						}
					}
				} else {
					alert(res.data.msg);
				}
			});
		},
		judge() {
			if (this.planLand == '' || this.planScope == '' || this.planRoadNetwork == '' || this.planSlowRoadNetwork == '' || this.intersections == '') {
				this.$message({
					message: '请上传所需文件',
					type: 'error'
				});
			} else {
				this.dialogFormVisible = false;
				this.createCase();
			}
		},
		getTime() {
			return this.formData.planDate;
		},

		ceComputed(){
			var params={
				caseId:this.$store.getters.getCaseInfo.caseId,
				filePath:"E:/ret/ret.shp",
				}
			caseinfo.ceComputed(params).then(res=>{
				if (res.data.code == 0) {
					var arr = JSON.parse('[' + res.data.jenksList + ']');
					this.$store.commit('setJenks', jenks(arr, 5));
					this.$store.commit('setCaseBasicData', res.data.areaCE);
					if (this.$route.path == '/detail') {
						this.$router.go(0);
					} else {
						this.$router.push('/detail');
					}
				} else {
					alert(res.data.msg);
				}
			});
		}
	}
};
</script>
<style scoped>
.btn4 {
	position: absolute;
	margin-left: -34px;
	margin-top: -65px;
}
.inputAll {
	width: 125px;
	position: absolute;
	margin-left: 30px;
}
.inputAll1 {
	width: 125px;
	position: absolute;
	margin-left: 146px;
	margin-top: -41px;
}
.select {
	margin-left: -248px;
	width: 120px;
}
.header1 {
	position: relative;
	width: 100%;
	height: 50px;
	background: linear-gradient(to bottom, #70d7a0, #5c6dc3);
}

.header1 .left {
	width: 300px;
}

.header1 .left img {
	margin-top: 7px;
	margin-left: 40px;
	width: 35px;
}

.header1 span {
	color: #ffffff;
	position: absolute;
	top: 16px;
	left: 80px;
}

.header1 ul {
	position: absolute;
	right: 40px;
	top: 16px;
	margin-right: 80px;
}

.header1 ul li {
	float: right;
	border-right: 1px solid #fff;
	padding: 0 10px;
	color: #fff;
	cursor: pointer;
}

.header1 ul li img {
	width: 12px;
}

.ulList .none {
	border: none;
}

.ulList .none1 {
	border: none;
	margin-right: -12px;
}

.ulList .btn {
	position: absolute;
	right: 30px;
	top: 16px;
	text-align: center;
	line-height: 20px;
	width: 58px;
	height: 22px;
	border: 1px solid white;
	cursor: pointer;
	color: #fff;
}

.ulList .btn1 {
	float: left;
	width: 28px;
}

.ulList .btn2 {
	float: left;
	width: 28px;
}

.ulList .active {
	background-color: #3c86d8;
	color: #fff;
}
.bgc {
	background-color: #fff;
	border: 1px solid rgb(220, 223, 230);
	color: rgb(192, 196, 204);
	margin-left: -265px;
}
.tip {
	font-size: 12px;
	color: rgb(192, 196, 204);
	margin-left: 60px;
}
.block {
	margin-left: 30px;
	margin-top: -30px;
}
.posi {
	text-align: center;
}
.btn {
	margin-top: -40px;
}
.posi .btn1 {
	margin-top: -8px;
	text-align: center;
}
.top {
	margin-top: -43px;
	margin-left: 10px;
}
.block1 {
	margin-left: 60px;
	margin-top: -10px;
	text-align: center;
}
.posi1 {
	text-align: center;
	margin-top: -15px;
}
.btn3 {
	margin-left: -268px;
}
.last {
	position: relative;
	margin-top: 50px;
	margin-right: 230px;
}
.widthSet {
	margin-left: -94px;
}
.el-upload__tip {
	margin-top: -40px;
	margin-left: 30px;
}
.float {
	float: left;
	margin-right: -243px;
}
</style>
