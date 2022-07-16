<template>
    <div class="home">
        <FullCalendar :options="calendarOptions" />
    </div>
</template>

<script>
import FullCalendar from '@fullcalendar/vue';
import dayGridPlugin from '@fullcalendar/daygrid';
import interactionPlugin from '@fullcalendar/interaction';
import tippy from 'tippy.js';
import 'tippy.js/dist/tippy.css'; // optional for styling

export default {
    name: 'Home',
    components: {
        FullCalendar,
    },
    data() {
        return {
            calendarOptions: {
                plugins: [dayGridPlugin, interactionPlugin],
                eventMouseEnter: this.handleDateClick,
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
            // console.log(event.view.getCurrentData());
            console.log(event.event.title);
        },
    },
};
</script>
