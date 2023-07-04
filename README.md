#include <stdio.h>
#include <stdlib.h>

#define MAX_STUDENTS 100

struct Student {
    int id;
    char name[50];
    int age;
};

struct Student database[MAX_STUDENTS];
int numStudents = 0;

void createStudent(int id, char name[], int age) {
    if (numStudents < MAX_STUDENTS) {
        struct Student newStudent;
        newStudent.id = id;
        strcpy(newStudent.name, name);
        newStudent.age = age;
        
        database[numStudents++] = newStudent;
        
        printf("Student created successfully.\n");
    } else {
        printf("Database is full. Cannot create new student.\n");
    }
}

void readStudent(int id) {
    int i;
    for (i = 0; i < numStudents; i++) {
        if (database[i].id == id) {
            printf("ID: %d\nName: %s\nAge: %d\n", database[i].id, database[i].name, database[i].age);
            return;
        }
    }
    
    printf("Student not found.\n");
}

void updateStudent(int id, char name[], int age) {
    int i;
    for (i = 0; i < numStudents; i++) {
        if (database[i].id == id) {
            strcpy(database[i].name, name);
            database[i].age = age;
            
            printf("Student updated successfully.\n");
            return;
        }
    }
    
    printf("Student not found.\n");
}

void deleteStudent(int id) {
    int i, found = 0;
    for (i = 0; i < numStudents; i++) {
        if (found) {
            database[i - 1] = database[i];
        } else if (database[i].id == id) {
            found = 1;
        }
    }
    
    if (found) {
        numStudents--;
        printf("Student deleted successfully.\n");
    } else {
        printf("Student not found.\n");
    }
}

int main() {
    createStudent(1, "John Doe", 20);
    createStudent(2, "Jane Smith", 22);
    
    readStudent(1);
    
    updateStudent(1, "John Smith", 21);
    
    readStudent(1);
    
    deleteStudent(2);
    
    readStudent(2);
    
    return 0;
}
