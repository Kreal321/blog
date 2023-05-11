---
title: Material Design
tags:
  - Angular
  - Angular Material Design
  - Bootstrap
---

## Angular Material Design

Angular Material is a set of high-quality UI components that implement Google's Material Design. It's built with and for Angular. The library is great and keeps getting better with time. 

## Using Angular Material Design with Bootstrap

Angular Material Design lacks some important features like a decent layout (grid) system, a CSS reset, and some CSS utilities that ease our life as developers.

1. Install Angular Material and Bootstrap

    ```zsh
    npm install @angular/material
    npm install bootstrap
    ```

2. Adding Bootstrap to the style

    ```scss title="src/style.scss"

    // 1. Include functions first (so you can manipulate colors, SVGs, calc, etc)
    @import "../node_modules/bootstrap/scss/functions";

    // 2. Include any default variable overrides here
    @import "styles/variables";

    // 3. Include remainder of required Bootstrap stylesheets
    @import "../node_modules/bootstrap/scss/variables";

    // 4. Include any default map overrides here
    @import "styles/maps";

    // 5. Include remainder of required parts
    @import "../node_modules/bootstrap/scss/maps";
    @import "../node_modules/bootstrap/scss/mixins";
    @import "../node_modules/bootstrap/scss/root";
    @import "../node_modules/bootstrap/scss/utilities";
    @import "../node_modules/bootstrap/scss/reboot";

    // 6. Optionally include any other parts as needed
    @import "../node_modules/bootstrap/scss/type";
    @import "../node_modules/bootstrap/scss/images";
    @import "../node_modules/bootstrap/scss/containers";
    @import "../node_modules/bootstrap/scss/grid";
    @import "../node_modules/bootstrap/scss/helpers";

    // 7. Optionally include utilities API last to generate classes based on the Sass map in `_utilities.scss`
    @import "../node_modules/bootstrap/scss/utilities/api";

    // 8. Add additional custom code here
    @import "styles/reset"

    ```

3. Fixing Reboot issues

    The reset.scss Sass file allows you to override some of the Bootstrap styles you don't want. That's why you've added it after all Bootstrap imports. For example,

    ```scss title="reset.scss"
    a {
    &.mat-button, &.mat-raised-button, &.mat-fab, &.mat-mini-fab, &.mat-list-item {
        &:hover {
        color: currentColor
        }
    }
    }
    ```