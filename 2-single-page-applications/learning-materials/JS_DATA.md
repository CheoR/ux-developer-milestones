# Working with Data

As software developers, our job is to work with data. We need to take raw data, and present it to humans in a way that they can understand it, and make decisions with it. Raw data is completely unusable, because modern systems are built on what's called tabular data, or normalized data.

In essence, spreadsheets.

We've all seen a spreadsheet before. Columns represent the values for each type of data we're collecting, and the rows represent the collection of **all** the data for each segment of our observations. In the spreadsheet below, we see data about rainfall over a ten year span.

![](./images/tabulardata.png)

In JavaScript, we can't create spreadsheeets, but we can represent their structure using arrays and objects.

## Arrays

Each row of data in the spreadsheet above is an array. A collection of data values.

```js
const _1948 = [3.4, 3.8, 4.0, 3.9, 3.5, 3.6, 3.6]
const _1949 = [4.3, 4.7, 5.0, 5.3, 6.1, 6.2, 6.7]
const _1950 = [6.5, 6.4, 6.3, 5.8, 5.5, 5.4, 5.0]
const _1951 = [3.7, 3.4, 3.4, 3.1, 3.0, 3.2, 3.1]
const _1952 = [5.8, 6.4, 6.7, 7.4, 7.4, 7.3, 7.5]
```

Then we can create a new array to store each row so that we have one collection that we can reference to get the raw data.

```js
const RainfallDatabase = [_1948, _1949, _1950, _1951, _1952]
```

This kind of storage is useful if we want to use functions to filter, average, summarize, or mean the data.

```js
// Copy this entire code example into a Quokka project
const _1948 = [3.4, 3.8, 4.0, 3.9, 3.5, 3.6, 3.6]
const _1949 = [4.3, 4.7, 5.0, 5.3, 6.1, 6.2, 6.7]
const _1950 = [6.5, 6.4, 6.3, 5.8, 5.5, 5.4, 5.0]
const _1951 = [3.7, 3.4, 3.4, 3.1, 3.0, 3.2, 3.1]
const _1952 = [5.8, 6.4, 6.7, 7.4, 7.4, 7.3, 7.5]

const RainfallDatabase = [_1948, _1949, _1950, _1951, _1952]

// Find out how much total rain has fallen over last 10 years
const allRainfall = RainfallDatabase.reduce(
  function(currentSet, nextSet) {
    return currentSet.concat(nextSet)
  }
).reduce(
  function(total, monthlyRainfall) {
    return total + monthlyRainfall
  }
)

console.log(allRainfall)
```

But if we want to look at specific years, we don't have a way of identifying a single set of data, e.g. get all rainfall for 1952.

## Objects and Arrays for Data

Let's combine objects, which will allow us to provide key names in order to identify the data, and arrays, which will hold the data sets themselves.

```js
const RainfallDatabase = {
  "1948" : [3.4, 3.8, 4.0, 3.9, 3.5, 3.6, 3.6],
  "1949" : [4.3, 4.7, 5.0, 5.3, 6.1, 6.2, 6.7],
  "1950" : [6.5, 6.4, 6.3, 5.8, 5.5, 5.4, 5.0],
  "1951" : [3.7, 3.4, 3.4, 3.1, 3.0, 3.2, 3.1],
  "1952" : [5.8, 6.4, 6.7, 7.4, 7.4, 7.3, 7.5]
}
```

We still have all the data, and although the calculations needed to perform the total rainfall for all 10 years would have different syntax, we can still do it.

```js
// Copy this entire code example into a Quokka project
const RainfallDatabase = {
  "1948" : [3.4, 3.8, 4.0, 3.9, 3.5, 3.6, 3.6],
  "1949" : [4.3, 4.7, 5.0, 5.3, 6.1, 6.2, 6.7],
  "1950" : [6.5, 6.4, 6.3, 5.8, 5.5, 5.4, 5.0],
  "1951" : [3.7, 3.4, 3.4, 3.1, 3.0, 3.2, 3.1],
  "1952" : [5.8, 6.4, 6.7, 7.4, 7.4, 7.3, 7.5]
}

/*
  Don't worry about understanding this code, it is here for
  display purposes only. That said, taking time to *try* to
  understand this code would be encouraged. Talk to the staff.
*/
yearlyRainData = [].concat
    .apply([], Object.values(RainfallDatabase))
    .reduce((sum, monthlyRainfall) => sum + monthlyRainfall)

console.log(yearlyRainData)
```

But now we can look at total rainfall per year since each set of data has a key (i.e. 1948, 1949, 1950, etc...).

```js
// Copy this entire code example into a Quokka project
const RainfallDatabase = {
  "1948" : [3.4, 3.8, 4.0, 3.9, 3.5, 3.6, 3.6],
  "1949" : [4.3, 4.7, 5.0, 5.3, 6.1, 6.2, 6.7],
  "1950" : [6.5, 6.4, 6.3, 5.8, 5.5, 5.4, 5.0],
  "1951" : [3.7, 3.4, 3.4, 3.1, 3.0, 3.2, 3.1],
  "1952" : [5.8, 6.4, 6.7, 7.4, 7.4, 7.3, 7.5]
}

for (let year in RainfallDatabase) {
  console.log(year, RainfallDatabase[year].reduce((s, r) => s + r))
}
```



