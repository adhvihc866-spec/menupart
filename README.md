
# menupart

include <stdio.h>
#include <stdlib.h>
#include <string.h>
struct Part {
char part_no[20];
char part_name[30];
char model_no[20];
char description[50];
struct Part *next;
};
struct Part *head = NULL;
void addPart() {
struct Part *newPart = (struct Part *)malloc(sizeof(struct Part));
if (newPart == NULL) {
printf("Memory allocation failed!\n");
exit(1);
}
printf("Enter Part Number (e.g., P1001) : ");
scanf("%s", newPart->part_no);
printf("Enter Part Name (e.g., Bolt) : ");
scanf(" %[^\n]", newPart->part_name);
printf("Enter Model Number (e.g., M2024) : ");
scanf("%s", newPart->model_no);
printf("Enter Description : ");
scanf(" %[^\n]", newPart->description);
newPart->next = head;
head = newPart;
printf("Part '%s' added to the inventory successfully.\n",
newPart->part_no);
}
void removePart() {
char key[20];
if (head == NULL) {
printf("Inventory is empty! Nothing to remove.\n");
return;
}
printf("Enter Part Number or Model Number to remove: ");
scanf("%s", key);
struct Part *temp = head, *prev = NULL;
while (temp != NULL) {
if (strcmp(temp->part_no, key) == 0 ||
strcmp(temp->model_no, key) == 0) {
if (prev == NULL) {
head = temp->next;
} else {
prev->next = temp->next;
}
printf("Obsolete Part (Part No: %s, Model: %s) removed.\n",
temp->part_no, temp->model_no);
free(temp);
return;
}
prev = temp;
temp = temp->next;
}
printf("Part with Part/Model Number '%s' not found.\n", key);
}
void searchPart() {
char key[20];
if (head == NULL) {
printf("Inventory is empty!\n");
return;
}
printf("Enter Part Number or Model Number to search: ");
scanf("%s", key);
struct Part *temp = head;
while (temp != NULL) {
if (strcmp(temp->part_no, key) == 0 ||
strcmp(temp->model_no, key) == 0) {
printf("\nPart Details Found:\n");
printf("Part Number : %s\n", temp->part_no);
printf("Part Name : %s\n", temp->part_name);
printf("Model Number : %s\n", temp->model_no);
printf("Description : %s\n", temp->description);
return;
}
temp = temp->next;
}
printf("Part with Part/Model Number '%s' not found.\n", key);
}
void displayParts() {
if (head == NULL) {
printf("Inventory is empty.\n");
return;
}
struct Part *temp = head;
printf("\n%-10s %-15s %-12s %-25s\n",
"Part_No", "Part_Name", "Model_No", "Description");
printf("------------------------------------------------------------------\n");
while (temp != NULL) {
printf("%-10s %-15s %-12s %-25s\n",
temp->part_no, temp->part_name,
temp->model_no, temp->description);
temp = temp->next;
}
}
int main() {
int choice;
while (1) {
printf("\n--- Machine Parts Inventory Menu ---\n");
printf("1. Add a New Part\n");
printf("2. Remove an Obsolete Part\n");
printf("3. Search and Display Part Details\n");
printf("4. Display All Parts\n");
printf("5. Exit\n");
printf("Enter your choice: ");
scanf("%d", &choice);
switch (choice) {
case 1: addPart(); break;
case 2: removePart(); break;
case 3: searchPart(); break;
case 4: displayParts(); break;
case 5:
printf("Exiting program.\n");
exit(0);
default:
printf("Invalid choice! Please try again.\n");
}
}
return 0;
}
