# Structures

Structures (or “**structs**”) are one of the most powerful data structures built into C. And allows us to store **multiple elements of data of any type** inside a single variable. If you are familiar with any object-oriented paradigms, this is the closest data structure that gets to an object (but without methods).

# Creating a Struct

Say for example, if we want to store a student’s name (we assume that’s going to be within 50 characters), student number (a string that contains no more than 10 characters), and GPA (as a floating point number) inside a single variable, we can define its type as a structure. Like so:

```c
struct student {
    char name[51];
    char student_num[11];
    float gpa;
};
// (Note that the semicolon is required)
```

Each data element that is inside a struct (in the above example it would be `name`, `student_num`, or `gpa`) is called a **field**. And the name of each field must be unique, since we will be using each field’s name to access them. And in order to access the fields inside of a struct, we would have to use the dot operator, like so:

```c
// First we create a variable with our struct as its type, like so:
struct student s;

// Then we can access its fields like so:
strcpy(s.name, "John");
strcpy(s.student_num, "123456789");
s.gpa = 3.95;

// We can even make arrays of structs if we need to:
struct student many_students[100];
```

**Important Note**: Unlike arrays, when we create a struct, the variable is **not a pointer to a memory address**. Thus when we do something like `struct student p = s;`, we would be creating a **separate copy** of the struct `s` rather than another a pointer referencing the same struct. This also means that if we were to pass a struct into a function as a parameter, we would be passing its **value, not its reference**.

Notice how that in the above example, every time when we have to create a new struct variable, we would have to type `struct student`. However, we can create an **alias** for that struct using the `typedef` keyword so that we don’t have to type the `struct` keyword, like so:

```c
typedef struct student {
    char name[51];
    char student_num[11];
    float gpa;
} Student;

// So that we can create struct variables like so:
Student s;
```

# Pointers to Structs

In cases where we have to dynamically allocate structs, we would have to use them through pointers to structs. And since dereferencing and then using the dot operator would be too tedious, C provides the arrow operator `->` to access the fields of a struct using its pointer.

```c
typedef struct student {
    char name[51];
    char student_num[11];
    float gpa;
} Student;

// Say we have a struct, and its pointer:
Student s, *p;
p = &s;

s.gpa = 4.0;

// Then we can access the gpa of s through p, like so:
printf("GPA: %f \n", p->gpa);

// This is the same as writing (*p).gpa
```

Since structs behave like normal variable types, dynamically allocating an array of structs can be done like so:

```c
Student *students = malloc(100 * sizeof(Student));
```