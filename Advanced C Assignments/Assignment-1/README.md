# Assignment-1

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