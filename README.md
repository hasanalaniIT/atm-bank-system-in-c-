"# atm-bank-system-in-c-" 
"# atm-bank-system-in-c-" 
"# atm-bank-system-in-c-" 

@@ -0,0 +1,336 @@
#include <stdio.h>                   /*Hasan Alani  B1905.090005*/
#include <string.h>
#include <conio.h>   
#include <stdlib.h>
                                   
struct users 
{
 char name[30];
 char surname[30];
 float balance ;
 int usernumber ;		
};

struct users acc[100];
int usernum;  
FILE *fp,*fp2,*fp3;

void display ();
void deposit ();
void withdraw ();
void userinfo ();
void newuser ();
void menu ();
               
int main()

{
 char choice;                /*used char beacuse it close if it was int value*/
 usernum=0;
 
  /* while(1){ /*            /*this loop is extra but its more safer if you use it*/
   
 printf("*********Wellcome To Hasan ALANI ATM**********\n") ;	
 display ();
 printf("\n**********************************************\n") ;	
 printf("TO CONTINUE \nEnter the choice you want with numbers :\n") ; 
 scanf("%c",&choice) ;	
 switch (choice)
 {
  case '1':
  newuser ();
  break;
  case '2':
  userinfo ();
  break;
  case '3':
  deposit ();
  break;
  case '4':
  withdraw();
  break;
  case '5':
  system ("cls") ;
  main();
  break;
  case '6':
  return 0;
  default :
   system("cls");              /*to clean the screen after any opreation*/
   printf("TO CONTINUE USE THE NUMBERS ON KEYBOARD PLEASE! (1/2/3/4/5/6) \n") ;
   main();
   break;
 	
  } 
      /* } */                  /*for the while loop*/
}
 void display()
 {
 	printf("\n1. Create a New User Account (sign up)\n") ;
 	printf("2. Aacount/User information \n") ;
 	printf("3. Deposit Money to Account \n") ;
 	printf("4. Withdraw Money from Account \n") ;
 	printf("5. Rest Screen (Clear) \n") ;
 	printf("6. EXIT (END) \n") ;
 }
 void newuser ()
 { 
   char name[30],surname[30];
   float balance=0;
   int i,usernumber;
   fflush(stdin);
  	 
   fp= fopen("Users info.bin","ab") ;  /*rest the old registerd users files if u create a new one*/
   fp2= fopen("NEW Users info.txt","w+") ;
   fp2= fopen("NEW Users info.txt","a+") ;
   fp3= fopen("Users info.bin","ab") ; 
   if (fp==NULL||fp2==NULL)
  {
  	printf("No Accounts ");
  	menu();
  }
   else {
   
   printf("\nEnter the first name:") ;
   scanf("%s",&name);
   printf("\nEnter the Last name:") ;
   scanf("%s",&surname);
   printf("\nPlease Enter the User Account Number (1 TO 100):");
   scanf("%d",&usernumber);
   
   strcpy(acc[usernumber].name,name) ;
   strcpy(acc[usernumber].surname,surname) ;
   acc[usernumber].usernumber=usernumber;  /*no need for strcpy beacuse they are not char verable*/
   acc[usernumber].balance=balance;        
                         
	
   printf("\nSuccess Account created and registerd!!!\n");
   fprintf(fp2,"\nUser info When Registerd\n");
   printf("User First Name : %s\n",acc[usernumber].name);
   fprintf(fp2,"User First Name : %s\n",acc[usernumber].name);
   
   printf("User Last Name (Surname) : %s\n",acc[usernumber].surname);	
  fprintf(fp2,"User Last Name (Surname) : %s\n",acc[usernumber].surname);
  
   printf("User Account Number : %d\n",acc[usernumber].usernumber);
   fprintf(fp2,"User Account Number : %d\n",acc[usernumber].usernumber);
   
   printf("User Account Balance (Money) : %f\n",acc[usernumber].balance);  
  fprintf(fp2,"User Account Balance (Money) : %f\n\n",acc[usernumber].balance); 
  for(i=0;i<usernumber;i++)
   { 
	 fprintf(fp,"%s\n",acc[usernumber].name);
    fprintf(fp,"%s\n",acc[usernumber].surname);       
    fprintf(fp,"%d\n",acc[usernumber].usernumber);    
    fprintf(fp,"%f\n",acc[usernumber].balance);    
	break;                                                   	
  }
}
 fclose(fp3); /*  it will only rigster one user if used*/
   menu();              /*calling the menu fucntion to go back*/
 }
 
 void menu()           /*a function to return to the main menu */
 { 
  char i ;
  printf("\nEnter  1  to go back to the Menu Screen(Display)\nEnter 0 To Exit (END) the ATM..:");
  scanf("%s",&i) ; /*it only worked with the &i i dont know how :D*/
  if(i=='1')
  {
  	main();
  }
  else if (i=='0')
  {
  	exit(0);
  }
   else 
  {
  	return menu() ; /*the return so it wont get copyed 2 times on output*/
  }
 	
 }
 
 void userinfo () 
{		
int i,usernum_g;
printf("Enter the User Account Number to Display Information :  ");
scanf("%d",&usernum_g);	  
fp3 = fopen("Users infodep.bin","ab+") ; 
fp = fopen("Users info.bin","rb") ; 
fp2= fopen("NEW Users info.txt","a+") ;
  if (fp==NULL)
  { 
  	printf("\nThis Account (User) [%d] is Not Availabe Or Registered.!!\n",usernum_g);
  	menu();
  }
  
  else 
   {
  for(i=0;i<=usernum_g;i++)
  {		
		fscanf(fp,"%s\n",&acc[i].name);	
		fscanf(fp,"%s\n",&acc[i].surname);;	
	  	fscanf(fp,"%d\n",&acc[i].usernumber);
		fscanf(fp,"%f\n",&acc[i].balance);	      
  } 
   
 for(i=0;i<=usernum_g;i++)  
  {
    if(acc[i].usernumber==usernum_g)
	{  
	 printf("User First Name : %s\n",acc[i].name);		
	 printf("User Last Name (Surname): %s\n",acc[i].surname);	
	 printf("User Account Number : %d\n",acc[i].usernumber); 	
	 printf("User Account Balance (Money) : %f\n",acc[i].balance);
       	
	 fprintf(fp2,"\nUser Full ACCOUNT information\n");
     fprintf(fp2,"User First Name : %s\n",acc[usernum_g].name);
	 fprintf(fp2,"User Last Name (Surname) : %s\n",acc[usernum_g].surname);
     fprintf(fp2,"User Account Number : %d\n",acc[usernum_g].usernumber);
     fprintf(fp2,"User Account Balance (Money) : %f\n\n",acc[usernum_g].balance); 
    	
     fprintf(fp3,"%s\n",acc[i].name);
	 fprintf(fp3,"%s\n",acc[i].surname);
     fprintf(fp3,"%d\n",acc[i].usernumber);
     fprintf(fp3,"%f\n",acc[i].balance); 
		  break;
	}
  } 
	}
  
    if (acc[i].usernumber!=usernum_g)
    {
      printf("\nThis Account (User) [%d] is Not Availabe Or Registered.!!\n",usernum_g);
      printf("\nPlease Enter A valid Account Number Or Register\n\n");
    }
    fclose(fp);
	fclose(fp2);  
	menu();
}

 void deposit ()
{  
fp3=  fopen("Users infodep.bin","rb") ;  
fp2= fopen("NEW Users info.txt","a+") ;
float deposit_m ;
int i,usernum_g;         

  printf("Enter the account or user number you want to deposit money for.:");
  scanf("%d",&usernum_g) ;
  
  fp=  fopen("Users info.bin","wb") ; 
  fclose(fp); 
for(i=0;i<usernum_g;i++)
  {
  fscanf(fp3,"%s\n",&acc[usernum_g].name);
  fscanf(fp3,"%s\n",&acc[usernum_g].surname);       /*to read the file info for this function*/
  fscanf(fp3,"%d\n",&acc[usernum_g].usernumber);    
  fscanf(fp3,"%f\n",&acc[usernum_g].balance);
  
  }
   if(acc[usernum_g].usernumber !=usernum_g)
   
   {
    printf("\nThis Account (User) [%d] is Not Availabe Or Registered.!!\n",usernum_g);
    printf("\nPlease Enter A valid Account Number Or Register\n\n");
	menu();   
   }
  else 
 {
  printf("\nthe money (balance) for this Account(User) %d is %f \n",usernum_g,acc[usernum_g].balance) ;
  printf("\nEnter Money you want to Deposit : ");
  scanf("%f",&deposit_m) ;
  
  while(usernum_g=acc[usernum_g].usernumber)
   { 	fp=  fopen("Users info.bin","ab") ;
   acc[usernum_g].balance=acc[usernum_g].balance+deposit_m;
   printf("\nThe new Money(Balance) for Account (user) %d is %f \n",usernum_g,acc[usernum_g].balance) ;
       
	fprintf(fp2,"\nUser After Deposit information\n");
	fprintf(fp2,"User First Name : %s\n",acc[usernum_g].name);
	fprintf(fp2,"User Last Name (Surname) : %s\n",acc[usernum_g].surname);
	fprintf(fp2,"User Account Number : %d\n",acc[usernum_g].usernumber);
	fprintf(fp2,"User Account Balance (Money) : %f\n\n",acc[usernum_g].balance);  
		 
for(i=0;i<usernum_g;i++) 
{
	fprintf(fp,"%s\n",acc[usernum_g].name);
    fprintf(fp,"%s\n",acc[usernum_g].surname);       /*to read the file info for this function*/
    fprintf(fp,"%d\n",acc[usernum_g].usernumber);    
    fprintf(fp,"%f\n",acc[usernum_g].balance);
    break;
}
   break;                       /*BREAK SO it wont do infinte loop*/
   }
   
    fclose(fp);      		         
	menu();  
 }		                  
}
 void withdraw ()
 
