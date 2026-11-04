
# Experiment No. 10 – String Matching Algorithms

**Created By:** Krish Mhatre

## C Program

```c
#include <stdio.h>
#include <string.h>

// Naive String Matching
void naive(char text[], char pat[]) {
    int n = strlen(text);
    int m = strlen(pat);
    int found = 0;

    for(int i = 0; i <= n - m; i++) {
        int j = 0;

        while(j < m && text[i + j] == pat[j])
            j++;

        if(j == m) {
            printf("Pattern found at index %d\n", i);
            found = 1;
        }
    }

    if(!found)
        printf("No match found.\n");
}

// Rabin-Karp Algorithm
void rabinKarp(char text[], char pat[]) {
    int n = strlen(text);
    int m = strlen(pat);
    int p = 0, t = 0, h = 1;
    int q = 101, found = 0;

    if(m > n) {
        printf("No match found.\n");
        return;
    }

    for(int i = 1; i < m; i++)
        h = (h * 256) % q;

    for(int i = 0; i < m; i++) {
        p = (256 * p + pat[i]) % q;
        t = (256 * t + text[i]) % q;
    }

    for(int i = 0; i <= n - m; i++) {
        if(p == t && strncmp(text + i, pat, m) == 0) {
            printf("Pattern found at index %d\n", i);
            found = 1;
        }

        if(i < n - m) {
            t = (256 * (t - text[i] * h) + text[i + m]) % q;

            if(t < 0)
                t += q;
        }
    }

    if(!found)
        printf("No match found.\n");
}

int main() {
    int choice;
    char text[100], pat[100];

    while(1) {
        printf("\n1. Naive String Matching\n");
        printf("2. Rabin-Karp\n");
        printf("3. Exit\n");
        printf("Enter choice: ");
        if(scanf("%d", &choice) != 1)
            return 1;

        if(choice == 3)
            break;

        if(choice != 1 && choice != 2) {
            printf("Invalid choice.\n");
            continue;
        }

        printf("Enter text: ");
        scanf("%99s", text);

        printf("Enter pattern: ");
        scanf("%99s", pat);

        if(choice == 1)
            naive(text, pat);
        else
            rabinKarp(text, pat);
    }

    printf("Exiting program.\n");
    return 0;
}
```

## Terminal Input (Copy and Paste)

After running the program, copy and paste the following input into your terminal.

This input tests both algorithms and then exits.

```text
1
ABAACAADAABAABA
ABA
2
ABAACAADAABAABA
ABA
3
```

## Output

```text
PS C:\AOA> gcc string.c -o string
PS C:\AOA> .\string.exe

1. Naive String Matching
2. Rabin-Karp
3. Exit
Enter choice: 1
Enter text: ABAACAADAABAABA
Enter pattern: ABA
Pattern found at index 0
Pattern found at index 9
Pattern found at index 12

1. Naive String Matching
2. Rabin-Karp
3. Exit
Enter choice: 2
Enter text: ABAACAADAABAABA
Enter pattern: ABA
Pattern found at index 0
Pattern found at index 9
Pattern found at index 12

1. Naive String Matching
2. Rabin-Karp
3. Exit
Enter choice: 3
Exiting program.
```

## Aim
To implement Naive String Matching and Rabin-Karp algorithms using C.

## Theory

### Naive String Matching
Naive String Matching is a simple algorithm used to find a pattern within a given text.

It compares the pattern with every possible position in the text until a match is found.

### Rabin-Karp Algorithm
Rabin-Karp is a string matching algorithm that uses hashing to search for patterns in a text.

It compares hash values first and verifies the characters whenever the hash values match.

## Algorithm

### Naive String Matching
1. Start the program.
2. Enter the text and pattern.
3. Compare the pattern with each substring.
4. If all characters match, display the index.
5. Repeat until the complete text is checked.

### Rabin-Karp
1. Start the program.
2. Enter the text and pattern.
3. Calculate the hash value of the pattern.
4. Calculate the hash of each text window.
5. Compare the hash values.
6. If hashes match, verify the characters.
7. Display the matching positions.

## How to Run

**Step 1:** Save as `string.c`.

**Step 2:** Compile:

```bash
gcc string.c -o string
```

**Step 3:** Run in PowerShell:

```powershell
.\string.exe
```

**Step 4:** Copy the input from the Terminal Input section and paste it into the terminal.

## Time Complexity

| Algorithm | Average Case | Worst Case |
|-----------|--------------|------------|
| Naive String Matching | O(n × m) | O(n × m) |
| Rabin-Karp | O(n + m) | O(n × m) |

**Auxiliary Space Complexity:** O(1) for both algorithms.

Where:
- n = Length of text
- m = Length of pattern

## Conclusion
Successfully implemented Naive String Matching and Rabin-Karp algorithms in C to find matching patterns within a given text.
