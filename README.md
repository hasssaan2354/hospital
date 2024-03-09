# hospital
#include <stdio.h>
#include <string.h>
#include <stdbool.h>
#define MAX_USERS 7
#define MAX_ROOMS 100

typedef struct {

char username[15];
char password[15];

} Patient;

typedef struct {

int room_number;
char status[10];
int patient_id;
char patient_name[50];
char patient_stat[50];

} RoomReservation;

Patient users[MAX_USERS] =
{
   {"hassaan", "hassaan123"},
   {"mohamed", "mohamed123"},
   {"seif", "seif123"},
   {"ahmed", "ahmed123"},
   {"mostafa", "mostafa123"}

};

void DISReservations(RoomReservation ROOMS[], int COUNTroom)
 {
    printf("\nCurrent hospital status:\n");
    printf("\nRoom Number  Status   Patient ID      Name             Status\n\n");
    for (int i = 0; i < COUNTroom; i++) {
        printf("%4d  %10s   %10d       %9s       %9s\n", ROOMS[i].room_number, ROOMS[i].status, ROOMS[i].patient_id, ROOMS[i].patient_name, ROOMS[i].patient_stat);
    }
    printf("\nTotal number of rooms: %d\n", COUNTroom);
}

void REMOVEReservation(RoomReservation ROOMS[], int COUNTroom)
{
int CHOISE=0;
int reservationFound = 0;
    printf("\nAvailable Rooms for Cancellation:\n");

    for (int i = 0; i < COUNTroom; i++)
    {
        if (strcmp(ROOMS[i].status, "Full") == 0)
         {printf("Room %d\n",  ROOMS[i].room_number);}
    }

printf("\nEnter the room number to cancel reservation (1-%d) or any button to cancel: ", COUNTroom);
    scanf("%d", &CHOISE);

    if (CHOISE >= 1 && CHOISE <= COUNTroom)
        {
    int roomIndex = CHOISE - 1;
          if (strcmp(ROOMS[roomIndex].status, "Full") == 0)
          {
            strcpy(ROOMS[roomIndex].status, "Empty");
              ROOMS[roomIndex].patient_id = 0;
              ROOMS[roomIndex].patient_name[0] = '\0';
              ROOMS[roomIndex].patient_stat[0] = '\0';
              printf("\nReservation for room %d canceled successfully.\n", ROOMS[roomIndex].room_number);
           }

    else {printf("\nRoom %d is already empty.\n", ROOMS[roomIndex].room_number);}
        }

    else if (CHOISE != 0) {printf("\nInvalid choice. Cancellation canceled.\n");}
    DISReservations(ROOMS, COUNTroom);
}

