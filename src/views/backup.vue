<template>
    <div class="home">
        <FullCalendar :options="calendarOptions" />

        <div id="template" style="">
            <div ref="tooltip" class="tooltip">
                <div class="title">
                    <p class="title-event">Casual leave</p>
                    <p class="day">1 DAY</p>
                    <p class="status">personal</p>
                </div>
                <div class="user-container">
                    <div class="user">
                        <div class="avatar-container">
                            <div class="avatar">
                                <p class="" style="margin: 0px">JH</p>
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

                // eventDidMount(info) {
                //     // const template = document.getElementById('template');
                //     // tippy(info.el, {
                //     //     content: template.innerHTML,
                //     //     animation: 'fade',
                //     //     allowHTML: true,
                //     //     theme: 'light',
                //     // });
                //     tippy(info.el, {
                //         content: 'template.innerHTML',
                //         render(instance) {
                //             // The recommended structure is to use the popper as an outer wrapper
                //             // element, with an inner `box` element
                //             const popper = document.createElement('div');
                //             const box = document.getElementById('template');

                //             popper.appendChild(box);

                //             function onUpdate(prevProps, nextProps) {
                //                 // DOM diffing
                //                 if (prevProps.content !== nextProps.content) {
                //                     box.textContent = nextProps.content;
                //                 }
                //             }

                //             // Return an object with two properties:
                //             // - `popper` (the root popper element)
                //             // - `onUpdate` callback whenever .setProps() or .setContent() is called
                //             return {
                //                 popper,
                //                 onUpdate, // optional
                //             };
                //         },
                //         animation: 'fade',
                //         allowHTML: true,
                //         theme: 'light',
                //     });
                // },
                initialView: 'dayGridMonth',
                events: [
                    {title: 'new event 1', date: '2022-07-02'},

                    {title: 'event 2', date: '2022-07-09'},
                ],
            },
        };
    },
    methods: {
        handleDateClick: function (arg) {
            alert('date click! ' + arg.dateStr);
        },
        // handleDateClick(event) {
        //     console.log(event);
        //     // tippy(event.el, {
        //     //     content: 'template.innerHTML',
        //     //     render(instance) {
        //     //         // The recommended structure is to use the popper as an outer wrapper
        //     //         // element, with an inner `box` element
        //     //         const popper = document.createElement('div');
        //     //         const box = document.getElementById('template');

        //     //         popper.appendChild(box);

        //     //         function onUpdate(prevProps, nextProps) {
        //     //             // DOM diffing
        //     //             if (prevProps.content !== nextProps.content) {
        //     //                 box.textContent = nextProps.content;
        //     //             }
        //     //         }

        //     //         // Return an object with two properties:
        //     //         // - `popper` (the root popper element)
        //     //         // - `onUpdate` callback whenever .setProps() or .setContent() is called
        //     //         return {
        //     //             popper,
        //     //             onUpdate, // optional
        //     //         };
        //     //     },
        //     //     animation: 'fade',
        //     //     allowHTML: true,
        //     //     theme: 'light',
        //     // });
        //     // // console.log(event);
        //     // // // console.log(event.view.getCurrentData());
        //     // // console.log(event.event.title);
        // },
    },
};
</script>

<style>
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
</style>
