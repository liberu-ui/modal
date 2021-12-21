<template>
    <teleport to="body">
        <fade @after-enter="$emit('show')"
            @after-leave="$emit('close')">
            <div class="modal is-active"
                v-bind="$attrs"
                v-if="visible">
                <div class="modal-background"/>
                <core-modal v-model:visible="visible">
                    <template #default="{ close }">
                        <div class="modal-content">
                            <slot :close="close"/>
                        </div>
                        <button class="modal-close is-large"
                            aria-label="close"
                            @click="close"/>
                    </template>
                </core-modal>
            </div>
        </fade>
    </teleport>
</template>

<script>
import { Fade } from '@enso-ui/transitions';
import CoreModal from '../renderless/CoreModal.vue';

export default {
    name: 'Modal',

    components: { CoreModal, Fade },

    emits: ['show', 'close'],

    inheritAttrs: false,

    data: () => ({
        visible: true,
    })
};
</script>
