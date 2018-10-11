# Introduction

This text was created as a resource for first year Game Development students in Mediastadi, Helsinki Vocational College.
Here is a list of additional learning resources for C# programming for Unity:
- [Official Microsoft C# documentation](https://docs.microsoft.com/en-us/dotnet/csharp/)
- [Official Unity learning resources](https://unity3d.com/learn)
- [Unity manual](https://docs.unity3d.com/Manual/index.html)

# Getting started
This tutorial assumes that you have basic knowledge of Unity editor. This includes knowing how to create GameObjects, the relation between GameObjects and their Components and knowing how to create project assets. No previous knowledge of programming is required, but this is a very fast crash course, and therefore depending on your level of programming skills you might need to read through the material several times before thing start to make sense. Over the course many concept have also links to external learning materials, such as the official Microsoft C# guides. If at any time you feel stuck or that you do not understand something, use them for help!

Keywords and other key concepts in the text are marked by *italics* and some concepts have direct links to additional resources describing them in more detail.

## New to programming?
Programming is a skill that requires abstract thinking. At times, understanding and learning the principles of programming can be hard. Don’t panic! While it may take time and effort, gradually you will get more and more skilled in programming. Keep learning, experimenting and creating - that is the (only) road to becoming an experienced game developer!

## Creating a script
In Unity, a new C# script is created either by choosing “Create” -> “C# Script” in Project window, right-clicking in project window and choosing “C# Script” from the context menu, or by selecting a GameObject and in Inspector window clicking “Add Component”  -> “New Script”. Let’screate one and name the script “MyFirstScript”. After you enter a name, the script will appear in the project view. 

## Anatomy of a Unity C# script
Double-click the script to open it up in the installed code editor (usually *Visual Studio* or *MonoDevelop*). Unity has already initialized the script with some boilerplate code that is useful for most of the scripts that we will create. It looks like this:

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class MyFirstScript : MonoBehaviour {

	// Use this for initialization
	void Start () {
		
	}
	
	// Update is called once per frame
	void Update () {
		
	}
}
```

Double slash (//) marks a comment line in C#, so any text on that line following the double slash will be ignored by the computer and is just meant for the coders as a way of documenting the code and making it easier to follow

The first three lines define a few existing code libraries for us to use. To access any existing code in a different *namespace* we need to use the keyword *using* followed by the namespace of that external code (this is similar to Packages in Java programming languages). These three libraries include common and useful methods we can now use when writing our own code.

In the C# language, a line of code always ends with a semicolon (;). The compiler (i.e. computer program that translates our written, human-readable code to something that the computer understands) does not care about line breaks, just semicolons when it is interpreting the code. Also, all other code except certain declarations (like the using statements) must reside inside *code blocks* marked with curly braces {}. Before the braces of a code block, we must also have a declaration for the identity of the code block.

## Classes
Next in our script, we have a line with the following code: *public class MyFirstScript: MonoBehaviour*. This line is a class declaration.  C# is an [Object-oriented programming (OOP) language](https://en.wikipedia.org/wiki/Object-oriented_programming), and in OOP languages all code we write will be part of a *class*. The *access modifier* at the beginning of the line defines if this class can be accessed from other classes we create. For now, we will always use the public modifier in front of a class declaration.

Following the class keyword is the name of our class. Keep in mind that two classes within a namespace cannot have same name! For our purposes this means that every class we create must have a unique name. Now that we have created a class called “MyFirstScript”, we cannot create another class with that same name, as the code compiler would not know which class we would be referring to each time.

After the colon we have a name of another class called *MonoBehaviour*. In C#, classes can [inherit](https://docs.microsoft.com/en-us/dotnet/csharp/tutorials/inheritance) from another class. The derived class (i.e. the class inheriting) automatically includes all the code in the *base* class unless otherwise defined. MonoBehaviour is one of Unity’s built-in classes, which any class (i.e. Script) we attach as a component to a *GameObject* must inherit from.

Class inheritance can be thought as creating a classification of things. We can first define generic things and then more specific things that also have all the characteristics of that generic group.  For example, we could have:

```
public class Fish 
{ 

     public float swimSpeed;

      // A method (i.e. named block of code)  that all fish have
      void Swim() 
       {
           // Code for swimming goes here
       }
}
```

Here we have a class called “Fish” that describes some generic attributes and behaviour shared by all fish, in this case a number value *field* “swimSpeed”, that can be defined separately for each fish, and a *method* called “Swim” (we’ll learn more about value *fields* and *methods* below). Then we can create another *class* that *inherits* from Fish:

```
public class Shark : Fish
{

      void ScarePeople() 
      {
          Swim();
          // Other code for scaring people goes here
      }

}
```

Our *class* Shark now automatically inherits the code in Fish *class*, including the *swimSpeed* variable and *Swim* method. We can call (i.e. execute the code in) this method by writing “Swim();”

We could then create other kinds of classes that derive from Fish, like Blowfish etc. that would all share the common characteristics of Fish class (swimSpeed field and Swim() method), but would not share the characteristics of Shark, like *ScarePeople()* method. Instead, it could implement some methods and characteristics specific to Blowfish. 


## Methods
Now, let’s continue going through the code in MyFirstScript class. inside the class code block Unity has auto-generated two methods called *Start()* and *Update()*. *Methods* in C# are blocks of code that always reside inside a *class* (or a *struct*, but we’ll come to that later)  and belong to that particular class. Methods consist of a *signature*, including the name of the method, and a code block. Methods are the place where we tell Unity to actually do stuff like move something on the screen or play a sound at the right time. 

The syntax for defining a method (i.e. method signature) is a bit different than what we used for defining a class. First, before the method name, we must declare if the method will return a *value*. Keyword *void* means no value is returned. Because methods are where the actual game code resides, they are usually named after an action that the code performs, like *Swim()* or *ScarePeople()*.

Code in methods is always executed from top to bottom, one line at a time. If another method is called within the method, execution will wait until the called method is completed and continue execution only then. Above in the Shark class example we have a method called *ScarePeople()*. Inside the method code block we *call* another method *Swim()*. This means that when we reach the line calling *Swim()*, the execution of *ScarePeople()* method will pause until the execution of *Swim()* method is complete.

There are some special methods that Unity will automatically call at certain points when our game is running. *Start* and *Update* are two of these. *Start* method is called once when the *scene* including our script is first loaded, and *Update* is called every *frame* (that is usually something from 30 to 200 times per second depending on the device our game is running). Other methods, like *Swim()* in our Fish class we need to call ourselves from some part of our code.


##Creating class instances
We’ve now learned that *methods* are where code for making things happen goes. But methods, like actions are something that an individual of a class does (there are exceptions to this, but we’ll learn about them soon enough). All sharks may be scary, but individual sharks actually perform the action of ScarePeople(). Luckily for games that is often exactly what we want. From a game design perspective, it would be very limiting if calling our method ScarePeople() would result in every shark in out game world trying to scare people at the same time.

First we must create individual *instances* of a class, such as our Shark class. In general C# programming new instances are created like this:

```
Shark bob = new Shark(); // For some strange reason this shark is called Bob
```

Now when we have an individual shark, we can call:

```
bob.ScarePeople();
```

And now only our Bob the Shark would start scaring people, while all the other sharks in our world would go on doing whatever fishy things they were doing.

## Class instancing in Unity
When we are making a game with Unity we actually don’t often use this method for creating individual instances of a class. You may remember that our class MyFirstScript inherits from *MonoBehaviour* - a special class in Unity. The benefit for this is that any class *inheriting* from MonoBehaviour can be attached as a component in a GameObject in Unity. What this means in practice is that when the *scene* containing the GameObject and our attached Script is loaded, Unity will automatically create an instance for us. 

## Variables and fields
C# coding also heavily uses *variables*. Variable has a defined *typ*e that can be set to different *values* for every *instance* and that value can also change during gameplay. Our Fish class has a variable declaration *public float swimSpeed*. Variables declared in the main body of a class (i.e. they are not declared inside any method), like *swimSpeed* are called *Fields*. They hold values for an attribute that every instance of that class will have, but the value or that attribute can vary from one instance to another. In this case we have defined the field *public* so that also other scripts can read or modify the value of that field. The second keyword defines the *type* of the field, in this case a *floating-point number*. Last, we have the name of the field.

Now, let’s go back to our friend Bob the Shark:

```
Shark bob = new Shark(); // For some strange reason this shark is called Bob
bob.swimSpeed = 11; // Bob is a good swimmer, so we’ll set his swim speed to 11
```

*Setting* variable values in C# is done with the equals sign (=), so on the second line we are stating that Bob’s swimSpeed is now 11. This is actually similar to what we did on the first line where we declared a variable of Type Shark, named bob, and set the variable to point to a new shark instance we just created.

Variables always have a *scope*, defining the visibility and lifetime of the variable. In general, variables are always bound to the code block they are declared in. Let’s look at an example:

```
public class Fish 
{ 

     public float swimSpeed; //this is a field because it is declared in the main body of the class

      // A method (i.e. named block of code)  that all fish have
      void Swim() 
       {
           int count = 0; //this variable is visible only inside the Swim() method code block

           while (count < 5)
           {
                string action = count +  “I’m swimming around” // we can access ‘count’ in here because we are inside the swim method code block
           }
           
           // variable ‘action’ is not accessible from here, only inside the code block following while keyword
       }

       //let’s make a new method for some more fishy stuff
       void Eat() 
       {
           //we can’t access ‘count’ or ‘action’ from here as they are in another code block, but we can access swimSpeed as it is a field that is declared in the main class code block
       }
}
```

Unlike *fields*, variables declared inside the class’ inner *code blocks* (an area inside curly braces {}) do not have an *access modifier*, because their access is always confined to the code block they are declared in.

**Naming conventions:** The agreed convention in C# is that *method* names start with an uppercase letter and *variable* names start with a lowercase letter. Names cannot have spaces, so most commonly used way of writing names that consist of multiple words is the [CamelCase](https://en.wikipedia.org/wiki/Camel_case), where spaces between words are replaced by starting every joined word with an uppercase letter (like our *swimSpeed* field and *ScarePeople()* method).

## Value types and reference types

One of the hardest concepts to wrap your head around in C# (or any other OOP language) is the distinction between [*value types* and *reference types*](https://docs.microsoft.com/en-us/dotnet/visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types). A variable such as Bob’s *swimSpeed* holds an actual, concrete value - in this case a number. This will be the case for many of the types we assign to variables, but not all. For some types, most commonly *class instances* and *arrays*, when we declare a variable of one of those types, it will be a *reference*. This means that the variable itself does not hold the concrete data, but instead an address that points to the actual *object*. This has some very important differences in how we can use these variables.

Let’s look at this example code block:
```
{

    Shark bob = new Shark();
    Float speedValue = 11;    
    bob.swimSpeed = speedValue;
    speedValue = 10;
    Debug.Log(bob.swimSpeed);

    Shark anotherBobReference = bob;
    anotherBobReference.swimSpeed = 10;
    Debug.Log(bob.swimSpeed);

}
```

On the first code line, we declare a *reference variable* of type Shark and assign to it the reference to a new instance of the Shark class we create. Second line, we create a new floating point number (a *value type*) variable called speedValue and set in to the value of 11.

Third is where things get a bit tricky. Remember that all *instances* of the Fish class have a field called swimSpeed (which Sharks, being *subclass* of Fish, inherit)? Here we set the field’s value for the Shark instance referenced by the variable ‘bob’ to whatever value is stored in the variable speedValue, in this case 11.

Fifth line, we just assign a new value to the variable speedValue. This will not change the value in shark’s swimSpeed field, so command *Debug.Log(bob.swimSpeed)* will print out in the Unity editor console ‘11’, which is the value we assigned on.

Now becomes the really tricky part: on seventh line, we declare another *reference variable* also type of Shark and set its reference to the same as *bob*. Both of these variables now reference or point to the same *instance* of Shark class (you can this the instance as an individual, actual beign). This means we can set a new value for the Shark’s swimSpeed by accessing the Shark through any of the *references* we have for that Shark instance, in this case *anotherBobReference*. Because both *bob* and *anotherBobReference* point to the same Shark, *Debug.Log(bob.swimSpeed)* will now print out ‘10’. 

Figuring out whether a variable is of value or reference type is tricky at first. Most common reference types are *class instances* and *arrays*, which are marked by brackets following the variable type in declaration (for example, *int[] integerArray*).

# Flow control
Just creating class instances, declaring variables and executing methods will not make for a very interesting game as the game would do exactly the same thing every time it is run. We need tools to give the code decisions to make and alter the flow of code execution based on those decisions. These tools are called the *flow control* and they are what we use to create the game logic for our games, i.e. what should happen in certain situations in our game. Flow control can be divided to three main categories that will be discussed here: selection, iteration and jump statements. 

*Selection statements* are used when we want to execute a part of our code if a certain condition is met, for example if the player is pressing a button. *Iteration statements* let us repeat a code block for multiple times depending on the conditions we define, while *jump statements* let us alter the flow of code execution by jumping forward and ignoring some parts of the code.

Selection and iteration statements operate on *conditions*. A condition is a *statement* that can only have one of two values - *true* or *false*. One example of a statement is ‘2 > 1’ (two is greater than one). This value will always be true, because, well, the statement two is greater that one is always true. The value can be stored to a variable of the type *boolean*, like this:

```
Shark bob = new Shark();
bob.swimSpeed = Random.Range(1, 15); //this is Unity’s built-in method for drawing a random number
bool bobIsFast = bob.swimSpeed > 10; // we are evaluating if the statement bob.swimSpeed is greater than 10 and storing the statement value (true or false)
Debug.Log(bobIsFast); //this will print out true or false depending on what number we drew for bob.swimSpeed;
```

*Conditional statements* can use any variables that are comparable to perform comparisons, like equal, greater than or smaller than. Further multiple *boolean* values can be compared with *logical operators* like **==** (logical EQUAL operator), **&&** (logical AND operator) and **||** (logical OR operator).

## Selection statements

### If - else
Selection statements are literally what the name suggests - depending on a *condition*, we select if we want to execute a certain code block. The most simple example of a selection statement looks like this:

```
if (bobIsFast == true)
{
   Debug.Log(“Wow! Bob is really fast!”);
}
```

First, we have a selection statement *if* followed by a condition in parethesis. In this case we check if the value of variable *bobIsFast* equals *true*. If this is the case, the code inside the following code block is executed. Otherwise, that code block is simply ignored. We could also check for the opposite case:

```
If (bobIsFast == false)
{
   Debug.Log(“Meh. Bob’s kinda slow.”);
}
```

More simple and readable way to do this is to use the *else* keyword:

```
if (bobIsFast == true)
{
   Debug.Log(“Wow! Bob is really fast!”);
}
else
{
   Debug.Log(“Meh. Bob’s kinda slow.”);
}
```

If the condition is true, we execute the first code block, otherwise we ignore that and instead execute the code block after else.

Also, because *bobIsFast* is a *boolea*n which already has a value of true or false, we can write the condition simply like this:

```
if (bobIsFast)
{
   Debug.Log(“Wow! Bob is really fast!”);
}
```

### Switch

Many times we need to handle a situation where a variable can have many different values that we need to react to. Maybe something like this:

```
if (playerName == “Luke”)
{
   Debug.Log(“Nooooooooooo!”);
}
If (playerName == “Han”)
{
   Debug.Log(“I have a bad feeling about this.”;
}
if (playerName == “Leia”)
{
   Debug.Log(“Aren’t you a little short for a stormtrooper?”;
}
If (playerName == “Chewbacca”)
{
   Debug.Log(“RWGWGWARAHHHHWWRGGWRWRW.”);
} 
```

You can see where this is going. It can be a lot of if condition checks and code that becomes hard to read. In these cases it can be easier to use the *switch* statement:

```
switch(playerName) // playerName variable is of type string
{
   case “Luke”:
      Debug.Log(“Nooooooooooo!”);
      break;
   case “Han”:
      Debug.Log(“I have a bad feeling about this.”;
      break;
   case “Leia”:
      Debug.Log(“Aren’t you a little short for a stormtrooper?”;
      break;
   case “Chewbacca”:
      Debug.Log(“RWGWGWARAHHHHWWRGGWRWRW.”);
      break;
   default:
      Debug.Log(“I don’t recognize that name.”);
      break;
}
```

Switch statement formatting differs quite a lot from what we saw in *if-else* statements. Here, the code block starts with statement keyword *switch* and the variable we are comparing different cases against. This most commonly used variable types are *int*, *string* and *enum*. 

Each *case* represent a single value that we are comparing against the variable in *switch* declaration. If variable *value* matches that case, we execute the code on the following lines until a *break* statement. Break means here the end of this specific case and the rest of the code block will be ignored. In *switch* code block we can also define a *default* case that will be executed if none of the previous cases were a match to our variable. If there is no default case defined and none of the cases match, the switch code block simply does nothing.

## Iteration statements

Iteration statements, as the name hints, loop or iterate over a certain block of code as long as some condition is true. These statements give us nice tools to repeat same lines of code for tasks like iterating over all enemies in the game to check if any of them have spotted the player.

### For
For-loop is a staple in practically every programming language. It offers a lot of control over the loop in a relatively simple package:

```
for (int i = 0; i < 10; i++)
{
   Debug.Log(i); // this will print out the value of i in the console 10 times
}
```
 
For statement definition consist of three parts inside the brackets: *initializer*, *condition* and *iterator* - separated with semicolons. In our example the *initializer* declares an *int* variable named *i* and sets its value to 0. *Condition* defines if the following code block should still be executed or if the loop is finished. While the condition is *true*, the loop will continue. Last, the *iterator* is a command that is done each time the for-loop code block has been executed. The example code above sets first i value to 0, evaluates if i is less than 10 and if that is the case executes the following code block. Then 1 will be added to the value of i (i++ is the shorthand for incrementing the value of i by one). Now condition is checked again: value of i is now 1, which is still less than 10 so the code block will be executed again.

After 10 loops, value of *i* will be 10 and the condition statement *(i < 10)* is *false*, so the loop is finished.

### Foreach
For *collections* of items, we have another option for iterating over all items in the collection. This is the *foreach* statement:

```
List<int> numberList = new List<int> {3, 1, 2, 6, 4, 5};
Foreach (int number in numberList)
{
    Debug.Log(number);
}
```

This loop goes over all items in the *numberList*. It starts from the first item, assigns the value to the *temporary variable* called number and executes the code inside the following code block. Then it moves to the next item, assigns that items value to the temporary variable, and so forth.

**Keep in mind that removing or adding items to the collection while iterating over it, is a big no-no and can result in errors that are very hard to identify!**

### While
This document is still a work in progress, for rest of flow control keywords, refer the [official C# documentation](https://docs.microsoft.com/en-us/dotnet/csharp/) for now!


### Do - While


## Jump statements

### Break

### Continue

### Return
