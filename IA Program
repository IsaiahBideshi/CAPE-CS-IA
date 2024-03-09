#include<stdlib.h>
#include<stdio.h>
#include<string.h>

//		Declares global variables:
char cmd[99], arg1[99], arg2[99], arg4[99];
int arg3;
float totalsales = 0.00, totalpurchases = 0.00, totalprofit = 0.00, allsales[12], allpurchases[12], allprofits[12];

char productnames[12][99];		//		array for product name and model for sorting.
char productmodels[12][99];

FILE *products = fopen("products.txt", "w+");



//	Structure for linked list
typedef struct node{		
	int year, stock, openstock;
	float price, sales, purchases, profit;
	char name[99], model[99];
	
	struct node *next;
}Node, *nodeptr;


// 		Function to make a node
nodeptr makenode(char name[99], char model[99], float price, int year, int openstock){
	nodeptr np = (nodeptr)malloc(sizeof(Node));
	
	strcpy(np -> name, name);
	strcpy(np -> model, model);
	
	np -> purchases = 0;
	np -> sales = 0;
	np -> profit = 0;
	np -> price = price;
	np -> year = year;
	np -> openstock = openstock;
	np -> stock = openstock;
	
	np -> next = NULL;
	return np;
}

//		Get the last node in the list
nodeptr getlast(nodeptr head){
	nodeptr curr = head;
	while((curr != NULL) && (curr -> next != NULL)){
		curr = curr -> next;
	}
	return curr;
}


//		Add member to the back of the list.
nodeptr addlast(nodeptr head, char name[99], char model[99], float price, int year, int openstock){
	nodeptr np = makenode(name, model, price, year, openstock);
	nodeptr last = getlast(head);
	if(last == NULL){
		return np;
	}
	last -> next = np;
	return head;
}

//		Print entire list
nodeptr printstock(nodeptr n){
	printf("Stock Table: \n");
	printf(" _______________________________________________________________ \n");
	printf("|Product  	|Model		|Price		|Year	|Stock	|\n");
	printf("|---------------------------------------------------------------|\n");
	
	while (n != NULL){
		if(strcmp(n -> name, "macbook") !=0 )
			printf("|%s		|%s		|$%5.2f	|%d	|%d	|\n", n -> name, n -> model, n -> price, n -> year, n -> stock);
		else
			printf("|%s	|%s		|$%5.2f	|%d	|%d	|\n", n -> name, n -> model, n -> price, n -> year, n -> stock);
		n = n -> next;
	}
	printf(" _______________________________________________________________ \n");
}

//		When a specific node needs to be altered use look for function to find it
nodeptr lookfor(nodeptr head, char name[99], char model[99]){
	while((strcmp(head -> model, model)!= 0) || (strcmp(head -> name, name)!= 0)){
		head = head -> next;
		if(head -> next == NULL)
			break;
	}
	
	if(strcmp(head -> model, model) == 0 && strcmp(head -> name, name) == 0)
		return head;
	else{
		nodeptr notfound = NULL;
		return notfound;
	}
}


//		if stock drops to 0 alert the user to 
void checkStock(nodeptr head){
	while(head != NULL){
		if(head -> stock == 0)
			printf("\n\n**********WARNING!**********\n%s %s NEEDS TO RESTOCK!", head -> name, head -> model);
		head = head -> next;
	}
}

//		prints arrays of information used in sort command.
void printArray(char arr1[][99], char arr2[][99], float arr3[]){	
	for(int x=0;x<12;x++){
		int y=x+1;
		
		printf("%d.%s %s 				-	$%.2f\n",y , arr1[x], arr2[x], arr3[x]);
	}
}

//		calculates total profit
void profit(){
	printf("Total sales 		-	$%.2f\n", totalsales);
	printf("Total Purchases		-	$%.2f\n", totalpurchases);
	totalprofit = totalsales - totalpurchases;
	printf("Profit			-	$%.2f\n", totalprofit);
}

//		function to put sales from all nodes to one array for sort.
void getAllSales(nodeptr head){		
	int x=0;
	while(head != NULL){
		allsales[x] = head -> sales;
		head = head -> next;
		x++;
	}
}

//		function to put purchases from all nodes to one array for sort.
void getAllPurchases(nodeptr head){	
	int x=0;
	while(head != NULL){
		allpurchases[x] = head -> purchases;
		head = head -> next;
		x++;
	}
}


//		function to put profit from all structs to one array for sort.
void getAllProfits(nodeptr head){		
	int x=0;
	while(head != NULL){
		allprofits[x] = head -> profit;
		head = head -> next;
		x++;
	}
}

