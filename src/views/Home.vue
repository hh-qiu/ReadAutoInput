<template>
  <div class="home">
    <el-form ref="form" :model="form" label-width="100px" style="margin:30px auto;padding:20px;">
      <el-row>
        <el-col :span="12">
          <el-form-item label="活动名称">
            <el-input v-model="form.name"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item label="活动区域">
            <el-select v-model="form.region" placeholder="请选择活动区域" style="width:100%">
              <el-option label="区域一" value="shanghai"></el-option>
              <el-option label="区域二" value="beijing"></el-option>
            </el-select>
          </el-form-item>
        </el-col>
      </el-row>
      <!-- <el-form-item label="活动名称">
        <el-input v-model="form.name"></el-input>
      </el-form-item>
      <el-form-item label="活动区域">
        <el-select v-model="form.region" placeholder="请选择活动区域">
          <el-option label="区域一" value="shanghai"></el-option>
          <el-option label="区域二" value="beijing"></el-option>
        </el-select>
      </el-form-item>-->
      <el-row>
        <el-col :span="12">
          <el-form-item label="活动物品">
            <read-auto-input
              v-model="form.msg"
              :valueKey="keymsg"
              :fetchSuggestions="this.querySearch"
            />
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item label="活动时间">
            <el-col :span="11">
              <el-date-picker
                type="date"
                placeholder="选择日期"
                v-model="form.date1"
                style="width: 100%;"
              ></el-date-picker>
            </el-col>
            <el-col class="line" :span="2">-</el-col>
            <el-col :span="11">
              <el-time-picker placeholder="选择时间" v-model="form.date2" style="width: 100%;"></el-time-picker>
            </el-col>
          </el-form-item>
        </el-col>
      </el-row>
      <!-- <el-form-item label="活动物品">
        <read-auto-input v-model="form.msg" :valueKey="keymsg" :fetchSuggestions="this.querySearch" style="width:230px;"/>
      </el-form-item>-->
      <el-row>
        <el-col :span="12">
          <el-form-item label="活动形式">
            <el-input type="textarea" v-model="form.desc"></el-input>
          </el-form-item>
        </el-col>
      </el-row>
      <el-form-item>
        <el-button type="primary" @click="onSubmit">立即创建</el-button>
        <el-button>取消</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
// @ is an alias to /src
import ReadAutoInput from "@/components/ReadAutoInput.vue";

export default {
  name: "Home",
  data() {
    return {
      restaurants: [],
      keymsg: "name",
      stylemsg:"width:300px;",
      form: {
        name: "",
        region: "",
        date1: "",
        date2: "",
        msg: "",
        desc: ""
      }
    };
  },
  methods: {
    onSubmit() {
      alert(JSON.stringify(this.form));
    },
    loadAll() {
      return [
        { name: "三全鲜食（北新泾店）", address: "长宁区新渔路144号" },
        {
          name: "Hot honey 首尔炸鸡（仙霞路）",
          address: "上海市长宁区淞虹路661号"
        },
        {
          name: "新旺角茶餐厅",
          address: "上海市普陀区真北路988号创邑金沙谷6号楼113"
        },
        { name: "泷千家(天山西路店)", address: "天山西路438号" },
        {
          name: "胖仙女纸杯蛋糕（上海凌空店）",
          address: "上海市长宁区金钟路968号1幢18号楼一层商铺18-101"
        },
        { name: "贡茶", address: "上海市长宁区金钟路633号" },
        {
          name: "豪大大香鸡排超级奶爸",
          address: "上海市嘉定区曹安公路曹安路1685号"
        },
        {
          name: "茶芝兰（奶茶，手抓饼）",
          address: "上海市普陀区同普路1435号"
        },
        { name: "十二泷町", address: "上海市北翟路1444弄81号B幢-107" },
        { name: "星移浓缩咖啡", address: "上海市嘉定区新郁路817号" },
        { name: "阿姨奶茶/豪大大", address: "嘉定区曹安路1611号" },
        { name: "新麦甜四季甜品炸鸡", address: "嘉定区曹安公路2383弄55号" },
        {
          name: "Monica摩托主题咖啡店",
          address: "嘉定区江桥镇曹安公路2409号1F，2383弄62号1F"
        }
      ];
    },
    querySearch(queryString, cb) {
      var restaurants = this.restaurants;
      var results = queryString
        ? restaurants.filter(this.createFilter(queryString))
        : restaurants;
      // 调用 callback 返回建议列表的数据
      //console.log(results);
      cb(results);
    },
    createFilter(queryString) {
      return restaurant => {
        return (
          restaurant.name.toLowerCase().indexOf(queryString.toLowerCase()) != -1
        );
      };
    }
  },
  mounted() {
    this.restaurants = this.loadAll();
  },
  components: {
    ReadAutoInput
  }
};
</script>

<style lang="scss">
// .el-autocomplete{
//   width:250px;
// }
</style>
