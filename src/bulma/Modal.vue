<template>
    <core-modal v-bind="$attrs"
        :transition-duration="transitionDuration">
        <template #default="{ close }">
            <fade>
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
        </template>
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
