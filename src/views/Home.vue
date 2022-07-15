<template>
    <div class="home">
        <FullCalendar :options="calendarOptions" />
    </div>
</template>

<script>
import FullCalendar from '@fullcalendar/vue';
import dayGridPlugin from '@fullcalendar/daygrid';
import interactionPlugin from '@fullcalendar/interaction';

export default {
    name: 'Home',
    components: {
        FullCalendar,
    },
    data() {
        return {
            calendarOptions: {
                plugins: [dayGridPlugin, interactionPlugin],
                initialView: 'dayGridMonth',
                events: [
                    {title: 'event 1', date: '2022-07-02'},
                    {title: 'event 2', date: '2022-07-30'},
                ],
            },
        };
    },
};
</script>

<style scoped></style>
