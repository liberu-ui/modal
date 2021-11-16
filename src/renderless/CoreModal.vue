<script>
import Vue from 'vue';

export default {
    name: 'CoreModal',

    props: {
        portal: {
            type: String,
            default: 'modals',
        },
        transitionDuration: {
            type: Number,
            default: 0,
        },
    },

    data: () => ({
        container: null,
    }),

    created() {
        this.setUpPortal();
    },

    mounted() {
        this.show();
    },

    beforeDestroy() {
        this.deregister();

        setTimeout(() => {
            if (this.$el.parentNode && this.$el.parentNode.className === this.portal) {
                this.container.$el.removeChild(this.$el);
            }
        }, this.transitionDuration);
    },

    methods: {
        createPortal() {
            const portal = new Vue({
                render: renderEl => renderEl('div'),
            }).$mount();

            this.$root.$el.appendChild(portal.$el);

            return portal;
        },
        deregister() {
            const registered = this.registered();
            registered.pop();
            this.updateBodyAttribute(registered);
        },
        close() {
            this.$emit('close');
        },
        isLast() {
            // eslint-disable-next-line no-underscore-dangle
            return this.registered().pop() === `${this._uid}`;
        },
        register() {
            // eslint-disable-next-line no-underscore-dangle
            this.updateBodyAttribute([...this.registered(), `${this._uid}`]);
        },
        registered() {
            const registered = document.body.getAttribute('registered-modals') || '';

            return registered.split(',').filter(modal => modal);
        },
        setListeners() {
            const closeOnEsc = e => (e.key === 'Escape'
                && this.isLast() ? this.close() : null);

            document.addEventListener('keydown', closeOnEsc);

            this.$once('hook:destroyed', () => document
                .removeEventListener('keydown', closeOnEsc));
        },
        setUpPortal() {
            const portal = document.querySelector(`.${this.portal}`);

            // eslint-disable-next-line no-underscore-dangle
            this.container = portal ? portal.__vue__ : this.createPortal();

            this.container.$el.className = this.portal;
        },
        show() {
            this.register();
            this.container.$el.appendChild(this.$el);
            this.setListeners();
            this.$emit('show');
        },
        updateBodyAttribute(registered) {
            document.body.setAttribute('registered-modals', registered.join(','));
        },
    },

    render() {
        return this.$slots.default({
            close: this.close,
            visible: this.visible,
        });
    },
};
</script>
