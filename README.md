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

There're tons of ways to compare equality of values in objects, but I'd use the function `isEqual()` from the [Lodash](https://lodash.com/docs#isEqual) library.

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

I've never wrote any code that uses `Promises`, but after learning about it from the [mentioned article](https://scotch.io/tutorials/javascript-promises-for-dummies) I chose to

```javascript
const fs = require('fs');

const reader = (filepath, callback) => fs.readFile(filepath, (err, content) => {
    if (err) {
        console.error('Failed to read files');
        return callback('');
    }
    return callback(content.toString());
});
reader('./somefile.txt', (content) => {
    //Reader always returns a string, an empty one if it can't read the file
    console.log(`Found content: ${content}`);
})
```
