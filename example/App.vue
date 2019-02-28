<template>
<div>
    <h1>🍞📅 TOAST UI Calendar + Vue</h1>
    <div>
        <select v-model="selectedView">
            <option v-for="(options, index) in viewModeOptions" :value="options.value" :key="index">
                {{options.title}}
            </option>
        </select>
        <span @click="onClickNavi($event)">
            <button type="button" class="btn btn-default btn-sm move-today" data-action="move-today">Today</button>
            <button type="button" class="btn btn-default btn-sm move-day" data-action="move-prev">Prev</button>
            <button type="button" class="btn btn-default btn-sm move-day" data-action="move-next">Next</button>
        </span>
        <span class="render-range">{{dateRange}}</span>
    </div>
    <calendar style="height: 800px"
              ref="tuiCal"
              :useDetailPopup="useDetailPopup"
              :view="selectedView"
              :calendars="calendarList"
              :schedules="scheduleList"
              :theme="theme"
              :template="template"
              :taskView="true"
              :scheduleView="true"
              :month="month"
              :week="week"
              :timezones="timezones"
              :disableDblClick="disableDblClick"
              :isReadOnly="isReadOnly"
              @clickSchedule="onClickSchedule"
              @clickDayname="onClickDayname"
              @beforeDeleteSchedule="onBeforeDeleteSchedule"
              @beforeCreateSchedule="onBeforeCreateSchedule"
              @beforeUpdateSchedule="onBeforeUpdateSchedule"
              @afterRenderSchedule="onAfterRenderSchedule"
              @clickTimezonesCollapseBtn="onClickTimezonesCollapseBtn"
    />
</div>
</template>
<script>
import 'tui-time-picker/dist/tui-time-picker.css';
import 'tui-date-picker/dist/tui-date-picker.css';
import 'tui-calendar/dist/tui-calendar.css';
import './app.css';

import {Calendar} from '../src/index';
import myTheme from './myTheme';

const today = new Date();

const getDate = (type, start, value, operator) => {
    start = new Date(start);
    type = type.charAt(0).toUpperCase() + type.slice(1);

    if (operator === '+') {
        start[`set${type}`](start[`get${type}`]() + value);
    } else {
        start[`set${type}`](start[`get${type}`]() - value);
    }

    return start;
};

