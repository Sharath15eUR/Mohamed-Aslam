# Assignment-2

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