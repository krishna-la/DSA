# DSA
Quick Sort:

#include <stdio.h>

// Function to swap elements
void swap(int* a, int* b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Partition function using last element as pivot
int partition(int arr[], int low, int high)
{
    int pivot = arr[high];
    int i = low - 1;

    for (int j = low; j < high; j++)
    {
        if (arr[j] < pivot)
        {
            i++;
            swap(&arr[i], &arr[j]);
        }
    }

    swap(&arr[i + 1], &arr[high]);

    return i + 1;
}

// QuickSort function
void quickSort(int arr[], int low, int high)
{
    if (low < high)
    {
        int pi = partition(arr, low, high);

        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

// Function to print array
void printArray(int arr[], int size)
{
    for (int i = 0; i < size; i++)
        printf("%d ", arr[i]);

    printf("\n");
}

// Main function
int main()
{
    int arr[100], n;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    printf("Enter elements:\n");

    for (int i = 0; i < n; i++)
        scanf("%d", &arr[i]);

    printf("Original Array: ");
    printArray(arr, n);

    quickSort(arr, 0, n - 1);

    printf("Sorted Array: ");
    printArray(arr, n);

    return 0;
}


-=-----------------------------------------------------\

  2. selection:

#include <stdio.h>

int main() {
    int a[100], n, i, j, temp; // Variables

    scanf("%d", &n); // Read size
    for(i = 0; i < n; i++)
        scanf("%d", &a[i]); // Read elements

    for(i = 0; i < n; i++) { // Select position
        for(j = i + 1; j < n; j++) { // Compare remaining elements
            if(a[i] > a[j]) { // Check smaller element
                temp = a[i]; // Store current element
                a[i] = a[j]; // Swap
                a[j] = temp; // Complete swap
            }
        }
    }

    for(i = 0; i < n; i++)
        printf("%d ", a[i]); // Print sorted array

    return 0;
}

--------------------------------
  3, insertion

    #include <stdio.h>

int main() {
    int a[100], n, i, j, key; // Variables

    scanf("%d", &n); // Read size
    for(i = 0; i < n; i++)
        scanf("%d", &a[i]); // Read elements

    for(i = 1; i < n; i++) { // Start from second element
        key = a[i]; // Store current element
        j = i - 1; // Previous index

        while(j >= 0 && a[j] > key) { // Find correct position
            a[j + 1] = a[j]; // Shift element right
            j--; // Move left
        }

        a[j + 1] = key; // Insert key
    }

    for(i = 0; i < n; i++)
        printf("%d ", a[i]); // Print sorted array

    return 0;
}

4. Stack using array
  #include <stdio.h>
#define MAX 100

int stack[MAX], top = -1; // Stack and top

void push() {
    int x;
    if(top == MAX - 1) // Check overflow
        printf("Stack Overflow\n");
    else {
        printf("Enter value: ");
        scanf("%d", &x);
        stack[++top] = x; // Insert element
    }
}

void pop() {
    if(top == -1) // Check underflow
        printf("Stack Underflow\n");
    else
        printf("Popped: %d\n", stack[top--]); // Remove top
}

void display() {
    int i;
    if(top == -1) // Check empty
        printf("Stack Empty\n");
    else
        for(i = top; i >= 0; i--)
            printf("%d\n", stack[i]); // Print top to bottom
}

int main() {
    int ch;
    do {
        printf("\n1.Push 2.Pop 3.Display 4.Exit\n");
        scanf("%d", &ch);

        switch(ch) {
            case 1: push(); break; // Insert
            case 2: pop(); break; // Delete
            case 3: display(); break; // Display
        }
    } while(ch != 4); // Repeat menu

    return 0;
}

==============
  5. queue using array
  #include <stdio.h>
#define MAX 100

int q[MAX], front = -1, rear = -1; // Queue variables

void insert() {
    int x;
    if(rear == MAX - 1) // Check full
        printf("Queue Full\n");
    else {
        printf("Enter value: ");
        scanf("%d", &x);
        if(front == -1) front = 0; // First element
        q[++rear] = x; // Insert at rear
    }
}

void delete() {
    if(front == -1 || front > rear) // Check empty
        printf("Queue Empty\n");
    else {
        printf("Deleted: %d\n", q[front++]); // Remove front
        if(front > rear) front = rear = -1; // Reset queue
    }
}

void display() {
    int i;
    if(front == -1) // Check empty
        printf("Queue Empty\n");
    else
        for(i = front; i <= rear; i++)
            printf("%d ", q[i]); // Print queue
}

int main() {
    int ch;
    do {
        printf("\n1.Insert 2.Delete 3.Display 4.Exit\n");
        scanf("%d", &ch);

        switch(ch) {
            case 1: insert(); break; // Enqueue
            case 2: delete(); break; // Dequeue
            case 3: display(); break; // Display
        }
    } while(ch != 4);

    return 0;
}

===========
  6. sLL
  #include <stdio.h>
#include <stdlib.h>

struct Node {
    int data; // Node data
    struct Node *next; // Next node address
};

struct Node *head = NULL; // First node

void insert() {
    struct Node *newnode, *temp;
    newnode = malloc(sizeof(struct Node)); // Allocate memory
    printf("Enter value: ");
    scanf("%d", &newnode->data);
    newnode->next = NULL; // Last node link

    if(head == NULL)
        head = newnode; // First node
    else {
        temp = head;
        while(temp->next != NULL)
            temp = temp->next; // Reach last node
        temp->next = newnode; // Attach new node
    }
}

void delete() {
    struct Node *temp = head, *prev = NULL;
    int x;
    printf("Enter value to delete: ");
    scanf("%d", &x);

    while(temp != NULL && temp->data != x) {
        prev = temp;
        temp = temp->next; // Search node
    }

    if(temp == NULL)
        printf("Not found\n");
    else {
        if(prev == NULL)
            head = temp->next; // Delete first node
        else
            prev->next = temp->next; // Bypass node
        free(temp); // Release memory
    }
}

void display() {
    struct Node *temp = head;
    while(temp != NULL) {
        printf("%d -> ", temp->data); // Print data
        temp = temp->next; // Move next
    }
    printf("NULL\n");
}

int main() {
    int ch;
    do {
        printf("\n1.Insert 2.Delete 3.Display 4.Exit\n");
        scanf("%d", &ch);
        if(ch == 1) insert();
        else if(ch == 2) delete();
        else if(ch == 3) display();
    } while(ch != 4);

    return 0;
}

==============================
  7. DLL
  #include <stdio.h>
#include <stdlib.h>

struct Node {
    int data; // Node data
    struct Node *prev, *next; // Previous and next
};

struct Node *head = NULL, *tail = NULL; // List ends

void insert() {
    struct Node *newnode = malloc(sizeof(struct Node)); // Create node
    printf("Enter value: ");
    scanf("%d", &newnode->data);
    newnode->next = NULL; // No next node
    newnode->prev = tail; // Previous is old tail

    if(head == NULL)
        head = newnode; // First node
    else
        tail->next = newnode; // Connect old tail

    tail = newnode; // Update tail
}

void delete() {
    struct Node *temp = head;
    int x;
    printf("Enter value: ");
    scanf("%d", &x);

    while(temp != NULL && temp->data != x)
        temp = temp->next; // Search node

    if(temp == NULL)
        printf("Not found\n");
    else {
        if(temp->prev != NULL)
            temp->prev->next = temp->next; // Update previous
        else
            head = temp->next; // Delete first

        if(temp->next != NULL)
            temp->next->prev = temp->prev; // Update next
        else
            tail = temp->prev; // Delete last

        free(temp); // Release memory
    }
}

void display() {
    struct Node *temp = head;
    while(temp != NULL) {
        printf("%d <-> ", temp->data); // Print data
        temp = temp->next; // Move forward
    }
    printf("NULL\n");
}

int main() {
    int ch;
    do {
        printf("\n1.Insert 2.Delete 3.Display 4.Exit\n");
        scanf("%d", &ch);
        if(ch == 1) insert();
        else if(ch == 2) delete();
        else if(ch == 3) display();
    } while(ch != 4);

    return 0;
}

==========================
  8. Circular LLL
  #include <stdio.h>
#include <stdlib.h>

struct Node {
    int data; // Node data
    struct Node *next; // Next node
};

struct Node *last = NULL; // Last node

void insert() {
    struct Node *newnode = malloc(sizeof(struct Node)); // Create node
    printf("Enter value: ");
    scanf("%d", &newnode->data);

    if(last == NULL) {
        newnode->next = newnode; // Point to itself
        last = newnode; // First and last
    } else {
        newnode->next = last->next; // Link to head
        last->next = newnode; // Update head
    }
}

void delete() {
    struct Node *temp, *prev;
    if(last == NULL) {
        printf("List Empty\n");
        return;
    }

    temp = last->next; // Start at head

    if(temp == last) {
        last = NULL; // Only one node
    } else {
        prev = temp;
        while(prev->next != last)
            prev = prev->next; // Find previous to last
        prev->next = last->next; // Remove last link
        temp = last; // Node to delete
        last = prev; // Update last
    }

    free(temp); // Release memory
}

void display() {
    struct Node *temp;
    if(last == NULL) {
        printf("List Empty\n");
        return;
    }

    temp = last->next; // Start at head
    do {
        printf("%d ", temp->data); // Print node
        temp = temp->next; // Move next
    } while(temp != last->next); // Stop at head again
}

int main() {
    int ch;
    do {
        printf("\n1.Insert 2.Delete 3.Display 4.Exit\n");
        scanf("%d", &ch);
        if(ch == 1) insert();
        else if(ch == 2) delete();
        else if(ch == 3) display();
    } while(ch != 4);

    return 0;
}


=========================
  9/ stack using linked list

  #include <stdio.h>
#include <stdlib.h>

struct Node {
    int data; // Data
    struct Node *next; // Next pointer
};

struct Node *top = NULL; // Stack top

void push() {
    struct Node *newnode = malloc(sizeof(struct Node)); // Create node
    printf("Enter value: ");
    scanf("%d", &newnode->data);
    newnode->next = top; // Link to old top
    top = newnode; // Update top
}

void pop() {
    struct Node *temp;
    if(top == NULL) {
        printf("Stack Empty\n");
        return;
    }
    temp = top; // Store top node
    printf("Popped: %d\n", temp->data);
    top = top->next; // Move top
    free(temp); // Delete old top
}

void display() {
    struct Node *temp = top;
    while(temp != NULL) {
        printf("%d -> ", temp->data); // Print data
        temp = temp->next; // Move next
    }
    printf("NULL\n");
}

int main() {
    int ch;
    do {
        printf("\n1.Push 2.Pop 3.Display 4.Exit\n");
        scanf("%d", &ch);
        if(ch == 1) push();
        else if(ch == 2) pop();
        else if(ch == 3) display();
    } while(ch != 4);

    return 0;
}

10. QUEUE sign LL

  #include <stdio.h>
#include <stdlib.h>

struct Node {
    int data; // Data
    struct Node *next; // Next pointer
};

struct Node *front = NULL, *rear = NULL; // Queue ends

void insert() {
    struct Node *newnode = malloc(sizeof(struct Node)); // Create node
    printf("Enter value: ");
    scanf("%d", &newnode->data);
    newnode->next = NULL; // Last node

    if(front == NULL)
        front = rear = newnode; // First node
    else {
        rear->next = newnode; // Connect new node
        rear = newnode; // Update rear
    }
}

void delete() {
    struct Node *temp;
    if(front == NULL) {
        printf("Queue Empty\n");
        return;
    }

    temp = front; // Store front
    printf("Deleted: %d\n", temp->data);
    front = front->next; // Move front

    if(front == NULL)
        rear = NULL; // Queue became empty

    free(temp); // Release memory
}

void display() {
    struct Node *temp = front;
    while(temp != NULL) {
        printf("%d -> ", temp->data); // Print data
        temp = temp->next; // Move next
    }
    printf("NULL\n");
}

int main() {
    int ch;
    do {
        printf("\n1.Insert 2.Delete 3.Display 4.Exit\n");
        scanf("%d", &ch);
        if(ch == 1) insert();
        else if(ch == 2) delete();
        else if(ch == 3) display();
    } while(ch != 4);

    return 0;
}


=-==================
  11. DIJKSTRA's Algo

  #include <stdio.h>

#define MAX 15
#define INF 999

int main() {
    int graph[MAX][MAX], dist[MAX], visited[MAX] = {0}; // Graph and arrays
    int n, source, i, j, u, min; // Variables

    printf("Enter number of vertices: ");
    scanf("%d", &n); // Read vertices

    printf("Enter adjacency matrix:\n");
    for(i = 0; i < n; i++)
        for(j = 0; j < n; j++)
            scanf("%d", &graph[i][j]); // Read edge weights

    printf("Enter source vertex (0 to %d): ", n - 1);
    scanf("%d", &source); // Read source

    for(i = 0; i < n; i++)
        dist[i] = INF; // Set infinity

    dist[source] = 0; // Source distance is zero

    for(i = 0; i < n; i++) {
        min = INF; // Reset minimum
        u = -1; // No vertex selected

        for(j = 0; j < n; j++) {
            if(!visited[j] && dist[j] < min) {
                min = dist[j]; // Update minimum
                u = j; // Select vertex
            }
        }

        if(u == -1) break; // No reachable vertex

        visited[u] = 1; // Mark visited

        for(j = 0; j < n; j++) {
            if(graph[u][j] > 0 && !visited[j] &&
               dist[u] + graph[u][j] < dist[j]) {
                dist[j] = dist[u] + graph[u][j]; // Update distance
            }
        }
    }

    printf("Shortest distances:\n");
    for(i = 0; i < n; i++) {
        if(dist[i] == INF)
            printf("%d -> %d : No path\n", source, i);
        else
            printf("%d -> %d : %d\n", source, i, dist[i]);
    }

    return 0;
}
