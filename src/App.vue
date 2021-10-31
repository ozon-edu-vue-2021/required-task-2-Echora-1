<script>
import DirList from '../public/static/node_modules.json'
import ItemDirectory from "./components/ItemDirectory";
import ItemLeave from "./components/ItemLeave";

export default {
  name: 'App',
  methods: {
    leaveHandler (value) {
      this.selectedLeave = value
    }
  },
  data() {
    return {
      selectedLeave: ''
    }
  },
  render(h) {
    const renderDirList = (item) => {
      const isItemDir = item.type === 'directory';

      if (isItemDir) {
        return h(ItemDirectory,  [
          h('span', {slot: 'directory-name'}, [item.name]),
          h('div', {slot: 'directory-content'}, item.contents.map(renderDirList)),
        ])
      } else {
        return h(
            ItemLeave,
            {
              props: {type: item.type, name: `${item.name}`, selectedLeave: this.selectedLeave },
              on: {onSelectedLeave: value => this.leaveHandler(value)}
            },
            [
              h(
                  'span',
                  {slot: 'default'},
                  [item.name]
              )
            ]
        )
      }
    }

    return renderDirList(DirList)
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
