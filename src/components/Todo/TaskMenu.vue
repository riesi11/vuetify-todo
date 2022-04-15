<template>
  <div>
    <v-menu
        bottom
        left
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn
            color="primary"
            icon
            v-bind="attrs"
            v-on="on"
        >
          <v-icon>mdi-dots-vertical</v-icon>
        </v-btn>
      </template>

      <v-list>
        <v-list-item
            v-for="(item, i) in items"
            :key="i"
            @click="handleClick(i)"
        >
          <v-list-item-icon>
            <v-icon v-text="item.icon"></v-icon>
          </v-list-item-icon>
          <v-list-item-title>{{ item.title }}</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>
    <dialog-edit
        v-if="dialogs.edit"
        @close="dialogs.edit = false"
        :task="task"
    >
    </dialog-edit>
    <dialog-due-date
        v-if="dialogs.dueDate"
        @close="dialogs.dueDate = false"
        :task="task"
    >
    </dialog-due-date>
    <dialog-delete
        v-if="dialogs.delete"
        @close="dialogs.delete = false"
        :task="task"
    >
    </dialog-delete>
  </div>

</template>

<script>
import DialogDelete from "@/components/Todo/Dialogs/DialogDelete";
import DialogEdit from "@/components/Todo/Dialogs/DialogEdit";
import DialogDueDate from "@/components/Todo/Dialogs/DialogDueDate";

export default {
  props: ['task'],
  data: () => ({
    dialogs: {
      delete: false,
      edit: false,
      dueDate: false
    },
    items: [
      { title: 'Edit',
      icon: 'mdi-pencil',
      click() {
        this.dialogs.edit = true
      }
      },
      { title: 'Due Date',
        icon: 'mdi-calendar',
        click() {
          this.dialogs.dueDate=true
        }
      },
      { title: 'Delete',
        icon: 'mdi-delete',
        click() {
          this.dialogs.delete = true
        }
      },
      { title: 'Sort',
        icon: 'mdi-drag-horizontal-variant',
        click() {
          if (!this.$store.state.search) {
            this.$store.commit('toggleSorting')
          }
          else {
            this.$store.commit('showSnackbar', 'How dare you search while sorting!')
          }
        }
      },
    ],
  }),
  methods: {
    handleClick(i){
      this.items[i].click.call(this)
    }
  },
  components: {
    'dialog-delete': DialogDelete,
    'dialog-edit': DialogEdit,
    'dialog-due-date': DialogDueDate,
  }
}
</script>

<style >

</style>