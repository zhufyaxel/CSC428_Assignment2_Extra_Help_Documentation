Extra Help Documentations for Assignment 2
====
Overview
---
This is an extra documentations for Assignment 2, to answer some common questions for the assignment 2's code. Most of the questions came from students' emails to TAs, further updates might be updated here.

Basic Level
---
Here I will use a very naive and useless case to show how the basic coding things work under this project, in order to keep the fairness for those people already figured out and started their works. The example case is:

1. Record how many times user press keys during each session
2. After ending each session, reset pressed time and recording which session it is.

### How to add extra variables for my projects？

In the life circle of this project, everything is object orientated and every usable variables will be better defined within class. You can still define global variables but this might make tons of unwanted issues, or makes the system more difficult to run. 

Since most of the events happened in the `Watch.js`, I would recommand you to define most of the variables you want to use in this class. The first thing to do is find the constructor and adding your variables like:

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

Since everything is in an OOP structure, if you want to define or use a variables, YOU CAN'T ONLY CALL ITS NAME, instead you have to define where this thing came from. `this` here means the variables are defined in this class. And you have to use the `this` here once you are using the parameters also in this class

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

Here as mentioned above, the `keyPressedTimes` needs you to claim where this variables came from, so once you want to use this variable in the `watch.js`, you have to use `this.state.keyPressedTimes` to claim where this variables came from

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

I think this should make sense and even you don't know how to write code, just following what is going on here you can also make things work.

Some of you may not know what JSON is, please check the reference [here](https://www.json.org/)

Common Questions
---
## Seems like Textarea can't update the input once going to next session?

Many of you finded the `<TextArea inputChar={this.state.inputChar}/>` line but can't figure out why after set inputChar into nothing, this area still have something to show up.

The reason is that the actually thing is this line will pass the `inputchar` into `textarea.js`, and the actual displayed input phrase is defined in the `textarea.js`, **NOT MEANS RENDER `inputchar` here**, considering the following ways to solve this issue:

1. Define a variable called `this.state.displayText`, figure out how to update this variable, and replace the `<TextArea \>` line with `<label>{this.state.displayText}<\label>`, and figure out how to typesetting the HTML

2. Figure out what is going on with `textarea.js` and figure out a way to reset `displayText` variable within the scope

## Swipe not working so well with my phone

Considering replace all the swipe event behaviors into `delete`, there are two events you have to edit if you want to do so, one is defiend in `keyboard.normal.js` and another in `keyboard.wip.js`

## Text is too small in my watch

Change the index.css and figure out how to apply this features in `watch.js`. Google and stackoverflow (sometimes W3School) are your best friends for those questions

## This React project is too terrible and I want to write my own

This is up to you, but no extra scores will be applied here for the A2 itself.

However, if you really did a totally new version and be prode of your progress, feel free to deliver an email to us.

## Any other suggestions

I will recommand you to clean up your data and do some basic calculations before you save data to files, as after coding and user study, you may believe you almost did everything. But you have to do the data analysis to get scores. If all the files are named as same file name and no extra informations you can use to derive what you need, that will be another nightmare time for you to clean up them.


