# Double-Linked-List-Menu
Double Linked List Menu

#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>

// Node Structure

struct node{
	int data;
	struct node *next;
	struct node *prev;
	};

struct node *HEAD = NULL;
struct node *TAIL = NULL;

// declare Function Prototypes

void menu();
void create();
void display();
void traverse_head();
void traverse_tail();
void add_head();
void add_tail();
void add_before();
void add_after();
void delete_head();
void delete_value();
void delete_tail();
void delete_whole();

void menu(){
	int choice; // for selecting the choice on what operation to do
	
	do{
		printf("\n\n<<<<< DOUBLE LINKED LIST CREATOR MENU >>>>>\n\n");
		printf("1. Create a Doubly Linked List\n");
		printf("2. Display the Doubly Linked List\n");
		printf("3. Traverse the List from Top to Bottom\n");
		printf("4. Traverse the List from Bottom to Top\n");
		printf("5. Add a Node at the Head\n");
		printf("6. Add a Node at the Tail\n");
		printf("7. Add a Node Before a Given Node\n");
		printf("8. Add a Node After a Given Node\n");
		printf("9. Delete a Node at the Head\n");
		printf("10. Delete a Node by Value of Given Node\n");
		printf("11. Delete a Node at the Tail\n");
		printf("12. Delete the Whole List\n");
		printf("13. Exit\n");
		
		printf("Enter your Choice: ");
		scanf("%d", &choice);
		
		system("cls");
		
		switch(choice){
			
			case 1:
				create();
				break;
			case 2:
				display();
				break;
			case 3:
				traverse_head();
				break;
			case 4:
				traverse_tail();
				break;
			case 5:
				add_head();
				break;
			case 6:
				add_tail();
				break;
			case 7:
				add_before();
				break;
			case 8:
				add_after();
				break;
			case 9:
				delete_head();
				break;
			case 10:
				delete_value();
				break;
			case 11:
				delete_tail();
				break;
			case 12:
				delete_whole();
				break;
			case 13:
				printf("Program Ended.\n");
				break;
			default:
				printf("Invalid input.\n");
		}
	}while(choice != 13);
}

int main(){
	menu();
	return 0;
}

void create(){
	struct node *NewNode;
	char Resp;
	
		// Allocate memory for New Node
		NewNode=(struct node*)malloc(sizeof(struct node));
		
		HEAD = NewNode;
		TAIL = NewNode;
		HEAD->prev = NULL;
		
		do{
			// Accept value for NewNode->data
			printf("Enter a Number: ");
			scanf("%d", &NewNode->data);
			
			printf("Add another node [Y/N]?: ");
			scanf(" %c", &Resp);
			Resp = toupper(Resp);
			
			if(Resp == 'Y'){
				// Allocate memory for NewNode->next
				NewNode->next = (struct node*)malloc(sizeof(struct node));
				
				NewNode->next->prev = NewNode;
				NewNode = NewNode->next;
				TAIL = NewNode;
			}
		}while(Resp == 'Y');
		
		TAIL->next = NULL;
		NewNode = NULL;
}

void display(){
	struct node *temp = HEAD;
	
	if(HEAD == NULL){
		printf("List is empty.\n");
		return;
	}
	
	printf("Here is your List: ");
	while(temp != NULL){
		printf("%d ", temp->data);
		temp = temp->next;
	}
	printf("\n");
}

void traverse_head(){
	struct node *TravNode;
	
	TravNode = HEAD;
	
	if(TravNode == NULL){
		printf("Doubly List is Empty!!!\n");
	}
	
	else{
		printf("Traversing List: ");
		
		do{
			printf("%d ", TravNode->data);
			TravNode = TravNode->next;
		}while(TravNode != NULL);
		printf("\n");
	}
}

void traverse_tail(){
	struct node *TravNode;
	
	TravNode = TAIL;
	
	if(TravNode == NULL){
		printf("Doubly List is Empty!!!\n");
	}
	else{
			printf("Traversing List: ");
		do{
			printf("%d ", TravNode->data);
			TravNode = TravNode->prev;
		}while(TravNode != NULL);
		printf("\n");
	}
}

void add_head(){
	struct node *NewNode;
	int value;	
		
		// if no value is entered
		if(HEAD == NULL){
       		printf("Doubly Linked List is Empty!!!\n");
        	return;
    	}
	
		// Allocate memory for New Node
		NewNode=(struct node*)malloc(sizeof(struct node));
		
		// Accept value to add at head
		printf("Enter value to add at the head: ");
		scanf("%d", &value);
		
		// Accept NewNode->data
		NewNode->data = value;
		NewNode->prev = NULL;
		NewNode->next = NULL;
		
		if(HEAD == NULL){
			HEAD = TAIL = NewNode;
		}
		else{
			NewNode->next = HEAD;
			HEAD->prev = NewNode;
			HEAD = NewNode;
		}
		NewNode = NULL;
}

void add_tail(){
	struct node *NewNode;
	int value;
	
		// if no value is entered
		if(HEAD == NULL){
       		printf("Doubly Linked List is Empty!!!\n");
        	return;
    	}	
	
		// Allocate memory for New Node
		NewNode=(struct node*)malloc(sizeof(struct node));
		
		// Accept value to add at tail
		printf("Enter value to add at the tail: ");
		scanf("%d", &value);
		
		// Accept NewNode->data
		NewNode->data = value;
		NewNode->prev = NULL;
		NewNode->next = NULL;
		
		if(TAIL == NULL){
			HEAD = TAIL = NewNode;
		}
		else{
			NewNode->prev = TAIL;
			TAIL->next = NewNode;
			TAIL = NewNode;
		}
		NewNode = NULL;
}

