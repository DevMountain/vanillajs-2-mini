<img src="https://s3.amazonaws.com/devmountain/readme-logo.png" width="250" align="right">

# Project Summary

In this project, we'll practice more vanilla JS DOM manipulation by creating a simple To Do List project. The basic HTML and CSS have been provided for you, and you will be adding in the Javascript to make the interface interactive.

## Example
![Example](https://github.com/DevMountain/vanillajs-2-mini/blob/master/img/Example.png)

### Step 1

#### Summary

In this step, we'll start creating our Javascript function for adding a todo item to our list when the `Add` button is pressed. We'll need to add the event listener, get the value from the input box, and create a new element in the list.

#### Instructions

- In `index.js`, create a new function called `addTodo` that takes in an `event` as a parameter.
- Use `document.createElement` to create a new `li` element that will hold our new todo item.
- We need to get the value of our input field to add it to our list. Use `getElementById` to get the `value` property of the input.
- Set the `innerText` property of our recently created `li` element to the `value` of the input we just found.
- Then, use `querySelector` to find the `ul` element in our page and use `appendChild` to insert the `li` element we created into the DOM.
- Finally, outside of your function, use `addEventListener` to listen for a `submit` event on the `form` element and run the `addTodo` function.
- Run the project and give it a try -- it doesn't work the way we expected. Because our `button` is inside a `form` element, it has a default action that is also running and interfering with our code. To fix this, at the beginning of the `addTodo` function, add `event.preventDefault()`

#### Solution

<details>
<summary>
<code>/index.js</code>
</summary>

```js
document.querySelector("form").addEventListener("submit", addTodo);

function addTodo(event) {
  event.preventDefault();
  const item = document.createElement("li");
  item.innerText = document.getElementById("item").value;

  const list = document.querySelector("ul");
  list.appendChild(item);
}
```

</details>

### Step 2

#### Summary

Now that we can add a todo item, we need to be able to remove them as well. In this step, we'll make some changes to our `addTodo` function so we have a way to remove todos. We'll need to add a delete button to each todo item and create an event listener for it.

#### Instructions

- In the `addTodo` function, after setting the `innerText` of the new `li` element, use `createElement` to create a new `button` element.
- Use `innerText` to put an `x` inside the button.
- Use `addEventListener` to listen for a `click` event on the button and run the `removeTodo` function. We will create that function later in this step.
- Now that the button has been created, add it to the `item` variable using `append`.
- Finally, outside of the `addTodo` function, create a new function called `removeTodo` that takes in an `event` parameter. When we click the button, we want to remove the entire list item. Since the button is a child of the list item, we can use `event.target.parentNode.remove()` to remove the entire list item.

#### Solution

<details>
<summary>
<code>/index.js</code>
</summary>

```js
document.querySelector("form").addEventListener("submit", addTodo);

function addTodo(event) {
  event.preventDefault();
  const item = document.createElement("li");
  item.innerText = document.getElementById("item").value;

  const button = document.createElement("button");
  button.innerText = "x";
  button.addEventListener("click", removeTodo);
  item.append(button);

  const list = document.querySelector("ul");
  list.appendChild(item);
}

function removeTodo(event) {
  event.target.parentNode.remove();
}
```

</details>

### Step 3

#### Summary

Now that we can add and remove items from our to do list, we can finish our app by allowing users to mark items as complete by clicking on a todo item. The CSS has already been set up to display list items differently if they have the `aria-checked` attribute set to `'true'`. We need to create a function that will toggle the `aria-checked` attribute between `'true'` and `'false'`.

#### Instructions

- In `index.js`, create a new function called `completeTodo` that takes in an `event` as a parameter.
  - Later, we will need to add this as an event handler for every list element.
- Use `event.target.getAttribute` to get the current value of the `aria-checked` attribute for the element that was clicked.
- If that value is not currently `'true'`, use `setAttribute` to change its value to `'true'`. Otherwise, use `setAttribute` to change its value to `'false'`.
- Finally, we need to add this function as an event handler for every item. In the `addTodo` function, after you create the `li` element, use `addEventListener` to listen for a `click` event and run the `completeTodo` function.

#### Solution

<details>
<summary>
<code>/index.js</code></summary>

```js
document.querySelector("form").addEventListener("submit", addTodo);

function addTodo(event) {
  event.preventDefault();
  const item = document.createElement("li");
  item.innerText = document.getElementById("item").value;
  item.addEventListener("click", completeTodo);

  const button = document.createElement("button");
  button.innerText = "x";
  button.addEventListener("click", removeTodo);
  item.append(button);

  const list = document.querySelector("ul");
  list.appendChild(item);
}

function removeTodo(event) {
  event.target.parentNode.remove();
}

function completeTodo(event) {
  const value = event.target.getAttribute("aria-checked");
  if (value !== "true") {
    event.target.setAttribute("aria-checked", "true");
  } else {
    event.target.setAttribute("aria-checked", "false");
  }
}
```

</details>

### Black Diamond

There is an `aside` element with a success message that should be displayed to users when a todo item is marked as completed. Add the Javascript needed to display that message for 2 seconds after a todo item is marked as complete. Hint: You may have to make some changes to `removeTodo` to keep the message from showing at the wrong time!

## Contributions

If you see a problem or a typo, please fork, make the necessary changes, and create a pull request so we can review your changes and merge them into the master repo and branch.

## Copyright

© DevMountain LLC, 2018. Unauthorized use and/or duplication of this material without express and written permission from DevMountain, LLC is strictly prohibited. Excerpts and links may be used, provided that full and clear credit is given to DevMountain with appropriate and specific direction to the original content.

<p align="center">
<img src="https://s3.amazonaws.com/devmountain/readme-logo.png" width="250">
</p>
