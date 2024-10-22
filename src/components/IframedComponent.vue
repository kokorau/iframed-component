<script lang="ts">
import {defineComponent, h, createApp } from 'vue';

export default defineComponent({
  name: 'RenderDivWithIframe',
  setup(_, { slots }) {
    // iframeのsrcdocにレンダリングするために内部でVueを立ち上げてマウントし、HTMLを取得
    const mountedApp = createApp({
      render: () => h('div', { class: 'my-div' }, slots.default?.())
    }).mount(document.createElement('div'))
    const srcdoc =  mountedApp.$el.outerHTML

    return () => [
      h('div', { class: 'my-div' }, [
        h('iframe', {
          id: 'my-iframe',
          srcdoc,
          style: 'width: 100%; height: 300px; border: 1px solid black;'
        })
      ])
    ];
  },
});
</script>