export default {
    name: 'App',
    components: {
        'calendar': Calendar
    },
    data() {
        return {
            viewModeOptions: [
                {
                    title: 'Monthly',
                    value: 'month'
                },
                {
                    title: 'Weekly',
                    value: 'week'
                },
                {
                    title: 'Daily',
                    value: 'day'
                }
            ],
            dateRange: '',
            selectedView: 'week',
            calendarList: [
                {
                    id: '0',
                    name: 'Private',
                    bgColor: '#9e5fff',
                    borderColor: '#9e5fff'
                },
                {
                    id: '1',
                    name: 'Company',
                    bgColor: '#00a9ff',
                    borderColor: '#00a9ff'
                }
            ],
            scheduleList: [
                {
                    id: '1',
                    calendarId: '0',
                    title: 'AMERICA NOTICIAS: PRIMERA EDICION: LOCAL (GP)',
                    category: 'allday',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 3, '+').toISOString()
                },
                {
                    id: '2',
                    calendarId: '0',
                    title: 'AMERICA NOTICIAS: PRIMERA EDICION (GP)',
                    category: 'allday',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 3, '+').toISOString()
                },
                {
                    id: '3',
                    calendarId: '0',
                    title: 'AMERICA DEPORTES (G)',
                    category: 'allday',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 3, '+').toISOString()
                },
                {
                    id: '4',
                    calendarId: '0',
                    title: 'AMERICA NOTICIAS: PRIMERA EDICION (GP)',
                    category: 'allday',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 3, '+').toISOString()
                },
                {
                    id: '5',
                    calendarId: '0',
                    title: 'TN. EL PRIVILEGIO DE AMAR (GP)',
                    category: 'allday',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 3, '+').toISOString()
                },
                {
                    id: '6',
                    calendarId: '0',
                    title: 'TN. MARIA MERCEDES (GP)',
                    category: 'allday',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 3, '+').toISOString()
                },
                {
                    id: '7',
                    calendarId: '0',
                    title: 'AMERICA NOTICIAS: EDICION DEL MEDIODIA (GP)',
                    category: 'allday',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 3, '+').toISOString()
                },
                {
                    id: '8',
                    calendarId: '0',
                    title: 'EN BOCA DE TODOS (GP)',
                    category: 'allday',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 3, '+').toISOString()
                },
                {
                    id: '9',
                    calendarId: '0',
                    title: 'AL FONDO HAY SITIO   (5° TEMPORADA) (G)',
                    category: 'allday',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 3, '+').toISOString()
                },
                {
                    id: '10',
                    calendarId: '0',
                    title: 'TN. CAER EN TENTACION (GP)',
                    category: 'allday',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 3, '+').toISOString()
                },
                {
                    id: '11',
                    calendarId: '0',
                    title: 'LA ROSA DE GUADALUPE',
                    category: 'allday',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 3, '+').toISOString()
                },
                {
                    id: '5',
                    calendarId: '1',
                    title: 'hOLAA',
                    category: 'milestone',
                    dueDateClass: '',
                    start: getDate('date', today, 1, '+').toISOString(),
                    end: getDate('date', today, 1, '+').toISOString(),
                    isReadOnly: true
                },
                {
                    id: '6',
                    calendarId: '1',
                    title: 'AMERICA ESPECTACULOS (REPETICION)',
                    category: 'time',
                    dueDateClass: '',
                    start: getDate('hours', today, 2, '-').toISOString(),
                    end: getDate('hours', today, 1, '-').toISOString(),
                    //isReadOnly: true
                },
                {
                    id: '7',
                    calendarId: '1',
                    title: 'AMERICA NOTICIAS (MATUTINO)',
                    category: 'time',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 1, '+').toISOString()
                },
                {
                    id: '8',
                    calendarId: '1',
                    title: 'AMERICA NOTICIAS: EDICION DEL SABADO (GP)',
                    category: 'time',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 1, '+').toISOString()
                },
                {
                    id: '9',
                    calendarId: '1',
                    title: 'ESTAS EN TODAS (5TA TEMPORADA)',
                    category: 'time',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 1, '+').toISOString()
                },
                {
                    id: '10',
                    calendarId: '1',
                    title: 'CINESCAPE (G)',
                    category: 'time',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 1, '+').toISOString()
                },
                {
                    id: '11',
                    calendarId: '1',
                    title: '(G) EL CHAVO DEL OCHO',
                    category: 'time',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 1, '+').toISOString()
                },
                {
                    id: '12',
                    calendarId: '1',
                    title: 'AUTOMUNDO(G)',
                    category: 'time',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 1, '+').toISOString()
                },
                {
                    id: '13',
                    calendarId: '1',
                    title: 'ESTAS EN TODAS (REPETICION)',
                    category: 'time',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 1, '+').toISOString()
                },
                {
                    id: '14',
                    calendarId: '1',
                    title: 'AMERICA NOTICIAS: EDICION DOMINICAL (GP)',
                    category: 'time',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 1, '+').toISOString()
                },
                {
                    id: '15',
                    calendarId: '1',
                    title: 'DOMINGO AL DIA (GP)',
                    category: 'time',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 1, '+').toISOString()
                },                
                {
                    id: '16',
                    calendarId: '1',
                    title: 'TEC(G)',
                    category: 'time',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 1, '+').toISOString()
                },
                {
                    id: '17',
                    calendarId: '1',
                    title: '(G) EL CHAVO DEL OCHO',
                    category: 'time',
                    dueDateClass: '',
                    start: today.toISOString(),
                    end: getDate('hours', today, 1, '+').toISOString()
                }     
            ],
            //columnas de zona horario en la vista weekly
            timezones: [{
                timezoneOffset: 540,
                displayLabel: 'GMT+09:00',
                tooltip: 'Seoul'
            }, {
                timezoneOffset: -420,
                displayLabel: 'GMT-08:00',
                tooltip: 'Los Angeles'
            }, {
                timezoneOffset: 540,
                displayLabel: 'GMT-05:00',
                tooltip: 'Lima'
            }],
            theme: myTheme,
            template: {
                milestone(schedule) {
                    return `<span style="color:#fff;background-color: ${schedule.bgColor};">${schedule.title}</span>`;
                },
                milestoneTitle() {
                    return 'Milestone';
                },
                allday(schedule) {
                    return `${schedule.title}<i class="fa fa-refresh"></i>`;
                },
                alldayTitle() {
                    return 'All Day';
                }
            },
            month: {
                startDayOfWeek: 0
            },
            week: {
                showTimezoneCollapseButton: true,
                timezonesCollapsed: true
            },
            taskView: true,
            scheduleView: true,
            useDetailPopup: true,
            disableDblClick: true,
            isReadOnly: false
        };
    },
    watch: {
        selectedView(newValue) {
            this.$refs.tuiCal.invoke('changeView', newValue, true);
            this.setRenderRangeText();
        }
    },
    methods: {//Implementar metodo para guardar los datos
        init() {
            this.setRenderRangeText();
        },
        setRenderRangeText() {
            const {invoke} = this.$refs.tuiCal;
            const view = invoke('getViewName');
            const calDate = invoke('getDate');
            const rangeStart = invoke('getDateRangeStart');
            const rangeEnd = invoke('getDateRangeEnd');
            let year = calDate.getFullYear();
            let month = calDate.getMonth() + 1;
            let date = calDate.getDate();
            let dateRangeText = '';
            let endMonth, endDate, start, end;

            switch (view) {
                case 'month':
                    dateRangeText = `${year}-${month}`;
                    break;
                case 'week':
                    year = rangeStart.getFullYear();
                    month = rangeStart.getMonth() + 1;
                    date = rangeStart.getDate();
                    endMonth = rangeEnd.getMonth() + 1;
                    endDate = rangeEnd.getDate();

                    start = `${year}-${month}-${date}`;
                    end = `${endMonth}-${endDate}`;
                    dateRangeText = `${start} ~ ${end}`;
                    break;
                default:
                    dateRangeText = `${year}-${month}-${date}`;
            }
            this.dateRange = dateRangeText;
        },
        onClickNavi(event) {
            if (event.target.tagName === 'BUTTON') {
                const {target} = event;
                let action = target.dataset ? target.dataset.action : target.getAttribute('data-action');
                action = action.replace('move-', '');

                this.$refs.tuiCal.invoke(action);
                this.setRenderRangeText();
            }
        },
        //Clic en un horario existente
        onClickSchedule(res) {
            console.group('onClickSchedule');
            console.log('MouseEvent : ', res.event);
            console.log('Calendar Info : ', res.calendar);
            console.log('Schedule Info : ', res.schedule);
            console.groupEnd();
        },
        //clic en el nombre del día en la cabecera de semana
        onClickDayname(res) {
            // view : week, day
            console.group('onClickDayname');
            console.log(res.date);
            console.groupEnd();
        },
        onBeforeDeleteSchedule(res) {
            console.group('onBeforeDeleteSchedule');
            console.log('Schedule Info : ', res.schedule);
            console.groupEnd();

            const idx = this.scheduleList.findIndex(item => item.id === res.schedule.id);
            this.scheduleList.splice(idx, 1);
        },
        onAfterRenderSchedule(res) {
            console.group('onAfterRenderSchedule');
            console.log('Schedule Info : ', res.schedule);
            console.groupEnd();
        },
        onBeforeCreateSchedule(e) {
            console.log(e);

            let category = 'time';

            if( e.isAllDay === true ) {
                category = 'allday';
            }

            //Implementacion
            this.scheduleList.push(
                {
                    id: e.id,
                    calendarId: e.calendarId,
                    title: e.title,
                    location: e.location,
                    //state: e.state, //no guarda
                    category: category, //time - allday
                    start: e.start,
                    end: e.end
                }
            );
        },
        onBeforeUpdateSchedule(event) {
            console.log(event+'update');
            let schedule = event.schedule;
            let startTime = event.start;
            let endTime = event.end;
             this.$refs.tuiCal.invoke('updateSchedule', schedule.id, schedule.calendarId, {
                start: startTime,
                end: endTime
             });
               
            // let schedule = event.schedule;
            // let startTime = event.start;
            // let endTime = event.end;

            // updateSchedule(schedule.id, schedule.calendarId, {
            //     start: startTime,
            //     end: endTime
            // });
        },
        onClickTimezonesCollapseBtn(timezonesCollapsed) {
            // view : week, day
            console.group('onClickTimezonesCollapseBtn');
            console.log('Is Collapsed Timezone? ', timezonesCollapsed);
            console.groupEnd();

            if (timezonesCollapsed) {
                this.theme['week.timegridLeft.width'] = '100px';
                this.theme['week.daygridLeft.width'] = '100px';
            } else {
                this.theme['week.timegridLeft.width'] = '50px';
                this.theme['week.daygridLeft.width'] = '50px';
            }
        }
    },
    mounted() {
        this.init();
    }
};
</script>
<style>
</style>
