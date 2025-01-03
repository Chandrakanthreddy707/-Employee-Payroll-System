#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_EMPLOYEES 100

typedef struct {
    int id;
    char name[100];
    float salary;
    float tax_deductions;
} Employee;

Employee employees[MAX_EMPLOYEES];
int employee_count = 0;

void add_employee() {
    if (employee_count >= MAX_EMPLOYEES) {
        printf("Max employee limit reached.\n");
        return;
    }

    Employee new_employee;
    printf("Enter ID: ");
    scanf("%d", &new_employee.id);
    printf("Enter name: ");
    scanf("%s", new_employee.name);
    printf("Enter salary: ");
    scanf("%f", &new_employee.salary);
    printf("Enter tax deductions: ");
    scanf("%f", &new_employee.tax_deductions);

    employees[employee_count++] = new_employee;
    printf("Employee added successfully.\n");
}

float calculate_net_salary(Employee emp) {
    return emp.salary - emp.tax_deductions;
}

void display_employee_details(int id) {
    for (int i = 0; i < employee_count; i++) {
        if (employees[i].id == id) {
            printf("ID: %d, Name: %s, Salary: %.2f, Tax Deductions: %.2f, Net Salary: %.2f\n",
                   employees[i].id, employees[i].name, employees[i].salary, employees[i].tax_deductions,
                   calculate_net_salary(employees[i]));
            return;
        }
    }
    printf("Employee not found.\n");
}

void update_salary_information(int id, float new_salary) {
    for (int i = 0; i < employee_count; i++) {
        if (employees[i].id == id) {
            employees[i].salary = new_salary;
            printf("Salary updated successfully.\n");
            return;
        }
    }
    printf("Employee not found.\n");
}

int main() {
    int choice, id;
    float new_salary;

    while (1) {
        printf("\nEmployee Payroll System\n");
        printf("1. Add New Employee\n");
        printf("2. Display Employee Payroll Details\n");
        printf("3. Update Salary Information\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                add_employee();
                break;
            case 2:
                printf("Enter Employee ID: ");
                scanf("%d", &id);
                display_employee_details(id);
                break;
            case 3:
                printf("Enter Employee ID: ");
                scanf("%d", &id);
                printf("Enter New Salary: ");
                scanf("%f", &new_salary);
                update_salary_information(id, new_salary);
                break;
            case 4:
                exit(0);
            default:
                printf("Invalid choice. Please try again.\n");
        }
    }

    return 0;
}
