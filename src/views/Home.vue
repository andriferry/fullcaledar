<template>
    <div class="home">
        <FullCalendar :options="calendarOptions" />
        <div id="tooltipTrial" role="tooltip">
            <div id="tooltip" class="tooltip">
                <div class="title">
                    <p class="title-event">Casual leave</p>
                    <p class="day">1 DAY</p>
                    <p class="status">personal</p>
                </div>
                <div class="user-container">
                    <div class="user">
                        <div class="avatar-container">
                            <div class="avatar">
                                <p class="" style="margin: 0px; padding: 10px">
                                    JH
                                </p>
                            </div>
                        </div>

                        <div class="user-info">
                            <p class="user-name" style="margin: 0px">
                                Janitha Harischandra
                            </p>
                            <p class="user-task" style="margin: 0px">
                                ArcticHare
                            </p>
                        </div>
                    </div>
                </div>

                <button role="button">View Details ></button>
                <button role="button" class="cancel">Cancel</button>
            </div>
            <div id="arrow" data-popper-arrow></div>
        </div>
    </div>
</template>

<script>
import FullCalendar from '@fullcalendar/vue';
import dayGridPlugin from '@fullcalendar/daygrid';
import interactionPlugin from '@fullcalendar/interaction';
import tippy from 'tippy.js/headless';
import 'tippy.js/dist/tippy.css'; // optional for styling
import 'tippy.js/animations/scale.css';
import Tooltips from '../components/Tooltips.vue';
import 'tippy.js/themes/light.css';
import {createPopper} from '@popperjs/core';

export default {
    name: 'Home',
    components: {
        FullCalendar,
    },
    data() {
        return {
            calendarOptions: {
                plugins: [dayGridPlugin, interactionPlugin],

                eventMouseEnter: info => this.renderTooltip(info),
                eventMouseLeave: info => this.closeTooltip(info),
                initialView: 'dayGridMonth',
                events: [
                    {title: 'new event 1', date: '2022-07-02'},
                    {title: 'event 2', date: '2022-07-09'},
                ],
            },
        };
    },
    methods: {
        closeTooltip(event) {
            const tooltip = document.getElementById('tooltipTrial');
            tooltip.removeAttribute('data-show');
        },
        renderTooltip(event) {
            const tooltip = document.getElementById('tooltipTrial');

            const popperInstance = createPopper(event.el, tooltip, {
                modifiers: [
                    {
                        name: 'offset',
                        options: {
                            offset: [0, 8],
                        },
                    },
                ],
            });

            function show() {
                tooltip.setAttribute('data-show', '');

                // We need to tell Popper to update the tooltip position
                // after we show the tooltip, otherwise it will be incorrect
                popperInstance.update();
            }

            show();

            // tippy(el, {
            //     content: 'template.innerHTML',
            //     render(instance) {
            //         const popper = document.createElement('div');
            //         const box = document.createElement('div');

            //         popper.appendChild(box);

            //         box.appendChild(tooltip);
            //         // function onUpdate(prevProps, nextProps) {
            //         //     if (prevProps.content !== nextProps.content) {
            //         //         box.textContent = nextProps.content;
            //         //     }
            //         // }

            //         return {
            //             popper,
            //             // onUpdate, // optional
            //         };
            //     },
            //     animation: 'fade',
            //     allowHTML: true,
            //     theme: 'light',
            // });
            // console.log(event);
            // // console.log(event.view.getCurrentData());
            // console.log(event.event.title);
        },
    },
};
</script>

<style>
.tooltip {
    width: 300px;
    font-family: 'Inter', sans-serif;
    background-color: white;
    box-shadow: 10px;
    margin: 20px;
    color: white;
    min-height: 100px;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.tooltip .title {
    padding: 20px;
}

.tooltip .title .title-event {
    color: teal;
    text-align: start;
    text-transform: uppercase;
    font-weight: 900;
    margin: 0px;
}
.tooltip .title .day {
    color: rgb(52, 49, 49);
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

.tooltip .user-container {
    background: whitesmoke;
}

.user-container .user {
    display: flex;
    color: rgb(52, 49, 49);
    gap: 1rem;
    margin: 0px 20px;
    height: 60px;
}
.user .avatar-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-content: center;
}

.user-container .user .avatar-container .avatar {
    width: 50px;
    height: 50px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-content: center;
    background: teal;
    border-radius: 50%;
    color: white;
    font-size: 20px;
    font-weight: 700;
}

.user .user-info {
    display: flex;
    flex-direction: column;
    align-content: center;
    justify-content: center;
}

.user .user-info p {
    text-align: start;
}

.user .user-info .user-name {
    color: rgb(52, 49, 49);
    font-weight: 600;
}
.user .user-task {
    color: grey;
    font-weight: 500;
}
.tooltip button {
    width: 100%;
    height: 50px;
    background-color: #38bdf8;
    border: 0px;
    text-transform: uppercase;
    font-weight: 900;
    color: white;
    cursor: pointer;
}

button.cancel {
    background-color: white;
    color: red;
    text-transform: none;
    font-weight: 700;
    font-size: 15px;
}
#tooltipTrial {
    z-index: 99;
    color: white;
    font-weight: bold;

    border-radius: 4px;
    display: none;
}
#tooltipTrial[data-show] {
    display: block;
}

#tooltipTrial[data-popper-placement^='top'] > #arrow {
    bottom: -4px;
}

#tooltipTrial[data-popper-placement^='bottom'] > #arrow {
    top: -4px;
}

#tooltipTrial[data-popper-placement^='left'] > #arrow {
    right: -4px;
}

#tooltipTrial[data-popper-placement^='right'] > #arrow {
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