//		puts all device names into arrays
void getNames(nodeptr head){
	int x=0;
	while(head != NULL){
		strcpy(productnames[x], head -> name);
		strcpy(productmodels[x], head -> model);
		head = head -> next;
		x++;
	}
}

//		function to sort float arrays in descending order and swap the corresponding name and model of the product.
void sort(float arr[], char arr1[][99], char arr2[][99], int size){
	int i, j;
	for(i=1; i<size;i++){
		int Ai = arr[i];
		char As[99];
		char As1[99];
		strcpy(As, arr1[i]);
		strcpy(As1, arr2[i]);
		j = i-1;
		while(j>=0 && arr[j] < Ai){
			arr[j+1]=arr[j];
			strcpy(arr1[j+1], arr1[j]);
			strcpy(arr2[j+1], arr2[j]);
			j--;
		}
		arr[j+1] = Ai;
		strcpy(arr1[j+1], As);
		strcpy(arr2[j+1], As1);
	}
}

//		function to say what the commands do and how to use them.
void help(){	
	printf("Commands: \n");
	printf("stop					- 	Stops the program. \n");
	printf("help 					- 	Shows a list of commands and how to use them. \n");
	printf("stock					- 	Shows the stock table. \n");
	printf("sold [PRODUCT] [MODEL] [AMOUNT]		- 	Decreases the stock of the specified product. \n");
	printf("purchased [PRODUCT] [MODEL] [AMOUNT] 	- 	Increases the stock of the specified product. (Markup is 20%%.)\n");	
	printf("stats [PRODUCT] [MODEL]			-	Shows profit, sales, purchases of a specified product. \n");
	printf("profit					- 	Shows total profits made. \n");
	printf("sort sales				-	Sorts products by sales. \n");
	printf("sort purchases				-	Sorts products by purchases. \n");
	printf("sort profit				-	Sorts products by profits. \n");
	printf("\n\nHow to use command: \n");
	printf(" - Anything in \'[]\' are parameters which is used to pass specific information into a command. \n \n");
	printf(" - To use a command without parameters eg. to see stock. Type \"stock\". \n \n");
	printf(" - To use a command with parameters eg. you sold 5 iphone 12\'s. Type \"sold iphone 12 5\". \n");
}


//		print all products' data to file
void fileout(nodeptr head){
	while(head != NULL){
		fprintf(products, "%s %s: \n", head -> name, head -> model);
		fprintf(products, " Price: $%.2f\n", head -> price);
		fprintf(products, " Profit: $%.2f\n", head -> profit);
		fprintf(products, " Purchases: $%.2f\n", head -> purchases);
		fprintf(products, " Sales: $%.2f\n", head -> sales);
		fprintf(products, " Stock: %d\n", head -> stock);
		fprintf(products, " Year: %d\n\n\n", head -> year);
		
		head = head -> next;
	}
}


void commandError(){
	printf("THERE WAS AN ERROR WITH YOUR COMMAND! PLEASE RE-ENTER! \n \n");
}


