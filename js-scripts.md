# JavaScript Snippets

### 1. Updating objects in an immutable way
**Includes: Destructuring Assignment, Spread operator, Immutable objects, Mutating immutable objects**
```javascript
const meal = {
  description: 'Dinner',
};
// 1. In an Immutable way, add a property to the
// meal called calories setting it's value to 200,
// then log the result to the console

const mealWithCalories = {
  ...meal,
  calories: 200
};

console.log(mealWithCalories);

// 2. In an Immutable way, increase the calories
// by 100 and print the result to the console

const mealWithIncreasedCalories = {
  ...mealWithCalories,
  calories: mealWithCalories.calories + 100,
};

console.log(mealWithIncreasedCalories);

// 3. In an Immutable way, remove the calories property and log the result to the console

const {calories, ...mealWithOutCalories} = mealWithIncreasedCalories;


console.log(mealWithOutCalories);
```

### 2. Updating arrays in an immutable way
**Includes: Map function, Filter function, Unnamed function**
```javascript
// 1. Create a constant named friends, which is an array that contains 2 names of your choosing.

const friends = ['Nate', 'Michael'];

// 2. Create a new constant named updatedFriends, which includes the friends array values plus one additional name

const updatedFriends = [...friends, 'Dustin'];

// 3. Create a new constant named friendNameLengths, which is based on the array updatedFriends, but instead of having the friends names, have the array store the length of each persons name.

const friendNameLengths = updatedFriends.map(nameToLength);

function nameToLength (name) {
  return name.length;
}

// 4. Create a new constant named shorterNamedFriends, which will be a list of the friends except the friends with the longest name.
const maxFriendLength = Math.max(...friendNameLengths);

const shorterNamedFriends = updatedFriends.filter(
  function(name){
    return name.length < maxFriendLength ;
  });

// 5. Print each constant to the console.

console.log(friends, updatedFriends, friendNameLengths, shorterNamedFriends);
```

### 3. Summarize information in an array
**Includes: Reduce function, Destructuring Assignment**
```javascript
const grades = [60, 55, 80, 90, 99, 92, 75, 72];

const total = grades.reduce(sum);

function sum(acc, grade){
  return acc + grade;
}

const count = grades.length;

//Passing empty object literal
const letterGradeCount = grades.reduce(groupByGrade, {});

function groupByGrade(acc, grade){
  //Destructuring, unpacks the current grade counts out of the accumulator and into grades a-f. The first time the function is called, the acc will only have an empty object, so there wont be any values for a-f and a will still be undefined. TO handle this we set it equal to a default value of 0 when the letter isn't found in the accumulator.

  const { a = 0, b = 0, c = 0, d = 0, f = 0} = acc;
  if(grade>=90){
    return {...acc, a: a + 1};
  }else if(grade>=80){
    return {...acc, b: b + 1};
  }else if(grade>=70){
    return {...acc, c: c + 1};
  }else if(grade>=60){
    return {...acc, d: d + 1};
  }else{
    return {...acc, f: f + 1};
  }
}

console.log(total, total / count, letterGradeCount);

```

### 4. Summarize information in an array
**Includes: Reduce function, Computed Properties**
```javascript
const reviews = [4.5, 4.0, 5.0, 2.0, 1.0, 5.0, 3.0, 4.0, 1.0, 5.0, 4.5, 3.0, 2.5, 2.0];

// 1. Using the reduce function, create an object that
// has properties for each review value, where the value
// of the property is the number of reviews with that score.
// for example, the answer should be shaped like this:
// { 4.5: 1, 4.0: 2 ...}

const countGroupedByReview = reviews.reduce(groupBy, {});

function groupBy (acc, review){
  const count = acc[review] || 0;
  return {...acc, [review]: count + 1}
}

console.log(countGroupedByReview);
```

### 5. Introduction to currying
**Includes: Reduce function**
```javascript
function greet(greeting){
  return function(name){
    return `${greeting} ${name}`;
  };
}

const friends = ['Nate', 'Jim', 'Scott', 'Dean'];

const friendGreetings = friends.map(greet('Good Morning'));

console.log(friendGreetings);
```

### 6. Introduction to currying
**Includes: Higher-Order functions, Closure**
```javascript
// create transforms to go from studentGrades, to studentFeedback

const studentGrades = [
  {name: 'Joe', grade: 88},
  {name: 'Jen', grade: 94},
  {name: 'Steph', grade: 77},
  {name: 'Allen', grade: 60},
  {name: 'Gina', grade: 54},
];

const messages = {
  a: 'Excellent Job',
  b: 'Nice Job',
  c: 'Well done',
  d: 'What happened',
  f: 'Not good',
};

function letterGrade(points){
  if(points >= 90){
    return 'a';
  } else if (points >= 80){
    return 'b';
  } else if (points >= 70){
    return 'c';
  } else if (points >= 60){
    return 'd';
  } else {
    return 'f';
  }
}

function feedBack(feedBackRules){
  return function(student){
    const grade = letterGrade(student.grade);
    const message = feedBackRules[grade];
    return `${message} ${student.name}, you got an ${grade}`;
  }
}

const gradeFeedback = studentGrades.map(feedBack(messages));

console.log(gradeFeedback);
```
<!-- ### 3. Summarize information in an array
**Includes: Reduce function**
```javascript

``` -->
