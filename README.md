
## Linux IPC-Message Queues

## NAME:Kailash Prabhu S
## REG NO:212224240068
## AIM:
To write a C program that receives a message from message queue and display them

## DESIGN STEPS:
## Step 1:
Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

## Step 2:
Write the C Program using Linux message queues API

## Step 3:
Execute the C Program for the desired output.

## PROGRAM:
C program that receives a message from message queue and display them
writer.c


    #include <stdio.h> 
    #include <sys/ipc.h> 
    #include <sys/msg.h> 


    struct mesg_buffer { 
	long mesg_type; 
	char mesg_text[100]; 
    } message; 
    int main() 
    { 	key_t key; 
	int msgid;
    // ftok to generate unique key 
	key = ftok("progfile", 65); 
	// msgget creates a message queue 
	// and returns identifier 
	msgid = msgget(key, 0666 | IPC_CREAT); 
	message.mesg_type = 1; 
	printf("Write Data : "); 
	gets(message.mesg_text); 
	// msgsnd to send message 
	msgsnd(msgid, &message, sizeof(message), 0); 
	// display the message 
	printf("Data send is : %s \n", message.mesg_text); 
	return 0; 
    }
    reader.c
    
    
    #include <stdio.h>
    #include <sys/ipc.h>
    #include <sys/msg.h>
    
    
    struct mesg_buffer {
    	long mesg_type;
    	char mesg_text[100];
    } message;
    int main()
    {
	key_t key;
	int msgid;
    	// ftok to generate unique key
	key = ftok("progfile", 65);
	// msgget creates a message queue
	// and returns identifier
	msgid = msgget(key, 0666 | IPC_CREAT);
	// msgrcv to receive message
	msgrcv(msgid, &message, sizeof(message), 1, 0);
	// display the message
	printf("Data Received is : %s \n",
			message.mesg_text);

	// to destroy the message queue
	msgctl(msgid, IPC_RMID, NULL);
	return 0;
    }
## OUTPUT

<img width="989" height="717" alt="494306937-b8b7eca1-e95c-493b-8c30-892d5780a11a" src="https://github.com/user-attachments/assets/59cb1f3b-87a3-44b4-967a-ac0f2a891109" />

## RESULT:
The programs are executed successfully.
