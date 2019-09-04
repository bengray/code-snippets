# code-snippets
Collection of useful, generic code snippets

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

## Creating an array mapping
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

## CSS Hack to highlight nested divs
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