<template>
    <div
        class="fixed pin grid gap-spacing w-screen h-screen p-spacing font-normal leading-normal text-default bg-screen"
        :class="mode"
    >
        <slot></slot>
    </div>
</template>

<script>
import echo from '../mixins/echo';
import saveState from 'vue-save-state';
import MemberService from '../services/member';

export default {
    props: ['members'],

    mixins: [echo, saveState],

    data() {
        return {
            mode: 'light-mode',
        };
    },

    methods: {
        getEventHandlers() {
            return {
                'Dashboard.UpdateAppearance': response => {
                    this.mode = response.mode;
                },
            };
        },

        getSaveStateConfig() {
            return {
                cacheKey: `dashboard`,
            };
        },
    },

    created() {
        MemberService.store(this.members);
    },
};
</script>
