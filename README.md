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

# Challenge Title
fibonacci sequence 2 ways

## Whiteboard Process

![fibonacci-white-board](https://user-images.githubusercontent.com/105818064/230519005-9fd62a61-dbc4-436b-91f5-ee8e5b0e8d0c.jpeg)


## Approach & Efficiency
I had to google what the fibonacci sequence was. Thankfully ive seen a pattern like that before
big O of recursive is O(2^n)
big O of iterative is O(n)

## Solution
```
function fibonacciRecursive(n) {
  if (n < 2) {
    return n;
  }
  return fibonacciRecursive(n-1) + fibonacciRecursive(n-2);
}

function fibonacciIterative(n) {
  let prev = 0, curr = 1;
  for (let i = 2; i <= n; i++) {
    let next = prev + curr;
    prev = curr;
    curr = next;
  }
  return curr;
}
```

# Challenge Title
Linked List

## Whiteboard Process
![linked-list-whiteboard](https://user-images.githubusercontent.com/105818064/231247440-a02d6327-904f-4c2a-b2ab-5220d17b6028.jpeg)




## Approach & Efficiency
To solve the problem, we will create a linked list with a node class that has a value and a next pointer. We will then implement methods to append nodes to the end of the list, insert nodes before a specific value, and insert nodes after a specific value.

The Time and Space Complexity is O(N)

## Solution
```
class Node {
  constructor(value) {
    this.value = value;  // The value of the node.
    this.next = null;  // The reference to the next node in the list.
  }
}

class LinkedList {
  constructor() {
    this.head = null;  // The first node in the list (also known as the head).
  }

  // This method adds a new node with the given value to the end of the list.
  append(value) {
    const new_node = new Node(value);
    if (!this.head) {  // If the list is empty, make this node the head.
      this.head = new_node;
    } else {
      // Traverse the list until we find the last node (i.e., the one with no next node).
      let current_node = this.head;
      while (current_node.next) {
        current_node = current_node.next;
      }
      // Add the new node to the end of the list.
      current_node.next = new_node;
    }
  }

  // This method adds a new node with the given new_value before the first node with the given value.
  insertBefore(value, new_value) {
    const new_node = new Node(new_value);
    if (!this.head) {  // If the list is empty, we can't insert anything before a value.
      throw new Error("Linked List is empty");
    }
    if (this.head.value === value) {  // If the value to insert before is the head, update the head.
      new_node.next = this.head;
      this.head = new_node;
      return;
    }
    // Traverse the list until we find the node with the value to insert before.
    let current_node = this.head;
    while (current_node.next) {
      if (current_node.next.value === value) {
        // Insert the new node before the node with the given value.
        new_node.next = current_node.next;
        current_node.next = new_node;
        return;
      }
      current_node = current_node.next;
    }
    // If we reach this point, the value to insert before was not found in the list.
    throw new Error(`Value ${value} not found in Linked List`);
  }

  // This method adds a new node with the given new_value after the first node with the given value.
  insertAfter(value, new_value) {
    const new_node = new Node(new_value);
    if (!this.head) {  // If the list is empty, we can't insert anything after a value.
      throw new Error("Linked List is empty");
    }
    // Traverse the list until we find the node with the given value.
    let current_node = this.head;
    while (current_node) {
      if (current_node.value === value) {
        // Insert the new node after the node with the given value.
        new_node.next = current_node.next;
        current_node.next = new_node;
        return;
      }
      current_node = current_node.next;
    }
    // If we reach this point, the value to insert after was not found in the list.
    throw new Error(`Value ${value} not found in Linked List`);
  }
}

module.exports = {LinkedList}
```

## Tests
```
const { LinkedList } = require("./LinkedList.js");

describe("Linked List", () => {
  let linked_list;

  beforeEach(() => {
    linked_list = new LinkedList();
  });

  test("Can successfully add a node to the end of the linked list", () => {
    linked_list.append(1);
    expect(linked_list.head.value).toBe(1);
    expect(linked_list.head.next).toBeNull();

    linked_list.append(2);
    expect(linked_list.head.value).toBe(1);
    expect(linked_list.head.next.value).toBe(2);
    expect(linked_list.head.next.next).toBeNull();
  });

  test("Can successfully add multiple nodes to the end of a linked list", () => {
    linked_list.append(1);
    linked_list.append(2);
    linked_list.append(3);
    expect(linked_list.head.value).toBe(1);
    expect(linked_list.head.next.value).toBe(2);
    expect(linked_list.head.next.next.value).toBe(3);
    expect(linked_list.head.next.next.next).toBeNull();
  });

  test("Can successfully insert a node before a node located in the middle of a linked list", () => {
    linked_list.append(1);
    linked_list.append(2);
    linked_list.append(4);
    linked_list.insertBefore(2, 3);
    expect(linked_list.head.value).toBe(1);
    expect(linked_list.head.next.value).toBe(3);
    expect(linked_list.head.next.next.value).toBe(2);
    expect(linked_list.head.next.next.next.value).toBe(4);
    expect(linked_list.head.next.next.next.next).toBeNull();
  });

  test("Can successfully insert a node before the first node of a linked list", () => {
    linked_list.append(1);
    linked_list.insertBefore(1, 0);
    expect(linked_list.head.value).toBe(0);
    expect(linked_list.head.next.value).toBe(1);
    expect(linked_list.head.next.next).toBeNull();
  });

  test("Can successfully insert after a node in the middle of the linked list", () => {
    linked_list.append(1);
    linked_list.append(2);
    linked_list.append(4);
    linked_list.insertAfter(2, 3);
    expect(linked_list.head.value).toBe(1);
    expect(linked_list.head.next.value).toBe(2);
    expect(linked_list.head.next.next.value).toBe(3);
    expect(linked_list.head.next.next.next.value).toBe(4);
    expect(linked_list.head.next.next.next.next).toBeNull();
  });

  test("Can successfully insert a node after the last node of the linked list", () => {
    linked_list.append(1);
    linked_list.append(2);
    linked_list.insertAfter(2, 3);
    expect(linked_list.head.value).toBe(1);
    expect(linked_list.head.next.value).toBe(2);
    expect(linked_list.head.next.next.value).toBe(3);
    expect(linked_list.head.next.next.next).toBeNull();
  });
});

```

# Challenge Title
Find Kth Element from the end

## Whiteboard Process

![KthIntFromEnd](https://user-images.githubusercontent.com/105818064/231344854-c14193c7-3e2d-4d01-972d-28304eefe8b8.jpg)


## Approach & Efficiency
The approach I used has two counter variables. It loops through the array at different speeds essentially. When the First pointer gets the end the second pointer will be k steps behind that

## Solution
```
class Node {
  constructor(value) {
    this.value = value;  // The value of the node.
    this.next = null;  // The reference to the next node in the list.
  }
}

class LinkedList {
  constructor() {
    this.head = null;  // The first node in the list (also known as the head).
  }

  // This method adds a new node with the given value to the end of the list.
  append(value) {
    const new_node = new Node(value);
    if (!this.head) {  // If the list is empty, make this node the head.
      this.head = new_node;
    } else {
      // Traverse the list until we find the last node (i.e., the one with no next node).
      let current_node = this.head;
      while (current_node.next) {
        current_node = current_node.next;
      }
      // Add the new node to the end of the list.
      current_node.next = new_node;
    }
  }

  // This method adds a new node with the given new_value before the first node with the given value.
  insertBefore(value, new_value) {
    const new_node = new Node(new_value);
    if (!this.head) {  // If the list is empty, we can't insert anything before a value.
      throw new Error("Linked List is empty");
    }
    if (this.head.value === value) {  // If the value to insert before is the head, update the head.
      new_node.next = this.head;
      this.head = new_node;
      return;
    }
    // Traverse the list until we find the node with the value to insert before.
    let current_node = this.head;
    while (current_node.next) {
      if (current_node.next.value === value) {
        // Insert the new node before the node with the given value.
        new_node.next = current_node.next;
        current_node.next = new_node;
        return;
      }
      current_node = current_node.next;
    }
    // If we reach this point, the value to insert before was not found in the list.
    throw new Error(`Value ${value} not found in Linked List`);
  }

  // This method adds a new node with the given new_value after the first node with the given value.
  insertAfter(value, new_value) {
    const new_node = new Node(new_value);
    if (!this.head) {  // If the list is empty, we can't insert anything after a value.
      throw new Error("Linked List is empty");
    }
    // Traverse the list until we find the node with the given value.
    let current_node = this.head;
    while (current_node) {
      if (current_node.value === value) {
        // Insert the new node after the node with the given value.
        new_node.next = current_node.next;
        current_node.next = new_node;
        return;
      }
      current_node = current_node.next;
    }
    // If we reach this point, the value to insert after was not found in the list.
    throw new Error(`Value ${value} not found in Linked List`);
  }

  // This method finds the kth node from the end of the list and returns its value.
findKthFromEnd(k) {
  if (!Number.isInteger(k) || k < 1) {
    throw new Error("k must be a positive integer");
  }
  let slow_pointer = this.head;
  let fast_pointer = this.head;
  for (let i = 0; i < k - 1; i++) {
    if (fast_pointer.next === null) {
      throw new Error(`There is no ${k}th element in the Linked List`);
    }
    fast_pointer = fast_pointer.next;
  }
  while (fast_pointer.next !== null) {
    slow_pointer = slow_pointer.next;
    fast_pointer = fast_pointer.next;
  }
  return slow_pointer.value;
}
}


module.exports = {LinkedList}
```

## Tests
```
const { LinkedList } = require("./LinkedList.js");

describe("Linked List", () => {
  let linked_list;

  beforeEach(() => {
    linked_list = new LinkedList();
  });

  test("Can successfully add a node to the end of the linked list", () => {
    linked_list.append(1);
    expect(linked_list.head.value).toBe(1);
    expect(linked_list.head.next).toBeNull();

    linked_list.append(2);
    expect(linked_list.head.value).toBe(1);
    expect(linked_list.head.next.value).toBe(2);
    expect(linked_list.head.next.next).toBeNull();
  });

  test("Can successfully add multiple nodes to the end of a linked list", () => {
    linked_list.append(1);
    linked_list.append(2);
    linked_list.append(3);
    expect(linked_list.head.value).toBe(1);
    expect(linked_list.head.next.value).toBe(2);
    expect(linked_list.head.next.next.value).toBe(3);
    expect(linked_list.head.next.next.next).toBeNull();
  });

  test("Can successfully insert a node before a node located in the middle of a linked list", () => {
    linked_list.append(1);
    linked_list.append(2);
    linked_list.append(4);
    linked_list.insertBefore(2, 3);
    expect(linked_list.head.value).toBe(1);
    expect(linked_list.head.next.value).toBe(3);
    expect(linked_list.head.next.next.value).toBe(2);
    expect(linked_list.head.next.next.next.value).toBe(4);
    expect(linked_list.head.next.next.next.next).toBeNull();
  });

  test("Can successfully insert a node before the first node of a linked list", () => {
    linked_list.append(1);
    linked_list.insertBefore(1, 0);
    expect(linked_list.head.value).toBe(0);
    expect(linked_list.head.next.value).toBe(1);
    expect(linked_list.head.next.next).toBeNull();
  });

  test("Can successfully insert after a node in the middle of the linked list", () => {
    linked_list.append(1);
    linked_list.append(2);
    linked_list.append(4);
    linked_list.insertAfter(2, 3);
    expect(linked_list.head.value).toBe(1);
    expect(linked_list.head.next.value).toBe(2);
    expect(linked_list.head.next.next.value).toBe(3);
    expect(linked_list.head.next.next.next.value).toBe(4);
    expect(linked_list.head.next.next.next.next).toBeNull();
  });

  test("Can successfully insert a node after the last node of the linked list", () => {
    linked_list.append(1);
    linked_list.append(2);
    linked_list.insertAfter(2, 3);
    expect(linked_list.head.value).toBe(1);
    expect(linked_list.head.next.value).toBe(2);
    expect(linked_list.head.next.next.value).toBe(3);
    expect(linked_list.head.next.next.next).toBeNull();
  });
});

describe('Methods', () => {
  describe('Find Kth From End', () => {
    test('throws an error if k is greater than the length of the linked list', () => {
      const linked_list = new LinkedList();
      linked_list.append(1);
      expect(() => linked_list.findKthFromEnd(2)).toThrowError('There is no 2th element in the Linked List');
    });

    test('throws an error if k is not a positive integer', () => {
      const linked_list = new LinkedList();
      linked_list.append(1);
      expect(() => linked_list.findKthFromEnd(-1)).toThrowError('k must be a positive integer');
      expect(() => linked_list.findKthFromEnd(0)).toThrowError('k must be a positive integer');
      expect(() => linked_list.findKthFromEnd(1.5)).toThrowError('k must be a positive integer');
    });

    test('returns the value of the only node in the list if k is 1 and the list has size 1', () => {
      const linked_list = new LinkedList();
      linked_list.append(1);
      expect(linked_list.findKthFromEnd(1)).toBe(1);
    });

    test('returns the value of the node in the middle of the list when k is not at the end', () => {
      const linked_list = new LinkedList();
      linked_list.append(1);
      linked_list.append(2);
      linked_list.append(3);
      linked_list.append(4);
      linked_list.append(5);
      expect(linked_list.findKthFromEnd(3)).toBe(3);
    });

    test('returns the value of the last node in the list when k is equal to the length of the list', () => {
      const linked_list = new LinkedList();
      linked_list.append(1);
      linked_list.append(2);
      linked_list.append(3);
      linked_list.append(4);
      linked_list.append(5);
      expect(linked_list.findKthFromEnd(5)).toBe(1);
    });
  });
});
```

# Challenge Title
Zipper Two Linked List

## Whiteboard Process

![Zipper](https://user-images.githubusercontent.com/105818064/231579770-73a82ca0-5501-48b8-a8c8-ad20a6f4fb2d.jpeg)



## Approach & Efficiency
The approach I used iterates over both input lists simultaneously, appending nodes from each list to the resulting list alternately. If one list is shorter than the other, it appends the remaining nodes of the longer list to the end of the resulting list. The function returns the resulting linked list.

Space Complextity O(1)
Time O(N)

## Solution
```
class Node {
  constructor(value) {
    this.value = value;  // The value of the node.
    this.next = null;  // The reference to the next node in the list.
  }
}

class LinkedList {
  constructor() {
    this.head = null;  // The first node in the list (also known as the head).
  }

  // This method adds a new node with the given value to the end of the list.
  append(value) {
    const new_node = new Node(value);
    if (!this.head) {  // If the list is empty, make this node the head.
      this.head = new_node;
    } else {
      // Traverse the list until we find the last node (i.e., the one with no next node).
      let current_node = this.head;
      while (current_node.next) {
        current_node = current_node.next;
      }
      // Add the new node to the end of the list.
      current_node.next = new_node;
    }
  }

  // This method adds a new node with the given new_value before the first node with the given value.
  insertBefore(value, new_value) {
    const new_node = new Node(new_value);
    if (!this.head) {  // If the list is empty, we can't insert anything before a value.
      throw new Error("Linked List is empty");
    }
    if (this.head.value === value) {  // If the value to insert before is the head, update the head.
      new_node.next = this.head;
      this.head = new_node;
      return;
    }
    // Traverse the list until we find the node with the value to insert before.
    let current_node = this.head;
    while (current_node.next) {
      if (current_node.next.value === value) {
        // Insert the new node before the node with the given value.
        new_node.next = current_node.next;
        current_node.next = new_node;
        return;
      }
      current_node = current_node.next;
    }
    // If we reach this point, the value to insert before was not found in the list.
    throw new Error(`Value ${value} not found in Linked List`);
  }

  // This method adds a new node with the given new_value after the first node with the given value.
  insertAfter(value, new_value) {
    const new_node = new Node(new_value);
    if (!this.head) {  // If the list is empty, we can't insert anything after a value.
      throw new Error("Linked List is empty");
    }
    // Traverse the list until we find the node with the given value.
    let current_node = this.head;
    while (current_node) {
      if (current_node.value === value) {
        // Insert the new node after the node with the given value.
        new_node.next = current_node.next;
        current_node.next = new_node;
        return;
      }
      current_node = current_node.next;
    }
    // If we reach this point, the value to insert after was not found in the list.
    throw new Error(`Value ${value} not found in Linked List`);
  }

  // This method finds the kth node from the end of the list and returns its value.
findKthFromEnd(k) {
  if (!Number.isInteger(k) || k < 0) {
    throw new Error("k must be a positive integer");
  }
  // initialize two variables
  let slow_pointer = this.head;
  let fast_pointer = this.head;
  // loop through the array having the slow pointer be k spaces behind the first one
  for (let i = 0; i < k; i++) {
    // throws an error if it gets to the end of the list before the count end
    if (fast_pointer.next === null) {
      throw new Error(`There is no ${k}th element in the Linked List`);
    }
    fast_pointer = fast_pointer.next;
  }
  while (fast_pointer.next !== null) {
    slow_pointer = slow_pointer.next;
    fast_pointer = fast_pointer.next;
  }
  // return the value once it gets to the end of the list
  
  return slow_pointer.value;
}
}



const firstList = new LinkedList();
firstList.append(1);
firstList.append(2);
firstList.append(3);

const secondList = new LinkedList();
secondList.append("a");
secondList.append("b");
secondList.append("c");

function zipLists(list1, list2) {
  const result = new LinkedList();
  let node1 = list1.head;
  let node2 = list2.head;
  while (node1 !== null && node2 !== null) {
    result.append(node1.value);
    result.append(node2.value);
    node1 = node1.next;
    node2 = node2.next;
  }
  // if either list has remaining nodes, append them to the result
  while (node1 !== null) {
    result.append(node1.value);
    node1 = node1.next;
  }
  while (node2 !== null) {
    result.append(node2.value);
    node2 = node2.next;
  }
  return result;
}

const zippedList = zipLists(firstList, secondList);
console.log(zippedList); // should print: 1 -> a -> 2 -> b -> 3 -> c -> null


module.exports = { LinkedList, zipLists };

```

## Tests
```
const { LinkedList, zipLists } = require("./LinkedList.js");

describe("Linked List", () => {
  let linked_list;

  beforeEach(() => {
    linked_list = new LinkedList();
  });

  test("Can successfully add a node to the end of the linked list", () => {
    linked_list.append(1);
    expect(linked_list.head.value).toBe(1);
    expect(linked_list.head.next).toBeNull();

    linked_list.append(2);
    expect(linked_list.head.value).toBe(1);
    expect(linked_list.head.next.value).toBe(2);
    expect(linked_list.head.next.next).toBeNull();
  });

  test("Can successfully add multiple nodes to the end of a linked list", () => {
    linked_list.append(1);
    linked_list.append(2);
    linked_list.append(3);
    expect(linked_list.head.value).toBe(1);
    expect(linked_list.head.next.value).toBe(2);
    expect(linked_list.head.next.next.value).toBe(3);
    expect(linked_list.head.next.next.next).toBeNull();
  });

  test("Can successfully insert a node before a node located in the middle of a linked list", () => {
    linked_list.append(1);
    linked_list.append(2);
    linked_list.append(4);
    linked_list.insertBefore(2, 3);
    expect(linked_list.head.value).toBe(1);
    expect(linked_list.head.next.value).toBe(3);
    expect(linked_list.head.next.next.value).toBe(2);
    expect(linked_list.head.next.next.next.value).toBe(4);
    expect(linked_list.head.next.next.next.next).toBeNull();
  });

  test("Can successfully insert a node before the first node of a linked list", () => {
    linked_list.append(1);
    linked_list.insertBefore(1, 0);
    expect(linked_list.head.value).toBe(0);
    expect(linked_list.head.next.value).toBe(1);
    expect(linked_list.head.next.next).toBeNull();
  });

  test("Can successfully insert after a node in the middle of the linked list", () => {
    linked_list.append(1);
    linked_list.append(2);
    linked_list.append(4);
    linked_list.insertAfter(2, 3);
    expect(linked_list.head.value).toBe(1);
    expect(linked_list.head.next.value).toBe(2);
    expect(linked_list.head.next.next.value).toBe(3);
    expect(linked_list.head.next.next.next.value).toBe(4);
    expect(linked_list.head.next.next.next.next).toBeNull();
  });

  test("Can successfully insert a node after the last node of the linked list", () => {
    linked_list.append(1);
    linked_list.append(2);
    linked_list.insertAfter(2, 3);
    expect(linked_list.head.value).toBe(1);
    expect(linked_list.head.next.value).toBe(2);
    expect(linked_list.head.next.next.value).toBe(3);
    expect(linked_list.head.next.next.next).toBeNull();
  });
});


  describe('Find Kth From End', () => {
    test('throws an error if k is greater than the length of the linked list', () => {
      const linked_list = new LinkedList();
      linked_list.append(1);
      expect(() => linked_list.findKthFromEnd(2)).toThrowError('There is no 2th element in the Linked List');
    });

    test('throws an error if k is not a positive integer', () => {
      const linked_list = new LinkedList();
      linked_list.append(1);
      expect(() => linked_list.findKthFromEnd(-1)).toThrowError('k must be a positive integer');
      expect(() => linked_list.findKthFromEnd(1.5)).toThrowError('k must be a positive integer');
    });

    test('returns the value of the only node in the list if k is 1 and the list has size 1', () => {
      const linked_list = new LinkedList();
      linked_list.append(1);
      expect(linked_list.findKthFromEnd(0)).toBe(1);
    });

    test('returns the value of the node in the middle of the list when k is not at the end', () => {
      const linked_list = new LinkedList();
      linked_list.append(1);
      linked_list.append(2);
      linked_list.append(3);
      linked_list.append(4);
      linked_list.append(5);
      expect(linked_list.findKthFromEnd(3)).toBe(2);
    });
    });

    describe("Zip Lists", () => {
    test("Can successfully zip two empty lists", () => {
      const list1 = new LinkedList();
      const list2 = new LinkedList();
      const result = zipLists(list1, list2);
      expect(result.head).toBeNull();
    });

    test("Can successfully zip two lists of equal length", () => {
      const list1 = new LinkedList();
      list1.append(1);
      list1.append(2);
      list1.append(3);
      const list2 = new LinkedList();
      list2.append("a");
      list2.append("b");
      list2.append("c");
      const result = zipLists(list1, list2);
      expect(result.head.value).toBe(1);
      expect(result.head.next.value).toBe("a");
      expect(result.head.next.next.value).toBe(2);
      expect(result.head.next.next.next.value).toBe("b");
      expect(result.head.next.next.next.next.value).toBe(3);
      expect(result.head.next.next.next.next.next.value).toBe("c");
      expect(result.head.next.next.next.next.next.next).toBeNull();
    });

    test("Can successfully zip two lists of different lengths (list1 is longer)", () => {
      const list1 = new LinkedList();
      list1.append(1);
      list1.append(2);
      list1.append(3);
      const list2 = new LinkedList();
      list2.append("a");
      list2.append("b");
      const result = zipLists(list1, list2);
      expect(result.head.value).toBe(1);
      expect(result.head.next.value).toBe("a");
      expect(result.head.next.next.value).toBe(2);
      expect(result.head.next.next.next.value).toBe("b");
      expect(result.head.next.next.next.next.value).toBe(3);
      expect(result.head.next.next.next.next.next).toBeNull();
    });

    test("Can successfully zip two lists of different lengths (list2 is longer)", () => {
      const list1 = new LinkedList();
      list1.append(1);
      list1.append(2);
      const list2 = new LinkedList();
      list2.append("a");
      list2.append("b");
      list2.append("c");
      const result = zipLists(list1, list2);
      expect(result.head.value).toBe(1);
      expect(result.head.next.value).toBe("a");
      expect(result.head.next.next.value).toBe(2);
      expect(result.head.next.next.next.value).toBe("b");
      expect(result.head.next.next.next.next.value).toBe("c");
      expect(result.head.next.next.next.next.next).toBeNull();
    });
  });
```

# Challenge Title
Stack and Queue

## Whiteboard Process


![stack-queue-whiteboard](https://user-images.githubusercontent.com/105818064/232340589-13825381-b54d-4b3b-9f6d-c8fb43af76d4.png)



## Approach & Efficiency
I just need to check if the next node was null to see where I was at on the list

Space Complextity O(1)
Time O(1)

## Solution
```
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class Stack {
  constructor() {
    this.top = null;
  }

  push(value) {
    const new_node = new Node(value);
    new_node.next = this.top;
    this.top = new_node;
  }

  pop() {
    if (this.is_empty()) {
      throw new Error("Stack is empty");
    }
    const value = this.top.value;
    this.top = this.top.next;
    return value;
  }

  peek() {
    if (this.is_empty()) {
      throw new Error("Stack is empty");
    }
    return this.top.value;
  }

  is_empty() {
    return this.top === null;
  }
}

class Queue {
  constructor() {
    this.front = null;
    this.back = null;
  }

  enqueue(value) {
    const new_node = new Node(value);
    if (this.is_empty()) {
      this.front = new_node;
      this.back = new_node;
    } else {
      this.back.next = new_node;
      this.back = new_node;
    }
  }

  dequeue() {
    if (this.is_empty()) {
      throw new Error("Queue is empty");
    }
    const value = this.front.value;
    this.front = this.front.next;
    if (this.front === null) {
      this.back = null;
    }
    return value;
  }

  peek() {
    if (this.is_empty()) {
      throw new Error("Queue is empty");
    }
    return this.front.value;
  }

  is_empty() {
    return this.front === null;
  }
}


```

## Tests
```
describe("Stack tests", function() {
  it("Can push a value onto a stack", function() {
    const stack = new Stack();
    stack.push(1);
    expect(stack.peek()).toEqual(1);
  });

  it("Can push multiple values onto a stack", function() {
    const stack = new Stack();
    stack.push(1);
    stack.push(2);
    stack.push(3);
    expect(stack.peek()).toEqual(3);
  });

  it("Can pop a value off the stack", function() {
    const stack = new Stack();
    stack.push(1);
    const value = stack.pop();
    expect(value).toEqual(1);
    expect(stack.is_empty()).toBeTruthy();
  });

  it("Can empty a stack after multiple pops", function() {
    const stack = new Stack();
    stack.push(1);
    stack.push(2);
    stack.pop();
    stack.pop();
    expect(stack.is_empty()).toBeTruthy();
  });

  it("Can peek the next item on the stack", function() {
    const stack = new Stack();
    stack.push(1);
    stack.push(2);
    expect(stack.peek()).toEqual(2);
  });

  it("Can instantiate an empty stack", function() {
    const stack = new Stack();
    expect(stack.is_empty()).toBeTruthy();
  });

  it("Calling pop or peek on empty stack raises exception", function() {
    const stack = new Stack();
    expect(() => stack.pop()).toThrow();
    expect(() => stack.peek()).toThrow();
  });
});

describe("Queue tests", function() {
  it("Can enqueue a value into a queue", function() {
    const queue = new Queue();
    queue.enqueue(1);
    expect(queue.peek()).toEqual(1);
  });

  it("Can enqueue multiple values into a queue", function() {
    const queue = new Queue();
    queue.enqueue(1);
    queue.enqueue(2);
    queue.enqueue(3);
    expect(queue.peek()).toEqual(1);
  });

  it("Can dequeue out of a queue the expected value", function() {
    const queue = new Queue();
    queue.enqueue(1);
    queue.enqueue(2);
    const value = queue.dequeue();
    expect(value).toEqual(1);
  });

  it("Can peek into a queue, seeing the expected value", function() {
    const queue = new Queue();
    queue.enqueue(1);
    queue.enqueue(2);
    expect(queue.peek()).toEqual(1);
  });

  it("Can empty a queue after multiple dequeues", function() {
    const queue = new Queue();
    queue.enqueue(1);
    queue.enqueue(2);
    queue.dequeue();
    queue.dequeue();
    expect(queue.is_empty()).toBeTruthy();
  });

  it("Can instantiate an empty queue", function() {
    const queue = new Queue();
    expect(queue.is_empty()).toBeTruthy();
  });

  it("Calling dequeue or peek on empty queue raises exception", function() {
    const queue = new Queue();
    expect(() => queue.dequeue()).toThrow();
    expect(() => queue.peek()).toThrow();
  });
});

```

# Challenge Title
PsuedoQueue

## Whiteboard Process

![PsuedoQueue](https://user-images.githubusercontent.com/105818064/232614991-3702ac9b-e962-4799-bf2b-a9d4cfcf596b.png)




## Approach & Efficiency
I used an approach similar to the tower and ring game, in order to get the items to behave like I wanted i needed to utilize the second stack and a LIFO approach on the second stack.

Space/Time Complextity: O(2n)


## Solution
```
class Stack {
  constructor() {
    this.items = [];
  }
  push(element) {
    this.items.push(element);
  }
  pop() {
    if (this.items.length === 0) {
      return "Underflow";
    }
    return this.items.pop();
  }
  peek() {
    return this.items[this.items.length - 1];
  }
  isEmpty() {
    return this.items.length === 0;
  }
}

class PseudoQueue {
  constructor() {
    this.stack1 = new Stack(); // Initialize first stack
    this.stack2 = new Stack(); // Initialize second stack
  }

  // Insert an element into the PseudoQueue using a first-in, first-out approach
  enqueue(value) {
    // To add an element to the front of the PseudoQueue, we need to first reverse the order of elements in stack1
    // We can do this by popping all elements from stack1 and pushing them onto stack2
    while (!this.stack1.isEmpty()) {
      this.stack2.push(this.stack1.pop());
    }
    // Once all elements are in stack2, we can push the new element onto stack1, which will add it to the front of the PseudoQueue
    this.stack1.push(value);
    // Finally, we need to reverse the order of elements again by popping them from stack2 and pushing them onto stack1
    while (!this.stack2.isEmpty()) {
      this.stack1.push(this.stack2.pop());
    }
    console.log(this.stack1)
  }

  // Remove and return the first element in the PseudoQueue using a first-in, first-out approach
  dequeue() {
    // If both stacks are empty, then the PseudoQueue is empty
    if (this.stack1.isEmpty() && this.stack2.isEmpty()) {
      return "Queue is empty";
    }
    // Otherwise, we can simply pop the top element from stack1, which will be the first element of the PseudoQueue
    return this.stack1.pop();
  }
}

module.exports = { PseudoQueue, Stack };

```

## Tests
```
const { PseudoQueue, Stack } = require("./PsuedoQueue.js");

describe("PseudoQueue", () => {
  let queue;

  beforeEach(() => {
    queue = new PseudoQueue();
  });

  it("should enqueue elements in first-in, first-out order", () => {
    queue.enqueue(20);
    queue.enqueue(15);
    queue.enqueue(10);
    queue.enqueue(5);

    expect(queue.stack1.items).toEqual([5, 10, 15, 20]);
  });

  it("should dequeue elements in first-in, first-out order", () => {
    queue.enqueue(20);
    queue.enqueue(15);
    queue.enqueue(10);
    queue.enqueue(5);

    expect(queue.dequeue()).toEqual(20);
    expect(queue.stack1.items).toEqual([5, 10, 15]);
    expect(queue.dequeue()).toEqual(15);
    expect(queue.stack1.items).toEqual([5, 10]);
    expect(queue.dequeue()).toEqual(10);
    expect(queue.stack1.items).toEqual([5]);
    expect(queue.dequeue()).toEqual(5);
    expect(queue.stack1.items).toEqual([]);
    expect(queue.dequeue()).toEqual("Queue is empty");
  });

  it("should enqueue an element after dequeuing", () => {
    queue.enqueue(20);
    queue.enqueue(15);
    queue.enqueue(10);
    queue.enqueue(5);

    queue.dequeue();
    expect(queue.stack1.items).toEqual([5, 10, 15]);
    queue.enqueue(40);
    expect(queue.stack1.items).toEqual([40, 5, 10, 15]);
  });
});


```

# Challenge Title
Animal Shelter Stack and Queue

## Whiteboard Process


![Screenshot 2023-04-18 at 4 39 09 PM](https://user-images.githubusercontent.com/105818064/232927845-408d1a09-e449-4abb-adf2-1c958ea886fb.png)




## Approach & Efficiency
I used several if then statements to look through the list and pick the applicable animal.

Space/Time Complextity: O(N)


## Solution
```
class AnimalShelter {
  constructor() {
    // Separate arrays to hold dogs and cats
    this.dogs = [];
    this.cats = [];
    // Counter to keep track of the order in which animals arrive at the shelter
    this.order = 1;
  }

  // Method to add an animal to the shelter
  enqueue(animal) {
    // Set the order of arrival for the animal
    animal.order = this.order;
    // Increment the order counter
    this.order++;

    // Add the animal to the appropriate array based on its species
    if (animal.species === "dog") {
      this.dogs.push(animal);
    } else if (animal.species === "cat") {
      this.cats.push(animal);
    }
  }

  // Method to remove an animal from the shelter based on preference
  dequeue(pref) {
    
    // If the preference is "dog" and there are dogs in the shelter, return the first dog
    if (pref === "dog" && this.dogs.length > 0) {
      return this.dogs.shift();
    // If the preference is "cat" and there are cats in the shelter, return the first cat
    } else if (pref === "cat" && this.cats.length > 0) {
      return this.cats.shift();
    // If the preferred animal is not available, return the animal that has been waiting in the shelter the longest
    } else {
      // If there are both dogs and cats in the shelter, compare the order of arrival of the first dog and the first cat,
      // and return the animal that has been waiting in the shelter the longest
      if (this.dogs.length > 0 && this.cats.length > 0) {
        if (this.dogs[0].order < this.cats[0].order) {
          return this.dogs.shift();
        } else {
          return this.cats.shift();
        }
      // If there are only dogs or only cats in the shelter, return the first animal in the corresponding array
      } else if (this.dogs.length > 0) {
        return this.dogs.shift();
      } else if (this.cats.length > 0) {
        return this.cats.shift();
      // If there are no animals in the shelter, return null
      } else {
        return null;
      }
    }
  }
}



```

## Tests
```
// Example usage:

// Create a new AnimalShelter instance
const animalShelter = new AnimalShelter();

class Dog {
  constructor(name) {
    this.name = name;
    this.species = "dog";
    this.order = 1;
  }
}

class Cat {
  constructor(name) {
    this.name = name;
    this.species = "cat";
    this.order = 1;
  }
}

// Enqueue some animals
animalShelter.enqueue(new Dog("Rufus"));
animalShelter.enqueue(new Cat("Fluffy"));
animalShelter.enqueue(new Dog("Buddy"));
animalShelter.enqueue(new Cat("Winston"));

// Check the dogs and cats arrays after enqueuing
console.log(animalShelter.dogs); // Output: [ { name: 'Rufus', species: 'dog', order: 0 }, { name: 'Buddy', species: 'dog', order: 2 } ]
console.log(animalShelter.cats); // Output: [ { name: 'Fluffy', species: 'cat', order: 1 }, { name: 'Winston', species: 'cat', order: 3 } ]

// Dequeue some animals based on preference
animalShelter.dequeue("dog"); // Output: { name: 'Rufus', species: 'dog', order: 0 }
animalShelter.dequeue("cat"); // Output: { name: 'Fluffy', species: 'cat', order: 1 }

// Check the dogs and cats arrays after dequeuing
console.log(animalShelter.dogs); // Output: [ { name: 'Buddy', species: 'dog', order: 2 } ]
console.log(animalShelter.cats); // Output: [ { name: 'Winston', species: 'cat', order: 3 } ]

// Dequeue an animal without specifying a preference
animalShelter.dequeue(); // Output: { name: 'Buddy', species: 'dog', order: 2 }

// Enqueue some more animals
animalShelter.enqueue(new Cat("Oliver"));
animalShelter.enqueue(new Dog("Hanzo"));

// Check the dogs and cats arrays after enqueuing more animals
console.log(animalShelter.dogs); // Output: [ { name: 'Hanzo', species: 'dog', order: 4 } ]
console.log(animalShelter.cats); // Output: [ { name: 'Winston', species: 'cat', order: 3 }, { name: 'Oliver', species: 'cat', order: 5 } ]

// Dequeue an animal
animalShelter.dequeue(); 

// Check the dogs and cats arrays after dequeuing an animal
console.log(animalShelter.dogs); // Output: [ { name: 'Hanzo', species: 'dog', order: 4 } ]
console.log(animalShelter.cats); // Output: [ { name: 'Oliver', species: 'cat', order: 5 } ]



```

# Challenge Title

Binary Search Tree

## Whiteboard Process



![Screenshot 2023-04-21 at 2 41 02 PM](https://user-images.githubusercontent.com/105818064/233738973-a69fbea4-0955-44b6-93b2-ac7ef375c41c.png)



## Approach & Efficiency


Space/Time Complextity: 
At worst it will have to look through the entire tree. O(N)

## Solution
```
// Define Node class with value, left child, and right child properties
class Node {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}

// Define Binary Tree class with root property and pre-order, in-order, and post-order traversal methods
class BinaryTree {
  constructor() {
    this.root = null;
  }

  // Depth First Traversal - Pre-order
  preOrder() {
    const result = [];

    function traverse(node) {
      if (node === null) return;

      result.push(node.value);
      traverse(node.left);
      traverse(node.right);
    }

    traverse(this.root);

    return result;
  }

  // Depth First Traversal - In-order
  inOrder() {
    const result = [];

    function traverse(node) {
      if (node === null) return;

      traverse(node.left);
      result.push(node.value);
      traverse(node.right);
    }

    traverse(this.root);

    return result;
  }

  // Depth First Traversal - Post-order
  postOrder() {
    const result = [];

    function traverse(node) {
      if (node === null) return;

      traverse(node.left);
      traverse(node.right);
      result.push(node.value);
    }

    traverse(this.root);

    return result;
  }
}

// Define Binary Search Tree class that extends Binary Tree class
class BinarySearchTree extends BinaryTree {
  constructor() {
    super();
  }

  // Add a new node with the given value in the correct location
  add(value) {
    const node = new Node(value);

    if (this.root === null) {
      this.root = node;
      return;
    }

    let current = this.root;

    while (true) {
      if (value < current.value) {
        if (current.left === null) {
          current.left = node;
          break;
        }
        current = current.left;
      } else if (value > current.value) {
        if (current.right === null) {
          current.right = node;
          break;
        }
        current = current.right;
      } else {
        // Value already exists in the tree
        break;
      }
    }
  }
  
  // Add a new node with the given value in the correct location
add(value) {
  // Create a new node object with the given value
  const node = new Node(value);

  // If the tree is empty, set the new node as the root
  if (this.root === null) {
    this.root = node;
    return;
  }

  // Otherwise, traverse the tree to find the correct location for the new node
  let current = this.root;

  while (true) {
    // If the value is less than the current node's value, move to the left child
    if (value < current.value) {
      // If the left child is null, add the new node as the left child
      if (current.left === null) {
        current.left = node;
        break;
      }
      // Otherwise, continue traversing the left subtree
      current = current.left;
    }
    // If the value is greater than the current node's value, move to the right child
    else if (value > current.value) {
      // If the right child is null, add the new node as the right child
      if (current.right === null) {
        current.right = node;
        break;
      }
      // Otherwise, continue traversing the right subtree
      current = current.right;
    }
    // If the value is equal to the current node's value, the value already exists in the tree
    else {
      break;
    }
  }
}


  // Check if the tree contains a node with the given value
  contains(value) {
    let current = this.root;

    while (current !== null) {
      if (value === current.value) {
        return true;
      } else if (value < current.value) {
        current = current.left;
      } else {
        current = current.right;
      }
    }

    return false;
  }
}
```

## Tests
```
describe('BinarySearchTree', () => {
  let bst;

  beforeEach(() => {
    bst = new BinarySearchTree();
    bst.add(5);
    bst.add(3);
    bst.add(7);
    bst.add(2);
    bst.add(4);
    bst.add(6);
    bst.add(8);
  });

  describe('contains', () => {
    it('should return true if the tree contains the value', () => {
      expect(bst.contains(2)).toBe(true);
    });

    it('should return false if the tree does not contain the value', () => {
      expect(bst.contains(9)).toBe(false);
    });
  });

  describe('preOrder', () => {
    it('should return an array of values in pre-order traversal', () => {
      expect(bst.preOrder()).toEqual([5, 3, 2, 4, 7, 6, 8]);
    });
  });

  describe('inOrder', () => {
    it('should return an array of values in in-order traversal', () => {
      expect(bst.inOrder()).toEqual([2, 3, 4, 5, 6, 7, 8]);
    });
  });

  describe('postOrder', () => {
    it('should return an array of values in post-order traversal', () => {
      expect(bst.postOrder()).toEqual([2, 4, 3, 6, 8, 7, 5]);
    });
  });
});


```

# Challenge Title
Binary Tree Value

## Whiteboard Process


![Screenshot 2023-04-24 at 5 06 57 PM](https://user-images.githubusercontent.com/105818064/234140991-745ee32e-3ac8-443f-8927-8d94869d0f98.png)




## Approach & Efficiency


Space/Time Complextity: 
Overall, the time complexity is O(n) and the space complexity is O(n) in the worst case. However, in a balanced binary tree, the space complexity is O(log n), which is much better.

## Solution
```
class BinaryTree {
  constructor(value = null) {
    this.value = value;
    this.leftChild = null;
    this.rightChild = null;
  }

  findMaximumValue() {
    if (this.value === null) {
      return null;
    }

    let maxVal = this.value;

    if (this.leftChild !== null) {
      maxVal = Math.max(maxVal, this.leftChild.findMaximumValue());
    }

    if (this.rightChild !== null) {
      maxVal = Math.max(maxVal, this.rightChild.findMaximumValue());
    }

    return maxVal;
  }
}

```

## Tests
```
describe('BinaryTree', () => {
  test('findMaximumValue returns the maximum value in the tree', () => {
    const tree = new BinaryTree(4);
    tree.leftChild = new BinaryTree(2);
    tree.rightChild = new BinaryTree(6);
    tree.leftChild.leftChild = new BinaryTree(1);
    tree.leftChild.rightChild = new BinaryTree(3);
    tree.rightChild.leftChild = new BinaryTree(5);
    tree.rightChild.rightChild = new BinaryTree(7);

    expect(tree.findMaximumValue()).toEqual(7);
  });

  test('findMaximumValue returns null for an empty tree', () => {
    const tree = new BinaryTree();

    expect(tree.findMaximumValue()).toBeNull();
  });
});
```

# Challenge Title
Breadth-first Traversal

## Whiteboard Process

![Screenshot 2023-04-25 at 2 58 53 PM](https://user-images.githubusercontent.com/105818064/234413654-c5a91605-7767-4de7-bb16-af3edbe71200.png)



## Approach & Efficiency
Starting from the root node of the tree, the algorithm adds the root node to the queue, then loops over the queue while it is not empty. For each node in the queue, the algorithm adds its left and right child nodes (if they exist) to the end of the queue. Then, the algorithm visits the node (i.e., adds its value to the output list) and removes it from the front of the queue.

Space/Time Complextity: 
Time: O(n) because it must visit each node in the tree
Space: O(w) depending on how wide the tree is 

## Solution
```
function breadthFirst(tree) {
  const result = [];
  const queue = [tree];

  while (queue.length > 0) {
    const node = queue.shift();
    result.push(node.value);

    if (node.left) {
      queue.push(node.left);
    }

    if (node.right) {
      queue.push(node.right);
    }
  }

  return result;
}

```

## Tests
```
describe("breadthFirst", () => {
  test("should return the correct order of nodes for the given tree", () => {
    const tree = new TreeNode(2);
    tree.left = new TreeNode(7);
    tree.right = new TreeNode(5);
    tree.left.left = new TreeNode(2);
    tree.left.right = new TreeNode(6);
    tree.right.right = new TreeNode(9);
    tree.left.right.left = new TreeNode(5);
    tree.left.right.right = new TreeNode(11);
    tree.right.right.left = new TreeNode(4);

    expect(breadthFirst(tree)).toEqual([2, 7, 5, 2, 6, 9, 5, 11, 4]);
  });
});
```

# Challenge Title
Tree Fizz-Buzz

## Whiteboard Process


![Screenshot 2023-04-26 at 8 26 12 PM](https://user-images.githubusercontent.com/105818064/234752398-d4cd1905-2599-46a2-a881-570b6e28fa35.png)




## Approach & Efficiency
The fizzBuzzTree function takes a k-ary tree as input and returns a new tree with the same structure but with the values modified based on the rules of FizzBuzz, by recursively traversing the tree and replacing the node values with the corresponding string values.

Space/Time Complextity: 
Time: O(n)
Space: O(w)

## Solution
```
class KNode {
  constructor(value, children = []) {
    this.value = value;
    this.children = children;
  }
}

function fizzBuzzTree(root) {
  const fizzBuzz = (value) => {
    if (value % 3 === 0 && value % 5 === 0) {
      return "FizzBuzz";
    } else if (value % 3 === 0) {
      return "Fizz";
    } else if (value % 5 === 0) {
      return "Buzz";
    } else {
      return String(value);
    }
  };

  const helper = (node) => {
    const newChildren = node.children.map((child) => helper(child));
    const newValue = fizzBuzz(node.value);
    return new KNode(newValue, newChildren);
  };

  return helper(root);
```

## Tests
```
test("returns a new tree with FizzBuzz values", () => {
  // create a sample k-ary tree
  const root = new KNode(1, [
    new KNode(2, [new KNode(4), new KNode(5), new KNode(6)]),
    new KNode(3, [new KNode(7), new KNode(15), new KNode(8)]),
  ]);

  // call fizzBuzzTree on the sample tree
  const newRoot = fizzBuzzTree(root);

  // check that the modified tree has the correct values at each node
  expect(newRoot.value).toEqual("Fizz");
  expect(newRoot.children[0].value).toEqual("2");
  expect(newRoot.children[0].children[0].value).toEqual("4");
  expect(newRoot.children[0].children[1].value).toEqual("Buzz");
  expect(newRoot.children[0].children[2].value).toEqual("Fizz");
  expect(newRoot.children[1].children[0].value).toEqual("7");
  expect(newRoot.children[1].children[1].value).toEqual("FizzBuzz");
  expect(newRoot.children[1].children[2].value).toEqual("8");
});

test("returns the original tree when all values are strings", () => {
  // create a sample k-ary tree with string values
  const root = new KNode("hello", [
    new KNode("world", [new KNode("foo"), new KNode("bar")]),
    new KNode("baz", [new KNode("qux"), new KNode("quux")]),
  ]);

  // call fizzBuzzTree on the sample tree
  const newRoot = fizzBuzzTree(root);

  // check that the modified tree has the same values as the original tree
  expect(newRoot.value).toEqual("hello");
  expect(newRoot.children[0].value).toEqual("world");
  expect(newRoot.children[0].children[0].value).toEqual("foo");
  expect(newRoot.children[0].children[1].value).toEqual("bar");
  expect(newRoot.children[1].value).toEqual("baz");
  expect(newRoot.children[1].children[0].value).toEqual("qux");
  expect(newRoot.children[1].children[1].value).toEqual("quux");
});


```

# Challenge Title
Lab 26

## Whiteboard Process






## Approach & Efficiency
The approach was I followed the directions

Space/Time Complextity: 
O(n^2)

## Solution
```
function Insert(sorted, value) {
  let i = 0;
  while (value > sorted[i]) {
    i++;
  }
  while (i < sorted.length) {
    const temp = sorted[i];
    sorted[i] = value;
    value = temp;
    i++;
  }
  sorted.push(value);
}

function InsertionSort(input) {
  const sorted = [input[0]];
  for (let i = 1; i < input.length; i++) {
    Insert(sorted, input[i]);
  }
  return sorted;
}

```

## Tests
```
// Test case 1: Empty array
const input1 = [];
const sorted1 = InsertionSort(input1);
console.log(sorted1); // output: []

// Test case 2: Single-element array
const input2 = [42];
const sorted2 = InsertionSort(input2);
console.log(sorted2); // output: [42]

// Test case 3: Array with multiple elements in random order
const input3 = [5, 2, 4, 6, 1, 3];
const sorted3 = InsertionSort(input3);
console.log(sorted3); // output: [1, 2, 3, 4, 5, 6]

// Test case 4: Array with duplicate elements
const input4 = [2, 1, 3, 2, 1];
const sorted4 = InsertionSort(input4);
console.log(sorted4); // output: [1, 1, 2, 2, 3]

// Test case 5: Array with negative numbers
const input5 = [-3, -1, -2, 0, -5, -4];
const sorted5 = InsertionSort(input5);
console.log(sorted5); // output: [-5, -4, -3, -2, -1, 0]


```

# Challenge Title
Sorting

## Whiteboard Process


No whiteboard required



## Approach & Efficiency
i sorted the stuff as required
Space/Time Complextity: 
O(n)

## Solution
```
// Sample movie objects
const movies = [
  {
    title: "The Shawshank Redemption",
    year: 1994,
    genres: ["Drama"],
  },
  {
    title: "Pulp Fiction",
    year: 1994,
    genres: ["Crime", "Drama"],
  },
  {
    title: "Inception",
    year: 2010,
    genres: ["Action", "Sci-Fi"],
  },
  {
    title: "The Godfather",
    year: 1972,
    genres: ["Crime", "Drama"],
  },
];

// Sort movies by most recent year first
function sortByYear(movies) {
  return movies.sort((a, b) => b.year - a.year);
}

// Sort movies alphabetically by title, ignoring leading "A"s, "An"s, or "The"s
function sortByTitle(movies) {
  return movies.sort((a, b) => {
    const titleA = a.title.replace(/^(A|An|The)\s+/i, '');
    const titleB = b.title.replace(/^(A|An|The)\s+/i, '');
    return titleA.localeCompare(titleB);
  });
}

// Testing the sorting functions
console.log(sortByYear(movies));
console.log(sortByTitle(movies));


```

## Tests
```
// Sample test data
const testMovies = [
  {
    title: "The Shawshank Redemption",
    year: 1994,
    genres: ["Drama"],
  },
  {
    title: "Pulp Fiction",
    year: 1994,
    genres: ["Crime", "Drama"],
  },
  {
    title: "Inception",
    year: 2010,
    genres: ["Action", "Sci-Fi"],
  },
  {
    title: "The Godfather",
    year: 1972,
    genres: ["Crime", "Drama"],
  },
];

// Test sortByYear function
test('sortByYear should sort movies by most recent year first', () => {
  const sortedMovies = sortByYear(testMovies);
  const years = sortedMovies.map(movie => movie.year);
  expect(years).toEqual([2010, 1994, 1994, 1972]);
});

// Test sortByTitle function
test('sortByTitle should sort movies alphabetically by title (ignoring leading "A", "An", "The")', () => {
  const sortedMovies = sortByTitle(testMovies);
  const titles = sortedMovies.map(movie => movie.title);
  expect(titles).toEqual([
    "Inception",
    "The Godfather",
    "Pulp Fiction",
    "The Shawshank Redemption",
  ]);
});


```

# Challenge Title
Hash Tables
## Whiteboard Process


![Screenshot 2023-05-12 at 12 11 48 PM](https://github.com/AnthonyKeith15/401-DSA/assets/105818064/661fc408-db12-4168-976b-09a53024eb0e)





## Approach & Efficiency

Start by initializing a fixed-size array to store key-value pairs. The size of the array can be determined based on the expected number of elements or a predefined constant.

When you want to store a key-value pair in the hashtable:

Use a hash function to calculate a hash value for the given key. The hash function should take the key and produce a unique or near-unique integer value.
Map the hash value to an index within the array using modulo division. This ensures that the index falls within the range of the array size.
If the array at the calculated index is empty, create a new bucket or list and insert the key-value pair.
If the array at the calculated index already has one or more key-value pairs, check if the key already exists within the bucket/list.
If the key exists, replace the associated value with the new value.
If the key does not exist, append the key-value pair to the end of the bucket/list.
When you want to retrieve the value associated with a given key from the hashtable:

Use the same hash function to calculate the hash value for the key.
Map the hash value to the corresponding index within the array using modulo division.
If the array at the calculated index is empty, the key does not exist in the hashtable.
If the array at the calculated index has one or more key-value pairs, search for the key within the bucket/list.
If the key is found, return the associated value.
If the key is not found within the bucket/list, the key does not exist in the hashtable.
When you want to check if a key exists in the hashtable:

Use the same hash function to calculate the hash value for the key.
Map the hash value to the corresponding index within the array using modulo division.
If the array at the calculated index is empty, the key does not exist in the hashtable.
If the array at the calculated index has one or more key-value pairs, search for the key within the bucket/list.
If the key is found, return true.
If the key is not found within the bucket/list, the key does not exist in the hashtable.
When you want to retrieve all the keys from the hashtable:

Traverse the entire array and collect all the keys from each non-empty bucket/list.
Return the collection of keys.
When you want to calculate the hash value for a given key:

Use a hash function specific to the datatype of the key to transform the key into a unique or near-unique integer value.
The hash function should produce the same hash value for the same key consistently.

Space/Time Complextity: 

The space complexity of the Hashtable class is O(n), where n is the number of key-value pairs stored in the hash table. This includes the space used for storing the keys and values in the array-based table.
The Time complexity is O(1) on average, with O(n) worst case scenario

## Solution
```
class HashTable {
  constructor() {
    this.size = 10; // initial size of the table
    this.table = new Array(this.size); // create an array to store key-value pairs
  }

  _hash(key) {
    // Calculate the hash value for the given key
    let hash = 0;
    for (let i = 0; i < key.length; i++) {
      // convert each character of the key to its ASCII code and add it to the hash
      hash = (hash + key.charCodeAt(i)) % this.size; // use modulo operator to ensure hash falls within table size
    }
    return hash; // return the calculated hash value
  }

  set(key, value) {
    const index = this._hash(key); // get the index in the table for the given key
    if (!this.table[index]) {
      // if the index is empty, create a new array and add the key-value pair to it
      this.table[index] = [[key, value]];
    } else {
      // if the index already has key-value pairs
      for (let i = 0; i < this.table[index].length; i++) {
        if (this.table[index][i][0] === key) {
          // if the key already exists, update its value
          this.table[index][i][1] = value;
          return;
        }
      }
      // if the key doesn't exist, add a new key-value pair to the existing array
      this.table[index].push([key, value]);
    }
  }

  get(key) {
    const index = this._hash(key); // get the index in the table for the given key
    if (!this.table[index]) {
      // if the index is empty, return undefined
      return undefined;
    }
    for (let i = 0; i < this.table[index].length; i++) {
      if (this.table[index][i][0] === key) {
        // if the key is found, return its value
        return this.table[index][i][1];
      }
    }
    // if the key is not found, return undefined
    return undefined;
  }

  has(key) {
    const index = this._hash(key); // get the index in the table for the given key
    if (!this.table[index]) {
      // if the index is empty, the key doesn't exist
      return false;
    }
    for (let i = 0; i < this.table[index].length; i++) {
      if (this.table[index][i][0] === key) {
        // if the key is found, return true
        return true;
      }
    }
    // if the key is not found, return false
    return false;
  }

  keys() {
    const keys = [];
    for (let i = 0; i < this.table.length; i++) {
      if (this.table[i]) {
        for (let j = 0; j < this.table[i].length; j++) {
          keys.push(this.table[i][j][0]); // add each key to the keys array
        }
      }
    }
    return keys; // return the array of keys
  }

  hash(key) {
    return this._hash(key); // return the hash value for the given key
  }
}


```

## Tests
```
const HashTable = require('./HashTable');

describe('HashTable', () => {
  let hashTable;

  beforeEach(() => {
    hashTable = new HashTable();
  });

  test('set and get', () => {
    hashTable.set('name', 'John');
    hashTable.set('age', 25);

    expect(hashTable.get('name')).toBe('John');
    expect(hashTable.get('age')).toBe(25);
  });

  test('set and get with collisions', () => {
    hashTable.set('name', 'John');
    hashTable.set('mane', 'Jane'); // collision with 'name'

    expect(hashTable.get('name')).toBe('John');
    expect(hashTable.get('mane')).toBe('Jane');
  });

  test('set and get with key replacement', () => {
    hashTable.set('name', 'John');
    hashTable.set('name', 'Jane'); // replace 'John' with 'Jane'

    expect(hashTable.get('name')).toBe('Jane');
  });

  test('has', () => {
    hashTable.set('name', 'John');
    hashTable.set('age', 25);

    expect(hashTable.has('name')).toBe(true);
    expect(hashTable.has('city')).toBe(false);
  });

  test('keys', () => {
    hashTable.set('name', 'John');
    hashTable.set('age', 25);

    const keys = hashTable.keys();
    expect(keys).toContain('name');
    expect(keys).toContain('age');
  });

  test('hash', () => {
    const hash = hashTable.hash('name');
    expect(typeof hash).toBe('number');
  });
});


```


# Challenge Title

hashmap-repeated-word

## Whiteboard Process



![Screenshot 2023-05-15 191104](https://github.com/AnthonyKeith15/401-DSA/assets/105818064/364235ab-ea30-42ef-8146-7d2a661b1d0d)



## Approach & Efficiency

The function takes the sentence, separates it into individual words, and then checks if any word is repeated. If it finds a word that shows up more than once, it tells you what that word is.

Space/Time Complextity:

Both space and time complexity are linear because at worst, the function has to go through the n number of words. This makes o(n) the time complexity

## Solution
```
function repeatedWord(string) {
  // Convert the string to lowercase and split it into an array of words using non-word characters as delimiters
  const words = string.toLowerCase().split(/\W+/);
  
  // Create a new Map to store the encountered words
  const wordMap = new Map();

  // Iterate over each word in the words array
  for (let word of words) {
    // Check if the word is already present in the wordMap
    if (wordMap.has(word)) {
      // If the word is repeated, return it
      return word;
    }

    // If the word is encountered for the first time, add it to the wordMap
    wordMap.set(word, true);
  }

  // If no repeated word is found, return an empty string
  return "";
}
```

## Tests
```
describe('repeatedWord', () => {
  it('should return the first repeated word in a string', () => {
    const sentence = "It was a queer, sultry summer, the summer they electrocuted the Rosenbergs, and I didn’t know what I was doing in New York...";
    const result = repeatedWord(sentence);
    expect(result).toBe('summer');
  });

  it('should return an empty string if no repeated word is found', () => {
    const sentence = "This is a test sentence without any repeated words.";
    const result = repeatedWord(sentence);
    expect(result).toBe('');
  });
});

```

# Challenge Title 32
tree-intersection

## Whiteboard Process

![Screenshot 2023-05-20 at 11 16 12 AM](https://github.com/AnthonyKeith15/401-DSA/assets/105818064/1057816b-8c3a-418b-8e13-0890ad52f6ba)


## Approach & Efficiency

Create a HashMap data structure to store the values encountered while traversing the first tree.
Traverse the first tree in any order (pre-order, in-order, or post-order) and add each encountered value to the HashMap.
Create an empty set to store the intersection values.
Traverse the second tree in the same order as the first tree.
For each encountered value in the second tree, check if it exists in the HashMap.If the value is found in the HashMap, add it to the intersection set.
After traversing the second tree, return the intersection set.

Space/Time Complextity: 
The time complexity of the algorithm is O(N + M), where N is the number of nodes in the first tree and M is the number of nodes in the second tree. The space complexity is O(N), as we store the values from the first tree in a HashMap.

## Solution
```
// Define a binary tree node
class TreeNode {
  constructor(value) {
    this.val = value;
    this.left = null;
    this.right = null;
  }
}

// Define the HashMap data structure
class HashMap {
  constructor() {
    this.map = {};
  }

  add(key) {
    this.map[key] = true;
  }

  has(key) {
    return this.map.hasOwnProperty(key);
  }
}

// Function to find intersection of values in two binary trees
function tree_intersection(tree1, tree2) {
  const valuesMap = new HashMap();
  const result = new Set();

  // Helper function to traverse the tree and add values to the map
  function traverseAndAddValues(node) {
    if (!node) return;

    valuesMap.add(node.val);

    traverseAndAddValues(node.left);
    traverseAndAddValues(node.right);
  }

  // Traverse the first tree and add its values to the map
  traverseAndAddValues(tree1);

  // Helper function to traverse the second tree and check for intersection
  function traverseAndCheckIntersection(node) {
    if (!node) return;

    if (valuesMap.has(node.val)) {
      result.add(node.val);
    }

    traverseAndCheckIntersection(node.left);
    traverseAndCheckIntersection(node.right);
  }

  // Traverse the second tree and check for intersection with the first tree
  traverseAndCheckIntersection(tree2);

  return result;
}
```

## Tests
```
// Create tree 1
const tree1 = new TreeNode(1);
tree1.left = new TreeNode(2);
tree1.right = new TreeNode(3);
tree1.left.left = new TreeNode(4);
tree1.left.right = new TreeNode(5);

// Create tree 2
const tree2 = new TreeNode(2);
tree2.left = new TreeNode(4);
tree2.right = new TreeNode(6);
tree2.left.left = new TreeNode(1);
tree2.left.right = new TreeNode(5);

// Find the intersection of values in tree1 and tree2
const intersectionSet = tree_intersection(tree1, tree2);


```

# Challenge Title 33

Left Join

## Whiteboard Process

![Screenshot 2023-05-20 at 11 22 18 AM](https://github.com/AnthonyKeith15/401-DSA/assets/105818064/2a7b4621-b673-402e-8a25-a6965033a772)

## Approach & Efficiency

1. Create an empty result data structure (e.g., an array, list, or dictionary).

2. Iterate through each key-value pair in the first hashmap (synonymsMap).

   - Create a row (e.g., an array, list, or dictionary) to store the key and corresponding value.

   - Append the value from the first hashmap to the row.

   - Check if the key exists in the second hashmap (antonymsMap).

     - If the key exists, append the corresponding value from the second hashmap to the row.

     - If the key doesn't exist, append NULL or an appropriate placeholder to the row.

   - Add the row to the result data structure.

3. Return the result data structure.

Space/Time Complextity: 

The time complexity of the leftJoin function is O(N), where N is the number of elements in the first hashmap (synonymsMap), and the space complexity is O(N), as the result array grows linearly with the number of elements in the first hashmap.

## Solution
```
function leftJoin(synonymsMap, antonymsMap) {
  const result = [];

  // Iterate through the keys of the first hashmap (synonymsMap)
  for (let [key, value] of synonymsMap) {
    const row = [key, value, null]; // Initialize the row with key and corresponding value from synonymsMap

    if (antonymsMap.has(key)) {
      // If the key exists in the second hashmap (antonymsMap)
      row[2] = antonymsMap.get(key); // Append the value from antonymsMap to the row
    }

    result.push(row); // Add the row to the result array
  }

  return result;
}
```

## Tests
```
INPUT
synonymsMap:
{
  "happy": "joyful",
  "sad": "unhappy",
  "big": "large"
}

antonymsMap:
{
  "happy": "sad",
  "sad": "happy",
  "small": "big"
}

OUTPUT
[  ["happy", "joyful", "sad"],
  ["sad", "unhappy", "happy"],
  ["big", "large", null]
]

```

# Challenge Title 35

Look at this.. Graaaaaaph

## Whiteboard Process


![Screenshot 2023-05-20 at 11 30 53 AM](https://github.com/AnthonyKeith15/401-DSA/assets/105818064/7213a7ed-381a-4e30-ac8f-babfa0d77a07)




## Approach & Efficiency

Create an instance of the Graph class.
Add a node to the graph using the addNode method and verify that it was successfully added.
Add an edge to the graph using the addEdge method and verify that the edge was successfully added.
Retrieve all nodes from the graph using the getNodes method and verify that the collection contains all the nodes in the graph.
Retrieve neighbors of a specific node using the getNeighbors method and verify that the collection contains the appropriate neighbors with the weights included.
Get the size of the graph using the size method and verify that it returns the correct number of nodes.
Create a graph with only one node and one edge, then verify that the node and edge are properly returned.

Space/Time Complextity: 

Adding a Node (addNode method): Time Complexity: O(1), Space Complexity: O(1)
Adding an Edge (addEdge method): Time Complexity: O(1), Space Complexity: O(1)
Retrieving Nodes (getNodes method): Time Complexity: O(N), Space Complexity: O(N)
Retrieving Neighbors (getNeighbors method): Time Complexity: O(1), Space Complexity: O(1)
Getting Size (size method): Time Complexity: O(1), Space Complexity: O(1)
Note: N represents the number of nodes in the graph.

## Solution
```
class Graph {
  constructor() {
    this.nodes = new Map();
  }

  addNode(value) {
    const node = {
      value: value,
      edges: new Map()
    };
    this.nodes.set(value, node);
    return node;
  }

  addEdge(node1, node2, weight = 0) {
    if (!this.nodes.has(node1) || !this.nodes.has(node2)) {
      throw new Error('Both nodes should already be in the graph.');
    }

    const edge = { node: node2, weight: weight };
    this.nodes.get(node1).edges.set(node2, edge);
  }

  getNodes() {
    return Array.from(this.nodes.values());
  }

  getNeighbors(node) {
    if (!this.nodes.has(node)) {
      return [];
    }

    const edges = this.nodes.get(node).edges;
    return Array.from(edges.values());
  }

  size() {
    return this.nodes.size;
  }
}

```

## Tests
```
// Import the necessary testing library (e.g., Jest)
const { TestScheduler } = require('jest');

// Import the Graph class implementation
const Graph = require('./Graph');

// Test case for adding a node to the graph
test('Node can be successfully added to the graph', () => {
  const graph = new Graph();
  graph.addNode('A');
  const nodes = graph.getNodes();
  expect(nodes.length).toBe(1);
  expect(nodes[0].value).toBe('A');
});

// Test case for adding an edge to the graph
test('An edge can be successfully added to the graph', () => {
  const graph = new Graph();
  graph.addNode('A');
  graph.addNode('B');
  graph.addEdge('A', 'B', 5);
  const neighbors = graph.getNeighbors('A');
  expect(neighbors.length).toBe(1);
  expect(neighbors[0].node).toBe('B');
  expect(neighbors[0].weight).toBe(5);
});

// Test case for retrieving all nodes from the graph
test('A collection of all nodes can be properly retrieved from the graph', () => {
  const graph = new Graph();
  graph.addNode('A');
  graph.addNode('B');
  graph.addNode('C');
  const nodes = graph.getNodes();
  expect(nodes.length).toBe(3);
  expect(nodes.map(node => node.value)).toEqual(expect.arrayContaining(['A', 'B', 'C']));
});

// Test case for retrieving appropriate neighbors from the graph
test('All appropriate neighbors can be retrieved from the graph', () => {
  const graph = new Graph();
  graph.addNode('A');
  graph.addNode('B');
  graph.addNode('C');
  graph.addEdge('A', 'B', 5);
  graph.addEdge('A', 'C', 10);
  const neighbors = graph.getNeighbors('A');
  expect(neighbors.length).toBe(2);
  expect(neighbors.map(neighbor => neighbor.node)).toEqual(expect.arrayContaining(['B', 'C']));
});

// Test case for retrieving neighbors with weight included
test('Neighbors are returned with the weight between nodes included', () => {
  const graph = new Graph();
  graph.addNode('A');
  graph.addNode('B');
  graph.addEdge('A', 'B', 5);
  const neighbors = graph.getNeighbors('A');
  expect(neighbors.length).toBe(1);
  expect(neighbors[0].node).toBe('B');
  expect(neighbors[0].weight).toBe(5);
});

// Test case for retrieving the proper size of the graph
test('The proper size is returned, representing the number of nodes in the graph', () => {
  const graph = new Graph();
  graph.addNode('A');
  graph.addNode('B');
  graph.addNode('C');
  const size = graph.size();
  expect(size).toBe(3);
});

// Test case for a graph with only one node and edge
test('A graph with only one node and edge can be properly returned', () => {
  const graph = new Graph();
  graph.addNode('A');
  graph.addEdge('A', 'A', 10);
  const nodes = graph.getNodes();
  const neighbors = graph.getNeighbors('A');
  const size = graph.size();
  expect(nodes.length).toBe(1);
  expect(neighbors.length).toBe(1);
  expect(neighbors[0].node).toBe('A');
  expect(neighbors[0].weight).toBe(10);
  expect(size).toBe(1);
});


```

# Challenge Title 36

graph-breadth-first

## Whiteboard Process

![Screenshot 2023-05-25 114546](https://github.com/AnthonyKeith15/401-DSA/assets/105818064/10950a8e-b41d-4f11-992e-d49306e22c3a)





## Approach & Efficiency
1. Create a queue and an empty visited set.
2. Enqueue the starting node into the queue and add it to the visited set.
3. While the queue is not empty:
     - Dequeue a node from the queue and process it.
     - Add the dequeued node to the collection of visited nodes.
     - Enqueue all unvisited neighbors of the dequeued node into the queue and add them to the visited set.
4. Return the collection of visited nodes.


Space/Time Complextity: 
The space complexity of the breadthFirst method is O(V), where V is the number of nodes in the graph, and the time complexity is O(V + E), where E is the total number of edges in the graph.

## Solution
```
class Node {
  constructor(value) {
    this.value = value;
    this.neighbors = [];
  }
}

class Graph {
  constructor() {
    this.nodes = [];
  }

  breadthFirst(startNode) {
    const visited = new Set();
    const queue = [startNode];
    const visitedOrder = [];

    visited.add(startNode);

    while (queue.length > 0) {
      const currentNode = queue.shift();
      visitedOrder.push(currentNode);

      for (const neighbor of currentNode.neighbors) {
        if (!visited.has(neighbor)) {
          visited.add(neighbor);
          queue.push(neighbor);
        }
      }
    }

    return visitedOrder;
  }
}

// Example usage:

// Create some nodes
const nodeA = new Node('A');
const nodeB = new Node('B');
const nodeC = new Node('C');
const nodeD = new Node('D');
const nodeE = new Node('E');

// Define connections between nodes
nodeA.neighbors.push(nodeB, nodeC);
nodeB.neighbors.push(nodeD, nodeE);
nodeC.neighbors.push(nodeE);
nodeE.neighbors.push(nodeD);

// Create a graph and add the nodes
const graph = new Graph();
graph.nodes.push(nodeA, nodeB, nodeC, nodeD, nodeE);

// Perform breadth-first search starting from nodeA
const visitedNodes = graph.breadthFirst(nodeA);

// Display the visited nodes in order
console.log(visitedNodes.map(node => node.value));

```

## Tests
```
const { Graph, Node } = require('./graph');

describe('Graph', () => {
  describe('breadthFirst', () => {
    it('should return the correct order of visited nodes in a simple graph', () => {
      // Create nodes
      const nodeA = new Node('A');
      const nodeB = new Node('B');
      const nodeC = new Node('C');
      const nodeD = new Node('D');
      const nodeE = new Node('E');

      // Define connections between nodes
      nodeA.neighbors.push(nodeB, nodeC);
      nodeB.neighbors.push(nodeD, nodeE);
      nodeC.neighbors.push(nodeE);
      nodeE.neighbors.push(nodeD);

      // Create a graph and add the nodes
      const graph = new Graph();
      graph.nodes.push(nodeA, nodeB, nodeC, nodeD, nodeE);

      // Perform breadth-first search starting from nodeA
      const visitedNodes = graph.breadthFirst(nodeA);

      // Verify the visited nodes are in the correct order
      expect(visitedNodes.map(node => node.value)).toEqual(['A', 'B', 'C', 'D', 'E']);
    });

    it('should return the correct order of visited nodes in a disconnected graph', () => {
      // Create nodes
      const nodeA = new Node('A');
      const nodeB = new Node('B');
      const nodeC = new Node('C');
      const nodeD = new Node('D');
      const nodeE = new Node('E');

      // Define connections between nodes
      nodeA.neighbors.push(nodeB, nodeC);
      nodeD.neighbors.push(nodeE);

      // Create a graph and add the nodes
      const graph = new Graph();
      graph.nodes.push(nodeA, nodeB, nodeC, nodeD, nodeE);

      // Perform breadth-first search starting from nodeA
      const visitedNodes = graph.breadthFirst(nodeA);

      // Verify the visited nodes are in the correct order
      expect(visitedNodes.map(node => node.value)).toEqual(['A', 'B', 'C']);
    });
  });
});


```

# Challenge Title 37

graph-business-trip

## Whiteboard Process


![Screenshot 2023-05-25 115540](https://github.com/AnthonyKeith15/401-DSA/assets/105818064/cc9034ad-1bdf-4eea-83de-cfc88dd119e9)




## Approach & Efficiency
Initialize a variable cost to 0.
Iterate over the array of city names from index 0 to n-1, where n is the length of the array.
For each iteration:
Get the current city name and the next city name.
Check if there is a direct flight available between the current city and the next city in the graph. If not, return null.
Add the cost of the direct flight between the current city and the next city to the cost variable.
Return the cost if the trip is possible. Otherwise, return null

Space/Time Complextity: 

The space complexity of the algorithm is O(1) as it doesn't use any additional data structures that grow with the input size, and the time complexity is O(n) where n is the number of cities in the array, as it iterates through the array once to determine the cost of the trip.

## Solution
```
function businessTrip(graph, cities) {
  let cost = 0;
  for (let i = 0; i < cities.length - 1; i++) {
    let currentCity = cities[i];
    let nextCity = cities[i + 1];
    if (!(currentCity in graph) || !(nextCity in graph[currentCity])) {
      return null; // Direct flight not available
    }
    cost += graph[currentCity][nextCity];
  }
  return cost;
}

```

## Tests
```
const { businessTrip } = require('./your-file-name');

describe('businessTrip', () => {
  // Define the graph for testing
  const graph = {
    'A': {'B': 100, 'C': 200},
    'B': {'A': 100, 'C': 50},
    'C': {'A': 200, 'B': 50}
  };

  it('should return the cost of the trip when it is possible', () => {
    expect(businessTrip(graph, ['A', 'B', 'C'])).toBe(150);
    expect(businessTrip(graph, ['A', 'C', 'B'])).toBe(150);
    expect(businessTrip(graph, ['C', 'A', 'B'])).toBe(250);
  });

  it('should return null when the trip is not possible', () => {
    expect(businessTrip(graph, ['A', 'C', 'D'])).toBeNull();
    expect(businessTrip(graph, ['A', 'D', 'B'])).toBeNull();
    expect(businessTrip(graph, ['B', 'C', 'A'])).toBeNull();
  });

  it('should return 0 cost for an empty trip', () => {
    expect(businessTrip(graph, [])).toBe(0);
  });

  it('should return null for a trip with only one city', () => {
    expect(businessTrip(graph, ['A'])).toBeNull();
    expect(businessTrip(graph, ['B'])).toBeNull();
    expect(businessTrip(graph, ['C'])).toBeNull();
  });
});


```

# Challenge Title 38

graph-depth-first

## Whiteboard Process



![Screenshot 2023-05-25 120433](https://github.com/AnthonyKeith15/401-DSA/assets/105818064/8f03885b-2853-4b87-b484-4958bb45ebd1)



## Approach & Efficiency

Initialize an empty set visited to keep track of visited nodes.
Initialize an empty collection (e.g., array, list) collection to store the nodes in their pre-order depth-first traversal order.
Define a recursive function dfs that takes a node as an argument.
In the dfs function:
Add the current node to the visited set.
Add the value of the current node to the collection.
Iterate through each neighbor of the current node:
If the neighbor has not been visited, recursively call dfs on the neighbor.
Call the dfs function with the starting node as the argument.
Return the collection.

Space/Time Complextity:

The time complexity of the depthFirst method is O(V + E), where V represents the number of vertices (nodes) in the graph and E represents the number of edges. This is because in the worst case, the method may visit all vertices and edges in the graph once during the depth-first traversal.

## Solution
```
class Node {
  constructor(value) {
    this.value = value;
    this.neighbors = [];
  }
}

class Graph {
  constructor() {
    this.nodes = [];
  }

  addNode(value) {
    this.nodes.push(new Node(value));
  }

  addEdge(node1, node2) {
    node1.neighbors.push(node2);
    node2.neighbors.push(node1);
  }

  depthFirst(startNode) {
    const visited = new Set();
    const collection = [];

    function dfs(node) {
      visited.add(node);
      collection.push(node.value);

      for (const neighbor of node.neighbors) {
        if (!visited.has(neighbor)) {
          dfs(neighbor);
        }
      }
    }

    dfs(startNode);
    return collection;
  }
}

```

## Tests
```
const { Graph } = require('./your-file-name');

describe('Graph', () => {
  it('should perform depth-first traversal correctly', () => {
    const graph = new Graph();

    const node1 = graph.addNode('A');
    const node2 = graph.addNode('B');
    const node3 = graph.addNode('C');
    const node4 = graph.addNode('D');
    const node5 = graph.addNode('E');

    graph.addEdge(node1, node2);
    graph.addEdge(node1, node3);
    graph.addEdge(node2, node4);
    graph.addEdge(node3, node4);
    graph.addEdge(node3, node5);
    
    const result = graph.depthFirst(node1);

    expect(result).toEqual(['A', 'B', 'D', 'C', 'E']);
  });
});


```


# Challenge Title

TEMPLATE (Scroll up to see this weeks challenge)
## Whiteboard Process






## Approach & Efficiency


Space/Time Complextity: 


## Solution
```

```

## Tests
```


```
