<template>
  <section>
    <label class="sr-only">Add todo</label>
    <input
      @keyup.enter="add"
      type="text"
      placeholder="Add a todo here ..."
      v-model.trim="value"
      required
    />
    <div class="truncate">Add your todo task above, hit Enter to submit.</div>
    <ul class="collection" v-for="todo in todos">
      <li
        class="collection-item"
        :key="todo"
        :value="todo.id"
        :style="[
          todo.completed
            ? 'textDecoration: line-through;'
            : 'textDecoration: none',
        ]"
      >
        {{ todo.text }}
        <button
          class="todo"
          type="button"
          @click="(event) => handleUpdateTodo(todo.id, event)"
        >
          <span v-if="todo.completed"><i class="fa fa-undo" /></span>
          <span v-else><i class="fa fa-check-circle" /></span>
        </button>
        <button
          class="todo"
          type="button"
          @click="(event) => handleDeleteTodo(todo.id, event)"
        >
          <span><i class="fa fa-times-circle"></i></span>
        </button>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  name: "TodoLayout",
  data() {
    return {
      todos: [
        { id: 0, text: "Fork repository", completed: false },
        {
          id: 1,
          text: "Open build and deploy settings and connect",
          completed: false,
        },
        { id: 2, text: "Push a new commit", completed: false },
      ],
      value: "",
    };
  },
  methods: {
    add() {
      console.log(this.todos.length);
      this.todos.push({
        id: this.todos.length,
        text: this.value,
        completed: false,
      });
      this.value = "";
    },
    handleUpdateTodo(index) {
      const newTodos = [...this.todos];
      newTodos[index].completed = !newTodos[index].completed;
      this.todos = newTodos;
    },
    handleDeleteTodo(ti) {
      console.log("delete todo with id: ", ti);
      this.todos.splice(ti, 1);
      this.todos = this.todos.filter(({ id }) => id !== ti);
    },
  },
};
</script>

<!--import React, { useState } from 'react';-->
<!--import Instructions from './Instructions/Instructions';-->
<!--import TodoInput from './TodoInput/TodoInput';-->
<!--import TodoList from './TodoList/TodoList';-->
<!--import Head from 'next/head';-->

<!--type FormElem = React.FormEvent<HTMLFormElement>-->

<!--interface ITodo {-->
<!--  text: string,-->
<!--  complete: boolean,-->
<!--}-->

<!--const TodoLayout = ({ initTodos }: { initTodos: ITodo[] }) => {-->
<!--    const [value, setValue] = useState<string>('');-->
<!--    const [todos, setTodos] =  useState<ITodo[]>(initTodos);-->

<!--    const addTodo = (text:string): void => {-->
<!--      const newTodos: ITodo[] = [...todos, {text, complete: false}];-->
<!--      setTodos(newTodos);-->
<!--    };-->

<!--    const handleSubmit = (e: FormElem): void => {-->
<!--      e.preventDefault();-->
<!--      addTodo(value);-->
<!--      setValue('')-->
<!--    };-->

<!--    const completeTodo = (index: number): void => {-->
<!--      const newTodos: ITodo[] = [ ...todos];-->
<!--      newTodos[index].complete = !newTodos[index].complete;-->
<!--      setTodos(newTodos)-->
<!--    };-->

<!--    const deleteTodo = (index: number) => {-->
<!--      const newTodos: ITodo[] = [ ...todos];-->
<!--      newTodos.splice(index, 1);-->
<!--      setTodos(newTodos);-->
<!--    };-->

<!--    return (-->
<!--      <section>-->
<!--        <TodoInput handleSubmit={handleSubmit} value={value} setValue={setValue} />-->
<!--          <Instructions />-->
<!--          <TodoList todos={todos} handleComplete={completeTodo} handleDelete={deleteTodo} />-->
<!--      </section>-->
<!--    );-->
<!--}-->

<!--export default TodoLayout;-->
