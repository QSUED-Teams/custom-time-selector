<template>
  <div class="g-index-wrap scrolls">
    <div class="g-form-label-box" style="flex-wrap: nowrap">
      <div class="g-label">会议时间：</div>
      <input :value="meetingStartTime?new Date(meetingStartTime).format('yyyy-MM-dd hh:mm:ss'):''" @click="slideShow=true" readonly style="width: calc((100% - 1.7rem - .5rem) / 3 * 2)" type="text" placeholder="选择开始时间">
    </div>
    <div class="g-form-label-box" style="flex-wrap: nowrap">
      <div class="g-label">民族：</div>
      <input :value="nation" @click="slideShow2=true" readonly style="width: calc((100% - 1.7rem - .5rem) / 3 * 2)" type="text" placeholder="选择民族">
    </div>
    <!--时间选择列表-->
    <v-slideSelect v-if="slideShow" :show="slideShow" :optionArray="options2" :initial="[new Date(meetingStartTime).getFullYear(),new Date(meetingStartTime).getMonth(meetingStartTime) + 1,new Date(meetingStartTime).getDate(), new Date(meetingStartTime).getHours() < 12?'上午':'下午', new Date(meetingStartTime).getHours(),new Date(meetingStartTime).getMinutes()]" @cancel="cancel" @getInfo="getInfo($event,1)"></v-slideSelect>

    <!--民族选择列表-->
    <v-slideSelect v-if="slideShow2" :show="slideShow2" :initial="[nation]" :optionArray="options1" @cancel="cancel" @getInfo="getInfo($event,2)"></v-slideSelect>
  </div>
</template>

<script>
import {mapState , mapMutations, mapActions} from 'vuex'

export default {
  name: 'App',
  data() {
    return {
      slideShow: false,
      slideShow2: false,
      meetingStartTime: new Date(),
      nation: '',
      options2: [
        {
          range: [Number(new Date().format('yyyy')), Number(new Date().format('yyyy')) + 1],
          unit: '',
          name: 'year'
        },
        {
          range: [1, 12],
          unit: '',
          name: 'month'
        },
        {
          range: [1, 31],
          unit: '',
          name: 'date'
        },
        {
          range: ['上午', '下午'],
          unit: '',
          name: 'halfDay'
        },
        {
          range: [0, 23],
          unit: '',
          name: 'hour'
        },
        {
          range: [0, 59],
          unit: '',
          name: 'minute'
        },
      ],//时间列表
      options1: [
        {
          range: ['汉族','壮族','满族','回族','苗族','维吾尔族','土家族','彝族','蒙古族','藏族','布依族','侗族','瑶族','朝鲜族','白族','哈尼族','哈萨克族','黎族','傣族','畲族','傈僳族','仡佬族','东乡族','高山族','拉祜族','水族','佤族','纳西族','羌族','土族','仫佬族','锡伯族','柯尔克孜族','达斡尔族','景颇族','毛南族','撒拉族','布朗族','塔吉克族','阿昌族','普米族','鄂温克族','怒族','京族','基诺族','德昂族','保安族','俄罗斯族','裕固族','乌孜别克族','门巴族','鄂伦春族','独龙族','塔塔尔族','赫哲族','珞巴族'],
          unit: '',
          name: 'nation'
        },
      ],//名族列表
    }
  },
  computed: {},
  mounted() {
    this.overscroll(document.querySelectorAll('.scrolls'));
  },
  components: {
  },
  methods: {
    //所有列表隐藏
    cancel () {
      this.slideShow = false;
      this.slideShow2 = false;
    },
    getInfo (val, type) {
      if (type === 1) {
        let time = `${val.year}/${val.month}/${val.date} ${val.hour}:${val.minute}:00`;
        this.meetingStartTime = new Date(time);
      } else {
        this.nation = val.nation;
      }
      this.cancel();
    },
    overscroll (els) {
      for (var i = 0; i < els.length; ++i) {
        var el = els[i];
        el.addEventListener('touchstart', function () {
          var top = this.scrollTop
            , totalScroll = this.scrollHeight
            , currentScroll = top + this.offsetHeight;
          if (top === 0) {
            this.scrollTop = 1;
          } else if (currentScroll === totalScroll) {
            this.scrollTop = top - 1;
          }
        });
        el.addEventListener('touchmove', function (evt) {
          if (this.offsetHeight < this.scrollHeight)
            evt._isScroller = true;
        });
      }
    }
  }
}
</script>

<style scoped lang="scss">
  @import '../assets/css/mixin';

  .g-index-wrap {
    -webkit-touch-callout: none; /* iOS Safari */

    -webkit-user-select: none; /* Chrome/Safari/Opera */

    -khtml-user-select: none; /* Konqueror */

    -moz-user-select: none; /* Firefox */

    -ms-user-select: none; /* Internet Explorer/Edge */

    user-select: none;
  }
  .g-form-label-box{
    display: flex;
    align-items: center;
    width: 50%;
    margin: 32px auto;
    flex-wrap: wrap;
    .g-label{
      width: 200px;
      line-height: 40px;
      @include sc(28px,#686868);
      text-align: right;
      margin-right: 10px;
      font-weight: 700;
    }
    input{
      flex-grow: 1;
      line-height: 56px;
      border: 2px solid #bbb;
      padding: 0 20px;
      @include sc(28px,#686868);
      border-radius: 4px;
      &::placeholder{
        @include sc(28px,#BBBBBB);
      }
    }
  }
</style>
