# Go Programming: Working with Data

## 3.1 Array Literals

### Definition:
An **array literal** in Go initializes an array with predefined values during its declaration. This concept aligns with arrays in C but provides enhanced readability and safety.

### Syntax:
```go
var arr = [5]int{1, 2, 3, 4, 5}
```

In C:
```c
int arr[5] = {1, 2, 3, 4, 5};
```

### Example: Handling Student IDs
Imagine managing student IDs in a fixed batch size.
```go
package main
import "fmt"

func main() {
    studentIDs := [3]int{101, 102, 103}
    for _, id := range studentIDs {
        fmt.Printf("Student ID: %d\n", id)
    }
}
```

In C:
```c
#include <stdio.h>

int main() {
    int studentIDs[3] = {101, 102, 103};
    for (int i = 0; i < 3; i++) {
        printf("Student ID: %d\n", studentIDs[i]);
    }
    return 0;
}
```

### Real-World Use Case:
In systems like library databases or small-scale IoT device tracking, arrays provide efficient and predictable data handling for fixed-size datasets.

[Learn more about arrays in Go](https://go.dev/doc/effective_go#arrays)

---

## 3.2 Multidimensional Arrays

### Definition:
A **multidimensional array** stores data in a tabular or grid-like format. In C, they are widely used for matrix operations, and Go supports a similar structure with better abstraction.

### Syntax:
```go
var matrix = [2][3]int{
    {1, 2, 3},
    {4, 5, 6},
}
```

In C:
```c
int matrix[2][3] = {
    {1, 2, 3},
    {4, 5, 6}
};
```

### Example: Matrix Multiplication
```go
package main
import "fmt"

func main() {
    matrixA := [2][2]int{
        {1, 2},
        {3, 4},
    }
    matrixB := [2][2]int{
        {5, 6},
        {7, 8},
    }
    var result [2][2]int

    for i := 0; i < 2; i++ {
        for j := 0; j < 2; j++ {
            for k := 0; k < 2; k++ {
                result[i][j] += matrixA[i][k] * matrixB[k][j]
            }
        }
    }
    fmt.Println("Resultant Matrix:", result)
}
```

In C:
```c
#include <stdio.h>

int main() {
    int matrixA[2][2] = {{1, 2}, {3, 4}};
    int matrixB[2][2] = {{5, 6}, {7, 8}};
    int result[2][2] = {0};

    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 2; j++) {
            for (int k = 0; k < 2; k++) {
                result[i][j] += matrixA[i][k] * matrixB[k][j];
            }
        }
    }

    printf("Resultant Matrix:\n");
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 2; j++) {
            printf("%d ", result[i][j]);
        }
        printf("\n");
    }
    return 0;
}
```

### Real-World Use Case:
Applications include image processing, computer graphics, and machine learning algorithms.

[Learn more about multidimensional arrays in Go](https://go.dev/doc/effective_go#arrays)

---

## 3.3 Array Parameters

### Passing Arrays to Functions:
In Go, arrays are passed **by value**. In C, arrays decay into pointers, allowing direct manipulation of the original data.

### Example: Calculating Average Marks
```go
package main
import "fmt"

func average(arr [5]float64) float64 {
    sum := 0.0
    for _, v := range arr {
        sum += v
    }
    return sum / float64(len(arr))
}

func main() {
    marks := [5]float64{85.5, 90.0, 78.5, 88.0, 92.0}
    fmt.Printf("Average Marks: %.2f\n", average(marks))
}
```

In C:
```c
#include <stdio.h>

float average(float arr[], int size) {
    float sum = 0;
    for (int i = 0; i < size; i++) {
        sum += arr[i];
    }
    return sum / size;
}

int main() {
    float marks[] = {85.5, 90.0, 78.5, 88.0, 92.0};
    printf("Average Marks: %.2f\n", average(marks, 5));
    return 0;
}
```

### Real-World Use Case:
Used in analytics dashboards for generating metrics like averages, sums, or other aggregates.

[Learn more about passing arrays in Go](https://go.dev/doc/effective_go#functions)

---

## 3.4 Slices and Slice Parameters

### Definition:
A **slice** is a dynamic abstraction over arrays. In C, similar functionality is achieved using pointers with manual memory management.

### Example: Managing Dynamic Inventory
```go
package main
import "fmt"

func addItem(inventory []string, item string) []string {
    return append(inventory, item)
}

func main() {
    inventory := []string{"Laptop", "Mouse"}
    inventory = addItem(inventory, "Keyboard")
    fmt.Println("Updated Inventory:", inventory)
}
```

In C (using dynamic memory allocation):
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

char **addItem(char **inventory, int *size, const char *item) {
    inventory = realloc(inventory, (*size + 1) * sizeof(char *));
    inventory[*size] = malloc(strlen(item) + 1);
    strcpy(inventory[*size], item);
    (*size)++;
    return inventory;
}

int main() {
    int size = 2;
    char **inventory = malloc(size * sizeof(char *));
    inventory[0] = strdup("Laptop");
    inventory[1] = strdup("Mouse");

    inventory = addItem(inventory, &size, "Keyboard");

    printf("Updated Inventory:\n");
    for (int i = 0; i < size; i++) {
        printf("%s\n", inventory[i]);
        free(inventory[i]);
    }
    free(inventory);
    return 0;
}
```

### Real-World Use Case:
Managing growing datasets, such as inventory systems or user-generated content.

[Learn more about slices in Go](https://go.dev/blog/slices-intro)

---

## 3.5 Multidimensional Slices

### Example: Variable-Length Row Data
```go
package main
import "fmt"

func main() {
    attendance := [][]string{
        {"Present", "Absent", "Present"},
        {"Absent", "Present"},
        {"Present", "Present", "Absent", "Present"},
    }
    for i, day := range attendance {
        fmt.Printf("Day %d Attendance: %v\n", i+1, day)
    }
}
```

[Learn more about slices and multidimensional slices](https://go.dev/blog/slices-intro)

---

## 3.6 Structures and Structure Parameters

### Example: Employee Management System
```go
package main
import "fmt"

type Employee struct {
    ID     int
    Name   string
    Salary float64
}

func giveRaise(e *Employee, percentage float64) {
    e.Salary += e.Salary * percentage / 100
}

func main() {
    emp := Employee{ID: 101, Name: "Alice", Salary: 50000}
    fmt.Println("Before Raise:", emp)
    giveRaise(&emp, 10)
    fmt.Println("After Raise:", emp)
}
```

In C:
```c
#include <stdio.h>

struct Employee {
    int ID;
    char Name[50];
    float Salary;
};

void giveRaise(struct Employee *e, float percentage) {
    e->Salary += e->Salary * percentage / 100;
}

int main() {
    struct Employee emp = {101, "Alice", 50000};
    printf("Before Raise: ID: %d, Name: %s, Salary: %.2f\n", emp.ID, emp.Name, emp.Salary);
    giveRaise(&emp, 10);
    printf("After Raise: ID: %d, Name: %s, Salary: %.2f\n", emp.ID, emp.Name, emp.Salary);
    return 0;
}
```

[Learn more about structs in Go](https://go.dev/doc/effective_go#structs)

---
