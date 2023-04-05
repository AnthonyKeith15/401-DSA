# Challenge Title
Reverse an Array

## Whiteboard Process

![Screenshot 2023-04-03 at 10 07 39 PM](https://user-images.githubusercontent.com/105818064/229692530-7c673e4b-172e-45e2-a0bf-45e6c7309fda.png)



## Approach & Efficiency
I took the for loop approach because I needed to count down a known number of times. The bigO is log(n)

## Solution
```
let revArr = [];
let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

for (let i = arr.length - 1; i >= 0; i--) {
    revArr.push(arr[i]);
}
```

# Challenge Title
Array Insert Shift

## Whiteboard Process

![white-board-2](https://user-images.githubusercontent.com/105818064/229971279-01d0a547-d7a2-43d3-aa85-1d584432ba1b.jpg)




## Approach & Efficiency
I took this approach because I couldnt use splice. I had to use what I knew about arrays to make it happen

## Solution
```
let arr = [2,4,6,-8];

let arr2 = [42,8,15,23,42];

let insertShitArray = (arr, value) => {
  let middleIndex = Math.ceil(arr.length / 2);
    const newArr = new Array(arr.length + 1);

  // Copy the first half of the original array to the new array.
  for (let i = 0; i < middleIndex; i++) {
    newArr[i] = arr[i];
  }

  // Insert the value at the middle index of the new array.
  newArr[middleIndex] = value;

  // Copy the second half of the original array to the new array.
  for (let i = middleIndex; i < arr.length; i++) {
    newArr[i + 1] = arr[i];
  }

  // Return the new array.
  return newArr;

}

insertShitArray(arr, 7);
insertShitArray(arr2, 99)
```

# Challenge Title
binary Search

## Whiteboard Process


![binary-white-board](https://user-images.githubusercontent.com/105818064/230225677-aa7f6d79-1fe2-4906-ad82-2bc6ee74145f.jpeg)



## Approach & Efficiency
This is similar to searching through a dictionary so I just divided the array and half. Then guess and check. Big O is o(log n)

## Solution
```
let sampleArr = [-131, -82, 0, 27, 42, 68, 179];

let otherArr = [4, 8, 14, 16, 23, 42];

function binarySearch(sortedArray, searchKey) {
  let start = 0;
  let end = sortedArray.length - 1;

  while (start <= end) {
    const mid = Math.floor((start + end) / 2);
    const midValue = sortedArray[mid];

    if (midValue === searchKey) {
      return mid;
    } else if (midValue < searchKey) {
      start = mid + 1;
    } else {
      end = mid - 1;
    }
  }

  return -1; // indicates searchKey is not in sortedArray
}

console.log(binarySearch(sampleArr, 42)) // returns 4
console.log(binarySearch(otherArr, 15)) // returns -1
```
