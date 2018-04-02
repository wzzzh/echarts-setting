# echarts-setting #
**vue-echarts日常配置项**
	 
	line: {
	  // 移入图表提示工具
	  tooltip: {
	    trigger: 'axis',
	    backgroundColor: 'rgba(255,255,255,0.7)',
	    padding: 0,
	    extraCssText: 'box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.3);',
		//自定义移入提示工具样式
	    formatter: function(param) {
	      return lineTip(param);
	    },
	  },

	  // 配置canvas的宽高及边距位置
	  grid: {
	    height:'317px;',
	    left: '2%',
	    right: '2%',
	    top: '2%',
	    containLabel: true
	  },
	  xAxis: [{
	    type: 'category',
	    boundaryGap: false,
		//X轴数据
	    data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日'],
	    axisLine: {
	      lineStyle: {
	        color: '#ccc'
	      }
	    },
		//x轴字体颜色
	    axisLabel: {
	      show: true,
	      textStyle: {
	        color: '#333'
	      }
	    },
	    // 标尺线的颜色，移入数据后的标尺线
	    axisPointer:{
	      lineStyle:{
	        color:'#d8dbdf'
	      },
	    }
	  }],
	
	  yAxis: [{
	    type: 'value',
	    name: '',
	    position: 'left',
		
	    axisLabel: {
	      formatter: '{value}'
	    },
	    axisTick: {
	      length: 10
	    },
		//Y轴坐标轴线性颜色
	    axisLine: {
	      lineStyle: {
	        color: 'transparent'
	      }
	    },
		//Y轴数值颜色
	    axisLabel: {
	      show: true,
	      textStyle: {
	        color: '#595959'
	      }
	    },
	    // 设置背景虚线
	    splitLine: { // 坐标轴在 grid 区域中的分隔线。
	      lineStyle: {
	        type: '',
	        color: '#eae9e9'
	      }
	    },
	  },
	  ],
	  series : [
	    {
	      // name:'邮件营销',
	      type:'line',
	      stack: '总量',
	      // 设置为曲线
	      smooth: true,

	      color:'#65a5f6',
		//区域线性颜色，渐变色
	      areaStyle:{
	        normal: {
	          color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
	            type: 'dotted',
	            offset: 0,
	            color: 'rgba(101,165,246,0.9)'
	          }, {
	            offset: 1,
	            color: 'rgba(101,165,246,0.1)'
	          }], false),
	          shadowColor: 'rgba(101,165,246,0.1)',
	          shadowBlur: 10
	        }
	      },
	      data:[120, 132, 101, 134, 90, 230, 210],
	      // 线条颜色
	      itemStyle: {
	        normal: {
	          color: 'rgb(101,165,246)',
	          borderColor: 'rgba(101,165,246,0.2)',
	        }
	      }
	    },
	  ]
	},

**vue,使用echarts用法**  

方法：（每次改变只是只需要重新调用一下方法 ）  

	drawLine(){
		//初始化配置项
		 let mychartOpt = echarts.init(document.getElementById('home-chart'));
		//缩放响应
		 window.addEventListener('resize',function(){
		   mychartOpt.resize()
		 });
		 mychartOpt.setOption(this.line);
	},

 
**自定义图表移入框样式**  

	function lineTip(ag) {
	  // console.log(ag)
	  var len = ag.length;
	  var div = '<div class="lineTip">';
	  div+='<h5>'+ ag[0]["name"]+'</h5>';
	  for( var i=0;i<len;i++){
	    div+= '<p>' + ag[i]['marker'] + ag[i]['seriesName'] + '<b style="position:absolute; right: 10px">' + ag[i]['data'] +'</b>' + '</p>';
	  }
	  div+= '</div>';
	return div;
	}
 