void ADDReservation(RoomReservation ROOMS[], int COUNTroom)
{
int choice, patientID, emptyRoomFound = 0;
char input[100];
printf("\nAvailable Rooms for Reservation:\n");

    for (int i = 0; i < COUNTroom; i++)
        {
          if (strcmp(ROOMS[i].status, "Empty") == 0)
          {
            printf("Room %d\n", ROOMS[i].room_number);
            emptyRoomFound = 1;
          }
        }
    printf("\nEnter the room number to add reservation (1-%d) or 0 to cancel: ", COUNTroom);
    scanf("%d", &choice);
    getchar();

    if (choice >= 1 && choice <= COUNTroom)
    {
        int roomIndex = choice - 1;
            char buffer[100];

            printf("\nEnter the patient ID to add reservation: ");
            scanf("%d", &patientID);
            printf("Enter patient ID one more time: ");

    while (true) {
    if (scanf("%d", &patientID) == 1) {
        printf("Patient ID entered: %d\n", patientID);
        break;
    } else {
        printf("\nInvalid input. Please enter a valid patient ID.\n");
        printf("Enter patient ID: ");
        scanf("%s", buffer);
    }
}
            getchar();
            printf("\nEnter the patient name: ");
            while (true) {
            fgets(input, sizeof(input), stdin);
            strtok(input, "\n");
            bool validInput = true;
            for (int i = 0; input[i] != '\0'; i++) {
            if (!isalpha(input[i]) && input[i] != ' ') {
            validInput = false;
            break;}
    }
    if (validInput) {
        strncpy(ROOMS[roomIndex].patient_name, input, sizeof(ROOMS[roomIndex].patient_name));
        break;
    } else {
        printf("\nInvalid input. Please enter a valid patient name.\n");
        printf("\nEnter the patient name: ");
    }
}
            strncpy(ROOMS[roomIndex].patient_name, input, sizeof(ROOMS[roomIndex].patient_name));
            printf("\nEnter the patient status: ");
while (true) {
    fgets(input, sizeof(input), stdin);
    strtok(input, "\n");
    bool validInput = true;
    for (int i = 0; input[i] != '\0'; i++) {
        if (!isalpha(input[i])) {
            validInput = false;
            break;
                                }
    }
    if (validInput) {
        strncpy(ROOMS[roomIndex].patient_stat, input, sizeof(ROOMS[roomIndex].patient_stat));
        break;
    } else {
        printf("\nInvalid input. Please enter a valid patient status.\n");
        printf("\nEnter the patient status: ");
    }
}
            strncpy(ROOMS[roomIndex].patient_stat, input, sizeof(ROOMS[roomIndex].patient_stat));
        bool patientFound = false;
        for (int i = 0; i < COUNTroom; i++) {
            if (ROOMS[i].patient_id == patientID) {

                strcpy(ROOMS[i].status, "Empty");
                ROOMS[i].patient_id = 0;
                ROOMS[i].patient_name[0] = '\0';
                ROOMS[i].patient_stat[0] = '\0';
                ROOMS[roomIndex].patient_id = patientID;
                strcpy(ROOMS[roomIndex].status, "Full");
                printf("\nPatient data updated successfully to room %d.\n", ROOMS[roomIndex].room_number);
                patientFound = true;
                break;
            }
        }
        if (!patientFound) {

            if (strcmp(ROOMS[roomIndex].status, "Empty") == 0) {

                ROOMS[roomIndex].patient_id = patientID;
                strcpy(ROOMS[roomIndex].status, "Full");
                printf("\nReservation added successfully to room %d.\n", ROOMS[roomIndex].room_number);
                                                               }
    else {printf("\nRoom %d is already occupied.\n", ROOMS[roomIndex].room_number);}
                           }
    }
    else if (choice != 0) {printf("\nInvalid choice. Reservation canceled.\n");}

    DISReservations(ROOMS, COUNTroom);
}

void login() {
    char username[20], password[20];
    int check = 0;
    printf("Enter username: ");
    scanf("%s", username);
    printf("Enter password: ");
    scanf("%s", password);

    for (int i = 0; i < MAX_USERS; i++)
        {
        if (strcmp(users[i].username, username) == 0 && strcmp(users[i].password, password) == 0)
        {check = 1;
            break;}
    }
    if (check == 1) {
        printf("\nUser login successful..\n\nWELCOME!\n");

 RoomReservation ROOMS[MAX_ROOMS] =
    {
        {1, "Full", 1456, "omar salah", "Recovering"}, {2, "Empty", 0, "", ""}, {3, "Full", 2456, "zeyad ahmed", "Recovering"}, {4, "Empty", 0, "", ""},
        {5, "Full", 2785, "seif hossam", "Recovering"}, {6, "Full", 2578, "shereen nor", "emergency"}, {7, "Empty", 0, "", ""},
        {8, "Full", 1245, "hania ahmed", "improving"}, {9, "Full", 2245, "hanaa ahmed", "emergency"}, {10, "Empty", 0, "", ""},
        {11, "Full", 2435, "ahmed salah", "emergency"}, {12, "Empty", 0, "", ""}, {13, "Empty", 0, "", ""}, {14, "Empty", 0, "", ""},
        {15, "Full", 1142, "hany wael", "emergency"}, {16, "Full", 1135, "ehab fady", "emergency"}, {17, "Empty", 0, "", ""},
        {18, "Full", 1254, "zeina ehab", "improving"}, {19, "Empty", 0, "", ""}, {20, "Full", 1114, "hany ahmed", "improving"}
    };

    int COUNTroom = 20;
    DISReservations(ROOMS, COUNTroom);
    int OPERATION;
    printf("\nChoose an operation:\n1. Add Reservation\n2. Cancel Reservation\n Or any button to cancel\n\nEnter your choice: ");
    scanf("%d", &OPERATION);

    if (OPERATION==1)
        {
    ADDReservation(ROOMS, COUNTroom);
    }

    else if (OPERATION==2){REMOVEReservation(ROOMS, COUNTroom);}
    else  {printf("\nOperation canceled.\n");}
}   else {printf("\nInvalid username or password! \n");}
}

int main() {

    login();
}
