<template>
    <div class="home">
        <FullCalendar :options="calendarOptions" />

        <div class="tooltip" style="">
            <div class="title">
                <p class="title-event">Casual leave</p>
                <p class="day">1 DAY</p>
                <p class="status">personal</p>
            </div>
            <div class="user">
                <p class="title-event">Casual leave</p>
                <p class="day">1 DAY</p>
                <p class="status">personal</p>
            </div>
        </div>
    </div>
</template>

<script>
import FullCalendar from '@fullcalendar/vue';
import dayGridPlugin from '@fullcalendar/daygrid';
import interactionPlugin from '@fullcalendar/interaction';
import tippy from 'tippy.js';
import 'tippy.js/dist/tippy.css'; // optional for styling
import 'tippy.js/animations/scale.css';

export default {
    name: 'Home',
    components: {
        FullCalendar,
    },
    data() {
        return {
            calendarOptions: {
                plugins: [dayGridPlugin, interactionPlugin],

                eventDidMount(info) {
                    tippy(info.el, {
                        content: info.event.title,
                        animation: 'fade',
                    });
                },
                initialView: 'dayGridMonth',
                events: [
                    {title: 'new event 1', date: '2022-07-02'},

                    {title: 'event 2', date: '2022-07-09'},
                ],
            },
        };
    },
    methods: {
        handleDateClick(event) {
            console.log(event);
            // console.log(event.view.getCurrentData());
            console.log(event.event.title);
        },
    },
};
</script>

<style scoped>
.tooltip {
    width: 300px;
    background-color: white;
    box-shadow: 10px;
    margin: 20px;
    color: white;
    min-height: 100px;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.tooltip .title {
    padding: 20px;
    /* display: flex;

    justify-content: start; */
}

.tooltip .title .title-event {
    color: teal;
    text-align: start;
    text-transform: uppercase;
    font-weight: 900;
    margin: 0px;
}
.tooltip .title .day {
    color: black;
    text-align: start;
    text-transform: uppercase;
    font-weight: 500;
    font-size: 20px;
    margin: 3px 0px;
}

.tooltip .title .status {
    color: gray;
    text-align: start;
    font-weight: 700;
    font-size: 13px;
    margin: 0px;
}
</style>
