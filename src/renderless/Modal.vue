<script>
import Vue from 'vue';

export default {
    props: {
        show: {
            type: Boolean,
            required: true,
        },
        portal: {
            type: String,
            required: true,
        },
    },

    data: () => ({
        container: null,
    }),

    computed: {
        portalSelector() {
            return `.${this.portal}`;
        },
    },

    created() {
        this.setUp();
    },

    mounted() {
        this.display();
    },

    methods: {
        setUp() {
            const portal = document.querySelector(this.portalSelector);

            this.container = portal
                ? portal.__vue__
                : this.createPortal();

            this.container.$el.className = this.portal;
        },
        createPortal() {
            const portal = new Vue({
                render: renderElement => renderElement('div'),
            }).$mount();

            document.body.appendChild(portal.$el);

            return portal;
        },
        display() {
            this.container.$el.appendChild(this.$el);
            this.setListeners();
        },
        close() {
            this.$emit('close');
        },
        setListeners() {
            const closeOnEsc = (e) => {
                if (this.show && e.key === 'Escape') {
                    this.close();
                }
            };

            document.addEventListener('keydown', closeOnEsc);

            this.$once('hook:destroyed', () => {
                document.removeEventListener('keydown', closeOnEsc);
            });
        },
    },

    render() {
        return this.$scopedSlots.default({
            close: this.close,
        });
    },
};
</script>
