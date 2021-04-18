# \#14: 💅 Adding Style

With Angular, we can give style to components in a way that will not affect the rest of the application. It's a good practice to encapsulate the component-related style this way.

We can also state general style rules to be used across the application. This is good for creating the same look-and-feel for all our components. For example, we can decide what color palette will be used as the theme of our app. Then, if we'd like to change the colors or offer different themes, we can change it in just one place, instead of in each component.

Angular gives us different style encapsulation methods, but we'll stick to the default.

The Angular CLI has generated a general stylesheet for us at ![](.gitbook/assets/css.svg)**style.css** in 📁**src** folder. Paste the following code into this file:

{% code title="style.css" %}
```css
html, body, div, span,
h1, p, ul, li {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}

body {
  line-height: 1;
  background: #f1f1f1;
  font-size: 16px;
  line-height: 22px;
  color: #404040;
  font-family: 'Lucida Grande', Verdana, sans-serif;
}

ol, ul {
  list-style: none;
}

.btn {
  background: lightseagreen;
  color: #fff;
  padding: 3px 10px;
  margin: 0 0 0 3px;
  border: none;
  border-radius: 5px;
  font-size: 12px;
  line-height: 24px;
  cursor: pointer;
  vertical-align: bottom;
}

.btn:hover {
  background: lightslategrey;
}
```
{% endcode %}

> How does the project know to look at this file? In the Angular CLI configuration file ![](.gitbook/assets/json.svg) **angular.json** under `apps[0].styles`, you can state the files for the build tool to take and add to the project. You can open the browser's dev tools and see the style inside the element:

```markup
<html>
  ...
  <head>
    ...
    <style type="text/css">
    ...Your style is here
    </style>
    ...
  </head>
  ...
</html>
```

Now let's add style specifically to the `todo-list-manager` component.

Open the file ![](.gitbook/assets/css.svg)**list-manager.component.css** and paste the following style inside:

{% code title="list-manager.component.css" %}
```css
.todo-app {
  position: relative;
  width: 400px;
  padding: 30px 30px 15px;
  background: white;
  border: 1px solid;
  border-color: #dfdcdc #d9d6d6 #ccc;
  border-radius: 2px;
  -webkit-box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  margin: 20px auto;
}

.todo-app::before, .todo-app::after {
  content: '';
  position: absolute;
  z-index: -1;
  height: 4px;
  background: white;
  border: 1px solid #ccc;
  border-radius: 2px;
}

.todo-app::after {
  bottom: -3px;
  left: 0;
  right: 0;
  -webkit-box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
}

.todo-app::before {
  bottom: -5px;
  left: 2px;
  right: 2px;
  border-color: #c4c4c4;
  -webkit-box-shadow: 0 1px 2px rgba(0, 0, 0, 0.15);
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.15);
}

.todo-app h1 {
  font-size: 52px;
  line-height: 52px;
  margin-bottom: 30px;
  font-weight: bold;
  text-align: center;
  letter-spacing: -0.8px;
}

.todo-add {
  margin-bottom: 20px;
}
```
{% endcode %}

How does this stylesheet get attached to the `todo-list-manager` component? Look at the file ![](.gitbook/assets/component.svg) **list-manager.component.ts**. One of the properties in the object passed to the `@Component` decorator is `styleUrls`. It's a list of stylesheets to be used by Angular, which encapsulates the style within the component.

Add the following style to ![](.gitbook/assets/css.svg) **input.component.css**:

{% code title="input.component.css" %}
```css
.todo-input {
  padding: 4px 10px 4px;
  font-size: 16px;
  font-family: 'Lucida Grande', Verdana, sans-serif;
  line-height: 20px;
  border: solid 1px #dddddd;
  border-radius: 5px;
  flex-grow: 1;
}

:host(:not([hidden])) {
  display: flex;
  justify-content: space-between;
  flex-grow: 1;
}
```
{% endcode %}

Add the following style to ![](.gitbook/assets/css.svg)**item.component.css**:

{% code title="item.component.css" %}
```css
.todo-item {
  padding: 10px 0;
  border-top: solid 1px #ddd;
  min-height: 30px;
  line-height: 30px;
  display: flex;
  justify-content: space-between;
}

.todo-checkbox {
  flex-shrink: 0;
  margin: auto 1ex auto 0;
}

.todo-title {
  flex-grow: 1;
  padding-left: 11px;
}

.btn-red {
  background: red;
}

.btn-red:hover {
  background: darkred;
}
```
{% endcode %}

Now you'll want to update your component templates to use all the CSS classes you just created.

In `ListManagerComponent`:

{% code title="list-manager.component.ts" %}
```typescript
<div class="todo-app">
  <h1>
    {{ title }}
  </h1>

  <todo-input (submit)="addItem($event)"></todo-input>

  <ul>
    <li *ngFor="let item of todoList">
      <todo-item [todoItem]="item"></todo-item>
    </li>
  </ul>
</div>
```
{% endcode %}

In `InputComponent`:

{% code title="input.component.ts" %}
```typescript
<input class="todo-input"
      [value]="title"
      (keyup.enter)="changeTitle($event.target.value)"
      #inputElement>
<button class="btn" (click)="changeTitle(inputElement.value)">
  Save
</button>
```
{% endcode %}

In `ItemComponent`:

{% code title="item.component.ts" %}
```typescript
<div class="todo-item">
  {{ todoItem.title }}
</div>
```
{% endcode %}

You can change the style as you wish - the size of elements, the colors - however you'd like!

{% hint style="info" %}
Note: You can use SCSS files in the project, which is a nicer way to write style. It has great features that help the developer. SCSS files are compiled to CSS when the project is built.
{% endhint %}



{% hint style="success" %}
[See the results on StackBlitz](https://stackblitz.com/github/angularbootcamp/todo-list-tutorial-steps/tree/step-13_Adding_Style)
{% endhint %}



