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

In this problem, we must find the first position of a character ch in a string. After we find it, we reverse the string from the start until that position. If the character is not there, we do nothing.

First, we use a for loop to look for the character. We save the position in a variable called targetIndex:

```c
int targetIndex = -1;
for (int i = 0; i < n; i++) {
    if (word[i] == ch) {
        targetIndex = i;
        break; 
    }
}
```

If the character is found, we start reversing. We use a two-pointer method. This means we have one pointer at the start (left) and one at the end (right). We swap them until they meet in the middle:

```c
int left = 0;
int right = targetIndex;

while (left < right) {
    char temp = word[left];
    word[left] = word[right];
    word[right] = temp;

    left++;
    right--;
}
```

In the main function, we use scanf so we can type the word and the character in the terminal. The code will then print the final result:

```c
char word[251];
char ch;

scanf("%s %c", word, &ch);

reversePrefix(word, ch);
printf("Result: %s\n", word);
```

#### Full Code
```c
#include <stdio.h>
#include <string.h>

char* reversePrefix(char* word, char ch) {
    int n = strlen(word);
    int targetIndex = -1;

    for (int i = 0; i < n; i++) {
        if (word[i] == ch) {
            targetIndex = i;
            break;
        }
    }

    if (targetIndex != -1) {
        int left = 0;
        int right = targetIndex;

        while (left < right) {
            char temp = word[left];
            word[left] = word[right];
            word[right] = temp;

            left++;
            right--;
        }
    }

    return word;
}

int main() {
    char word[251];
    char ch;

    scanf ("%s %c", word, &ch);

    reversePrefix(word, ch);

    printf("Result: %s\n", word);

    return 0;
}
```
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

In this problem, we simulate a queue of students and a stack of sandwiches. If the student at the front likes the top sandwich, they take it and leave. If not, they move to the back of the line. We stop when nobody in the line wants the sandwich currently at the top.

1. Initializing the Queue

First, we create a queue using an array. We use front and rear variables to track the line. We copy all the students from the input into this queue array so we can move them around:

```c
int queue[100];
int front = 0;
int rear = n;

for (int i = 0; i < n; i++) {
    queue[i] = students[i]; 
}
```

2. Simulation Logic

We use a while loop to run the simulation. We also use a variable called rotationsWithoutEating. If this number becomes equal to the number of students currently left in line, it means everyone has passed the sandwich and nobody wants it, so the process stops:

```c
int stackIndex = 0;
int rotationsWithoutEating = 0;

while ((rear - front) > 0 && rotationsWithoutEating < (rear - front)) {

    if (queue[front] == sandwiches[stackIndex]) {
        front++;
        stackIndex++;
        rotationsWithoutEating = 0; 
    } else {
        queue[rear] = queue[front];
        rear++;
        front++;
        rotationsWithoutEating++;
    }
}
```

3. Main Function and Input

In the main function, we take the input for the number of students, their preferences (0 or 1), and the sandwich stack order from the terminal using scanf:

```c
int main() {
    int n;
    scanf("%d", &n);

    int students[100];
    int sandwiches[100];

    for (int i = 0; i < n; i++) {
        scanf("%d", &students[i]);
    }

    for (int i = 0; i < n; i++) {
        scanf("%d", &sandwiches[i]);
    }

    int result = countStudents(students, n, sandwiches);
    printf("Students unable to eat: %d\n", result);

    return 0;
}
```

#### Full Code
```c
#include <stdio.h>
#include <stdlib.h>

int countStudents(int* students, int n, int* sandwiches) {
    int queue[100];
    int front = 0;
    int rear = n;

    for (int i = 0; i < n; i++) {
        queue[i] = students[i]; //copying the students into queue array
    }

    int stackIndex = 0;
    int rotationsWithoutEating = 0;

    while ((rear - front) > 0 && rotationsWithoutEating < (rear - front)) {

        if (queue[front] == sandwiches[stackIndex]) {
            front++;
            stackIndex++;
            rotationsWithoutEating = 0;
        } else {
            queue[rear] = queue[front];
            rear++;
            front++;
            rotationsWithoutEating++;
        }
    }

    return (rear - front);
}

int main() {
    int n;
    scanf ("%d", &n);

    int students[100];
    int sandwiches[100];

    for (int i = 0; i < n; i++) {
        scanf("%d", &students[i]);
    }

    for (int i = 0; i < n; i++) {
        scanf("%d", &sandwiches[i]);
    }

    int result = countStudents(students, n, sandwiches);
    printf("Students unable to eat: %d\n", result);

    return 0;
}

```

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

In this problem, friends sit in a circle and play an elimination game. We count $k$ friends clockwise, and the $k$-th friend leaves the game. We repeat this until only one person is left. We use a Queue to simulate the circle.

1. Initializing the Queue

We use an array to act as our queue and use malloc to make sure we have enough space for all the rotations. We fill the queue with friends numbered from `1 to n`

```c
int *queue = (int*)malloc(n * n * sizeof(int));
int front = 0;
int rear = 0;

for (int i = 1; i <= n; i++) {
    queue[rear++] = i;
}
```

2. Game Simulation

To move "clockwise," we take a friend from the front and move them to the rear. We do this `k-1` times. On the `k-th` count, we simply remove the friend from the front and do not add them back. We repeat this until only one person remains

```c
while ((rear - front) > 1) {
    for (int i = 0; i < k - 1; i++) {
        queue[rear++] = queue[front++];
    }
    front++;
}

int winner = queue[front];
free(queue);
return winner;
```

3. Main Function and Input

In the main function, we use scanf to get the number of friends `(n)` and the step count `(k)` from the terminal. The program then prints the number of the final winner

```c
int main() {
    int n, k;
    scanf ("%d %d", &n, &k);

    int winner = findTheWinner(n, k);
    printf("The winner is friend: %d\n", winner);

    return 0;
}
```

#### Full Code

```c
#include <stdio.h>
#include <stdlib.h>

int findTheWinner(int n, int k) {
    int *queue = (int*)malloc(n * n * sizeof(int));
    int front = 0;
    int rear = 0;

    for (int i = 1; i <= n; i++) {
        queue[rear++] = i;
    }

    while ((rear - front) > 1) {
        for (int i = 0; i < k - 1; i++) {
            queue[rear++] = queue[front++];
        }
        front++;
    }

    int winner = queue[front];
    free(queue);
    return winner;
}

int main() {
    int n, k;
    scanf ("%d %d", &n, &k);

    int winner = findTheWinner(n, k);
    printf("The winner is friend: %d\n", winner);

    return 0;
}
```
### 3. Screenshot
