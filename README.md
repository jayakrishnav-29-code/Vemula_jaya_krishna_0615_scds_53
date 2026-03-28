# Vemula_jaya_krishna_0615_scds_53


/*Q1: Reverse a String using Stack
Write a C program to reverse a given string using a stack.
Example:
Input: DATA
Output: ATAD*/

Algorithm
1)Start
2)Declare a stack (array) and initialize top = -1
3)Read the input string
4) Traverse the string from left to right
       i)Push each character onto the stack
5)Traverse the string again
      i)Pop characters from the stack and store back into the string
6)Print the reversed string
7)Stop

#include <stdio.h>
#include <string.h>
#define MAX 100
char stack[MAX];
int top = -1;
void push(char ch) {
    if (top == MAX - 1) {
        printf("Stack Overflow\n");
    } else {
        stack[++top] = ch;
    }
}
char pop() {
    if (top == -1) {
        printf("Stack Underflow\n");
        return '\0';
    } else {
        return stack[top--];
    }
}

int main() {
    char str[MAX];
    int i, len;
    printf("Enter a string: ");
    scanf("%s", str);
    len = strlen(str);
    // Push all characters into stack
    for (i = 0; i < len; i++) {
        push(str[i]);
    }
    for (i = 0; i < len; i++) {
        str[i] = pop();
    }
    printf("Reversed string: %s\n", str);
    return 0;
}



/*Q2: Balanced Parentheses
Write a C program using a stack to check whether the parentheses in an expression are
balanced.
Example:
Input: (A+B)*(C-D)
Output: Balanced Expression*/


Algorithm
1)Start
2)Initialize empty stack
3)Read expression
4)For each character:
     i)Push opening brackets
     ii)For closing brackets:
          i)If stack empty → Not Balanced
           ii)Pop and check match
5)If stack empty → Balanced, else Not Balanced
6)Stop

#include <stdio.h>
#include <string.h>
#define MAX 100
char stack[MAX];
int top = -1;
void push(char ch) {
    stack[++top] = ch;
}
char pop() {
    return stack[top--];
}
int match(char a, char b) {
    return (a=='('&&b==')') || (a=='{'&&b=='}') || (a=='['&&b==']');
}
int main() {
    char exp[MAX];
    int i;
    printf("Enter expression: ");
    scanf("%s", exp);
    for(i=0; i<strlen(exp); i++) {
        if(exp[i]=='(' || exp[i]=='{' || exp[i]=='[')
            push(exp[i]);
        else if(exp[i]==')' || exp[i]=='}' || exp[i]==']') {
            if(top==-1 || !match(pop(), exp[i])) {
                printf("Not Balanced Expression\n");
                return 0;
            }
        }
    }
    if(top==-1)
        printf("Balanced Expression\n");
    else
        printf("Not Balanced Expression\n");
    return 0;
}


/*Q3: Next Greater Element
Write a C program to find the Next Greater Element for each element in an array
using a stack.
Example:
Input: 4 5 2 10 8
Output:
4 → 5
5 → 10
2 → 10
10 → -1
8 → -1 */

Algorithm
1)Start
2)Read array elements
3)Initialize empty stack
4)Traverse array from right to left
      Pop elements smaller than or equal to current
      If stack empty → result = -1
      Else → result = top of stack
      Push current element to stack
5)Print results
6)Stop


#include <stdio.h>
#define MAX 100
int stack[MAX];
int top = -1;
void push(int x) {
    stack[++top] = x;
}
int pop() {
    return stack[top--];
}
int peek() {
    return stack[top];
}
int isEmpty() {
    return top == -1;
}
int main() {
    int arr[MAX], res[MAX];
    int n, i;
    printf("Enter number of elements: ");
    scanf("%d", &n);
    printf("Enter elements: ");
    for(i = 0; i < n; i++)
        scanf("%d", &arr[i]);
    for(i = n - 1; i >= 0; i--) {
        while(!isEmpty() && peek() <= arr[i])
            pop();
        if(isEmpty())
            res[i] = -1;
        else
            res[i] = peek();
        push(arr[i]);
    }
    printf("Next Greater Elements:\n");
    for(i = 0; i < n; i++) {
        printf("%d -> %d\n", arr[i], res[i]);
    }
    return 0;
}

/*Q4: Printer Queue Simulation
Write a C program to simulate a printer queue system using queue operations.
Operations to support:
• Add document to queue
• Print document
• Display pending documents*/




