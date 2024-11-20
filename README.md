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

<details>
<Summary><b>Assignment 9</b></Summary>

#### Explain why we need to create a model to retrieve or send JSON data. Will an error occur if we don't create a model first?
It ensures data structure consistency and type safety. It helps validate and manage the data format, making it easier to handle in the code.
If we don't create a model, an error won't always occur, but issues like unexpected data formats, runtime errors, or misinterpreted fields might arise, especially in strongly-typed languages like TypeScript or Dart. Models also improve code readability and maintainability.
#### Explain the function of the http library that you implemented for this task.
The http library is used to handle network requests in this task. Its primary functions include:

- Sending Requests: It enables the app to send HTTP request methods like GET, POST, PUT, and DELETE to interact with APIs.
- Receiving Responses: It retrieves data from the server, typically in JSON format, for further processing.
- Send data to the server: It sends data to the server, for example in JSON format, for further processing.

#### Explain the function of CookieRequest and why it’s necessary to share the CookieRequest instance with all components in the Flutter app.
The CookieRequest class in Flutter manages HTTP requests while preserving cookies across sessions. Its key functions include:

- Cookie Management: It stores cookies sent by the server (e.g., session tokens), ensuring that subsequent requests include these cookies for authenticated communication.
- Session Persistence: It helps maintain user sessions, allowing features like login, authentication, and personalization to work seamlessly.
- Simplified State Management: By handling cookies automatically, it reduces the need to manually manage authentication headers or tokens.

It's necessary to share the CookieRequest instance with all components in the Flutter app because it's essential for managing secure, stateful communication in the Flutter app. 

Sharing a single CookieRequest instance across all components ensures:

Consistency: All parts of the app use the same session and cookies, avoiding discrepancies or redundant logins.
Efficiency: It reduces memory usage and redundant cookie reloading by centralizing cookie storage.
Ease of Maintenance: A single shared instance simplifies debugging and ensures consistent behavior throughout the app.

#### Explain the mechanism of data transmission, from input to display in Flutter.
- Data Input: User enters data through the Flutter interface (e.g., a form or button).

- Sending Request: The input data is sent to the server using http or CookieRequest in a specific format (e.g., JSON).

- Backend Processing
1. The Django server receives the request data.
2. The backend processes the data (e.g., saves it to a database or performs calculations).
3. Django returns a response in JSON format.
Receiving Response

- The Flutter app receives the server's response.

- Decoding Data:The JSON response is converted into Dart objects (using a model).

-Displaying Data: The converted data is displayed in the Flutter interface.

#### Explain the authentication mechanism from login, register, to logout. Start from inputting account data in Flutter to Django’s completion of the authentication process and display of the menu in Flutter.

##### Login Process
1. Input Data: The user enters their email and password in the Flutter app.
1. Sending Request: The data is sent to the Django login endpoint using CookieRequest.
3. Backend Processing:
- Django verifies the user's credentials.
- If successful, the server returns an authentication cookie.
4. Storing Status: The cookie is saved in CookieRequest for use in subsequent requests.
5. Display Menu: After a successful login, the app displays the main menu based on the user's login status.
##### Registration Process
1. Input Data: The user enters account information (e.g., name, email, password).
2. Sending Request: The data is sent to the Django registration endpoint using http or CookieRequest.
3. Backend Processing:
- Django saves the new user data to the database.
- Django returns a success response.
4. Notification: Flutter displays a success or error message based on the response.
##### Logout Process
1. Logout Request: Flutter sends a request to the Django logout endpoint using CookieRequest.
2. Delete Cookie: Django deletes the user's session.
3. Update Status: The Flutter app updates the user's status to logged out.
4. Navigation: The user is redirected to the login page.
#### Explain how you implement the checklist above step by step! (not just following the tutorial).

##### Authentication functionality
Create a new app in Django for authentication and integration with Flutter to create products with the command:
```
python manage.py startapp authentication
```
and add this to `authentication/views.py`