int main(){
	nodeptr devices = NULL;
	
	devices = addlast(devices, (char *)"iphone", (char *)"12", 649.00, 2020, 56);
	devices = addlast(devices, (char *)"iphone", (char *)"13", 649.00, 2021, 43);
	devices = addlast(devices, (char *)"iphone", (char *)"14", 649.00, 2022, 74);
	
	devices = addlast(devices, (char *)"ipad", (char *)"pro", 799, 2022, 64);
	devices = addlast(devices, (char *)"ipad", (char *)"air", 599, 2020, 59);
	devices = addlast(devices, (char *)"ipad", (char *)"mini", 499, 2019, 33);
	
	devices = addlast(devices, (char *)"macbook", (char *)"pro", 1999, 2021, 57);
	devices = addlast(devices, (char *)"macbook", (char *)"m2", 1199, 2022, 56);
	devices = addlast(devices, (char *)"macbook", (char *)"m1", 999, 2019, 49);
	
	devices = addlast(devices, (char *)"imac", (char *)"pro", 5999, 2019, 13);
	devices = addlast(devices, (char *)"imac", (char *)"studio", 1999, 2022, 9);
	devices = addlast(devices, (char *)"imac", (char *)"mini", 699, 2019, 16);
	

	
	printf("\n************************************************************ ");
	printf("\n*******************  Stock generator  ********************** ");
	printf("\n************************************************************ \n \n");
	
	printf("This is a stock updater for NJ\'s Tech Store. \nUse this program to update the stock when sales and purchases are made.\n \n");
	
	help();
	getNames(devices);		//		put all device names and models into an array
	
	while(1){
		printf("\n \nEnter command or type 'help' to show a list of commands: \n");
		scanf("%s", &cmd);		//	asks for command.
		
		if(strcmp(cmd, "stock") == 0){		//	if command is stock print stock table
			system("cls");
			printstock(devices);
		}
		
		else if(strcmp(cmd, "help") == 0){		//	if command is help print list of commands
			system("cls");
			help();
		}
	
		else if(strcmp(cmd, "stop") == 0){		//	if command is stop stop the program
			system("cls");					//	clear the screen after entering a command
			profit();
			fileout(devices);
			return 0;
		}
		
		else if(strcmp(cmd, "profit") == 0){
			system("cls");
			profit();
		}
		
		
		//******************SORT COMMAND******************
		else if(strcmp(cmd, "sort") == 0){	//	if cmd is "sort" ask for parameter 1.
			scanf("%s", &arg1);
			system("cls");

			if(strcmp(arg1, "sales") == 0){	// if arg1 is "sales" call getAllSales() and sort().
				getAllSales(devices);
				sort(allsales, productnames, productmodels , 12);
				
				printf("Product:				-	Sales: \n");
				printArray(productnames, productmodels, allsales);
			}
			
			else if(strcmp(arg1, "purchases") == 0){	// if arg1 is "purchases" call getAllPurchases() and sort().
				getAllPurchases(devices);
				sort(allpurchases, productnames, productmodels, 12);
				
				printf("Product:				-	Purchases: \n");
				printArray(productnames, productmodels, allpurchases);
			}
			
			else if(strcmp(arg1, "profit") == 0){	// if arg1 is "profit" call getAllProfits() and sort().
				getAllProfits(devices);
				sort(allprofits, productnames, productmodels, 12);
				
				printf("Product:				-	Profit: \n\n");
				printArray(productnames, productmodels, allprofits);
			}
			else{
				commandError();	
			}
		}
		
		
		//	******************SOLD COMMAND******************
		else if(strcmp(cmd, "sold") == 0){		//	if command is sold change adjust product values accordingly.
			scanf("%s %s %d", &arg1, &arg2, &arg3);
			system("cls");
			
			nodeptr np = lookfor(devices, arg1, arg2);		//	look for product in list to be sold so values can be adjusted
			if(np == NULL)									//	lookfor() returns a empty node if the device was not found
				commandError();
			else{
				if(np -> stock >= arg3){			//	checks if stock is more than how much user is trying to sell if it isn't give error message.
					np -> stock -= arg3;
					np -> sales += np -> price * arg3;
					totalsales += np -> price * arg3;
					np -> profit = np -> sales - np -> purchases;
					printf("Sold %d %s %s. New Stock is %d\n", arg3, np -> name, np -> model, np -> stock);
				}
				else
					printf("You don\'t have enough stock to sell.\n\n");
			}
		}
		
		//	******************PURCHASED COMMAND******************
		else if(strcmp(cmd, "purchased") == 0){
			scanf("%s %s %d", &arg1, &arg2, &arg3);
			system("cls");
			
			nodeptr np = lookfor(devices, arg1, arg2);
			if(np == NULL)									//	lookfor() returns a empty node if the device was not found
				commandError();	
			else{
				np -> stock += arg3;
				np -> purchases += (np -> price / 1.2) * arg3;		//	calculates 20% markup based on selling price
				totalpurchases += (np -> price / 1.2) * arg3;
				np -> profit = np -> sales - np -> purchases;
				
				printf("Purchased %d %s %s. New Stock is %d", arg3, np -> name, np -> model, np -> stock);
			}
		}
		
		//	******************STATS COMAND******************
		else if(strcmp(cmd, "stats") == 0){		//	if cmd is "stats" ask for 2 more parameters being the name and model of the product you want the stats for.
			scanf("%s %s", &arg1, &arg2);
			system("cls");
			
			int sold;
			int purchased;
			float profit;
			nodeptr np = NULL;
			
			
			np = lookfor(devices, arg1, arg2);
			if(np == NULL){
				commandError();
			}
			else{
				sold = np -> sales / np -> price;
				purchased = np -> stock + sold - np -> openstock;
				
				printf("%s %s stats: \n", arg1, arg2);
				printf("Units sold		- 	%d units\n", sold);
				printf("Sales			- 	$%.2f \n \n", np -> sales);
				
				printf("Units purchased		-	%d units\n", purchased);
				printf("Purchases		-	$%.2f \n \n", np -> purchases);
				
				printf("Profit			-	$%.2f \n", np -> profit);
			}
		}
		
		else{
			system("cls");
			commandError();		//	if non of the commands are entered then there was an error with the command
		}
			
		checkStock(devices);
	}
	fclose(products);
	return 0;
}





































