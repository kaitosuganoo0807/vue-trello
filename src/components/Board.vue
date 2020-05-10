<template>
  <div>
    <header>
      Vue Trello
    </header>
    <main>
      <p class="info-line">All: {{ totalCardCount }} タスク</p>
      <draggable class="list-index" :list="lists" @end="movingList">
        <list v-for="(item, index) in lists"
            :key="item.id"
            :title="item.title"
            :listIndex="index"
            :cards="item.cards"
            @change="movingCard"
        />
        <list-add />
      </draggable>
    </main>
  </div>
</template>

<script>
import draggable from 'vuedraggable'
import ListAdd from './ListAdd'
import List from './List'
import { mapState } from 'vuex'

export default {
  components: {
    ListAdd,
    List,
    draggable,
  },
  computed: {
    ...mapState([
      'lists'
    ]),
    totalCardCount() {
      return this.$store.getters.totalCardCount
    }
  },
  methods: {
    movingCard: function() {
      this.$store.dispatch('updateList', { lists: this.lists })
    },
    movingList: function() {
      this.$store.dispatch('updateList', { lists: this.lists })
    }
  }
}
</script>