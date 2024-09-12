<script>
import { ref } from 'vue'

export default {
  name: 'App',
  setup() {
    const userItems = ref([
      {
        id: 1,
        name: "Shoes 1",
        selected:false,
        category:"massSelect"
      },
      {
        id: 2,
        name: "Shoes 2",
        selected:false,
        category:"massSelect"
      },
      {
        id: 3,
        name: "Shoes 3",
        selected:false,
        category:"massSelect"
      },
      {
        id: 4,
        name: "Shoes 4",
        selected:false,
        category:"massSelect"
      },
      {
        id: 5,
        name: "T-shirt 1",
        selected:false,
        category:"massSelect"
      },
      {
        id: 6,
        name: "T-shirt 2",
        selected:false,
        category:"massSelect"
      },
      {
        id: 7,
        name: "T-shirt 3",
        selected:false,
        category:"massSelect"
      },
      {
        id: 8,
        name: "T-shirt 4",
        selected:false,
        category:"massSelect"
      }, 
      {
        id: 11,
        name: "Jacket 1",
        selected:false,
        category:"singleSelect"
      },
      {
        id: 12,
        name: "Jacket 2",
        selected:false,
        category:"singleSelect"
      },
      {
        id: 13,
        name: "Jacket 3",
        selected:false,
        category:"singleSelect"
      },
      {
        id: 14,
        name: "Jacket 4",
        selected:false,
        category:"singleSelect"
      },
      {
        id: 15,
        name: "Hoodie 1",
        selected:false,
        category:"singleSelect"
      },
      {
        id: 16,
        name: "Hoodie 2",
        selected:false,
        category:"singleSelect"
      },
      {
        id: 17,
        name: "Hoodie 3",
        selected:false,
        category:"singleSelect"
      },
      {
        id: 18,
        name: "Hoodie 4",
        selected:false,
        category:"singleSelect"
      }
    ])
    const userCategories = ref([
      {
        id: 0,
        title: 'Items',
        selSum:0,
        max:6,
        select: "massSelect",
        el: [],
      },
      {
        id: 1,
        title: 'Items',
        selSum:0,
        max:1,
        select: "singleSelect",
        el: [],
      }
    ])

    function onSelect(item, category) {
      if (category.selSum < category.max)
      {
        category.el.push(item);
        item.selected=true;
        category.selSum+=1;
      }
    }
    function onDiSelect(item, category) {
      if (category.selSum > 0)
      {
        category.el = category.el.filter((el) => el !== item);
        item.selected=false;
        category.selSum-=1;
      }
    }

    return {
      userItems,
      userCategories,
      onSelect,
      onDiSelect
    }
  }
}
</script>

<template>
  <header>
    <div v-for="userCategory in userCategories" class="category">
      <div class="category-container">
        <div v-for="userItem in userCategory.el"
            class="draggable"
            @click="onDiSelect(userItem, userCategories[userCategory.id])">
          <h5>{{ userItem.name }}</h5>
        </div>
      </div>
      <span v-if="userCategory.id===0">
        Selected: {{ userCategory.selSum }} / 6
      </span>
    </div>
  </header>

  <main>
    <div class="element-container">
      <div v-for="userItem in userItems.filter(x => x.selected === false && x.category==='massSelect')"
            class="draggable"
            @click="onSelect(userItem, userCategories[0])">
        <h5>{{ userItem.name }}</h5>
      </div>
    </div>
    <div class="element-container">
      <div v-for="userItem in userItems.filter(x => x.selected === false && x.category==='singleSelect')"
            class="draggable"
            @click="onSelect(userItem, userCategories[1])">
        <h5>{{ userItem.name }}</h5>
      </div>
    </div>
  </main>
</template>

<style scoped>
header {
  width: 1200px;
  display: flex;
  justify-content: space-between;
}
main {
  margin-top: 10em;
  display: flex;
  justify-content: space-evenly;
}

.element-container {
  display: flex;
  width: 25em;
  padding: 1em;
  background: var(--color-heading);
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-around;
  align-content: space-around;
  border-radius: 1em;
}
.category {
  display: flex;
  min-width: 9em;
  height: 9em;
  padding: 15px;
  border-radius: 5px;
  background: #2c3e50;
  margin-bottom: 10px;
  justify-content: space-around;
  flex-direction: column;
}
.category-container {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  .draggable {
    background: var(--vt-c-text-dark-1);
    color: var(--vt-c-text-light-1);
    margin: 5px;
  }
}

.category h4 {
  color: white;
}

.draggable {
  background: var(--color-accent);
  height: 5em;
  width: 5em;
  padding: 1em;
  border-radius: 5px;
  margin-bottom: 5px;
}

.draggable h5 {
  margin: 0;
}
</style>
