## SignUp_page
---
# Creating Signup_page as a Stateful Widget
```dart
class SignUpScreen extends StatefulWidget{
//class a blueprint which name is SignupScreen
//and this is a instance of stateful widget
const SignUpScreen({key? key}) : super(key: key);
//{key? key} is a constructor and ? means can be null
which makes this optional//

@override
State<SignupScreen> createState() => _SignUpScreenState();
//state is a class that holds multiple widgets in flutter
//we create signupscreen state which returns _SignupScreenStates()
//What does _SignupScreenState has?--its below👇

}
class _SignUpScreenState extends State<SignUpScreen>{
//the _signupscreenstate is a instance of Signupscreen
//which is instance of statefull widget
//ie signupscreenstate<signupscreen<stateful widget
final FirebaseAuth _auth = FirebaseAuth.instance
final TextEditingController _emailcontroller = TextEditingController();
final TextEditingController _passwordController = TextEditingController();
final TextEditingController _displayname = TextEditingcontroller();
User? _user

//Here we allow _auth to hold data for FirebaseAuth.instance
//same for other textcontrollers

@override

void initState(){
super.initstate();
ListenToAuthState
}

//
void ListenToAuthState(){
_auth.authStateChanger().listen((User? user){
setState(() => _user = user)
});
}



@override
Widget build(BuildContext context) {
  final ThemeData = Theme.of(context);
  return FutureBuilder(
    future: _auth.currentUser?.reload(), // Reload the user to get the latest data
    builder: (context, snapshot) {
      if (snapshot.connectionState == ConnectionState.done) {
        displayName = _auth.currentUser?.displayName;
        return Scaffold(
          body: SafeArea(
            child: SingleChildScrollView(
              child: Column(
                children: [
                  Text(
                    'Welcome, $displayName', // Display the fetched display name
                    style: TextStyle(
                      fontSize: 20,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                  // Rest of your code...
                ],
              ),
            ),
          ),
          // Rest of your code...
        );
      } else {
        return CircularProgressIndicator(); // Show a loading spinner while waiting
      }
    },
  );
}
