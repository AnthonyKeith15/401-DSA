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
