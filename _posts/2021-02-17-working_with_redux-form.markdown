---
layout: post
title:      "Working with redux-form"
date:       2021-02-17 19:29:12 +0000
permalink:  working_with_redux-form
---

While working through my final project at Flatiron, I came across redux-form. Redux-form wraps basic form inputs so that redux knows about the form values.

This is accomplished just like wiring up components to Redux. The form data is held in state thanks to Redux and we can pass that data and validate it in a cleaner and more efficeient manner.

Building a form is just as intuative as regular HTML. The reduxForm() function works similar to react-redux’s connect() function. Your `<form>` HTML element gets wrapped in this function to enable redux-form's functionality, essientially creating a form component. From there, you can add `Field` components that work like `<input>` tags and `FieldArray` components that work like `<select>` tags. 

For example:

```
<form onSubmit={handleSubmit}>
      <div>
        <label>First Name</label>
        <div>
          <Field
            name="firstName"
            component="input"
            type="text"
            placeholder="First Name"
```      

You can see the `<Field>` component includes props that are passed to redux-form to handle. These should look similar to a regular `<input>` tag.

You can also enable radio buttons by setting the `<Field>` prop `type` to `"radio"` or `"checkbox"` just like regular HTML.

Exporting the form involves a familiar looking syntax. Just like using Redux's `connect()` function, redux-form uses `export default reduxForm({  form: 'example' })(ExampleForm)`.
        "#Getting Familiar With Redux Form"


