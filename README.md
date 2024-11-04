## Assignment 7

### Explain what are stateless widgets and stateful widgets, and explain the difference between them.
stateless widget: widget that dont change (static). Example: text, icon. RaisedButton

stateful widget: widget that can change its properties during run-time (dynamic). Example: Checkbox, radio button, slilder

The difference between the two widgets are stateless widgets doesn't depend on any data change/behavior change, while stateful widget can be updated during runtime based on users action or data change. Stateless widgets do not have a state, they will be rendered once and won't update themselves, but will only be updated when external data changes, but stateful widgets have an internal state and can re-render if the input data changes or if widget’s state changes.

### Mention the widgets that you have used for this project and its uses.
- MaterialApp: The root widget of the application that sets up the theme and routes.
- Scaffold: Provides a structure for the visual interface, including an app bar, body, and other elements.
- AppBar: Displays a material design app bar at the top of the screen.
- Center: Centers its child widget within itself.
- Column: Lays out its children in a vertical array.
- Row: Lays out its children in a horizontal array.
- ElevatedButton: A material design button that elevates when pressed, used for interactive actions.
- InkWell : Gives an effect/action to a clickable element.
- SnackBar: Displays a brief message at the bottom of the screen.
- Card: A material design card that can contain content and actions about an information.
- Padding: Adds padding around a widget.
- Text: Displays a string of text with a single style.

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