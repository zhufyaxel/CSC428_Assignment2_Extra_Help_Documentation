Extra Help Documentations for Assignment 2
====
Overview
---
This is an extra documentation for Assignment 2. Most of the questions came from students' e-mails to TAs, further updates might be implemented if necessary.

Basic Examples for beginners 
---
To keep fairness for those people already figured out and started their works, here I will use a very naive and useless example to show how the basic coding thing works under this project. The example case is:

1. Recording how many times user press keys during each session
2. After ending each session, reset pressed time and recording which session it is.

### How to add extra variables for my projects？

In the life circle of this project, everything is object orientated, so it will be better to define variables within classes. You can still define global variables, but this might cause tons of unwanted issues, or even mess up the lifecycle of the whole system if you did something wrong.

Since most of the events happened in the `Watch.js`, I would recommend you to define most of the variables you want to use in this class. The first thing to do is find the constructor and adding your variables like:

```javascript
constructor(props){
    //......Something the software already did, ignore them and adding your staffs from this.state, don't delete them unless you know what is going on

    this.state = {
        inputPhrase: "",
        inputChar: "", // above are something already done
        keyPressedTimes: 0 // new variable within the this.state
    };

    this.sessionIndex = 0;// Another new variable, but outside the state scope

}
```

Some of you may not know why you need a "this" here. That symbol is used to define the variables within the scope of the class, and in the Javascript class constructor, you do not need to use a `var` to claim a new variable. (But you still have to use `var` if you want to define a temporary local variable). The symbol `this` here means the variables are defined in this class(`watch.js`). And you have to use the `this` here once you are using the parameters also in this class

### How to update variables after press keys

Within this project there are multiple events happen, but within the `watch.js`, the most powerful event is the `onKeyCharReceived`, which works as its name shows

In our examples, we will do the case as:

```javascript
onKeyCharReceived = (c) => {
    this.setState({inputChar : c});
    this.state.inputPhrase += c; // don't change the above unless you know what ppened here
    this.state.keyPressedTimes += 1;
};

```

Here as mentioned above, the `keyPressedTimes` needs you to claim where this variables came from, so once you want to use this variable in the `watch.js`, you have to use `this.state.keyPressedTimes` to claim this variable is from the current class.

### How to reset variables after press save buttons
```javascript
saveData = () => {
    let log_file = JSON.stringify({
        targetPhrase: this.targetPhrase,
        inputPhrase: this.state.inputPhrase,
        keyPressedTimes: this.state.keyPressedTimes // here I will save this variables
    })
    var fileName = "results_" + this.sessionIndex + ".txt";
    download(log_file, fileName, "text/plain"); // here I using sessionIndex to set the file name, as this is a one time parameters, it can be a temp local variables here.

    //After download, Reset variables here
    this.state = {
        inputPhrase: "",
        inputChar: "", // above are something already done
        keyPressedTimes: 0 // new variable within the this.state
    };

    this.sessionIndex += 1;// update the sessionIndex here
}
```

I think this should be straightforward and even you don't know how to write code, just following what is going on here you can also make things work.

Some of you may not know what JSON is, please check the reference [here](https://www.json.org/)

Common Questions
---
## Seems like Textarea can't update the input once going to next session?

Many of you finded the `<TextArea inputChar={this.state.inputChar}/>` line but can't figure out why after set inputChar into nothing, this area still have something to show up.

What this line did is to pass the `inputchar` into `textarea.js`, rather than render the `inputchar` directly. The displayed input phrase is defined in the `textarea.js`. So consider following ways to solve this issue:

1. Define a variable called `this.state.displayText`, figure out how to update this variable, and replace the `<TextArea \>` line with `<label>{this.state.displayText}<\label>`, and figure out how to typesetting the HTML

2. Figure out what is going on with `textarea.js` and figure out a way to reset `displayText` variable within the scope

## Swipe not working so well with my phone

Consider replacing all the swipe event behaviors into `delete`, there are two events you have to edit if you want to do so, one is defined in `keyboard.normal.js` and another in `keyboard.wip.js`

## Text is too small in my watch

Change the index.css and figure out how to apply those features in `watch.js`. Google and stackoverflow (sometimes W3School) are your best friends for those general html questions

## How I debug my project?
Using `console.log` and open console within your browser when you are running your projects. References: [ref1](https://www.w3schools.com/jsref/met_console_log.asp), [ref2](https://www.google.com/search?q=how+to+open+console+in+chrome)

## This React project is too terrible and I want to write my own

This is up to you, but no extra scores will be applied here for the A2 itself.

However, if you really made a new version of the project and be prode of your progress, feel free to email us.

## Any other suggestions?

I will recommend you to clean up your data and do some necessary calculations before you save data to files, as after coding and user study, you may believe you almost did everything. But you have to do the data analysis to get scores. If all the files are named as the same file name and no extra information you can use to derive what you need, that will be another nightmare time for you to clean up them.


