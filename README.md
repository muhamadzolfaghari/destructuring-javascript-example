# Destructuring javascript example
An example for better use of destructuring in JavaScript.

`Destructuring` can help to reduce the number of codes, but without control data it can become a nightmare!

## An example of destructuring in wrong way

Here use of the destructuring but in the wrong way which leads stop program with an error.

```javascript
const data = null;
const { dataKey } = data;
```

It is necessary to check data in case of be validate, to avoid from error.
Make sure data be valid before doing destructuring an array specifically when you get data from an HTTP request or somewhere is outside your code, such as localStorage which data maybe have nullish value for example, `undefined` or `null` value.

## Destructuring an Array

### An example of an uncontrolled data of `Array` type
The following code has a nullish value which leads stop program with an error.

```javascript
function getFirstSecondThirdAndRest(data) {
  const [first, second, third, ...rest] = data;

  return { first, second, third, rest };
}

getFirstSecondThirdAndRest(null);
```
### Steps of validate an array data

1. Check availability of data
2. Check type of data
3. Check length of array

### An example of a controlled data of `Array` type

```javascript
function getFirstSecondThirdAndRest(data) {
  if (!data) {
    throw new Error("Data are not defined");
  }

  if (!Array.isArray(data)) {
    throw new Error("Data are not an array");
  }

  if (data.length < 4) {
    throw new Error("Data are not have enough members");
  }

  const [first, second, third, ...rest] = data;

  return { first, second, third, rest };
}

getFirstSecondThirdAndRest(null);
```

## Destructuring an Object

Make sure the type of data be valid before doing destructuring an object. In general array also is an object, you have to use `Array.isArray` to get fully certain about the correct object type for incorrect array type.

### An example of an uncontrolled data of `Object` type

The following code has a array value which leads stop program with an error.

```javascript
function extractNameAndFamily(data) {
  const { name, family } = data;

  return { name, family };
}

extractNameAndFamily([]);
```

### Steps of validate an object data

1. Check availability of data
2. Check type of data
4. Check object to have data

### An example of a controlled data of `Object` type

```javascript
function extractNameAndFamily(data) {
  if (!data) {
    throw new Error("Data are not defined");
  }

  if (typeof data !== "object" || Array.isArray(data)) {
    throw new Error("Data are not an object");
  }

  const { name, family } = data;

  if (![name, family].filter(Boolean).length) {
    throw new Error("Data are not have enough keys");
  }

  return { name, family };
}

extractNameAndFamily([]);
```

## Keep code out of error!
The double question mark, or `??` and set default data, are allowed you to have control on a nullish data which means you safety destructuring an object or array without encountering with any errors.

Take this into account, this method is only useful when the strict on data existence doesn't matter but for better coding let others know what happening to your code when set invalid data.

### An example of a controlled data with define default value

```javascript
const [first, second, third, fourth] = data ?? [];
const [name, family, age, id] = data ?? {};
```
