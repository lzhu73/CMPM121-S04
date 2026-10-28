##S04 Code Smells

Group Members:
Liya Zhu
Anna Zhang
Desi Herrerias
Rheann Kunita

### Introduction: 

### Code Smell #1: Long Parameter List
A function that requires too many parameters from existing data structures. It arises by trying to pass everything needed by the function as a parameter, keep increaseing parameter list as program grows, or trying to pass data indivially instead of pass them as an object. This will cause the function hard to call with higher risk of mistakes, and low readability.

Prevention/Refactoring:
Pass parameter by object instead of passing parameter indivially.
Replace parameter with query.
Use global variable can prevent long parameter list but will cause another code smell Global Data.

Example #1:
Language: c++

void createCharacter(string name, int health, int attack,
                     int defense, int speed, int level,
                     int experience);

This function requires too many parameters which makes it hard to read and easy to make mistakes. For example, we might messed up with the parameters that are all the same type.

Fixed Version:
struct Character {
  string name;
  int health;
  int attack;
  int defense;
  int speed;
  int level;
  int experience;
};
void createCharacter(const Character& character);

This makes the function easier to maintain, since we only need to pass one object instead of seven individual parameters. If we want to add more character attributes in the future, we can update the struct without changing the function's parameter list.




### Code Smell #2: Duplicated Code:
The same/similar code structure exists in multiple difference instances throughout the code. When making structural changes, these duplicated structures need to be all altered individually. By refacotring the duplicated code into an object, function, method, etc, the code can easily be modified by making the change in only a single location rather than in multiple locations throughout the program.


Prevention/Refactoring:
Extract Function - Extract repeating section of code from function and make it its own function elsewhere in the code.
Slide Statements - Rearrange code so that sections related to each other are close together.
Pull up - Define method used multiple times thorughout the code earlier, so that later portions of code can reference the method.

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

Example # 2 - 
Language: Python
example from https://dev.to/alexis_jean/avoid-duplicate-code-with-dry-a-simple-python-example-2ke7

def calculate_rectangle_area(width, height):
    area = width * height
    print(f"The area of the rectangle is {area}")

def calculate_square_area(side):
    area = side * side
    print(f"The area of the square is {area}")

def calculate_triangle_area(base, height):
    area = 0.5 * base * height
    print(f"The area of the triangle is {area}")

This group of functions each have a separate print statement that has the shape name hard coded into the print statement, which does work, but makes each statement less reusable. 

The Extract Code method can be utilized by making a separate print shape statement that can be used with all three shape area functions, plus any more that need to be made in the future.

Fixed version

def print_area(shape, area):
    print(f"The area of the {shape} is {area}")

def calculate_rectangle_area(width, height):
    area = width * height
    print_area("rectangle", area)

def calculate_square_area(side):
    area = side * side
    print_area("square", area)

def calculate_triangle_area(base, height):
    area = 0.5 * base * height
    print_area("triangle", area)