```
from django.contrib.auth import authenticate, login as auth_login, logout as auth_logout
from django.http import JsonResponse
from django.views.decorators.csrf import csrf_exempt
from django.contrib.auth.models import User
import json

@csrf_exempt
def login(request):
    username = request.POST['username']
    password = request.POST['password']
    user = authenticate(username=username, password=password)
    if user is not None:
        if user.is_active:
            auth_login(request, user)
            # Successful login status.
            return JsonResponse({
                "username": user.username,
                "status": True,
                "message": "Login successful!"
                # Add other data if you want to send data to Flutter.
            }, status=200)
        else:
            return JsonResponse({
                "status": False,
                "message": "Login failed, account disabled."
            }, status=401)

    else:
        return JsonResponse({
            "status": False,
            "message": "Login failed, check email or password again."
        }, status=401)
    

@csrf_exempt
def register(request):
    if request.method == 'POST':
        data = json.loads(request.body)
        username = data['username']
        password1 = data['password1']
        password2 = data['password2']

        # Check if the passwords match
        if password1 != password2:
            return JsonResponse({
                "status": False,
                "message": "Passwords do not match."
            }, status=400)

        # Check if the username is already taken
        if User.objects.filter(username=username).exists():
            return JsonResponse({
                "status": False,
                "message": "Username already exists."
            }, status=400)

        # Create the new user
        user = User.objects.create_user(username=username, password=password1)
        user.save()

        return JsonResponse({
            "username": user.username,
            "status": 'success',
            "message": "User created successfully!"
        }, status=200)

    else:
        return JsonResponse({
            "status": False,
            "message": "Invalid request method."
        }, status=400)

@csrf_exempt
def logout(request):
    username = request.user.username

    try:
        auth_logout(request)
        return JsonResponse({
            "username": username,
            "status": True,
            "message": "Logged out successfully!"
        }, status=200)
    except:
        return JsonResponse({
        "status": False,
        "message": "Logout failed."
        }, status=401)
```

add routing in `authentication/urls.py`
```
from django.urls import path
from authentication.views import login, register, logout

app_name = 'authentication'

urlpatterns = [
    path('login/', login, name='login'),
    path('register/', register, name='register'),
    path('logout/', logout, name='logout'),

]
```

add function in `main/views.py` for adding products in Flutter
```
@csrf_exempt
def create_product_flutter(request):
    if request.method == 'POST':

        data = json.loads(request.body)
        new_product = Product.objects.create(
            user=request.user,
            name=data["name"],
            price=int(data["price"]),
            description=data["description"]
            color=data["color"]

        )

        new_product.save()

        return JsonResponse({"status": "success"}, status=200)
    else:
        return JsonResponse({"status": "error"}, status=401)
```
then add routing in `main/urls.py`

```
from django.urls import path, include
from main.views import (
      ...
    create_product_flutter,
)

app_name = 'main'
urlpatterns = [
    path('', show_main, name = 'show_main'),
        ...
        path('auth/', include('authentication.urls')),
        path('create-flutter/', create_product_flutter, name='create-flutter'),

]
```

Create Flutter authentication logic in `register.dart`

