# custom-time-selector

基于vue-awesome-swiper的时间或者自定义选择器

# parameter

show: Boolean;//控制内部元素显示隐藏

optionArray: Array;//选项数组,需要进行选择的选项

    (example: options2:[
              {
    
                range: [1, 12],//数字范围，内部自己会补全中间数字
                unit: '', //单位，控制需要显示的单位           
                name: 'month'//该选项的名称，用于取值，唯一值
              },
              //自定义选项
              {
                range: ['汉族','壮族','满族','回族','苗族','维吾尔族','土家族','彝族','蒙古族','藏族','布依族','侗族','瑶族','朝鲜族','白族','哈尼族','哈萨克族','黎族','傣族','畲族','傈僳族','仡佬族','东乡族','高山族','拉祜族','水族','佤族','纳西族','羌族','土族','仫佬族','锡伯族','柯尔克孜族','达斡尔族','景颇族','毛南族','撒拉族','布朗族','塔吉克族','阿昌族','普米族','鄂温克族','怒族','京族','基诺族','德昂族','保安族','俄罗斯族','裕固族','乌孜别克族','门巴族','鄂伦春族','独龙族','塔塔尔族','赫哲族','珞巴族'],
                unit: '',
                name: 'nation'
              },
    ])
    时间选择器输入值参照：
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
          ]
    
initial: Array;//单向显示数组,选择器打开时默认选择的值；注意需与选项数组(optionArray)的选项位置一致

    (example: options2:[
              {
    
                range: [1, 12],//数字范围，内部自己会补全中间数字
                unit: '', //单位，控制需要显示的单位           
                name: 'month'//该选项的名称，用于取值，唯一值
              },
              {
                range: [1, 31],
                unit: '',
                name: 'date'
              },]//选项数组
              initial:[month,date] 
    
    )
# callback

cancel: function;//关闭选择器函数

getInfo: function;//获取选择的值的函数

# demo

https://qsued-teams.github.io/custom-time-selector/dist/index.html#/index
