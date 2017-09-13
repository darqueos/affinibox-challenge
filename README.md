# Developer Application - Eduardo Quadros

## Cover Letter

Lorem ipsum...

## Questions

### Git

#### Question 01: What are the steps you need to take before you can clone this project?

After installation, I should set my user profile:

```bash
git config --global user.name "Eduardo Quadros"
git congit --global user.email "quadros.ea@gmail.com"
```

Considering I have access to the repository:

```bash
git clone git@gitlab.com:affinibox-public/dev-candidates.git
```

#### Question 02: How could you create a branch with your name?

To help maintaining code through development, testing and production phases, different branches are used. Usually `master` branch is reserved for production code. This creates a branch based on the latest work from a hypothetical branch named `development`:

```bash
git checkout -b "eduardo" "development"
```

#### Question 03: Create a new file named .txt

As suggested:

```bash
cat > file.txt

Hello, world.

```

#### Question 04: Create a commit with that file

First I need to exclusively add the file so git can track it:

```bash
git add file.txt
```

Then commit to it:

```bash
git commit -m "Add a new text file."
```

#### Question 05: What would be the command to push your branch?

```bash
git push -u origin eduardo
```

The `-u` option will make tracking easier.

#### Question 06: Why would you push your branch?

First and foremost, to avoid losing work. Pushing to remote can spread copies and make it accessible to collaborators.

#### Question 07: Why would a push fail? How would you solve it?

Network; a previous branch with the same name; something messed up with settings... an endless list. To solve it, I need to make sure I can properly push new branches, and that nothing conflicts.

#### Question 08: What would be the command to merge your branch into master?

Since I based my work on `development`, I need to merge my code to it before merging to `master`. But the same principle applies:

```bash
git checkout development
```

And make sure I have the latest work commited to `development`:

```bash
git pull origin development
git merge eduardo
git push origin development
```

#### Question 09: Why would you merge?

To literally add my work to the existing code so collaborators can integrate new features or add bug fixes to production code.

### JavaScript

#### Question 10: What would be the code to get the value of the input from the `event`?

The event produced is called `KeyboardEvent`. To extract a raw value, I would:

```javascript
document.getElementById("foo").onkeypress = (event) => {
    console.log(event.key);
}
```

#### Question 11: What would be the code to get the value of the input from the `event`?

I would grab the `keyCode` property from the event. The **ENTER** key is set to **13**.

```javascript
document.getElementById("foo").onkeypress = (event) => {
    if (event.keyCode == 13) {
        console.log("Enter key pressed.");
    }
}
```

#### Question 12: Use map and filter to convert `'12 as 12 as 12'.split(' ')` to `[12,12,12]`.

First, I convert all strings to numbers:

```javascript
var a = "12 as 12 as 12".split(" ");

a = a.map((element) => {
    return Number(element);
});
```

Which results in `[12, NaN, 12, NaN, 12]`. Now I need to filter numbers:

```javascript
a = a.filter((element) => {
    return !(isNaN(element));
});
```

And there you have it: `[12,12,12]`.

#### Question 13: Answer with the code you wrote.

To extract properties from objects, I must:

```javascript
Object.keys(theObject);
```

I also need to iterate on keys and values to add them to an appropriate position on the new object.

```javascript
theArray.forEach((element) => {
    /* Iterate through elements. */
});
```

The final result is:

```javascript
var a = "[{a: 1}, {b: 2}, {c: 3}]";

a = a.reduce((accumulator, element) => {
    Object.keys(element).forEach((item) => {
        accumulator[item] = element[item];
    });
    return accumulator;
}, {});

console.log(a);
```

Which outputs: `{ a: 1, b: 2, c: 3 }`.

#### Question 14: What will be the printed message? How would you compare the objects `A` and `B`?

It prints "*JavaScript thinks these objects are not equal*" because JS only compares values for primitive types. For any other type it compares using references. Since `A` and `B` are different instances of objects allocated in different memory positions, testing will always result in `false`.

