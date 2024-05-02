# Expense-Tracker
```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#define MAX_EXPENSES 100
struct Expense {
char description[100];
float amount;
char category[50];
};
struct Expense expenses[MAX_EXPENSES];
float expenseLimit;
int expenseCount = 0;
float previousMonthsSum = 0;
void ClearData() {
memset(expenses, 0, sizeof(expenses));
expenseCount = 0;
previousMonthsSum = 0;
}
void EnterData() {
if (expenseCount < MAX_EXPENSES) {
printf("Enter category: ");
scanf("%s", expenses[expenseCount].category);
printf("Enter amount: ");
scanf("%f", &expenses[expenseCount].amount);
printf("Enter Description: ");
scanf("%s", expenses[expenseCount].description);
expenseCount++;
} else {
printf("Expense limit reached. Cannot add more expenses.\n");
}
}
void GenerateReport() {
if (expenseCount == 0) {
printf("No data entered. Please enter data before generating a report.\n");
return;
}
printf("Generating report...\n");
float currentMonthSum = 0;
printf("Category\t Description\t Amount\n");
for (int i = 0; i < expenseCount; i++) {
printf("%s\t %s\t %.2f\n", expenses[i].category, expenses[i].description,
expenses[i].amount);
currentMonthSum += expenses[i].amount;
}
printf("Total Expense this month: %.2f\n", currentMonthSum);
if (currentMonthSum > expenseLimit) {
float extra = currentMonthSum - expenseLimit;
printf("You have exceeded your expense limit. You have spent %.2f more\n",
extra);
}
else {
float saved = expenseLimit - currentMonthSum;
printf("Yay! You saved %.2f this month\n", saved);
}
if (expenseCount > 1) {
float previousMonthsSum = 0;
for (int i = 0; i < expenseCount - 1; i++) {
previousMonthsSum += expenses[i].amount;
}
if (currentMonthSum > previousMonthsSum) {
printf("This month's expenses are higher than the previous month.\n");
} else if (currentMonthSum < previousMonthsSum) {
printf("Congratulations! You spent less this month compared to the previous month.\n");
} else {
printf("This month's expenses are the same as the previous month.\n");
}
} else {
printf("No previous data for comparison. Monthly comparisons set to 0.\n");
}
}
void SetLimit() {
printf("Enter your expense limit: ");
scanf("%f", &expenseLimit);
}
int main() {
int choice;
SetLimit();
while (getchar() != '\n');
while (1) {
printf("\nEnter your choice: 1) Enter data 2) Generate report 3) Change expense limit 4) Clear data 5) Exit\n");
scanf("%d", &choice);
while (getchar() != '\n');
switch (choice) {
case 1:
EnterData();
while (getchar() != '\n');
break;
case 2:
GenerateReport();
break;
case 3:
SetLimit();
break;
case 4:
ClearData();
printf("Data cleared.\n");
break;
case 5:
printf("Exiting program. Goodbye!\n");
exit(0);
default:
printf("Invalid choice. Please enter a valid option.\n");
}
}
return 0;
}
```
