## Additional Problems

The following exercises are from Cracking the Coding Interview byGayle Laakmann Mcdoweell.

1. The following code computes the product of a and b. What is its runtime?
```java
int product(int a, int b) {
    int sum = 0;
    for (int i = 0; i < b; i++) {
        sum += a;
    }
    return sum;
}
```

Answer: `O(b)` -> The for loop just iterates through `b`.

2. The following code computes `a^b`. What is its runtime?
```java
int power(int a, int b) {
    if(b < 0){
        return 0; //error
    } else if (b == 0) {
        return 1;
    } else {
        return a * power(a, b - 1);
    }
}
```

Answer: `O(b)` -> This recursive code iterates through `b` calls since for each iterating we are subtracting 1 to b.

3. The following code computes `a % b`. What is its runtime?
```java
int mod(int a, int b) {
    if (b <= 0) {
        return -1;
    }
    int div = a / b;
    return a - div * b;
}
```

Answer: `O(1)` -> All the work here is constant.

4. The following code performs integer division. What is its runtime (assume a and b are both positive)?
```java
int div(int a, int b) {
    int count = 0;
    int sum = b;
    while (sum <= a) {
        sum += b;
        count++
    }
    return count
}
```

Answer: `O(a/b)` -> For this question I initially though of `O(b)` because I saw that we add `a` each time, but that will be the case if b was equal to 1. Notice that if we increase b to 2, now it will take `a/2` iterations. Therefore `a/b` 

5. The following code computes the [integer] square root of a number. If the number is not a perfect square (there is no integer square root), then it returns -1.
It does by successive guessing. If n is 100, it first guesses 50. Too high? Try something lower - halfway between 1 and 50. What is its runtime?

```java
int sqrt(int n) {
    return sqrt_helper(n, 1, n);
}

int sqrt_helper(int n, int min, int max) {
    if(max < min) return -1; // no square root

    int guess = (min + max) / 2;
    if (guess * guess == n) {// found it!
        return guess;
    } else if (guess * guess < n) { // too low
        return sqrt_helper(n, guess + 1, max); // try higher
    } else {
        return sqrt_helper(n, min, guess - 1); // try lower
    }
}
```

Answer: `O(log N)` -> This algorithm is equivalent to a binary search to find the square root.

6. The following code computes the [integer] square root of a number. If the number is not a perfect square, then it returns -1. It does this by trying increasingly large numbers until it finds the right value (or is too high). What is its runtime?
```java
int sqrt(int n) {
    for (int guess = 1; guess * guess <= n; guess++) {
        if (guess * guess == n){
            return guess
        }
    }
    return -1;
}
```

Answer: `O(sqrt(N))` -> This is just a straightforward loop that stops when guess * guess > n (or, in other words, when guess > sqrt(n)).

7. If a binary search tree is not balanced, how long it might take (worst case) to find an element in it?

Answer - `O(N)` -> If a binary search tree is not balanced, that would mean that there is no specific organization among the nodes of the tree. Therefore, we would need to check every single node of the tree. 

8. You are looking for a specific value in a binary tree, but the tree is not a binary search tree. What is the time complexity of this?

Answer - `O(N)` -> Similar to the answer above. Without any property ordering on the tree, we might have to search through all the nodes of the tree.

9. The `appendToNew` method appends a value to an array by creating a new, longer array and returning this longer array. You have used the `appendToNew` method to create a copyArray function that repeatedly calls `appendToNew`. How long does copying the array take?

```java
int[] copyArray(int[] array) {
    int[] copy = new int[0];
    for (int value : array) {
        copy = appendToNew(copy, value);
    }
    return copy;
}

int[] appendToNew(int[] array. int value) {
    //copy all elements over to new array
    int[bigger] = new int[array.length + 1];
    for (int i = 0; i < array.length; i++){
        bigger[i] = array[i];
    }

    // add new element
    bigger[bigger.length - 1] = value;
    return bigger;
}
```

Answer: `O(N^2)` -> The function is  `appendToNew` for each value of the original array, that already has a time complexity of `O(N)`, additionally `appendToNew` is copying all elements of the current array to a new one plus adding the new value `O(N)`. We then have `O(N * N)` -> `O(N^2)`

10. The following code sums the digits in a number. What is its big O time?
```java
int sumDigits(int n) {
    int sum = 0;
    while(n > 0){
        sum += n % 10;
        n /= 10;
    }
    return sum;
}
```

Answer: `O(log N)` -> Initially though of `O(N)` but the reason was because I thought that N was the number of integers the number had. It is important notice these details. 

11. The following code prints all strings of length `k` where the characters are in sorted order. It does this by generating all strings of length k and then checking if each is sorted. What is its runtime?
```java
void printSortedStrings(int remaining) {
    printSortedStrings(remaining, "");
}

void printSortedStrings(int remaining, String prefix) {
    if (remaining == 0){
        if (isInOrder(prefix)) {
            System.out.println(prefix);
        }
    } else {
        for (char c = 'a'; c <= 'z'; c++) {
            printSortedStrings(remaining - 1, prefix + c);
        }
    }
}

boolean isInOrder(String s) {
    boolean isInOrder = true;
    for (int i = 1; i < s.length(); i++) {
        if (s.charAt(i -1) > s.charAt(i)) {
            isInOrder = false;
        }
    }
    return isInOrder;
}
```

Answer: `O(k(c^k))` -> where k is the length of the string and c is the number of characters in the alphabet. It takes `O(c^k)` time to generate each string. Then we need, to check that each of these is sorted, which takes O(k) time. 

12. The following code computes the intersection (the number of elements in common) of two arrays. It assumes that neither array has duplicates. It computes the intersection by sorting one array (array b) and the iterating through array `a` checking (via binary search) if each value is in `b`. What is its runtime?
```java
int intersection(int[] a, int[] b) {
    mergesort(b);

    int intersect = 0;
    for (int x : a) {
        if (binarySearch(b, x) >= 0 {
            intersect++;
        })
    }

    return intersect;
}
```

Answer: `O(b log b + a lob b)` -> Merger sort takes `O(b log b)` time. Then once it is sorted, for each element in a, we do a binary search `O(log b)`. The second part will take `O(a log b)`.