{ 
  fp2= fopen("NEW Users info.txt","a+") ;
  fp3=  fopen("Users info.bin","rb") ;
  
  float withdraw_m;
  int i,usernum_g; 
  fp=  fopen("Users info.bin","wb") ; 
  fclose(fp); 
          
  printf("Enter The Account (User) Number you want to withdraw money from : ");
  scanf("%d",&usernum_g);
 for(i=0;i<usernum_g;i++)
  {
  fscanf(fp3,"%s\n",&acc[usernum_g].name);
  fscanf(fp3,"%s\n",&acc[usernum_g].surname);       /*to read the file info for this function*/
  fscanf(fp3,"%d\n",&acc[usernum_g].usernumber);    
  fscanf(fp3,"%f\n",&acc[usernum_g].balance);
 }
 if(acc[usernum_g].usernumber !=usernum_g)
   {
    printf("\nThis Account (User) [%d] is Not Availabe Or Registered.!!\n",usernum_g);
    printf("\nPlease Enter A valid Account Number Or Register\n\n");
	menu();   
   }
   else
  
    printf("\nThe Money (Balance) for this Account (user) %d is %f \n",usernum_g,acc[usernum_g].balance);
    printf("\nEnter the amount of Money to Withdraw from the Account :");
    scanf("%f",&withdraw_m);
   
   if(withdraw_m>acc[usernum_g].balance)
   {
   	printf("\nNot Enough Money to Withdraw From Account\n\n") ;
   	menu();
   }
   else
    { 
      while(usernum_g=acc[usernum_g].usernumber)
     {
   	  acc[usernum_g].balance=acc[usernum_g].balance-withdraw_m;
   	  printf("\nThe new Money(Balance) for the Account (user) %d is %f \n",usernum_g,acc[usernum_g].balance) ;
	   fp=  fopen("Users info.bin","ab") ;
	   
	    fprintf(fp2,"\nUser After Withdraw information\n");
		fprintf(fp2,"User First Name : %s\n",acc[usernum_g].name);
	    fprintf(fp2,"User Last Name (Surname) : %s\n",acc[usernum_g].surname);
	    fprintf(fp2,"User Account Number : %d\n",acc[usernum_g].usernumber);
	    fprintf(fp2,"User Account Balance (Money) : %f\n\n",acc[usernum_g].balance);
	            
	for(i=0;i<usernum_g;i++)
	{
       fprintf(fp,"%s\n",acc[usernum_g].name);
       fprintf(fp,"%s\n",acc[usernum_g].surname);       /*to read the file info for this function*/
       fprintf(fp,"%d\n",acc[usernum_g].usernumber);    
       fprintf(fp,"%f\n",acc[usernum_g].balance);
       break;
    }
	   break;                    /*BREAK SO it wont do infinte loop*/
     }
    fclose(fp);     
	fclose(fp2);   
	fclose(fp3);     
 	menu();	
    }		
}
