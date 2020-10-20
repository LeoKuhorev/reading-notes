## SASS

SASS (Syntactically Awesome StyleSheets)

Can use 2 file extensions:

- `.scss` (like regular .css but with extra features)
- `.sass` (uses indentation instead of curly braces)

### Variables

Prefixed with `$`

    $my-font: Helvetica, sans-serif

    body {
        font: $my-font
    }

### Nesting

    nav {
        ul {
            <...>
        }

        li {
            <...>
        }
    }

### Modules

If name of the module starts with an underscore (`_buttons.scss`) the compiler will ignore it. To bring this module into another file use `@use 'buttons'`, then you can use variables from this module `buttons.$font`

### Mixins

    @mixin transform(#property) {
        -webkit-transform: $property;
        -ms-transform: $property;
        transform: $property;
    }

    .box { @include transform(rotate(30deg)); }

### Inheritance

    %message-shared {
        border: 1px solid black;
        padding: 10px;
    }

    .message {
        @extend %message-shared;
    }

    .message-success {
        @extend %message-shared;
        border-color: green;
    }

### Conditionals

    @mixin triangle($size, $color, $direction) {
        height: 0;
        width: 0;

        border-color: transparent;
        border-style: solid;
        border-width: $size / 2;

        @if $direction == up {
            border-bottom-color: $color;
        } @else if $direction == down {
            border-top-color: $color
        }
    }

    .next {
        @include triangle(5px, black, right);
    }

## Django-SASS processor

[more info here](https://github.com/jrief/django-sass-processor#introduction)

[Go back](../README.md)
