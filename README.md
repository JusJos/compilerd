# <img alt="Kalvium" src="https://kalvium.community/images/sidebar-2d-logo.svg" width="80"/> Kalvium

---

<!-- [![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url] -->


## Changes Made
Compilerd is an online code judge for evaluating code submissions passed to it. It compiles and executes code in several languages and returns the result and various other properties in the response. The judge supports several languages including C++, Python, C, JavaScript (Node.js) and Java. 

The image was built using docker, used OPEN_API KEYS, Corrected versions of various dependencies, used Postman for query execution, and configured language scripts for support. 

The functionality of GO and PHP are added, and changes are made to the following configs:
app.config.js
language.config.js
test.js
code.services.js


## Quick Usage :
We will run the project locally and try to make a request to see a sample use case :
  - Clone the repo : ```git clone <web-url>```
  - Change directory to the project's root folder.
  - Install dependencies : ```npm install```
  - Build docker image : ```docker build -t <tag> .```
  - Run the docker container with the built image : ```docker run -p 3000:3000 -e OPENAI_API_KEY=<your-api-key> -e ALLOWED_RAM=<allowed-ram-value> <image-name>```
  - Now we have the service running on localhost ```http://localhost:3000/```
  - Open postman and try to make a POST request on ```http://localhost:3000/api/execute/``` with given payload :
  
  - Added to Language.Config:
  ```
  [GO]: {
        compile: 'go build -o solution solution.go',
        run: './solution', // Corrected the run command
        timeout: 10,
        filename: 'solution.go',
        memory: ALLOWED_RAM * ONE_MB,
    },
    [PHP]: {
        compile: null, // PHP is an interpreted language
        run: 'php solution.php',
        timeout: 10,
        filename: 'solution.php',
        memory: ALLOWED_RAM * ONE_MB,
        }
  ```
    

## Languages supported :
  - C
  - CPP
  - Python
  - Java
  - Node.js
  - Ruby
  NEWLY ADDED:
  - GO
  - PHP

### Making changes:
  - Make sure to create a new branch on top of the main branch : ```git checkout -b <name>```
  - After making changes we can commit them using ```git commit -am <commit-name>```


### Running tests : 
  - It is important to make sure that changes are not breaking, hence they should be tested aginst provided suite of test cases in repo.
  - Run the server in a docker container by using below commands :
    - ```docker build -t <tag-name> .```
    - ```docker run -p 3000:3000 -e OPENAI_API_KEY=<your-api-key> -e ALLOWED_RAM=<allowed-ram-value> <image-name>```
  - Execute the test script by running command ```node ./tests/test.js```
  - Summary can be seen on the console when all the tests have finished.


### tests.js :
```
{
        name: 'go: addition',
        reqObject: {
            language: 'go',
            script: `
package main
import "fmt"
func main() {
var a, b int
fmt.Scanf("%d %d", &a, &b)
fmt.Println(a + b)
}`,
            stdin: '5 3',
        },
        expectedResponse: {
            val: '8\n',
            status: 200,
            error: 0,
        },

name: 'php: addition',
        reqObject: {
            language: 'php',
            script: `<?php
fscanf(STDIN, "%d %d", $a, $b);
echo $a + $b;
?>`,
            stdin: '5 3',
        },
        expectedResponse: {
            val: '8',
            status: 200,
            error: 0,
        },

```

