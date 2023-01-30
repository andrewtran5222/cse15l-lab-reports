# Lab Report 2
Welcome to CSE 15L Lab Report 2. This week we're dealing with servers. Yeah, real hackerman stuff. 

## Part 1
I set up the `StringServer.java` file to run on my computer at `localhost:5222`. I input the link `http://localhost:5222/add-message?s=hello`, as seen at the top.

![Image](Lab2sc1.PNG)

I did it again, but this time with the input link `http://localhost:5222/add-message?s=hello%20again`.

![Image](Lab2sc2.PNG)

**Which methods in your code are called?**
There are the `handleRequest`, `getPath`, `equals`, `format`, `contains`, and the `main` methods. 

**What are the relevant arguments to those methods, and the values of any relevant fields of the class?**
* `handleRequest`: Takes the `(URI url)` argument, which takes entire URL as an input. There is a string named `line` which initializes as an empty string but will later be modified to be the input to the `format` method. 
* `equals`: Takes in a string as an argument and compares it to the current string.
* `format`: Formats a string with formatting methods and is returned to the server.
* `contains`: Checks if a string contains a certain substring (the argument).

**How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.**
The value of `url` doesn't change, it represents the input from the user, and is then picked apart.
The `line` value changes based on the input if the correct path and query is provided. It updates based on the query and adds a line break to the end. 

## Part 2
I chose to look at the `averageWithoutLowest` function. 
Input 1 and 2 are working inputs, but input 3 is a failure-incuding input.

![Image](Lab2sc3.PNG)
![Image](Lab2sc4.PNG)

The method as it is written records the value of the lowest number, but not the index, meaning that if there are multiple values of the lowest number, they will all not be included in the sum that calculates the average, leading to a lower average than expected. (It should only remove 1 number.)

The method before is as follows: 
 ```
 static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    for(double num: arr) {
      if(num < lowest) { lowest = num; }
    }
    double sum = 0;
    for(double num: arr) {
      if(num != lowest) { sum += num; }
    }
    return sum / (arr.length - 1);
  }
 ```
 After: 
   static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    int lowestIndex = 0;
    for(int i = 0; i < arr.length; i++) {
      if(arr[i] < arr[lowestIndex]) { lowestIndex = i; }
    }
    double sum = 0;
    for(int i = 0; i < arr.length; i++) {
      if(i != lowestIndex) { sum += num; }
    }
    return sum / (arr.length - 1);
  }
```
This way the method ensures it doesn't count the index with the lowest value in it, not all indexes with the lowest value. 

# Part 3
* One thing I learned was that the `assertEqualsDouble` method with the argument `(double expected, double actual)` is actually deprecated, with the argument `(double expected, double actual, double index)` being preferred instead. I'm not entirely sure what the index represents yet, but I used it for now. 
* Another thing I learned was that inputting a space into a query gets it converted into %20, the ASCII code for space, in some formats, since spaces aren't typically allowed. 
