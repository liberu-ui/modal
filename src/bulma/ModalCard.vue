<template>
    <teleport to="body">
        <fade @after-enter="$emit('show')"
            @after-leave="$emit('close')">
            <div class="modal is-active"
                 v-if="visible">
                <div class="modal-background"/>
                <core-modal v-model:visible="visible">
                    <template #default="{ close }">
                        <fade>
                            <div class="modal-card">
                                <header class="modal-card-head">
                                    <slot name="header"
                                        :close="close"/>
                                </header>
                                <section class="modal-card-body">
                                    <slot name="body"
                                        :close="close"/>
                                </section>
                                <footer class="modal-card-foot">
                                    <slot name="footer"
                                        :close="close"/>
                                </footer>
                            </div>
                            <button class="modal-close is-large"
                                aria-label="close"
                                @click="close"/>
                        </fade>
                    </template>
                </core-modal>
            </div>
        </fade>
    </teleport>
</template>

<script>
import { Fade } from '@liberu-ui/transitions';
import CoreModal from '../renderless/CoreModal.vue';

export default {
    name: 'ModalCard',

    components: { CoreModal, Fade },

    emits: ['close', 'show'],

    data: () => ({
        visible: true,
    }),
};
</script>