```
import 'dart:convert';
import 'package:flutter/material.dart';
import 'package:cherry_store/screens/login.dart';
import 'package:pbp_django_auth/pbp_django_auth.dart';
import 'package:provider/provider.dart';

class RegisterPage extends StatefulWidget {
  const RegisterPage({super.key});

  @override
  State<RegisterPage> createState() => _RegisterPageState();
}

class _RegisterPageState extends State<RegisterPage> {
  final _usernameController = TextEditingController();
  final _passwordController = TextEditingController();
  final _confirmPasswordController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    final request = context.watch<CookieRequest>();
    return Scaffold(
      appBar: AppBar(
        title: const Text('Register'),
        leading: IconButton(
          icon: const Icon(Icons.arrow_back),
          onPressed: () {
            Navigator.pop(context);
          },
        ),
      ),
      body: Center(
        child: SingleChildScrollView(
          padding: const EdgeInsets.all(16.0),
          child: Card(
            elevation: 8,
            shape: RoundedRectangleBorder(
              borderRadius: BorderRadius.circular(12.0),
            ),
            child: Padding(
              padding: const EdgeInsets.all(20.0),
              child: Column(
                mainAxisSize: MainAxisSize.min,
                children: <Widget>[
                  const Text(
                    'Register',
                    style: TextStyle(
                      fontSize: 24.0,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                  const SizedBox(height: 30.0),
                  TextFormField(
                    controller: _usernameController,
                    decoration: const InputDecoration(
                      labelText: 'Username',
                      hintText: 'Enter your username',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                    validator: (value) {
                      if (value == null || value.isEmpty) {
                        return 'Please enter your username';
                      }
                      return null;
                    },
                  ),
                  const SizedBox(height: 12.0),
                  TextFormField(
                    controller: _passwordController,
                    decoration: const InputDecoration(
                      labelText: 'Password',
                      hintText: 'Enter your password',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                    obscureText: true,
                    validator: (value) {
                      if (value == null || value.isEmpty) {
                        return 'Please enter your password';
                      }
                      return null;
                    },
                  ),
                  const SizedBox(height: 12.0),
                  TextFormField(
                    controller: _confirmPasswordController,
                    decoration: const InputDecoration(
                      labelText: 'Confirm Password',
                      hintText: 'Confirm your password',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                    obscureText: true,
                    validator: (value) {
                      if (value == null || value.isEmpty) {
                        return 'Please confirm your password';
                      }
                      return null;
                    },
                  ),
                  const SizedBox(height: 24.0),
                  ElevatedButton(
                    onPressed: () async {
                      String username = _usernameController.text;
                      String password1 = _passwordController.text;
                      String password2 = _confirmPasswordController.text;

                      // Check credentials

                      final response = await request.postJson(
                          "http://localhost:8000/auth/register/",
                          jsonEncode({
                            "username": username,
                            "password1": password1,
                            "password2": password2,
                          }));
                      if (context.mounted) {
                        if (response['status'] == 'success') {
                          ScaffoldMessenger.of(context).showSnackBar(
                            const SnackBar(
                              content: Text('Successfully registered!'),
                            ),
                          );
                          Navigator.pushReplacement(
                            context,
                            MaterialPageRoute(
                                builder: (context) => const LoginPage()),
                          );
                        } else {
                          ScaffoldMessenger.of(context).showSnackBar(
                            const SnackBar(
                              content: Text('Failed to register!'),
                            ),
                          );
                        }
                      }
                    },
                    style: ElevatedButton.styleFrom(
                      foregroundColor: Colors.white,
                      minimumSize: const Size(double.infinity, 50),
                      backgroundColor: Theme.of(context).colorScheme.primary,
                      padding: const EdgeInsets.symmetric(vertical: 16.0),
                    ),
                    child: const Text('Register'),
                  ),
                ],
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```
`login.dart`

