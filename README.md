##S04 Code Smells

Group Members:
Liya Zhu
Anna Zhang
Desi Herrerias
Rheann Kunita

###Introduction: 

###Code Smell #1: Long Parameter List
A function that requires too many parameters from existing data structures. It arises by trying to pass everything needed by the function as a parameter, keep increaseing parameter list as program grows, or trying to pass data indivially instead of pass them as an object. This will cause the function hard to call with higher risk of mistakes, and low readability.

Prevention/Refactoring:
Pass parameter by object instead of passing parameter indivially.
Replace parameter with query.
Use global variable can prevent long parameter list but will cause another code smell Global Data.

Examples:



###Code Smell #2: Duplicated Code:
The same/similar code structure exists in multiple difference instances throughout the code. When making structural changes, these duplicated structures need to be all altered individually. By refacotring the duplicated code into an object, function, method, etc, the code can easily be modified by making the change in only a single location rather than in multiple locations throughout the program.


Prevention/Refactoring:
Pull up method - Define method used multiple times thorughout the code earlier, so that later portions of code can reference the method. 

Example # 1 - 
Language: p5.js

fill(colors[get_random_color()]); 
The line above is repeated in multiple locations throughout the project. The line changes the fill color to a random value choosen from the colors[] list. The code can be refactored by creating the following function:

function set_random_color(){
  fill(colors[get_random_color()]); 
}

Even though this change won't save any lines of code, in fact it technically adds 3 extra lines, it makes the code more readable by replacaing every instance of 

fill(colors[get_random_color()]);

with a simple function call:

set_random_color();

Additionally, if changes need to made to how a color is randomly generated, only a single function needs to be changed compared to changing every single instance of 
fill(colors[get_random_color()]); 

