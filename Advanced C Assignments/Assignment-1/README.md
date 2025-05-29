# 1

```C
#include <stdio.h>
#include <string.h>

#define MAX_ENTRIES 3
#define MAX_ENTRY_LENGTH 100
#define TOTAL_DAYS 7

// Structure to represent a day and its schedule
typedef struct {
    char nameOfDay[10];
    char agenda[MAX_ENTRIES][MAX_ENTRY_LENGTH];
    int agendaCount;
} ScheduleDay;

// Set up the names and initial data for the week
void setupWeek(ScheduleDay weekPlan[]) {
    char *weekDays[TOTAL_DAYS] = {"Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"};

    for (int d = 0; d < TOTAL_DAYS; d++) {
        strcpy(weekPlan[d].nameOfDay, weekDays[d]);
        weekPlan[d].agendaCount = 0;
    }
}

// Return the index of a day given its name (case-insensitive)
int findDayIndex(char *inputDay, ScheduleDay weekPlan[]) {
    for (int i = 0; i < TOTAL_DAYS; i++) {
        if (strcasecmp(weekPlan[i].nameOfDay, inputDay) == 0)
            return i;
    }
    return -1; // Not found
}

// Allow user to add agenda items to a specific day
void addAgenda(ScheduleDay weekPlan[]) {
    char selectedDay[10];
    printf("Enter the day you want to add agenda items to (e.g., Monday): ");
    scanf("%s", selectedDay);

    int dayIdx = findDayIndex(selectedDay, weekPlan);
    if (dayIdx == -1) {
        printf("Invalid day name!\n");
        return;
    }

    if (weekPlan[dayIdx].agendaCount >= MAX_ENTRIES) {
        printf("Maximum number of items already added for %s.\n", weekPlan[dayIdx].nameOfDay);
        return;
    }

    int slotsLeft = MAX_ENTRIES - weekPlan[dayIdx].agendaCount;
    printf("You can add up to %d more item(s).\n", slotsLeft);

    getchar(); // Clear buffer

    for (int i = 0; i < slotsLeft; i++) {
        char entryBuffer[MAX_ENTRY_LENGTH];
        printf("Enter agenda item %d (or type 'done' to stop): ", i + 1);
        fgets(entryBuffer, MAX_ENTRY_LENGTH, stdin);
        entryBuffer[strcspn(entryBuffer, "\n")] = '\0'; // Remove newline

        if (strcasecmp(entryBuffer, "done") == 0)
            break;

        strcpy(weekPlan[dayIdx].agenda[weekPlan[dayIdx].agendaCount], entryBuffer);
        weekPlan[dayIdx].agendaCount++;
    }
}

// Display the agenda for each day of the week
void viewAgenda(ScheduleDay weekPlan[]) {
    printf("\nWeekly Schedule:\n");
    for (int i = 0; i < TOTAL_DAYS; i++) {
        printf("%s:\n", weekPlan[i].nameOfDay);
        if (weekPlan[i].agendaCount == 0) {
            printf("  No items scheduled.\n");
        } else {
            for (int j = 0; j < weekPlan[i].agendaCount; j++) {
                printf("  - %s\n", weekPlan[i].agenda[j]);
            }
        }
    }
}

int main() {
    ScheduleDay weekPlan[TOTAL_DAYS];
    setupWeek(weekPlan);

    int menuChoice;
    do {
        printf("\nMenu:\n1. Add Agenda Items\n2. View Schedule\n3. Exit\nSelect an option: ");
        scanf("%d", &menuChoice);

        switch (menuChoice) {
            case 1:
                addAgenda(weekPlan);
                break;
            case 2:
                viewAgenda(weekPlan);
                break;
            case 3:
                printf("Program terminated.\n");
                break;
            default:
                printf("Invalid selection. Please choose 1, 2, or 3.\n");
        }
    } while (menuChoice != 3);

    return 0;
}

```

# 2

```C
#include <stdio.h>

// Function to shift elements to the right by 1 position using pointers
void shiftRightByOne(int* leftPtr, int* rightPtr) {
    int tempVal = *rightPtr;
    while (rightPtr > leftPtr) {
        *rightPtr = *(rightPtr - 1);
        rightPtr--;
    }
    *leftPtr = tempVal;
}

// Main rearrangement function to move even numbers to the front
void segregateEvenOdd(int* array, int length) {
    int* evenPos = array;
    int* scanPos = array;

    while (scanPos < array + length) {
        if (*scanPos % 2 == 0) {
            if (scanPos != evenPos) {
                // Save the even number
                int evenNum = *scanPos;

                // Shift all elements between evenPos and scanPos to the right by one
                int* tempPtr = scanPos;
                while (tempPtr > evenPos) {
                    *tempPtr = *(tempPtr - 1);
                    tempPtr--;
                }

                *evenPos = evenNum;
            }
            evenPos++;
        }
        scanPos++;
    }
}

// Helper function to print the array
void displayArray(int* array, int length) {
    for (int* ptr = array; ptr < array + length; ptr++) {
        printf("%d ", *ptr);
    }
    printf("\n");
}

// Example usage
int main() {
    int numbers[] = {1, 2, 3, 4, 5, 6};
    int size = sizeof(numbers) / sizeof(numbers[0]);

    printf("Original array:\n");
    displayArray(numbers, size);

    segregateEvenOdd(numbers, size);

    printf("Rearranged array:\n");
    displayArray(numbers, size);

    return 0;
}

```

# 3

```C
#include <stdio.h>
#include <stdbool.h>

// Binary search in a sorted array (row)
bool binarySearch(int row[], int size, int key) {
    int left = 0;
    int right = size - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (row[mid] == key) {
            return true;
        } else if (row[mid] < key) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return false;
}

// Search key in n x n matrix using binary search on each row
bool searchMatrixWithBinary(int matrix[][4], int n, int key) {
    for (int i = 0; i < n; i++) {
        if (binarySearch(matrix[i], n, key)) {
            return true;
        }
    }
    return false;
}

int main() {
    int size = 4;
    int matrix[4][4] = {
        {5, 12, 17, 23},
        {9, 14, 20, 27},
        {13, 18, 22, 30},
        {16, 19, 25, 35}
    };

    int keyToFind = 22;
    if (searchMatrixWithBinary(matrix, size, keyToFind)) {
        printf("Key %d found in the matrix.\n", keyToFind);
    } else {
        printf("Key %d not found in the matrix.\n", keyToFind);
    }

    return 0;
}

```