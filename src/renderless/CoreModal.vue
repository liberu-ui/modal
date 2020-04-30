<script>
import Vue from 'vue';

export default {
    name: 'CoreModal',

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

    data: () => ({
        container: null,
    }),

    created() {
        this.setUp();
    },

    mounted() {
        this.display();
    },

    methods: {
        setUp() {
            const portal = document.querySelector(`.${this.portal}`);

            this.container = portal
                ? portal.__vue__
                : this.createPortal();

            this.container.$el.className = this.portal;
        },
        createPortal() {
            const portal = new Vue({
                render: renderEl => renderEl('div'),
            }).$mount();

            document.body
                .querySelector('div')
                .appendChild(portal.$el);

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
            this.register();

            document.addEventListener('keydown', this.closeOnEsc);

            this.$once('hook:destroyed', () => {
                document.removeEventListener('keydown', this.closeOnEsc);
            });
        },
        closeOnEsc(e) {
            if (this.show && e.key === 'Escape' && this.isLast()) {
                this.close();
            }
        },
        register() {
            const registered = this.registered();
            // eslint-disable-next-line no-underscore-dangle
            registered.push(this._uid);
            this.setBodyAttribute(registered);
        },
        deregister() {
            const registered = this.registered();
            registered.pop();
            this.setBodyAttribute(registered);
        },
        isLast() {
            const registered = this.registered();
            // eslint-disable-next-line no-underscore-dangle
            return registered.indexOf(`${this._uid}`) === registered.length - 1;
        },
        registered() {
            const registered = document.body.getAttribute('registered-modals') || '';

            return registered.split(',').filter(modal => modal);
        },
        setBodyAttribute(registered) {
            document.body.setAttribute('registered-modals', registered.join(','));
        },
    },

    render() {
        return this.$scopedSlots.default({
            close: this.close,
        });
    },

    beforeDestroy() {
        this.deregister();
    }
};
</script>
