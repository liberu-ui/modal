<template>
    <fade>
        <div class="modal is-active">
            <div class="modal-background"/>
            <div class="modal-content">
                <slot/>
            </div>
            <core-modal v-bind="$attrs"
                :transition-duration="transitionDuration">
                <template #default="{ close }">
                    <button class="modal-close is-large"
                        aria-label="close"
                        @click="close"/>
                </template>
            </core-modal>
        </div>
    </fade>
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
