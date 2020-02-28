# Possible `ember-radio-button` Alternative

In response to the comments on this [pull request](https://github.com/yapplabs/ember-radio-button/pull/99), I decided to take a stab at devising a slightly more modern approach to radio buttons in Ember. The API defined below is similar to what [ember-radio-button](https://github.com/yapplabs/ember-radio-button) provides, but the introduction of Angle Bracket Invocation with `...attributes` allows us to decrease the amount of arguments needed.

## `RadioButton` component

### Usage

```handlebars
<RadioButton
  @groupValue={{this.groupValue}}
  @onChange={{this.updateGroupValue}}
  @value="option-1"
/>

<RadioButton
  @groupValue={{this.groupValue}}
  @onChange={{this.updateGroupValue}}
  @value="option-2"
/>
```

A radio button will be marked as checked when the `@value` argument equals the `@groupValue` argument.

### Arguments

#### `@groupValue`

> Current value of the radio button group.

#### `@onChange`

> Callback that will be invoked if the radio button's checked state changes as a result of a user interaction. The new group value and original event will be passed along as arguments.

#### `@value`

> Value of the radio button itself.

### Attributes

Additional attributes and modifiers will be spread onto the radio button's `input` element using `...attributes`.

## `RadioButtonGroup` component

This contextual component could be used to avoid having to pass the `@groupValue` and `@onChange` arguments to each `RadioButton` component.

### Usage

```handlebars
<RadioButtonGroup
  @name="group-name"
  @onChange={{this.updateGroupValue}}
  @value={{this.groupValue}}
  as |group|
>
  <group.RadioButton @value="option-1" />
  <group.RadioButton @value="option-2" />
</RadioButtonGroup>
```

### Arguments

#### `@name` (required?)

> Name of the radio button group.

#### `@onChange`

> Callback that will be invoked if one of the radio button's checked state changes as a result of a user interaction. The new group value and original event will be passed along as arguments.

#### `@value`

> Current value of the radio button group.

## Remarks / unresolved questions

- I think the `RadioButton` component should only render an `input` element. The usage of a `label` element should be the responsibility of the consuming application.
- Would the `RadioButtonGroup` component be a useful addition or does it seem unnecessary?
- Should support for checked and unchecked related classes be provided? Styling could also be done using the `checked` attribute?
- Are all argument names clear enough?
- Using Glimmer components would mean, support officially starts at `v3.15`?
