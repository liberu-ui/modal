<template>
    <core-modal :show="show"
        :portal="portal"
        v-on="$listeners">
        <fade slot-scope="{ close }">
            <div :class="['modal', { 'is-active': show }]"
                v-if="show">
                <div class="modal-background"/>
                <div class="modal-card">
                    <header class="modal-card-head">
                        <slot name="header"/>
                    </header>
                    <section class="modal-card-body">
                        <slot name="body"/>
                    </section>
                    <footer class="modal-card-foot">
                        <slot name="footer"/>
                    </footer>
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
