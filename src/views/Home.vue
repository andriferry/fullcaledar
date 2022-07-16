<template>
    <div class="home">
        <FullCalendar :options="calendarOptions" />
        <div id="tooltip-box" role="tooltip">
            <Tooltips :currentEvent="currentEvent" :timeline="timeline" />

            <div id="arrow" data-popper-arrow></div>
        </div>
    </div>
</template>

<script>
import FullCalendar from '@fullcalendar/vue';
import dayGridPlugin from '@fullcalendar/daygrid';
import interactionPlugin from '@fullcalendar/interaction';
import Tooltips from '../components/Tooltips.vue';
import {createPopper} from '@popperjs/core';

export default {
    name: 'Home',
    components: {
        FullCalendar,
        Tooltips,
    },
    data() {
        return {
            currentEvent: '',
            timeline: '',
            calendarOptions: {
                plugins: [dayGridPlugin, interactionPlugin],
                eventMouseEnter: info => this.renderTooltip(info),
                eventMouseLeave: info => this.closeTooltip(info),
                initialView: 'dayGridMonth',
                events: [
                    {title: 'James', date: '2022-07-02'},
                    {title: 'John', start: '2022-07-09', end: '2022-07-11'},
                    {title: 'Thomas', date: '2022-07-09'},
                    {
                        title: 'Tomy',
                        start: '2022-07-20',
                        end: '2022-07-30',
                    },
                ],
            },
        };
    },
    methods: {
        closeTooltip() {
            const tooltip = document.getElementById('tooltip-box');

            tooltip.addEventListener('mouseleave', event => {
                tooltip.removeAttribute('data-show');
            });
        },
        calculateDayRange(event) {
            const startDate = new Date(event.event._instance.range.start);
            const endDate = new Date(event.event._instance.range.end);

            const minute = 1000 * 60;
            const hour = minute * 60;
            const day = hour * 24;
            const calculateDay = endDate.getTime() - startDate.getTime();

            this.timeline = Math.round(calculateDay / day);
        },
        renderTooltip(event) {
            this.calculateDayRange(event);
            this.currentEvent = event.event.title;

            const tooltip = document.getElementById('tooltip-box');

            const popperInstance = createPopper(event.el, tooltip, {
                modifiers: [
                    {
                        name: 'offset',
                        options: {
                            offset: [-70, 8],
                        },
                    },
                ],
            });

            tooltip.setAttribute('data-show', '');
            popperInstance.update();
        },
    },
};
</script>

<style>
#tooltip-box {
    z-index: 99;
    color: white;
    background-color: white;
    font-weight: bold;
    border-radius: 4px;
    display: none;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}
#tooltip-box[data-show] {
    display: block;
}

#tooltip-box[data-popper-placement^='top'] > #arrow {
    bottom: -4px;
}

#tooltip-box[data-popper-placement^='bottom'] > #arrow {
    top: -4px;
}

#tooltip-box[data-popper-placement^='left'] > #arrow {
    right: -4px;
}

#tooltip-box[data-popper-placement^='right'] > #arrow {
    left: -4px;
}

#arrow,
#arrow::before {
    position: absolute;
    width: 8px;
    height: 8px;
    background: inherit;
}

#arrow {
    visibility: hidden;
}

#arrow::before {
    visibility: visible;
    content: '';
    transform: rotate(45deg);
}
</style>
