<template>
    <fade :show="show"
        :portal="portal"
        v-on="$listeners">
        <div slot-scope="{ hide }"
            :class="['modal animated', { 'is-active': show }]"
            v-if="show">
            <div class="modal-background"/>
            <div class="modal-content">
                <slot/>
            </div>
            <button class="modal-close is-large"
                aria-label="close"
                @click="hide"/>
        </div>
    </fade>
</template>

<script>

import Fade from '../../transitions/Fade.vue';

export default {
    name: 'Modal',

    components: { Fade },

    props: {
        show: {
            type: Boolean,
            required: true,
        },
        portal: {
            type: String,
            default: 'modals',
        },
    },
};

</script>
