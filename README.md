## Assignment 7

### Explain what are stateless widgets and stateful widgets, and explain the difference between them.
stateless widget: widget that dont change (static). Example: text, icon. RaisedButton
stateful widget: widget that can change its properties during run-time (dynamic). Example: Checkbox, radio button, slilder

The difference between the two widgets are stateless widgets doesn't depend on any data change/behavior change, while stateful widget can be updated during runtime based on users action or data change. Stateless widgets do not have a state, they will be rendered once and won't update themselves, but will only be updated when external data changes, but stateful widgets have an internal state and can re-render if the input data changes or if widget’s state changes.

### Mention the widgets that you have used for this project and its uses.

### What is the use-case for setState()? Explain the variable that can be affected by setState().

The setState() function is used to update the state variables of a component or widget. When setState() is called, it triggers a re-render, updating the UI based on the new state values. It's essential when:

- Updating a counter, text, or any value displayed to the user after a user interaction.
- Change the appearance of an element in response to user input, such as button press, form submission, or slider adjustment.
- Fetch data asynchronously and update the view once the data is loaded.

Variables Affected by setState()
Any state variable that represents the dynamic properties of a component or widget can be updated within setState(). These variables are typically:

- State variables like counters, flags, or lists representing interactive UI elements.
- UI-related properties such as colors, visibility toggles, or dimensions that change dynamically.

### Explain the difference between const and final keyword.

const:
- Declares compile-time constants, meaning the value must be known at compile time.
- const variables are implicitly final and cannot be modified once assigned.
- Can be used to define a constant value at a class level or in widget trees.

Example:

```
const int myNumber = 10;
```

final:

Declares a run-time constant, which can be assigned only once but doesn’t need to be known at compile time. Useful when a variable's value can only be assigned at runtime but won’t change afterward.

Example:

```
final DateTime currentDate = DateTime.now();
```

-->
const is used for compile-time constants and is more restrictive.
final is used when a value should only be assigned once but is determined at runtime, providing more flexibility.

- Explain how you implemented the checklist above step-by-step.