# [Script used for vscode setup](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbU10WDBZSnJDMnhjTXdDMG1FRENfV19yQzNEQXxBQ3Jtc0tuQURYNGwwVG1MUk5tVzNCQTNyek9VVHRtbVZjLVRacDdCeDhqRklkTXR5UzI5MUptS1NGVlgwZ3RrSFlDcWo4Z0k0ZWNYRDk1SDdKR3VOV2VyR1Q1aGFWNzlWSExGY25Ra0RPRVFvaDJ5bVREbHBoOA&q=https%3A%2F%2Ftakeuforward.org%2Fset-up%2Fhow-to-set-up-visual-studio-code-for-c-cp-and-dsa%2F&v=h3uDCJ5mvgw)

```json 
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Compile and run",
      "type": "shell",
      "command": "",
      "args": [
        "copy",
        "\"${file}\"",
        "${workspaceFolder}\\jspwTest.cpp",
        "&&",
        "g++",
        "jspwTest.cpp",
        "-o",
        "jspwTest",
        "&&",
        "jspwTest",
        "<",
        "input.txt",
        ">",
        "output.txt",
        "&&",
        "del",
        "jspwTest.exe",
        "&&",
        "del",
        "jspwTest.cpp"
      ],
      "presentation": {
        "reveal": "never"
      },
      "group": {
        "kind": "build",
        "isDefault": true,
      },
      "problemMatcher": {
        "owner": "cpp",
        "fileLocation": [
          "relative",
          "${workspaceRoot}"
        ],
        "pattern": {
          "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning|error):\\s+(.*)$",
          "file": 1,
          "line": 2,
          "column": 3,
          "severity": 4,
          "message": 5
        }
      }
    }
  ]
}
```

set default terminal to cmd first
# basic input and output 

```c++
// getting a whole line as input 
#include <iostream> 
#include <string> 
int main(){
	std::string testInput; 
	std::getline(std::cin, testInput); 
	std::cout << testInput << std::endl; 
}
```

# Time complexity 

## 3 rules for time complexity 

1. time complexity should be expressed in terms of the worst case scenario. 
2. avoid constants 
3. avoid lower values

Time complexity is the rate with which the time taken to execute a code snippet increases. we use big O notation to express time complexity. it is the measure of amount of time taken for an algorithm to run as a function of it's input size. 

## for competitive programming 

most servers on competitive programming platforms take 1second to execute 10^8 operations. If the time limit given is 1second, your code should execute roughly in O(10^8). Substitute the input size given in the question into your time complexity to check. 

if the time limit is 5 seconds, your code should execute in 5 * O(10^8) and so on. 

# Space complexity 

Never do anything to the input!! It might take less space but is not worth it. You should not modify the input that is given to you. use a separate variable to store manipulations 

space complexity describes the amount of memory used by a snippet of code. denoted using big O notation 

space complexity = auxiliary space (space used to solve the problem) + input space (space used to store the input)






