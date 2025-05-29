# Assignment-3

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