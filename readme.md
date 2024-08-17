# Frontend-Assessment

## Build Setup

```bash
# install dependencies
$ yarn install

# serve with hot reload at localhost:3000
$ yarn dev

# build for production and launch server
$ yarn build
$ yarn start

# generate static project
$ yarn generate
```
Exercise 1
---
I have created a landing page with card animations and redirection to each exercise.
The project is built with Nuxt.js and VueJs framework. I also have made use of the 
layouts directory to have one uniform page layout for both exercises it just differs
on the content. The design image files are at path `assets/exercise1`.

Exercise 2
---
I have created a page with an accordion component in which it's behavior is according
to the requirements mentioned.

###### Bonus points
* Improve the user experience with meaningful animations/transitions.
    * I have used simple transitions for the tabs, accordion basically the whole exercise 2

* Design and styling.
    * I made sure to have a slight touch of color synchronization on the components

* Explain why the result of `('b' + 'a' + + 'a' + 'a').toLowerCase()` is `banana`. 
    * Answer: In the context of the expression you provided `('b' + 'a' + + 'a' + 'a').toLowerCase()`, the `unary plus (+)` if paired with any string as long as it is not a numeric literal it will attempt to convert the string ('a' or any string) to a number. However, since 'a' is not a valid numeric literal, So this part `+ 'a'` in the expression results in NaN, which contributes to the final string `'baNaNa'` then if converted to lowercase it now becomes `banana`.