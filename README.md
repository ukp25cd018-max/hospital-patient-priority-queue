# hospital-patient-priority-queue

#include <stdio.h>
#include <string.h>

#define MAX 20

struct Patient
{
    char name[20];
    int priority;
};

struct Patient queue[MAX];
int count = 0;

void addPatient(char name[], int priority)
{
    if (count == MAX)
    {
        printf("Queue is full!\n");
        return;
    }

    strcpy(queue[count].name, name);
    queue[count].priority = priority;
    count++;

    printf("Patient %s added successfully.\n", name);
}

void treatNext()
{
    int i, pos;

    if (count == 0)
    {
        printf("No patients waiting.\n");
        return;
    }

    pos = 0;

    for (i = 1; i < count; i++)
    {
        if (queue[i].priority < queue[pos].priority)
        {
            pos = i;
        }
    }

    printf("Treating patient: %s\n", queue[pos].name);
    printf("Priority: %d\n", queue[pos].priority);

    for (i = pos; i < count - 1; i++)
    {
        queue[i] = queue[i + 1];
    }

    count--;
}

int main()
{
    addPatient("P1", 3);
    addPatient("P2", 1);
    addPatient("P3", 2);
    addPatient("P4", 1);
    addPatient("P5", 3);
    addPatient("P6", 2);

    printf("\n--- Treatment Order ---\n");

    while (count > 0)
    {
        treatNext();
    }

    printf("\n--- Emergency Patient Test ---\n");

    addPatient("P1", 3);
    addPatient("P2", 2);
    addPatient("P3", 3);

    printf("\nTreating 2 patients:\n");
    treatNext();
    treatNext();

    printf("\nAdding new Emergency patient...\n");
    addPatient("Emergency", 1);

    printf("\nNext patient:\n");
    treatNext();

    return 0;
}