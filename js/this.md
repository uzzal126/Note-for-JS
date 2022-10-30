### What is this?
* নরমাল ভাবে this সাধারণত window/global অবজেক্ট কে refer করে।
* যখন কোনো একটা মেথড কে কোন একটা অবজেক্ট থেকে কল করা হয় তখন this ঐ অবজেক্ট কে refer করে 
* কোন একটা function এর ভিতরে this সাধারণত window/global অবজেক্ট কে রেফার করে।
* strict mode এ function এর ভিতরের this মূলত undefined
* Arrow function এর নিজের কোনো this নেই, সে মূলত তার parent এর this use করে। 
সরাসরি Arrow function এর this মূলত window/global অবজেক্ট কে রেফার করে।
তবে কোন একটা normal function এর ভিতরে যদি arrow  function ব্যবহার করা হয় তাহলে সেই arrow function এর this তার parent Object কে refer করবে। 
কারণ নরমাল বা main function কে কল করা হয়েছে সেই অবজেক্ট এর ভিতরে থেকে 

```
const myObject = {
    myArrowFunction: null,
    myMethod: function () {
        this.myArrowFunction = () => console.log(this);
    }
};

myObject.myMethod()
```

**নোট:** এখানে বিবেচ্য বিষয় হচ্ছে, যে function এ this ব্যবহার করা হয়েছে তাকে মূলত কল করেছে কে। 
যদি তাকে কোনো অবজেক্ট এর ভিতরে কল করা হয়ে থাকে তাহলে this মূলত সেই অবজেক্ট কেই রেফার করবে অন্যথায় this window / global  অবজেক্ট কে রেফার করবে। 

### Javascript: call(), apply() and bind()
যখন কোন একটা outer  function থেকে  this দিয়ে অন্য কোনো Object এর property কে access করতে হয় তখন call, apply অথবা bind ব্যবহার করতে হয়। 
call এবং apply সাধারণত নিজে নিজেই automatic call হয়ে যায়। 
তবে bind মূলত main function টা কেই রিটার্ন করে। সুতরাং প্রয়োজন অনুসারে সেই ফাঙ্কশন টা কে আবার কল করতে হয়। 

call, apply and bind তিনটা মেথড ই প্রথম Argument হিসেবে target Object  টাকে রিসিভ করে এবং this এর ভ্যালু হিসেবে সেই Object টা কে সেট করে দেয়। 

call এবং bind আনলিমিটেড arguments রিসিভ করতে পারে তবে প্রথম argument হিসেবে target Object কেই নিবে। 

আর Call এর সাথে Apply এর মূল পার্থক্য হলো call একাধিক arguments , দিয়ে দিয়ে নিতে পারে কিন্তু Apply মূলত দুইটা আর্গুমেন্ট রিসিভ করতে পারে যার প্রথম টা target Object এবং দ্বিতীয় টা একটা array তবে array এর ভিতরে একাধিক element থাকতে পারে। 

#### Apply vs. Call vs. Bind Examples

#### Call

```
let person1 = {
    firstName: 'Ridwan', 
    lastName: 'Hossain'
};

function myFunc(greeting, age) {
    console.log(`${greeting}, I am ${this.firstName} ${this.lastName} & I am ${age} years old`);
}

myFunc.call(person1, 'Hello', 1);

```


#### Apply

```
let person2 = {
    firstName: 'Ridwan', 
    lastName: 'Hossain'
};

function myFunc(greeting, age) {
    console.log(`${greeting}, I am ${this.firstName} ${this.lastName} & I am ${age} years old`);
}

myFunc.apply(person2, ['Hello', 1]);
```

#### Bind

```
let person1 = {
    firstName: 'Ridwan', 
    lastName: 'Hossain'
};

function myFunc(greeting, age) {
    console.log(`${greeting}, I am ${this.firstName} ${this.lastName} & I am ${age} years old`);
}

let result = myFunc.bind(person1, 'Hello', 1);
result()
```