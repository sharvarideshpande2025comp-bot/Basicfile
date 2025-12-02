# Basicfile
#include <stdio.h>

int main()
{
    FILE *fp;
    int choice;
    char filename[] = "data.txt";
    char text[200];
    char ch;
    
    printf("\n===== SIMPLE FILE MENU =====");
    printf("\n1. Write a line to data.txt (Simple)");
    printf("\n2. Read ONE line from data.txt (Simple)");
    printf("\n3. Display data.txt (Char by Char)");
    printf("\n4. Exit");
    
    printf("\nEnter your choice (1-4): ");
    scanf("%d", &choice);
    
    switch (choice)
    {
        case 1:
            fp = fopen(filename, "w");

            if (fp == NULL) {
                printf("Error opening file for writing!\n");
                break;
            }

            printf("Enter text to write (one line only): ");
            getchar();
            
            fgets(text, 200, stdin);

            fprintf(fp, "%s", text);

            fclose(fp);
            printf("Data written to data.txt\n");
            break;

        case 2:
            fp = fopen(filename, "r");

            if (fp == NULL) {
                printf("data.txt not found!\n");
                break;
            }

            printf("\n--- Reading ONE Line using fscanf ---\n");

            if (fscanf(fp, "%199[^\n]", text) == 1) {
                printf("Read data: %s\n", text);
            } else {
                printf("Could not read data or file is empty.\n");
            }
            fclose(fp);
            break;

        case 3:
            fp = fopen(filename, "r");

            if (fp == NULL) {
                printf("data.txt not found!\n");
                break;
            }
            printf("\n--- Displaying character by character ---\n");

            while ((ch = fgetc(fp)) != EOF) {
                
                putchar(ch);
            }
            
            fclose(fp);
            printf("\n--- End of file display ---\n");
            break;
            
        case 4:
            printf("Exiting the program. Goodbye!\n");
            return 0;

        default:
            printf("Invalid choice! \n");
    }

    return 0;
}