Algorithm
1)Start
2)Initialize queue (front = rear = -1)
3)Repeat menu:
    Insert document (enqueue)
    Print document (dequeue)
     Display queue
4)Handle overflow and underflow conditions
5)Stop



#include <stdio.h>
#include <string.h>
#define MAX 5
char queue[MAX][50];  // Queue to store document names
int front = -1, rear = -1;
void enqueue(char doc[]) {
    if (rear == MAX - 1) {
        printf("Queue Overflow (Printer Queue Full)\n");
        return;
    }
    if (front == -1)
        front = 0;
    rear++;
    strcpy(queue[rear], doc);
    printf("Document added to queue\n");
}
void dequeue() {
    if (front == -1 || front > rear) {
        printf("Queue Underflow (No documents to print)\n");
        return;
    }
    printf("Printing document: %s\n", queue[front]);
    front++;
}
void display() {
    if (front == -1 || front > rear) {
        printf("No pending documents\n");
        return;
    }
    printf("Pending documents:\n");
    for (int i = front; i <= rear; i++) {
        printf("%s\n", queue[i]);
    }
}

int main() {
    int choice;
    char doc[50];
    do {
        printf("\n--- Printer Queue Menu ---\n");
        printf("1. Add Document\n");
        printf("2. Print Document\n");
        printf("3. Display Queue\n");
        printf("4. Exit\n");
        printf("Enter choice: ");
        scanf("%d", &choice);
        switch(choice) {
            case 1:
                printf("Enter document name: ");
                scanf("%s", doc);
                enqueue(doc);
                break;
            case 2:
                dequeue();
                break;
            case 3:
                display();
                break;
            case 4:
                printf("Exiting...\n");
                break;
            default:
                printf("Invalid choice\n");
        }
    } while(choice != 4);
    return 0;
}






Q5: Circular Queue Basic Operations
Write a C program to implement a Circular Queue using an array.
The program should support the following operations:
• Enqueue – Insert an element into the circular queue.
• Dequeue – Remove an element from the circular queue.
• Peek – Display the front element of the queue without removing it.
• Display – Show all elements currently present in the queue.
The program should be menu driven so that the user can select and perform different
operations on the circular queue.



Algorithm
1)Start
2)Initialize front = rear = -1
3)For Enqueue:
       Check overflow → (rear + 1) % MAX == front
       Insert element and update rear
4)For Dequeue:
      Check underflow → queue empty
      Remove element and update front
5)For Peek:
      Display front element
6)For Display:
      Traverse from front to rear circularly
7)Repeat using menu until exit
8)Stop


#include <stdio.h>
#define MAX 5
int queue[MAX];
int front = -1, rear = -1;
void enqueue(int value) {
    if ((rear + 1) % MAX == front) {
        printf("Queue Overflow\n");
        return;
    }
    if (front == -1)
        front = 0;
    rear = (rear + 1) % MAX;
    queue[rear] = value;
    printf("Inserted: %d\n", value);
}
void dequeue() {
    if (front == -1) {
        printf("Queue Underflow\n");
        return;
    }
    printf("Deleted: %d\n", queue[front]);
    if (front == rear) {
        front = rear = -1;
    } else {
        front = (front + 1) % MAX;
    }
}
void peek() {
    if (front == -1) {
        printf("Queue is Empty\n");
    } else {
        printf("Front element: %d\n", queue[front]);
    }
}
void display() {
    if (front == -1) {
        printf("Queue is Empty\n");
        return;
    }
    int i = front;
    printf("Queue elements:\n");
    while (1) {
        printf("%d ", queue[i]);
        if (i == rear)
            break;
        i = (i + 1) % MAX;
    }
    printf("\n");
}

int main() {
    int choice, value;
    do {
        printf("\n--- Circular Queue Menu ---\n");
        printf("1. Enqueue\n");
        printf("2. Dequeue\n");
        printf("3. Peek\n");
        printf("4. Display\n");
        printf("5. Exit\n");
        printf("Enter choice: ");
        scanf("%d", &choice);
        switch(choice) {
            case 1:
                printf("Enter value: ");
                scanf("%d", &value);
                enqueue(value);
                break;
            case 2:
                dequeue();
                break;
            case 3:
                peek();
                break;
            case 4:
                display();
                break;
            case 5:
                printf("Exiting...\n");
                break;
            default:
                printf("Invalid choice\n");
        }
    } while(choice != 5);
    return 0;
}








