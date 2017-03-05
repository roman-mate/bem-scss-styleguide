# Jalyna's SCSS & BEM Styleguide

> No matter what methodology you choose to use in your projects, you will benefit from the advantages of more structured CSS and UI. Some styles are less strict and more flexible, while others are easier to understand and adapt in a team.
> 
> -- getbem.com

## Other helpful resources

- [BEM Introduction](http://getbem.com/introduction/)
- [BEM FAQ](http://getbem.com/faq/)
- [Airbnb CSS/Sass Styleguide](https://github.com/airbnb/css)

## Table Of Contents

1. [BEM](#bem)
  - [Element Nesting](#element-nesting)
  - [Modifier Usage](#modifier-usage)
  - [Blocks in Blocks](#blocks-in-blocks)

## BEM

### Element Nesting

#### Bad

```scss
.menu {
  li {
    list-style: none;
    margin: 0;
    padding: 0;

    a {
      color: $my-blue;
      text-decoration: none;
    }
  }
}
```

```html
<ul class="menu">
  <li><a href="#">My Link</a></li>
  <li><a href="#">My Second Link</a></li>
</ul>
```

#### Good

```scss
.menu {
  &__item {
    list-style: none;
    margin: 0;
    padding: 0;
  }

  &__link {
    color: $my-blue;
    text-decoration: none;
  }
}
```

```html
<ul class="menu">
  <li class="menu__item"><a href="#" class="menu__link">My Link</a></li>
  <li class="menu__item"><a href="#" class="menu__link">My Second Link</a></li>
</ul>
```

### Modifier Usage

#### Bad

```scss
.menu {
  &__item {
    list-style: none;
    margin: 0;
    padding: 0;

    &:first-child .menu__link {
      border-left: 1px solid $my-blue;
    }
  }

  &__link {
    color: $my-blue;
    text-decoration: none;
  }

  &__active {
    color: $my-green;
  }
}
```

```html
<ul class="menu">
  <li class="menu__item">
    <a href="#" class="menu__link">My Link</a>
  </li>
  <li class="menu__item">
    <a href="#" class="menu__link menu__active">My Second Link</a>
  </li>
</ul>
```


#### Good

```scss
.menu {
  &__item {
    list-style: none;
    margin: 0;
    padding: 0;
  }

  &__link {
    color: $my-blue;
    text-decoration: none;

    &--first {
      border-left: 1px solid $my-blue;
    }

    &--active {
      color: $my-green;
    }
  }
}
```

```html
<ul class="menu">
  <li class="menu__item">
    <a href="#" class="menu__link menu__link--first">My Link</a>
  </li>
  <li class="menu__item">
    <a href="#" class="menu__link menu__link--active">My Second Link</a>
  </li>
</ul>
```


### Blocks in Blocks

#### Bad

```scss
// header.scss
.header {
  &__menu {
    // ...
  }

  .button {
    margin: 0;
  }
}

// button.scss
.button {
  background: $my-blue;
  color: $white;
  margin: 5px 0;
  padding: 10px;

  &--primary {
    background: $my-green;
  }
}
```

```html
<div class="header">
  <ul class="header__menu">...</ul>
  <a href="#" class="button button--primary">
    My awesome Button
  </a>
</div>
```


#### Good

```scss
// header.scss
.header {
  &__menu {
    // ...
  }
}

// button.scss
.button {
  background: $my-blue;
  color: $white;
  margin: 5px 0;
  padding: 10px;

  &--primary {
    background: $my-green;
  }

  &--no-margin {
    margin: 0;
  }
}
```

```html
<div class="header">
  <ul class="header__menu">...</ul>
  <a href="#" class="button button--primary button--no-margin">
    My awesome Button
  </a>
</div>
```
