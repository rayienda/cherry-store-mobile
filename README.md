<details>
<Summary><b>Assignment 7</b></Summary>

## Assignment 7

### Explain what are stateless widgets and stateful widgets, and explain the difference between them.
stateless widget: widget that dont change (static). Example: Text, Icon, Container

stateful widget: widget that can change its properties during run-time (dynamic). Example: Checkbox, Slider

The difference between the two widgets are stateless widgets doesn't depend on any data change/behavior change, while stateful widget can be updated during runtime based on users action or data change. Stateless widgets do not have a state, they will be rendered once and won't update themselves, but will only be updated when external data changes, but stateful widgets have an internal state and can re-render if the input data changes or if widget’s state changes.

### Mention the widgets that you have used for this project and its uses.
- MaterialApp: The root widget of the application that sets up the theme and routes.
- Scaffold: Provides a structure for the visual interface, including an app bar, body, and other elements.
- AppBar: Displays a material design app bar at the top of the screen.
- Center: Centers its child widget within itself.
- Column: Lays out its children in a vertical array.
- Row: Lays out its children in a horizontal array.
- ElevatedButton: A material design button that elevates when pressed, used for interactive actions.
- GridView: Displays items in a grid or table format. Used to display a menu of product items in a neat layout.
- InkWell : Gives an effect/action to a clickable element.
- SnackBar: Displays a brief message at the bottom of the screen.
- Card: A material design card that can contain content and actions about an information.
- Padding: Adds padding around a widget.
- Text: Displays a string of text with a single style.

### What is the use-case for setState()? Explain the variable that can be affected by setState().

The setState() function is used to update the state variables of a component or widget. When setState() is called, it triggers a re-render, updating the UI based on the new state values. It's important when:

- Updating a counter, text, or any value displayed to the user after a user interaction
- Change the appearance of an element in response to user input, such as button press, form submission, or slider adjustment
- Fetch data asynchronously and update the view once the data is loaded

Variables that can be affected by setState():

- State variables like counters, flags, or lists representing interactive UI elements
- UI-related properties such as colors, visibility toggles, or dimensions that change dynamically

Examples:

items: If the ItemHomepage list is changed (e.g. adding or removing items), we need to call setState() to update the GridView with the latest data
npm, name, className: If there are changes to the user data (NPM, name, class), setState() allows these data updates to be displayed directly in the UI

By using setstate(), the application will update the display according to the latest data

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

### Explain how you implemented the checklist above step-by-step.

- Create a new flutter project
run the command `flutter create cherry_store` to create a new flutter project

- Make a new file `menu.dart` and fill with this (explanations on the comments):

```
import 'package:flutter/material.dart'; 

// Create a card with NPM, Name, and Class
class MyHomePage extends StatelessWidget {
  final String npm = '2306172735'; // NPM
  final String name = 'Rayienda Hasmaradana Najlamahsa'; // Name
  final String className = 'PBD'; // Class
  final List<ItemHomepage> items = [ // Create a button card with icon
         ItemHomepage("View Product", Icons.mood),
         ItemHomepage("Add Product", Icons.add),
         ItemHomepage("Logout", Icons.logout),
  ];
  MyHomePage({super.key});

  // Integrating Infocard and Itemcard to display on the homepage
  @override
  Widget build(BuildContext context) {
    // Scaffold provides the basic structure of the page with the AppBar and body.
    return Scaffold(
      // AppBar is the top part of the page that displays the title.
      appBar: AppBar(
        title: const Text(
          'Cherry Store',
          style: TextStyle(
            color: Colors.white,
            fontWeight: FontWeight.bold,
          ),
        ),
        // The background color of the AppBar is obtained from the application theme color scheme.
        backgroundColor: Theme.of(context).colorScheme.primary,
      ),
      // Body of the page with paddings around it.
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        // Place the widget vertically in a column.
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.center,
          children: [
            // Row to display 3 InfoCard horizontally.
            Row(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: [
                InfoCard(title: 'NPM', content: npm),
                InfoCard(title: 'Name', content: name),
                InfoCard(title: 'Class', content: className),
              ],
            ),

            // Give a vertical space of 16 units.
            const SizedBox(height: 16.0),

            // Place the following widget in the center of the page.
            Center(
              child: Column(
                // Place the text and grid item vertically.

                children: [
                  // Display the welcome message with bold font and size 18.
                  const Padding(
                    padding: EdgeInsets.only(top: 16.0),
                    child: Text(
                      'Welcome to Cherry Store',
                      style: TextStyle(
                        fontWeight: FontWeight.bold,
                        fontSize: 18.0,
                      ),
                    ),
                  ),

                  // Grid to display ItemCard in a 3 column grid.
                  GridView.count(
                    primary: true,
                    padding: const EdgeInsets.all(20),
                    crossAxisSpacing: 10,
                    mainAxisSpacing: 10,
                    crossAxisCount: 3,
                    // To ensure that the grid fits its height.
                    shrinkWrap: true,

                    // Display ItemCard for each item in the items list.
                    children: items.map((ItemHomepage item) {
                      return ItemCard(item);
                    }).toList(),
                  ),
                ],
              ),
            ),
          ],
        ),
      ),
    );
  }
}

class InfoCard extends StatelessWidget {
  // Card information that displays the title and content.

  final String title;  // Card title.
  final String content;  // Card content.

  const InfoCard({super.key, required this.title, required this.content});

  @override
  Widget build(BuildContext context) {
    return Card(
      // Create a card box with a shadow.
      elevation: 2.0,
      child: Container(
        // Set the size and spacing within the card.
        width: MediaQuery.of(context).size.width / 3.5, // Adjust with the width of the device used.
        padding: const EdgeInsets.all(16.0),
        // Place the title and content vertically.
        child: Column(
          children: [
            Text(
              title,
              style: const TextStyle(fontWeight: FontWeight.bold),
            ),
            const SizedBox(height: 8.0),
            Text(content),
          ],
        ),
      ),
    );
  }
}

class ItemHomepage {
    final String name;
    final IconData icon;

    ItemHomepage(this.name, this.icon);
}

class ItemCard extends StatelessWidget {
  // Display the card with an icon and name.

  final ItemHomepage item; 
  
  const ItemCard(this.item, {super.key}); 

    @override
  Widget build(BuildContext context) {
    // Assign different colors based on the item name
    Color getButtonColor() {
      switch (item.name) {
        case "View Product":
          return Colors.lightBlue; // Color for "View Product" button
        case "Add Product":
          return Colors.lightGreen; // Color for "Add Product" button
        case "Logout":
          return Colors.red; // Color for "Logout" button
        default:
          return Theme.of(context).colorScheme.secondary;
      }
    }

    return Material(
      color: getButtonColor(),
      borderRadius: BorderRadius.circular(12),
      child: InkWell(
        onTap: () {
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(
              SnackBar(content: Text("You have pressed the ${item.name} button!"))
            );
        },
        child: Container(
          padding: const EdgeInsets.all(8),
          child: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Icon(
                  item.icon,
                  color: Colors.white,
                  size: 30.0,
                ),
                const Padding(padding: EdgeInsets.all(3)),
                Text(
                  item.name,
                  textAlign: TextAlign.center,
                  style: const TextStyle(color: Colors.white),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```

