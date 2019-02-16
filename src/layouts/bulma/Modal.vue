<template>
    <renderless-modal :show="show"
        :portal="portal"
        v-on="$listeners">
        <fade slot-scope="{ close }">
            <div :class="['modal animated', { 'is-active': show }]"
                v-if="show">
                <div class="modal-background"/>
                <div class="modal-content">
                    <slot/>
                </div>
                <button class="modal-close is-large"
                    aria-label="close"
                    @click="close"/>
            </div>
        </fade>
    </renderless-modal>
</template>

<script>

import { Fade } from '@enso-ui/transitions';
import RenderlessModal from '../../renderless/Modal.vue';

export default {
    name: 'Modal',

    components: { RenderlessModal, Fade },

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
