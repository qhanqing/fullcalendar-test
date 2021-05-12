安装<br/>
npm install --save @fullcalendar/core @fullcalendar/daygrid <br/>
npm install --save @fullcalendar/interaction <br/>
npm install --save @fullcalendar/timegrid <br/>
npm install --save @fullcalendar/list <br/>
<br/>
官方文档
https://fullcalendar.io/docs/initialDate <br/>
插件索引
https://fullcalendar.io/docs/plugin-index

特殊插件 tooltip提示插件  <br/>
tippy.js
npm i tippy.js

###图表

![Image text](src/assets/state/index.png)

###安装使用
###### 1、安装
npm install --save @fullcalendar/core @fullcalendar/daygrid <br/>
npm install --save @fullcalendar/interaction <br/>
npm install --save @fullcalendar/timegrid <br/>
npm install --save @fullcalendar/list <br/>

###### 2、使用
在要使用的页面中加入以下依赖 <br/>


    import {Calendar} from '@fullcalendar/core';//npm install --save @fullcalendar/core @fullcalendar/daygrid
    import dayGridPlugin from '@fullcalendar/daygrid';
    import interactionPlugin from '@fullcalendar/interaction'//npm install --save @fullcalendar/interaction
    import timeGridPlugin from '@fullcalendar/timegrid';//npm install --save @fullcalendar/timegrid
    import listPlugin from '@fullcalendar/list';//npm install --save @fullcalendar/list
    import esLocale from "@fullcalendar/core/locales/es"
    import frLocale from "@fullcalendar/core/locales/fr"
    
    import tippy from 'tippy.js' //npm i tippy.js
    import 'tippy.js/dist/tippy.css'
    import '../assets/css/light.css'
    import 'tippy.js/animations/scale.css'
    
初始化加载

    mounted() {
                let that = this
                var calendarEl = document.getElementById('calendar');
                let calendar = new Calendar(calendarEl, {
                    plugins: [dayGridPlugin, timeGridPlugin, interactionPlugin, listPlugin],
                    schedulerLicenseKey: 'CC-Attribution-NonCommercial-NoDerivatives',//试用版 免费版码
                    initialView: 'dayGridMonth',
                    initialDate: '2021-01-07',
                    navLinks: true, //可以单击日期/星期名称来浏览视图
                    displayEventEnd: true,//展示结束时间
                    locales: [esLocale, frLocale],//用于转中文
                    locale: "zh",//用于转中文
                    buttonText: {today: '今天', month: '月', week: '周', day: '天', list: '列表'},
                    headerToolbar: {
                        left: 'prev,next today',
                        center: 'title',
                        right: 'dayGridMonth,timeGridWeek,timeGridDay,listWeek'
                    },
                    eventMouseEnter: function (info) {
                        let arr = that.events.filter(item => {
                            return item.id == info.event.id
                        })
    
                        let detail = arr[0]
                        //鼠标移入
                        tippy(info.el, {
                            content: '<div style=\'width: 200px;padding: 10px; \'>' +
                                '<div style=\'color: #666666\'>' +
                                '<div style="font-weight:700;border-bottom: 1px solid #CCCCCC;line-height: 36px">' + detail.title + '</div>' +
                                '<div style="line-height: 20px;display: inline-block;"><div style=\'width:100px;font-weight:700;padding-right: 5px\'>开始时间:</div><ul>' +  detail.start+ '</ul></div>' +
                                '<div style="line-height: 20px;display: inline-block;"><div style=\'width:100px;font-weight:700;padding-right: 5px\'>结束时间:</div><ul>' + detail.end + '</ul></div>' +
                                '</div>' +
                                '</div>',
                            theme: 'light',
                            interactive: true,
                            placement: 'right-end',
                            allowHTML: true
                        })
                    },
                    eventClick: function (info) {
                        //点击某一条
                        console.log("点击某一条", info)
                    },
                    //点击
                    events: function (info, successCallback, failureCallback) {
                        //点击切换月份 从后端获取数据
                        that.al(info, successCallback, failureCallback)
                    },
                });
                calendar.on('dateClick', function (info) {
                    //点击某一个日程 点击某一个日程
                    console.log('clicked on ' + info.dateStr);
                    that.clickUse(info.dateStr)
                });
                calendar.render();
            },
