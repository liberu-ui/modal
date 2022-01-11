<script>
export default {
    name: 'CoreModal',

    props: {
        visible: {
            type: Boolean,
            required: true,
        },
    },

    emits: ['update:visible'],

    mounted() {
        document.addEventListener('keydown', this.closeOnEsc);
    },

    beforeUnmount() {
        document.removeEventListener('keydown', this.closeOnEsc);
    },

    methods: {
        closeOnEsc({ key }) {
            if (key === 'Escape') {
                this.close();
            }
        },
        close() {
            this.$emit('update:visible', false);
        },
    },

    render() {
        return this.$slots.default({
            close: this.close,
        });
    },
};
</script>