```
import 'package:cherry_store/screens/menu.dart';
import 'package:flutter/material.dart';
import 'package:pbp_django_auth/pbp_django_auth.dart';
import 'package:provider/provider.dart';
import 'package:cherry_store/screens/register.dart';

void main() {
  runApp(const LoginApp());
}

class LoginApp extends StatelessWidget {
  const LoginApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Login',
      theme: ThemeData(
        useMaterial3: true,
        colorScheme: ColorScheme.fromSwatch(
          primarySwatch: Colors.deepPurple,
        ).copyWith(secondary: Colors.deepPurple[400]),
      ),
      home: const LoginPage(),
    );
  }
}

class LoginPage extends StatefulWidget {
  const LoginPage({super.key});

  @override
  State<LoginPage> createState() => _LoginPageState();
}

class _LoginPageState extends State<LoginPage> {
  final TextEditingController _usernameController = TextEditingController();
  final TextEditingController _passwordController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    final request = context.watch<CookieRequest>();

    return Scaffold(
      appBar: AppBar(
        title: const Text('Login'),
      ),
      body: Center(
        child: SingleChildScrollView(
          padding: const EdgeInsets.all(16.0),
          child: Card(
            elevation: 8,
            shape: RoundedRectangleBorder(
              borderRadius: BorderRadius.circular(12.0),
            ),
            child: Padding(
              padding: const EdgeInsets.all(20.0),
              child: Column(
                mainAxisSize: MainAxisSize.min,
                children: [
                  const Text(
                    'Login',
                    style: TextStyle(
                      fontSize: 24.0,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                  const SizedBox(height: 30.0),
                  TextField(
                    controller: _usernameController,
                    decoration: const InputDecoration(
                      labelText: 'Username',
                      hintText: 'Enter your username',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                  ),
                  const SizedBox(height: 12.0),
                  TextField(
                    controller: _passwordController,
                    decoration: const InputDecoration(
                      labelText: 'Password',
                      hintText: 'Enter your password',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                    obscureText: true,
                  ),
                  const SizedBox(height: 24.0),
                  ElevatedButton(
                    onPressed: () async {
                      String username = _usernameController.text;
                      String password = _passwordController.text;

		  // Check credentials

                      final response = await request
                          .login("http://localhost:8000/auth/login/", {
                        'username': username,
                        'password': password,
                      });

                      if (request.loggedIn) {
                        String message = response['message'];
                        String uname = response['username'];
                        if (context.mounted) {
                          Navigator.pushReplacement(
                            context,
                            MaterialPageRoute(
                                builder: (context) => MyHomePage()),
                          );
                          ScaffoldMessenger.of(context)
                            ..hideCurrentSnackBar()
                            ..showSnackBar(
                              SnackBar(
                                  content:
                                      Text("$message Welcome, $uname.")),
                            );
                        }
                      } else {
                        if (context.mounted) {
                          showDialog(
                            context: context,
                            builder: (context) => AlertDialog(
                              title: const Text('Login Failed'),
                              content: Text(response['message']),
                              actions: [
                                TextButton(
                                  child: const Text('OK'),
                                  onPressed: () {
                                    Navigator.pop(context);
                                  },
                                ),
                              ],
                            ),
                          );
                        }
                      }
                    },
                    style: ElevatedButton.styleFrom(
                      foregroundColor: Colors.white,
                      minimumSize: const Size(double.infinity, 50),
                      backgroundColor: Theme.of(context).colorScheme.primary,
                      padding: const EdgeInsets.symmetric(vertical: 16.0),
                    ),
                    child: const Text('Login'),
                  ),
                  const SizedBox(height: 36.0),
                  GestureDetector(
                    onTap: () {
                      Navigator.push(
                        context,
                        MaterialPageRoute(
                            builder: (context) => const RegisterPage()),
                      );
                    },
                    child: Text(
                      'Don\'t have an account? Register',
                      style: TextStyle(
                        color: Theme.of(context).colorScheme.primary,
                        fontSize: 16.0,
                      ),
                    ),
                  ),
                ],
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

#### Creating Product List page
`list_product.dart`

```
import 'package:flutter/material.dart';
import 'package:cherry_store/models/product_entry.dart';
import 'package:cherry_store/widgets/left_drawer.dart';
import 'package:pbp_django_auth/pbp_django_auth.dart';
import 'package:provider/provider.dart';
import 'package:cherry_store/widgets/product_details.dart';

class ProductEntryPage extends StatefulWidget {
  const ProductEntryPage({super.key});

  @override
  State<ProductEntryPage> createState() => _ProductEntryPageState();
}

class _ProductEntryPageState extends State<ProductEntryPage> {
  Future<List<ProductEntry>> fetchProduct(CookieRequest request) async {
    final response = await request.get('http://localhost:8000/json/');
    
    // Decoding the response into JSON
    var data = response;
    
    // Convert json data to a ProductEntry object
    List<ProductEntry> listProduct = [];
    for (var d in data) {
      if (d != null) {
        listProduct.add(ProductEntry.fromJson(d));
      }
    }
    return listProduct;
  }
  
