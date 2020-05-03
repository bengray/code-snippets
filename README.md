# CODE SNIPPETS
Collection of useful, generic code snippets.  I didn't come up with all these. I found some, made some; use as you see fit.

## Common regex patterns
### Valid Email:
```/\b[\w.!#$%&’*+\/=?^`{|}~-]+@[\w-]+(?:\.[\w-]+)*\b/```

### Valid IPv4 address
```/\b(?:(?:25[0-5]|2[0-4]\d|[01]?\d\d?)\.){3}(?:25[0-5]|2[0-4]\d|[01]?\d\d?)\b/```

### Alpha-numeric, literals, digits, lowercase, uppercase
```
\w                //alpha-numeric only
[a-zA-Z]          //literals only
\d                //digits only
[a-z]             //lowercase literal only
[A-Z]             //uppercase literal only
```

## Arrays
### Check if arrays are equal
```
const areEqual = arr => arr.length > 0 && arr.every(item => item === arr[0]);
// areEqual([1, 2, 3, 4]) === false
// areEqual(['hello', 'hello', 'hello']) === true
```

### Convert array of strings to an array of numbers
```
const toNumbers = arr => arr.map(x => +x);
// toNumbers(['2', '3', '4']) returns [2, 3, 4]
```

### Find length of longest string in an array
```
const findLongest = words => Math.max(...(words.map(el => el.length)));
// findLongest(['always','look','on','the','bright','side','of','life']) === 6;
```

### Flatten an array
```
const flat = arr => arr.reduce((a, b) => Array.isArray(b) ? [...a, ...flat(b)] : [...a, b], []);

// Or
const flat = arr => arr.flat();

// flat(['cat', ['lion', 'tiger']]) returns ['cat', 'lion', 'tiger']
```

### Get a random item from an array
```
const randomItem = arr => arr[(Math.random() * arr.length) | 0];
```

### Get the average from an array
```
const average = arr => arr.reduce((a, b) => a + b, 0) / arr.length;
```

### Get the unique values from an array
```
const unique = arr => [...new Set(arr)];
```

### Creating an array mapping
Imagine two arrays of objects. Each object has a unique 'id' value.

You need to iterate through each array, and compare each object in the FIRST array with its
matching item in the SECOND array.  You _could_ iterate through the first array, and then inside
that for-loop you could then iterate through the second array.  But this is bad.

Instead, build a key map of the second array, then you only need to step through each array once.

 ```
const arrayOne = [
    {
        id: '123',
        name: 'ben'
    },
    {
        id: '456',
        name: 'joe'
    }
];

const arrayTwo = [
    {
        id: '123',
        name: 'ben'
    },
    {
        id: '456',
        name: 'joe'
    }
];

function createHashMap({array, key}) {
    const keyMap = {};
    array.forEach(element => {
        keyMap[element[key]] = element;
    });
    /*
    *   returns an object like this
    *   {
    *       123: {id: '123', name: 'ben'},
    *       456: {id: '456', name: 'joe}
    *   }
    */
    return keyMap;
}

const arrayTwoMap = createHashMap({
    array: arrayTwo,
    key: 'id'
});

// iterate through the first array
arrayOne.forEach(item => {
    // Add a check to make sure the item exists in arrayTwo
    if (arrayTwoMap[item.id]) {

        compareTheItemsInEachArray(item.name, arrayTwoMap[item.id].name) // first arguemnt is the "name" from the first array, second argument is the same key from the second array.
    }
})
```

## Numbers
### Check if a number is prime
```
const isPrime = num => (num > 1) && Array(Math.floor(Math.sqrt(num)) - 1).fill(0).map((_, i) => i + 2).every(i => num % i !== 0);
```

### Check if a number is a power of two
```
const isPowerOfTwo = number => (number & (number - 1)) === 0;
// isPowerOfTwo(256) === true
// isPowerOfTwo(129) === false
```

### Compute greatest common denomitator between two numbers
```
const gcd = (a, b) => b === 0 ? a : gcd(b, a % b);

// gcd(10, 15) === 5
```

### Convert a string to a number
```
const toNumber = str => +str;
// toNumber('42') === 42
```

### Generate random number within a range
```
const random = (min, max) => Math.floor(Math.random() * (max - min + 1)) + min;
```

### Prefix an integer with zeroes
```
const prefixWithZeros = (number, length) => String(number).padStart(length, '0');

// prefixWithZeros(42, 5) === '00042'
```

## Strings
### Capitalize a string
```
const capitalize = str => `${str.charAt(0).toUpperCase()}${str.slice(1)}`;
// capitalize('hello world') === 'Hello world'
```

### Capitalize the first letter of each word in a sentence
```
const uppercaseWords = str => str.split(' ').map(w => `${w.charAt(0).toUpperCase()}${w.slice(1)}`).join(' ');
// uppercaseWords('hello world') === 'Hello World'
```

### Check if a string contains whitespace
```
const containsWhitespace = str => str => /\s/.test(str);
// containsWhitespace('hello world') === true
```

### Check if a string is lowercase
```
const isLowerCase = str => str === str.toLowerCase();
```

### Check if a string is uppercase
```
const isUpperCase = str => str === str.toUpperCase();
```

### Get file extension from a file
```
const ext = fileName => fileName.split('.').pop();
```

### Get the file name from a URL
```
const fileName = url => url.substring(url.lastIndexOf('/') + 1);
// fileName('http://domain.com/path/to/document.pdf') === 'document.pdf'
```

### Remove spaces from a string
```
const removeSpaces = str => str.replace(/\s/g, '');

// removeSpaces('hel lo wor ld') === 'helloworld'
```

### Replace all line breaks with <br> elements
```
const nl2br = str => str.replace(new RegExp('\r?\n', 'g'), '<br>');

// In React
str.split('\n').map((item, index) => <React.Fragment key={index}>{item}<br /></React.Fragment>)
```



## MISC

### CSS Hack to highlight nested divs
```
* { background-color: rgba(255,0,0,.2); }
* * { background-color: rgba(0,255,0,.2); }
* * * { background-color: rgba(0,0,255,.2); }
* * * * { background-color: rgba(255,0,255,.2); }
* * * * * { background-color: rgba(0,255,255,.2); }
* * * * * * { background-color: rgba(255,255,0,.2); }
* * * * * * * { background-color: rgba(255,0,0,.2); }
* * * * * * * * { background-color: rgba(0,255,0,.2); }
* * * * * * * * * { background-color: rgba(0,0,255,.2); }
```

### Check if code is running in Node.js
```
const isNode = typeof process !== 'undefined' && process.versions != null && process.versions.node != null;
```

### Check if code is running in the browser
```
const isBrowser = typeof window === 'object' && typeof document === 'object';
```

### Emulate a dice throw
```
const throwdice = () => ~~(Math.random() * 6) + 1;
// throwdice() === 4
// throwdice() === 1
// throwdice() === 6
```
