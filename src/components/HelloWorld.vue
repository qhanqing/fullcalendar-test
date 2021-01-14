<template>
    <div>
        <div id="calendar"></div>
    </div>
</template>

<script>
    import {Calendar} from '@fullcalendar/core';//npm install --save @fullcalendar/core @fullcalendar/daygrid
    import dayGridPlugin from '@fullcalendar/daygrid';
    import interactionPlugin from '@fullcalendar/interaction'//npm install --save @fullcalendar/interaction
    import timeGridPlugin from '@fullcalendar/timegrid';//npm install --save @fullcalendar/timegrid
    import listPlugin from '@fullcalendar/list';//npm install --save @fullcalendar/list
    import esLocale from "@fullcalendar/core/locales/es"
    import frLocale from "@fullcalendar/core/locales/fr"

    export default {
        name: 'HelloWorld',

        mounted() {
            let that = this
            var calendarEl = document.getElementById('calendar');
            let calendar = new Calendar(calendarEl, {
                plugins: [dayGridPlugin, timeGridPlugin, interactionPlugin, listPlugin],
                initialView: 'dayGridMonth',
                initialDate: '2021-01-07',
                navLinks: true, //可以单击日期/星期名称来浏览视图
                locales: [esLocale, frLocale],//用于转中文
                locale: "zh",//用于转中文
                buttonText: {today: '今天', month: '月', week: '周', day: '天', list: '列表'},
                headerToolbar: {
                    left: 'prev,next today',
                    center: 'title',
                    right: 'dayGridMonth,timeGridWeek,timeGridDay,listWeek'
                },
                events: function (info, successCallback, failureCallback) {
                    that.al(info, successCallback, failureCallback)
                },
            });
            calendar.on('dateClick', function (info) {
                //点击某一个日程
                console.log('clicked on ' + info.dateStr);
            });
            calendar.render();
        },
        methods: {
            // eslint-disable-next-line no-unused-vars
            al(info, successCallback, failureCallback) {
                this.getList()
                successCallback(this.events);
            },
            //点击切换月份 从后端获取数据
            getList() {

            },
        },
        data() {
            return {
                events: [
                    {
                        title: '单独的',
                        start: '2021-01-01'
                    },
                    {
                        title: '福房网',
                        start: '2021-01-07',
                        end: '2021-01-10'
                    },
                    {
                        groupId: '999',
                        title: '还房贷',
                        start: '2021-01-09T16:00:00'
                    },
                    {
                        groupId: '999',
                        title: '噶发',
                        start: '2021-01-16T16:00:00'
                    },
                    {
                        title: '尬歌',
                        start: '2021-01-11',
                        end: '2021-01-13'
                    },
                    {
                        title: '个嘿嘿',
                        start: '2021-01-12T10:30:00',
                        end: '2021-01-12T12:30:00'
                    },
                    {
                        title: '拐个弯',
                        start: '2021-01-12T12:00:00'
                    },
                    {
                        title: '吊袜带wad',
                        start: '2021-01-12T14:30:00'
                    },
                    {
                        title: '拖后天到天虹',
                        start: '2021-01-13T07:00:00'
                    },
                    {
                        title: '精华贴的话人',
                        url: 'http://google.com/',
                        start: '2021-01-28'
                    }
                ]
            }
        }
    }
</script>

<style scoped>

</style>