void add_before(){
	struct node *NewNode, *Current;
	int value, before_val;
	int flag = 0;
	
		// Allocate memory for New Node
		NewNode=(struct node*)malloc(sizeof(struct node));
		
		// Accept value to add before another node
		printf("Enter value for new node: ");
		scanf("%d", &value);
		
		// Accept NewNode->data
		NewNode->data = value;
		NewNode->prev = NULL;
		NewNode->next = NULL;
		
		// Accept value to insert before value
		printf("Insert before what value in the list?: ");
		scanf("%d", &before_val);
		
		Current = HEAD;
		
		// if no value is entered
		if(Current == NULL){
       		printf("Doubly Linked List is Empty!!!\n");
        	return;
    	}
    	
    	else{
    		
			while(flag == 0 && Current != NULL){
			
			if(Current->data == before_val){
				flag = 1;
			}
			
			else{
				Current = Current->next;
			}
		}
		
		if(flag == 0){
			printf("The Value where the NewNode will be inserted before does not exist");
			free(NewNode);
		}
		
		else{
			
			if(Current == HEAD){
				NewNode->next = HEAD;
				HEAD->prev = NewNode;
				HEAD = NewNode;
			}
			
			else{
				NewNode->next = Current;
				NewNode->prev = Current->prev;
				Current->prev->next = NewNode;
				Current->prev = NewNode;
			}
			
			Current = NewNode = NULL;
			
			printf("Node inserted successfully!!!");
		}
	}		
}

void add_after(){
	struct node *NewNode, *Current;
	int value, after_val;
	int flag = 0;
	
		// Allocate memory for New Node
		NewNode=(struct node*)malloc(sizeof(struct node));
		
		// Accept value to add after another node
		printf("Enter value for new node: ");
		scanf("%d", &value);
		
		// Accept NewNode->data
		NewNode->data = value;
		NewNode->prev = NULL;
		NewNode->next = NULL;
		
		// Accept value to insert after value
		printf("Insert after what value in the list?: ");
		scanf("%d", &after_val);
		
		Current = HEAD;
		
		// if no value is entered
		if(Current == NULL){
       		printf("Doubly Linked List is Empty!!!\n");
        	return;
    	}
    	
    	else{
    		
    			while(flag == 0 && Current != NULL){
			
				if(Current->data == after_val){
					flag = 1;
				}
			
				else{
					Current = Current->next;
				}
			}
		
			if(flag == 0){
				printf("The Value where the NewNode will be inserted after does not exist");
				free(NewNode);
			}
		
			else{
			
				if(Current == TAIL){
					NewNode->prev = TAIL;
					TAIL->next = NewNode;
					TAIL = NewNode;
				}
			
				else{
					NewNode->next = Current->next;
					NewNode->prev = Current;
					Current->next->prev = NewNode;
					Current->next = NewNode;
				}
				
				Current = NewNode = NULL;
			
				printf("Node inserted successfully!!!");
		}
	}
}

void delete_head(){
	struct node *DelNode;
	
		DelNode = HEAD;
	
		// if no value is entered
		if(DelNode == NULL){
			printf("Doubly Linked List is Empty!!!\n");
		}
		
		else{
			
			HEAD = HEAD->next;
			
			if(HEAD != NULL){
				HEAD->prev = NULL;
			}
			
			else{
				TAIL = NULL;
			}
			
			DelNode->next = NULL;
			free(DelNode);
			DelNode = NULL;
			
			printf("Node deleted successfully!\n");
		}
}

void delete_value(){
	struct node *DelNode;
	int delete_val;
	int flag = 0;
	
		DelNode = HEAD;
		
		// if no value is entered
		if(DelNode == NULL){
			printf("Doubly Linked List is Empty!!!\n");
		}
		
		printf("Enter value to delete in the list: ");
		scanf("%d", &delete_val);
		
		// Finding the value
		while(flag == 0 && DelNode != NULL){
			if(DelNode->data == delete_val){
				flag = 1;
			}
			
			else{
				DelNode = DelNode->next;
			}
		}
		
		if(flag == 0){
			printf("The value to be deleted does not exist!!!\n");
		}
		
		else{
			
			// Delete head
			if(DelNode == HEAD){
				HEAD = HEAD->next;
				
				if(HEAD != NULL){
					HEAD->prev = NULL;
				}
				
				else{
					TAIL = NULL;
				}
			}
			
			// Delete tail
			else if(DelNode == TAIL){
				TAIL = TAIL->prev;
				TAIL->next = NULL;
			}
			
			// Delete middle 
			else{
				DelNode->prev->next = DelNode->next;
				DelNode->next->prev = DelNode->prev;
			}
			
			free(DelNode);
			DelNode = NULL;
			
			printf("Node deleted successfully!!!\n");
		}	
}

void delete_tail(){
	struct node *DelNode;
	
		DelNode = TAIL;
	
		// if no value is entered
		if(DelNode == NULL){
			printf("Doubly Linked List is Empty!!!\n");
		}
		
		else{
			
			TAIL = TAIL->prev;
			
			if(TAIL != NULL){
				TAIL->next = NULL;
			}
			
			else{
				HEAD = NULL;
			}
			
			DelNode->prev = NULL;
			free(DelNode);
			DelNode = NULL;
			
			printf("Node deleted successfully!\n");
		}
}

void delete_whole(){
	struct node *temp;
	
	if(HEAD == NULL){
		printf("Doubly Linked List is already empty!!!\n");
	}
	
	while(HEAD != NULL){
		temp = HEAD;
		HEAD = HEAD->next;
		free(temp);
	}
	
	TAIL = NULL;
	
	printf("Whole list is deleted successfully!!!\n");
}
