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
