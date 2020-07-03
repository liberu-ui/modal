<template>
    <core-modal :transition-duration="transitionDuration"
        v-bind="$attrs"
        v-on="$listeners">
        <fade slot-scope="{ close }">
            <div class="modal is-active">
                <div class="modal-background"/>
                <div class="modal-content">
                    <slot/>
                </div>
                <button class="modal-close is-large"
                    aria-label="close"
                    @click="close"/>
            </div>
        </fade>
    </core-modal>
</template>

<script>
import { Fade } from '@enso-ui/transitions';
import CoreModal from '../renderless/CoreModal.vue';

export default {
    name: 'Modal',

    components: { CoreModal, Fade },

    props: {
        transitionDuration: {
            type: Number,
            default: 500,
        },
    },
};
</script>