There're tons of ways to compare equality of values in objects, but I'd use the function `_.isEqual()` from the [Lodash](https://lodash.com/docs#isEqual) library.

#### Question 15: Answer with the code of your implementation.

As desired:

```javascript
function upperKey(object) {
    let key = (Object.keys(object))[0];
    let value = (Object.values(object))[0];
    let newObject = {};

    newObject[key.toUpperCase()] = (typeof(value) === "object")
        ? upperKey(value)
        : value;
    return newObject;
}
```

#### Question 16: Answer with the code you wrote.

Since I was given the choice, I chose the **fetch API** here. It's important to say I strongly dislike jQuery in favor for **VanillaJS**. Also, I've read about Axios and I kind of like it. Maybe I'll use it for future projects.

```html
<script type="text/javascript">
    const URL = "https://jsonplaceholder.typicode.com/posts/1";
    const responseTitleKey = "title"

    fetch(URL).then((response) => {
        response.json().then((data) => {
            console.log(data[responseTitleKey]);
        });
    }).catch((error) => {
        console.log(error);
    });
</script>
```

#### Question 17: Write a simple line of code to show you know `setTimeout`

The function bellow displays an alert after 3 seconds:

```javascript
const sayHello = () => {
    alert("Delayed hello, world!");
}

setTimeout(sayHello, 3000);
```

#### Question 18: Explain what it does

`setInterval` executes a code repeatedly with some time interval in between. `clearInterval` is self-explanatory.

#### Question 19: Write a simple line of code to show you know `setInterval` and `clearInterval`

The block bellow will log numbers to console indefinitely until `cancelRepeat` is called.

```javascript
let count = 0;

const intervalID = setInterval(() => {
    console.log(count++);
}, 2000);

function cancelRepeat(ID) {
    clearInterval(ID);
}
```

#### Question 20: Convert the code above use `Promises` instead of callbacks

I've never wrote any code that uses `Promises`, but after learning about it from the [mentioned article](https://scotch.io/tutorials/javascript-promises-for-dummies) I chose to implement this using ES2017 specification, which includes `async` and `await` keywords that I find are interesting to use:

Here I define some constants:

```javascript
const fs = require("fs");
const fp = "./somefile.txt";
```

Then I create a function to encapsulate the Promise code:

```javascript
async function tryToRead(filepath) {
    return new Promise((resolve, reject) => {
        fs.readFile(filepath, (error, content) => {
            if (error) {
                reject(new Error("Failed to read file."));
            } else {
                resolve(content.toString());
            }
        });
    });
}
```

And then a function to use `try` and `catch`:

```javascript
async function read(filepath) {
    try {
        let content = await tryToRead(filepath);
        console.log(`Found content: ${content}`);
    } catch (error) {
        console.log(error);
    }
};
```

Finally, call the `read` function:

```javascript
read(fp);
```

#### Question 21: What is the resulting phrase?

The program outputs the following to the console:

```bash
Hello Maria, my name is Jimmy
Hello Maria, my name is not Jimmy
```

#### Question 22: How does it work?

The first line is pretty trivial, but the second one works by binding a new value to the `this` scope in `Person`. It replaces the `name` property within the function scope, without actually replacing the value within the class.

### Nodejs

#### Question 23: What file / line you had to change?

I don't know much about **Webpack** as I'd like, so instead I inspected the page to find the hex code for the *gameboy* and then searched for it in the project folder. Then replaced `efcc19` for the *steelblue* color:

```less
// file /src/containers/index.less
// line 84

background: #4682b4;
```

#### Question 24: Show the command to add lodash to this project

The easiest way is to use `npm`:

```bash
npm i --save lodash
```

#### Question 25: `npm` install would know lodash is a dependency on fresh install? If so, how?

No, although I'm not certain. Lodash could be a dependency of another dependency. Anyway, I could add it to `package.json`.

#### Question 26: What is the result of the statement above?

```javascript
{A: 1, B: 2, C: 3}
```

#### Question 27: What is the result of the statement above?

```javascript
{a: 1, b: 2, c: 3}
```

#### Question 28: Implement the function above using lodash and answer with the source

This one took me a lot of effort, because I actually have to deal with: `[{},{},{}]`.

```javascript

const foo = (...args) => {
    return _.chain(input)
            .map((item) => [_.head(_.keys(item)).toUpperCase(), _.head(_.values(item))])
            .fromPairs()
            .value()
}
```

#### Question 29: Add a script to package JSON so that:

First, I create the scrip itself:

```bash
cat > hello.js

console.log("Hello world!");
```

Then I have to add the script to `package.json` for `npm` to be able to find it:

```json
"scripts": {
    "start": "webpack-dev-server --progress",
    "build": "rm -rf ./build/* && webpack --config ./webpack.production.config.js --progress && ls ./build",
    "hello": "node hello.js"
}
```

#### Question 30: Write a code that prints the contents of the env variable

`envTest.js` should look like this:

```javascript
console.log(process.env.MY_VAR);
```

#### Question 31: What is the value of the statement, `__dirname + '/server'`?

It should be the full path for the `server` folder in the system.

#### Question 32: Answer with your code for `readMany`

After a quick glance at `bluebird` docs, I read that `readFileAsync()` throws an error in case of failure:

```javascript
const B = require('bluebird');
const _ = require('lodash');
const fs = B.promisifyAll(require('fs'));
const errorMessage = "<file empty or non-existing>";

const readMany = (...filepaths) => B.all(
    _.map(filepaths, filepath =>
        fs.readFileAsync(filepath)
          .then(content => content.toString())
          .catch(error => errorMessage)
    )
);

readMany('./fileone','./filetwo', './filethree').then(contents => console.log(contents.join('\n')))
```

#### Question 33: Give the npm command to install all the external dependencies

Dependencies are listed as requirements within `myserver.js`.

```bash
npm install express cookie-parser body-parser
```

#### Question 34: Answer with your code for `app.use('/sum', (req, res, next) => { ... })`

First, I have to reorder the endpoint callback a few lines up, otherwise it won't call it. Then:

```javascript
app.use("/sum", (req, res, next) => {
    res.json(Number(req.query["a"]) + Number(req.query["b"]));
});
```

### ES2015

#### Question 35: Rewrite `times` in the least number of characters as possible using arrow functions.

Function composition is awesome!

```javascript
const times = t => x => x * t;
```

#### Question 36: What was the command you used?

After creating `file_a.js` and `file_b.js` and put them in a new folder, I had install babel using a specific preset:

```bash
npm install --save-dev babel-cli babel-preset-es2015
```

Use **Babel** to transpile files:

```bash
node_modules/.bin/babel . -d ./dist
```

All I have to do to make sure it all works is run:

```bash
node file_b.js
```

#### Question 37: Will the code above work?

Yes!

#### Question 38: Why to import just `map`?

I'm just gonna quote Bruce from [Stackoverflow](https://stackoverflow.com/questions/35250500/correct-way-to-import-lodash):

*`import _map from 'lodash/has'` is better because lodash holds all it's functions in a single file, so rather than import the whole 'lodash' library at 100k, it's better to just import lodash's `_map` function which is maybe 2k.*

#### Question 39: Answer with your implementation of `arrTimes`

It's for functionalities like these that the beauty of functional programming stands out:

```javascript
const arrTimes = (multiplier, ...args) => {
    return args.map((element) => {
        return multiplier * element;
    });
}

const test = arrTimes(10, 1, 2, 3, 4);
console.log(test);
```

### React

#### Question 40: In a few words, what is React?

React is a JavaScript library for building interfaces. Its strenght is component based and the virtual DOM diff algorithms.

#### Question 41: In a few words, what is React Native?

React Native is a framework to build Android and iOS apps using JavaScript and works very similarly to React. It's different from typical hybrid framworks because it compiles JS to native code. I've never used it, but the fact that Instagram, Airbnb and even Tesla are using it is reason enough to pay attention.

#### Question 42: For all the methods of the class above, answer the questions:

##### Constructor 
1. It provides a way to execute something before the component initialization.
2. props - An object containing state.
3. This is used when the component will initialize with some state.

##### ComponentWillMount
1. It's called before `render()`.
2. None.
3. It's the only hook called if one's doing server rendering.

##### ComponentDidMount
1. Called immediately after the component is mounted.
2. None.
3. Great for doing network requests, as setting new state will trigger a re-rendering.

##### ComponentWillUnmount
1. Called before umnounting and the component gets destroyed.
2. None.
3. Used to perform any cleaning.

##### ComponentWillReceiveProps
1. Called before a mounted component gets new props.
2. nextProps - object containing the state to get updated.
3. To compare state changes.

##### ShouldComponentUpdate
1. Is called before rendering when new props or state are being received.
2. nextProps, nextState
3. Useful to tell React a component do not need to re-render after an update. Note that a render may still occur.

##### Render
1. It puts everything together and returns a component or an actual DOM element.
2. No parameters here.
3. It's required.

### SQL

#### Question 43: a `SELECT` statement that reads all the `TradingNames` of the `AffinityGroup`
#### Question 44: a `SELECT` with `JOIN` that reads all the `Name`s of the owners of an `AffinityGroup`
#### Question 45: the statement that reads all the `Name`s of Users that are not owners of an `AffinityGroup`:
#### Question 46: the first select ordering by `AffinityGroup`.`TradingName`
#### Question 47: a query that returns only the first letter of the name and the full surname for every user

### Linux

#### Question 48: What would be the command to open all css files in a folder using Sublime from terminal using the commands above?

I'd build a regex to match all CSS extensions.

```
"*.(css|sass|scss|less)"
```

And then attach it to the `find` command:

```bash
find /a_folder -type f -regextype "posix-extended" -iregex "*.(css|sass|scss|less)" | xargs subl
```

#### Question 49: What would be the command to access `root` on `192.168.1.10` on port `2222`?

It's:

```bash
ssh root@192.168.1.10 -p 2222
```

#### Question 50: Based on the examples above, what would be command to change `white` to `aliceblue` in all CSS files in a folder?

I would combine the previous command to find all CSS files within a folder:

```bash
find /a_folder -type f -regextype "posix-extended" -iregex "*.(css|sass|scss|less)"
```

To the command to replace text within a file:

```bash
find /a_folder -type f -regextype "posix-extended" -iregex "*.(css|sass|scss|less)" -exec sed -i 's/times/vezes/g' "{}" \;
```

### Docker

#### Question 51: In your own words, what is a container and why to use it?

A container is basically an alternative to virtual machines for isolated environments. It runs on the same kernel and filesystem as the host OS, so it requires a lot less space and RAM.

#### Question 52: In your own words, what is Docker?

Docker is a container platform, and its power comes from the Dockerfile, an intuitive way to handle configuration.

#### Question 53: How to this Dockerfile so instead of copying `node_modules` from the local machine it installs using `npm`.

By replacing line 9 for:

```Dockerfile
RUN npm install
```

#### Question 54: Knowing the above, answer with the command to start a `Postgres` container on your machine at port `5432`.

```bash
docker run -p 5432:5432 -e POSTGRES_PASSWORD=mysecretpassword postgres
```

#### Question 55: What was the variable and what was it's value?

The variable was `POSTGRES_PASSWORD` and its value was `mysecretpassword`.

#### Question 56: What would be the command to start a mysql instance?

```bash
docker run -p 3306:3306 -e MYSQL_ROOT_PASSWORD=mySecretPassword mysql
```

### Kubernetes

#### Question 57: Explain what is kubernetes in your own words? (portuguese, if needed)

From what I learned, Kubernetes is a container orchestration platform. It can be used to clusterize containers, managing scaling, individual configuration, and monitoring data.

### CSS

#### Question 58: What is the color of the text of the `a` element?

Following the CSS specificity order, the `<a>` element will inherit color from:

```css
#root a {
    color: green;
}
```

#### Question 59: How to make it so the items are in a column and it look like:

I simply added these lines to `.my-menu` class:

```css
flex-direction: column;
justify-content: space-between;
```

#### Question 60: How to make it so the items are centralized on the page with the space around them, like:

The CSS will look like this:

```css
.my-menu {
    display: flex;
    height: 100%;
    width: 100%;
    flex-direction: column;
    justify-content: center;
}

.my-link {
    display: flex;
    justify-content: center;
}
```

### English

No problem! I would like to take the time to thank you for a concise test. Looking forward to hearing from you and possibly get a feedback. Regards!
