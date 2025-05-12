
List Rendering
We can use the v-for directive to render a list of elements based on a source array:

template
<ul>
  <li v-for="todo in todos" :key="todo.id">
    {{ todo.text }}
  </li>
</ul>
Here todo is a local variable representing the array element currently being iterated on. It's only accessible on or inside the v-for element, similar to a function scope.

Notice how we are also giving each todo object a unique id, and binding it as the special key attribute for each <li>. The key allows Vue to accurately move each <li> to match the position of its corresponding object in the array.

There are two ways to update the list:

Call mutating methods on the source array:

js
todos.value.push(newTodo)
Replace the array with a new one:

js
todos.value = todos.value.filter(/* ... */)
Here we have a simple todo list - try to implement the logic for addTodo() and removeTodo() methods to make it work!

More details on v-for: Guide - List Rendering
=======
## Computed Property

Let's keep building on top of the todo list from the last step. Here, we've already added a toggle functionality to each todo. This is done by adding a done property to each todo object, and using v-model to bind it to a checkbox:

template
<li v-for="todo in todos">
  <input type="checkbox" v-model="todo.done">
  ...
</li>
The next improvement we can add is to be able to hide already completed todos. We already have a button that toggles the hideCompleted state. But how do we render different list items based on that state?

Introducing computed(). We can create a computed ref that computes its .value based on other reactive data sources:

js
import { ref, computed } from 'vue'

const hideCompleted = ref(false)
const todos = ref([
  /* ... */
])

const filteredTodos = computed(() => {
  // return filtered todos based on
  // `todos.value` & `hideCompleted.value`
})
diff
- <li v-for="todo in todos">
+ <li v-for="todo in filteredTodos">
A computed property tracks other reactive state used in its computation as dependencies. It caches the result and automatically updates it when its dependencies change.

Now, try to add the filteredTodos computed property and implement its computation logic! If implemented correctly, checking off a todo when hiding completed items should instantly hide it as well.
>>>>>>> tutorial
