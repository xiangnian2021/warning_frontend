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
            <el-button plain @click='btnClick'>提交</el-button>
          </div>
        </el-col>
      </el-tab-pane>
      <el-tab-pane label="二级" name="second">
        <el-col :span='24'>
          <div class='grid-content'>
            <el-input type='textarea' :rows='20' placeholder='请输入二级' v-model='textarea2'></el-input>
            <el-button plain>提交</el-button>
          </div>
        </el-col></el-tab-pane>
      <el-tab-pane label="三级" name="third">
        <el-col :span='24'>
        <div class='grid-content'>
          <el-input type='textarea' :rows='20' placeholder='请输入三级' v-model='textarea3'></el-input>
          <el-button plain>提交</el-button>
        </div>
      </el-col>
      </el-tab-pane>
    </el-tabs>
    </el-row>
  </div>
</template>
<script>
export default {
  data () {
    return {
      activeName: 'first',
      textarea1: '',
      textarea2: '',
      textarea3: '',
      value: '武隆隧道进口右线',
      options: [{'id': 39, 'name': '武隆隧道进口右线'}, {'id': 34, 'name': '白马山二号隧道出口左线'}]
    }
  },
  methods: {
    handleClick (tab, event) {
      console.log(tab, event)
    },
    btnClick () {
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
    &:last-child {
      margin-bottom: 0;
    }
  }
  .el-col {
    border-radius: 4px;
  }
  .grid-content button{margin: 10px;}
</style>