- Perform add, commit, and push to GitHub

</details>

<details>
<Summary><b>Assignment 8</b></Summary>

### What is the purpose of const in Flutter? Explain the advantages of using const in Flutter code. When should we use const, and when should it not be used?

The const keyword is used to create compile-time constants. It indicates that the value of a variable or widget is constant and will not change. This allows the Flutter framework to optimize the performance and memory usage of the application.

Advantages:
- Performance Optimization:
Compile-Time Constants: const widgets are created at compile time, which reduces the overhead of creating them at runtime.
Reduced Rebuilds: Since const widgets are immutable, they do not need to be rebuilt when the widget tree is rebuilt, leading to improved performance.

- Memory Efficiency:
Single Instance: const widgets are canonicalized, meaning that identical const widgets share the same instance in memory, and it reduces memory usage.

- Code Readability and Maintenance:
Clear Intent: Using const makes it clear that a widget or value is immutable, improving code readability and maintainability.

We should use const for: 
- immutable widgets: for widgets that don't change during the use of the application
- constant values: for values that are known at compile time and doesn't change
- reusable widgets: for reusable widgets that are used multiple times with the same properties

When we should not use const:
We should avoid using const for dynamic values or widgets that rely on changing data, as they need to rebuild or update based on user interaction or app state changes.

### Explain and compare the usage of Column and Row in Flutter. Provide example implementations of each layout widget!

Column
Purpose: Arranges its children vertically.
Main Axis: Vertical (top to bottom).
Cross Axis: Horizontal (left to right).

Example:
```
import 'package:flutter/material.dart';

Column(
  mainAxisAlignment: MainAxisAlignment.center,
  crossAxisAlignment: CrossAxisAlignment.start,
  children: [
    Text('Line 1'),
    Text('Line 2'),
    ElevatedButton(
      onPressed: () {},
      child: Text('Click Me'),
    ),
  ],
)
```

Row
Purpose: Arranges its children horizontally.
Main Axis: Horizontal (left to right).
Cross Axis: Vertical (top to bottom).

```
import 'package:flutter/material.dart';

Row(
  mainAxisAlignment: MainAxisAlignment.spaceAround,
  crossAxisAlignment: CrossAxisAlignment.center,
  children: [
    Icon(Icons.star),
    Text('Hello'),
    ElevatedButton(
      onPressed: () {},
      child: Text('Click Me'),
    ),
  ],
)

```
### List the input elements you used on the form page in this assignment. Are there other Flutter input elements you didn’t use in this assignment? Explain!
- TextFormField: for text input in forms
- AlertDialog: to display pop-up message
- ElevatedButton: used for creating a button that can be pressed

Other input elements that's not used in this assignment:
- DropdownButtonFormField: for selecting an option from a predefined list
- Checkbox: for taking boolean input
- Radio: for selecting of one option from a group of options
- Switch: for toggling between on/off states
- Slider:  for selecting a value from a continuous range
- DatePicker: to select a date from a calendar
- TimePicker: to select a time
- RangeSlider: for selecting a range of values, ex: price range

### How do you set the theme within a Flutter application to ensure consistency? Did you implement a theme in your application?
Yes, I implement a theme for my application by setting up a primary theme within the main.dart file. I defined a theme by using the ThemeData constructor. I used a pink primary swatch and a deep red as the secondary color.

### How do you manage navigation in a multi-page Flutter application?
In a multi-page Flutter application, navigation is managed using the Navigator class. We can use methods like `Navigator.push` to navigate to a new page, `Navigator.pop` to go back to the previous page, and `Navigator.pushReplacement` to replace the current page with a new one.
</details>