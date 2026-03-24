# strukdat-mini-project-01
---

## A. Stack

### 1. Case Explanation

**Case: Reverse prefix of word**
Given a 0-indexed string `word` and a character `ch`, reverse the segment of `word` that starts at index `0` and ends at the index of the first occurrence of `ch` (inclusive). If the character `ch` does not exist in `word`, do nothing.

For example, if `word = "abcdefd"` and `ch = "d"`, then you should reverse the segment that starts at `0` and ends at `3` (inclusive). The resulting string will be `"dcbaefd"`.
Return the resulting string.

```
Example 1:
Input: word = "abcdefd", ch = "d"
Output: "dcbaefd"
Explanation: The first occurrence of "d" is at index 3. 
Reverse the part of word from 0 to 3 (inclusive), the resulting string is "dcbaefd".
```

```
Example 2:
  Input: word = "xyxzxe", ch = "z"
  Output: "zxyxxe"
  Explanation: The first and only occurrence of "z" is at index 3.
  Reverse the part of word from 0 to 3 (inclusive), the resulting string is "zxyxxe".
```

```
Example 3:
  Input: word = "abcd", ch = "z"
  Output: "abcd"
  Explanation: "z" does not exist in word.
You should not do any reverse operation, the resulting string is "abcd".
```

### 2. Steps & Code Snippets

### 3. Screenshot

## B. Queue

### 1. Case Explanation

**Case: Number of students unable to eat lunch**
The school cafeteria offers circular and square sandwiches at lunch break, referred to by numbers `0` and `1` respectively. All students stand in a queue. Each student either prefers square or circular sandwiches.

The number of sandwiches in the cafeteria is equal to the number of students. The sandwiches are placed in a **stack**. At each step:

If the student at the front of the queue prefers the sandwich on the top of the stack, they will take it and leave the queue.
Otherwise, they will leave it and go to the queue's end.
This continues until none of the queue students want to take the top sandwich and are thus unable to eat.

You are given two integer arrays `students` and `sandwiches` where `sandwiches[i]` is the type of the `i​​​​​​th` sandwich in the stack (`i = 0` is the top of the stack) and `students[j]` is the preference of the `j​​​​​​th student` in the initial queue (`j = 0` is the front of the queue). Return the number of students that are unable to eat.

```
Example 1:
  Input: students = [1,1,0,0], sandwiches = [0,1,0,1]
  Output: 0 

  Explanation:
- Front student leaves the top sandwich and returns to the end of the line making students = [1,0,0,1].
- Front student leaves the top sandwich and returns to the end of the line making students = [0,0,1,1].
- Front student takes the top sandwich and leaves the line making students = [0,1,1] and sandwiches = [1,0,1].
- Front student leaves the top sandwich and returns to the end of the line making students = [1,1,0].
- Front student takes the top sandwich and leaves the line making students = [1,0] and sandwiches = [0,1].
- Front student leaves the top sandwich and returns to the end of the line making students = [0,1].
- Front student takes the top sandwich and leaves the line making students = [1] and sandwiches = [1].
- Front student takes the top sandwich and leaves the line making students = [] and sandwiches = [].
Hence all students are able to eat.
```

```
Example 2:
  Input: students = [1,1,1,0,0,1], sandwiches = [1,0,0,0,1,1]
  Output: 3
```

### 2. Steps & Code Snippets

### 3. Screenshot

## C. Dequeue

### 1. Case Explanation

**Case: Find the winner of the circular game"**
There are `n` friends that are playing a game. The friends are sitting in a circle and are numbered from `1` to `n` in **clockwise order**. More formally, moving clockwise from the `ith` friend brings you to the `(i+1)th` friend for `1 <= i < n`, and moving clockwise from the nth friend brings you to the 1st friend.

The rules of the game are as follows:

1. Start at the 1st friend.
2. Count the next k friends in the clockwise direction including the friend you started at. The counting wraps around the circle and may count some friends more than once.
3. The last friend you counted leaves the circle and loses the game.
4. If there is still more than one friend in the circle, go back to step 2 starting from the friend immediately clockwise of the friend who just lost and repeat.
5. Else, the last friend in the circle wins the game.

Given the number of friends, `n`, and an integer `k`, return the winner of the game.

```
Example 1
  Input: n = 5, k = 2
  Output: 3
  Explanation: Here are the steps of the game:
    1) Start at friend 1.
    2) Count 2 friends clockwise, which are friends 1 and 2.
    3) Friend 2 leaves the circle. Next start is friend 3.
    4) Count 2 friends clockwise, which are friends 3 and 4.
    5) Friend 4 leaves the circle. Next start is friend 5.
    6) Count 2 friends clockwise, which are friends 5 and 1.
    7) Friend 1 leaves the circle. Next start is friend 3.
    8) Count 2 friends clockwise, which are friends 3 and 5.
    9) Friend 5 leaves the circle. Only friend 3 is left, so they are the winner.
```

```
Example 2:
  Input: n = 6, k = 5
  Output: 1
  Explanation: The friends leave in this order: 5, 4, 6, 2, 3. The winner is friend 1.
```

### 2. Steps & Code Snippets

### 3. Screenshot
