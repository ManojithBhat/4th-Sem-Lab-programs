# Horspool string matching algorithm

``` c
#include <stdio.h>
#include <string.h>
#define MAX 256

int t[MAX];  // Shift table
int count = 0;  // For counting the number of shifts

// Function to create the shift table
void shifttable(char pat[]) {
    int i, m;
    m = strlen(pat);  // Length of the pattern
    for (i = 0; i < MAX; i++)
        t[i] = m;  // Initialize all shifts to the length of the pattern
    for (i = 0; i < m - 1; i++)
        t[(int)pat[i]] = m - 1 - i;  // Set shift values for each character in the pattern
}

int horspool(char src[], char pat[]) {
    int i, j, k, m, n;
    n = strlen(src);  // Length of the source string
    m = strlen(pat);  // Length of the pattern
    i = m - 1;  // Start from the end of the first window

    while (i < n) {
        k = 0;
        while ((k < m) && (pat[m - 1 - k] == src[i - k]))  // Compare pattern with current window
            k++;
        if (k == m)  // If match is found
            return i - m + 1;
        else
            i += t[(int)src[i]];  // Shift the window according to the shift table
        count++;
    }

    return -1;  // If no match is found
}

int main() {
    char src[100], pat[10];
    int pos;

    printf("\nEnter the main source string: ");
    gets(src);

    printf("\nEnter the pattern to be searched: ");
    gets(pat);

    shifttable(pat);  // Create the shift table

    pos = horspool(src, pat);  // Search for the pattern

    if (pos >= 0)
        printf("\nFound at %d position", pos + 1);
    else
        printf("\nString match failed");

    printf("\nNumber of shifts are %d\n", count);
    return 0;
}

```

### output 

``` bash
Enter the main source string:This is a test text to search the pattern tester

Enter the pattern to be searched: tester

Found at 42 position
Number of shifts are 11
```
