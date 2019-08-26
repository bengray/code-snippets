# code-snippets
Collection of useful, generic code snippets I find

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
    if (arrayTwoMap[item] && arrayTwoMap[item.id]) {

        compareTheItemsInEachArray(item.name, arrayTwoMap[item.id].name) // first arguemnt is the "name" from the first array, second argument is the same key from the second array.
    }
})
```