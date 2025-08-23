# Traversing Elements

Sometimes, certain elements on the page would not have an easily identifiable selector.

In this example, let's say I want to select the 3rd button of `two-form`. 
```
<section>
    <button></button>
    <button></button>
    <form class="some-form">
        <button></button>
        <button></button>
        <button></button>
        <button></button>
    </form>
    <form class="two-form">
        <button></button>
        <button></button>
        <button></button>
        <button></button>
    </form>
</section>
```

However, none of the buttons have a unique id I can select.

We will need to select a parent first and then grab its children elements from there.

### `find()`
Searches all descendants (not just direct children).

Can go as deep as needed to find matching elements inside the DOM tree.

### `children()`
Returns only direct child elements of the selected element.

Does not search deeply into nested levels

### `eq`


What if in this example, I want to select the `section` element that has the `super-button` button?
```
<section>
</section>
<section>
</section>
<section>
    <button class="super-button"></button>
</section>
<section>
</section>
<section>
</section>
```

### `parent()`
