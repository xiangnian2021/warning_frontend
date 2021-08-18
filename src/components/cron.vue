<template lang='html'>
  <div class='main_content'>
    <el-row :gutter='20' class='alignLeft'>
      <el-select v-model='value' placeholder='请选择'>
              <el-option
                v-for='item in options'
                :key='item.id'
                :label='item.name'
                :value='item.name'>
              </el-option>
      </el-select>
    </el-row>
    <el-row :gutter='20'>
      <el-tabs v-model="activeName" type="border-card" @tab-click="handleClick">
      <el-tab-pane label="一级" name="first">
        <el-col :span='24'>
          <div class='grid-content'>
            <el-input type='textarea' :rows='20' placeholder='请输入一级' v-model='textarea1'></el-input>
            <el-button plain @click="btnClick('first',textarea1)">提交</el-button>
          </div>
        </el-col>
      </el-tab-pane>
      <el-tab-pane label="二级" name="second">
        <el-col :span='24'>
          <div class='grid-content'>
            <el-input type='textarea' :rows='20' placeholder='请输入二级' v-model='textarea2'></el-input>
            <el-button plain @click="btnClick('second',textarea2)">提交</el-button>
          </div>
        </el-col></el-tab-pane>
      <el-tab-pane label="三级" name="third">
        <el-col :span='24'>
        <div class='grid-content'>
          <el-input type='textarea' :rows='20' placeholder='请输入三级' v-model='textarea3'></el-input>
          <el-button plain @click="btnClick('third',textarea3)">提交</el-button>
        </div>
      </el-col>
      </el-tab-pane>
    </el-tabs>
    </el-row>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  data () {
    return {
      activeName: 'first',
      textarea1: '',
      textarea2: '',
      textarea3: '',
      value: '武隆隧道进口右线',
      secId: '',
      options: [{'id': 39, 'name': '武隆隧道进口右线'}, {'id': 34, 'name': '白马山二号隧道出口左线'}]
    }
  },
  methods: {
    handleClick (tab, event) {
      console.log(tab, event)
    },
    btnClick (type, textarea) {
      let formdata = new FormData()
      this.handleSelect(this.value)
      console.log(this.secId)
      formdata.append('value', this.secId)
      formdata.append('work_point_name', this.value)
      formdata.append('type', type)
      formdata.append('content', textarea)
      formdata.append('type', 1)
      axios.post('http://117.36.76.198:36695/dtu/show/', formdata).then(res => {
        if (res.status === 200) {
          this.path = res.path
          this.$message({type: 'success', message: res.data.msg})
        }
      })
    },
    handleSelect (val) {
      this.options.forEach((item, index) => {
        if (item.name === val) {
          console.log(item.id)
          this.secId = item.id
        }
      })
    }
  },
  created () {
  }
}
</script>

<style lang='css'>
.main_content{width:96%;margin:30px}
.alignLeft{text-align: left;}
 .el-row {
    margin-bottom: 20px;
  }
  .el-col {
    border-radius: 4px;
  }
  .grid-content button{margin: 10px;}
</style>
