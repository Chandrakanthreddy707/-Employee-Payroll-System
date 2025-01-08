#include <stdio.h>
#include <string.h>

#define MAX_EMPLOYEES 100
#define MAX_NAME_LENGTH 50

typedef struct {
    char name[MAX_NAME_LENGTH];
    int id;
    float hours_worked;
    float hourly_rate;
    float salary;
} Employee;

void addEmployee(Employee employees[], int *num_employees) {
    if (*num_employees >= MAX_EMPLOYEES) {
        printf("Cannot add more employees. Maximum limit reached.\n");
        return;
    }
    printf("Enter the name of employee %d: ", *num_employees + 1);
    scanf("%s", employees[*num_employees].name);
    printf("Enter the ID of employee %d: ", *num_employees + 1);
    scanf("%d", &employees[*num_employees].id);
    printf("Enter the hours worked by employee %d: ", *num_employees + 1);
    scanf("%f", &employees[*num_employees].hours_worked);
    printf("Enter the hourly rate of employee %d: ", *num_employees + 1);
    scanf("%f", &employees[*num_employees].hourly_rate);
    employees[*num_employees].salary = employees[*num_employees].hours_worked * employees[*num_employees].hourly_rate;
    (*num_employees)++;
}

void displayEmployees(Employee employees[], int num_employees) {
    printf("\nEmployee Payroll List:\n");
    for (int i = 0; i < num_employees; i++) {
        printf("Name: %s, ID: %d, Hours Worked: %.2f, Hourly Rate: %.2f, Salary: %.2f\n",
               employees[i].name, employees[i].id, employees[i].hours_worked, employees[i].hourly_rate, employees[i].salary);
    }
}

int main() {
    Employee employees[MAX_EMPLOYEES];
    int num_employees = 0;
    int choice;
    while (1) {
        printf("\nEmployee Payroll Management System\n");
        printf("1. Add Employee\n");
        printf("2. Display Employees\n");
        printf("3. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        switch (choice) {
            case 1:
                addEmployee(employees, &num_employees);
                break;
            case 2:
                displayEmployees(employees, num_employees);
                break;
            case 3:
                return 0;
            default:
                printf("Invalid choice. Please try again.\n");
        }
    }
    return 0;
}
