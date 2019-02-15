<template>
    <renderless-modal :show="show"
        v-bind="$attrs"
        v-on="$listeners">
        <transition slot-scope="{ hide }"
            appear
            enter-active-class="fadeIn"
            leave-active-class="fadeOut"
            @after-leave="$emit('after-leave')">
            <slot :hide="hide"
                v-if="show"/>
        </transition>
    </renderless-modal>
</template>

<script>

import RenderlessModal from '../renderless/Modal.vue';

export default {
    components: { RenderlessModal },

    props: {
        show: {
            type: Boolean,
            required: true,
        },
    },
};

</script>
