# Matestack's Vue.js APIs \[WIP\]

## Event Hub

Matestack offers an event hub, which can be used to communicate between components.

### Emitting events

`app/matestack/components/some_component.js`

```javascript
import Vue from "vue/dist/vue.esm";
import MatestackUiCore from "matestack-ui-core";

Vue.component('some-component', {
  mixins: [MatestackUiCore.componentMixin],
  data() {
    return {}
  },
  mounted(){
    MatestackUiCore.eventHub.$emit("some-event", { some: "optional data" })
  }
})
```

Use `MatestackUiCore.eventHub.$emit(EVENT_NAME, OPTIONAL PAYLOAD)`

### Receiving events

`app/matestack/components/some_component.js`

```javascript
import Vue from "vue/dist/vue.esm";
import MatestackUiCore from "matestack-ui-core";

Vue.component('some-component', {
  mixins: [MatestackUiCore.componentMixin],
  data() {
    return {}
  },
  methods: {
    reactToEvent(payload){
      console.log(payload)
    }
  },
  mounted(){
    MatestackUiCore.eventHub.$on("some-event", this.reactToEvent)
  },
  beforeDestroy(){
    MatestackUiCore.eventHub.$off("some-event", this.reactToEvent)
  }
})
```

Make sure to cancel the event listener within the `beforeDestroy` hook!