  @override
  Widget build(BuildContext context) {
    final request = context.watch<CookieRequest>();
    return Scaffold(
      appBar: AppBar(
        title: const Text('Product Entry List'),
        backgroundColor: Theme.of(context).colorScheme.primary,
        foregroundColor: Colors.white,
      ),
      drawer: const LeftDrawer(),
      body: FutureBuilder(
        future: fetchProduct(request),
        builder: (context, AsyncSnapshot snapshot) {
          if (snapshot.data == null) {
            return const Center(child: CircularProgressIndicator());
          } else {
            if (!snapshot.hasData) {
              return const Column(
                children: [
                  Text(
                    'There is no product data in Cherry Store.',
                    style: TextStyle(fontSize: 20, color: Color(0xff59A5D8)),
                  ),
                  SizedBox(height: 8),
                ],
              );
            } else {
              return ListView.builder(
                itemCount: snapshot.data!.length,
                itemBuilder: (context, index) {
                  final product = snapshot.data![index];
                  return InkWell(
                    onTap: () {
                      Navigator.push(
                        context,
                        MaterialPageRoute(
                          builder: (context) => ProductDetailsPage(product: product),
                        ),
                      );
                    },
                    child: Card(
                      margin: const EdgeInsets.symmetric(horizontal: 16, vertical: 12),
                      child: Container(
                        decoration: BoxDecoration(
                          border: Border.all(
                            color: Colors.grey, // Color of the border
                            width: 1, // Width of the border
                          ),
                          borderRadius: BorderRadius.circular(12), // Border radius of the container
                        ),
                        padding: const EdgeInsets.all(20.0),
                        child: Column(
                          mainAxisAlignment: MainAxisAlignment.start,
                          crossAxisAlignment: CrossAxisAlignment.start,
                          children: [
                            Text(
                              "${snapshot.data![index].fields.name}",
                              style: const TextStyle(
                                fontSize: 18.0,
                                fontWeight: FontWeight.bold,
                              ),
                            ),
                            const SizedBox(height: 10),
                            Text("${snapshot.data![index].fields.description}"),
                            const SizedBox(height: 10),
                            Text("${snapshot.data![index].fields.price}"),
                            const SizedBox(height: 10),
                            Text("${snapshot.data![index].fields.color}")
                          ],
                        ),
                      ),
                    ),
                  );
                },
              );
            }
          }
        },
      ),
    );
  }
}
```

To accomodate the Django model object, we need to make a custom model in Dart.

`product_entry.dart`

```
// To parse this JSON data, do
//
//     final productEntry = productEntryFromJson(jsonString);

import 'dart:convert';

List<ProductEntry> productEntryFromJson(String str) => List<ProductEntry>.from(json.decode(str).map((x) => ProductEntry.fromJson(x)));

String productEntryToJson(List<ProductEntry> data) => json.encode(List<dynamic>.from(data.map((x) => x.toJson())));

class ProductEntry {
    String model;
    String pk;
    Fields fields;

    ProductEntry({
        required this.model,
        required this.pk,
        required this.fields,
    });

    factory ProductEntry.fromJson(Map<String, dynamic> json) => ProductEntry(
        model: json["model"],
        pk: json["pk"],
        fields: Fields.fromJson(json["fields"]),
    );

    Map<String, dynamic> toJson() => {
        "model": model,
        "pk": pk,
        "fields": fields.toJson(),
    };
}

class Fields {
    int user;
    String name;
    int price;
    String description;
    String color;

    Fields({
        required this.user,
        required this.name,
        required this.price,
        required this.description,
        required this.color,
    });

    factory Fields.fromJson(Map<String, dynamic> json) => Fields(
        user: json["user"],
        name: json["name"],
        price: json["price"],
        description: json["description"],
        color: json["color"],
    );

    Map<String, dynamic> toJson() => {
        "user": user,
        "name": name,
        "price": price,
        "description": description,
        "color": color,
    };
}
```
Making detail page for each item listed

```
import 'package:flutter/material.dart'; 
import 'package:cherry_store/models/product_entry.dart'; 
class ProductDetailsPage extends StatelessWidget {
  final ProductEntry product;
  const ProductDetailsPage({super.key, required this.product});
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(product.fields.name), 
        centerTitle: true,
        actions: <Widget>[
          IconButton(
            icon: const Icon(Icons.chevron_left),
            onPressed: () => Navigator.pop(context), 
          ),
        ], // Widget[]
      ), // AppBar
      body: SingleChildScrollView(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              product.fields.name,
              style: const TextStyle(fontSize: 24, fontWeight: FontWeight.bold),
            ), // Text
            const SizedBox(height: 10),
            Text("Description: ${product.fields.description}", style: const TextStyle(fontSize: 16)),
            const SizedBox(height: 10),
            Text("Price: ${product.fields.price}", style: const TextStyle(fontSize: 16)),
            const SizedBox(height: 10),
            Text("Color: ${product.fields.color}", style: const TextStyle(fontSize: 16)),
          ],
        ),
      ),
    );
  }
}
```

</details>
