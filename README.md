//JAN 10 2020
//JASPER FOO SEH KIUN
//TP
//C PROGRAMMING ASSIGNMENT
//TRAINING COURSE PACKAGE MANAGEMENT SYSTEM
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <string.h>
struct login
{
	char fname[100];
	char lname[100];
	char username[20];
	int gender;
};
void view();
void usercourse();
void book();
void main();
void signup();
void login();
void payment();
void cancel();
void change();
void finddate();
void checkexist();
void teambuildleft();
void rangeteambuild();
void viewteambuilding();
void viewcomm();
void rangecomm();
void commleft();
void rangecorpcargrow();
void corpcargrowleft();
void viewcorpcargrow();
void conflictmanageleft();
void rangeconflictmanage();
void viewconflictmanage();
void rangesoftdes();
void softdesleft();
void viewsoftdes();
void rangewebdevelop();
void webdevelopleft();
void viewwebdevelop();
void rangecloudcomp();
void cloudcompleft();
void viewcloudcomp();
void rangemobdesdev();
void mobdesdevleft();
void viewmobdesdev();
void cashiersystem();

FILE *fptr, *fp;
int capacity, capacity1, capacity2, capacity3;
int capacity4, capacity5, capacity6, capacity7;
float total = 0, mealtype;
float newTotal = 0;
int option, newuser = 0;
int status = 0;
int gender;
char enteruname[100];
char *course;
int paymenttype, cardno, expiration, cvv;
float pay, left;

void main()// the menu
{
	printf("\n_______________________________________________________________________\n");
	printf("---------------TRAINING COURSE PACKAGE MANAGEMENT SYSTEM---------------\n");
	printf("______________________________M_E_N_U__________________________________\n\n\n");
	printf("<<1>> to view course\t\t\t\t<<2>> to make a booking\n\n");
	printf("<<3>> to view participants Information\t\t<<4>> to change course\n\n");
	printf("<<5>> to find a course based on the date\t<<6>> for cancellation\n\n");
	printf("<<7>> for cashier system\t\t\t<<8>> to exit\n\n");
	printf("_______________________________________________________________________\n");
	printf("Select an Option: ");

	scanf("%d", &option);
	switch (option)
	{
	case 1:
		view(); // to view the courses
		break;
	case 2:
		do {
			printf("\nNew Member?"); // ask user if the participant is new member
			printf("\n(1)YES\n(2)NO\n");
			scanf("%d", &newuser);
			if (newuser == 1)
			{
				printf("\n------REGISTER------\n");
				checkexist();
				break;
			}
			else if (newuser == 2)
			{
				login();
				break;
			}
			else
			{
				printf("\nPlease Enter a Valid Number!\n");
			}
		} while (newuser < 1 || newuser > 2);
	case 3:
		usercourse();// to view user information
		break;
	case 4:
		change();// if user wants to change course
		break;
	case 5:
		finddate();// check available courses by date
		break;
	case 6:
		cancel(); // if user wants to cancel
		break;
	case 7:
		cashiersystem();//make payment
		break;
	case 8:
		exit(0);
	default:
		printf("\nPLEASE ENTER A VALID NUMBER!\n");
		main();
	}
}
void checkexist()//to check if username already taken
{
	printf("\nEnter Username : ");
	scanf("%s", enteruname);
	strcat(enteruname, ".txt");
	fptr = fopen(enteruname, "r");
	if (fptr == NULL)
	{
		signup();
	}
	else
	{
		printf("\n\nUsername already taken\n");
		printf("Please enter another username\n");
		checkexist();
	}
}
void signup()//registering new particants
{
	struct login l;
	printf("\nRetype Username : ");
	scanf("%s", &l.username);
	fptr = fopen(enteruname, "r");

	sprintf(enteruname, "%s.txt", &l.username);//name a text file based on the username
	fptr = fopen(enteruname, "a+");
	printf("\nEnter first name : ");
	scanf("%s", &l.fname);

	printf("\nEnter last name : ");
	scanf("%s", &l.lname);
	do {
		printf("\nEnter gender : ");
		printf("\n1.Male\n2.Female\n");
		scanf("%d", &gender);
		if (gender == 1)
		{
			fprintf(fptr, "USERNAME = %s\n", &l.username);//store in participant's text file
			fprintf(fptr, "FIRST NAME = %s\n", &l.fname);
			fprintf(fptr, "LAST NAME = %s\n", &l.lname);
			fprintf(fptr, "GENDER = male\n");
		}
		else if (gender == 2)
		{
			fprintf(fptr, "USERNAME = %s\n", &l.username);
			fprintf(fptr, "FIRSTNAME = %s\n", &l.fname);
			fprintf(fptr, "LASTNAME = %s\n", &l.lname);
			fprintf(fptr, "GENDER = female\n");
		}
		else
		{
			printf("\nPlease Enter a Valid Number!\n");
		}

	} while (gender < 1 || gender > 2);

	fclose(fptr);
	printf("\nParticipant's Username is\n[%s]\n", &l.username);
	printf("\nLet's get started\n");
	system("pause");
	printf("\nPress any key to proceed");
	system("cls");
	book();
}
void login()// logging in participants
{
	printf("\n----LOGIN----");
	printf("\nUsername : ");
	scanf("%s", enteruname);
	strcat(enteruname, ".txt");  //enter file name without .txt
	fptr = fopen(enteruname, "r");

	if (fptr == NULL)
	{
		printf("Username not found!!!");
		login();
	}
	else
	{
		printf("\n===Login Successful===\n");
		book();
	}
}
void view()//view all the courses that company has
{
	system("CLS");
	printf("==================================================================================================================\n");
	printf("\t\t\t\t\t      Knowledgebase Academy\n");
	printf("==================================================================================================================");
	printf("\n  SOFT SKILLS                 DAY            DATE              ADMIN FEE        FEE   MEAL(VEGAN)  MEAL(NON-VEGAN)\n");
	printf("1. Team building             3 days    11-13 December 2019        50            800       75              50\n");
	printf("2. Communications            3 days     9-11 December 2019        50            650       50              25\n");
	printf("3. Corporate Career Growth   3 days    15-17 November 2019        50            750       50              25\n");
	printf("4. Conflict Management       5 days    15-19 December 2019        50            600       50              25\n");
	printf("==================================================================================================================");
	printf("\n  COMPUTING SKILLS            DAY            DATE              ADMIN FEE        FEE   MEAL(VEGAN)  MEAL(NON-VEGAN)\n");
	printf("5. Software Design           5 days    16-20 November 2019        50            1000      50              25\n");
	printf("6. Web Development           5 days    5-9 October 2019           50            1100      75              50\n");
	printf("7. Cloud Computing           3 days    23-25 December 2019        50            1300      50              25\n");
	printf("8. Mobile Content Design     5 day     5-9 December 2019          50            1200      75              50\n");
	printf("   and Development\n");
	printf("==================================================================================================================\n");
	main();
}
void book()//booking courses
{
	fptr = fopen(enteruname, "a+");
	int category, skills, choose;
	float fee = 0;
	course = NULL;
	char *date;
	date = NULL;
	float adminFee = 50;
	float meal = 0;
	float input = 0;

	do {
		printf("\nSelect a Category:");

		do {
			printf("\nPress [1] for Soft Skills\nPress [2] for Computing skills\n");
			scanf("%d", &category);
			if (category == 1)
			{
				fprintf(fptr, "\nCategory= Soft skills\n");
				printf("\n  SOFT SKILLS                 DAY            DATE              ADMIN FEE        FEE   MEAL(VEGAN)  MEAL(NON-VEGAN)\n");
				printf("1. Team building             3 days    11-13 December 2019        50            800       75              50\n");
				printf("2. Communications            3 days     9-11 December 2019        50            650       50              25\n");
				printf("3. Corporate Career Growth   3 days    15-17 November 2019        50            750       50              25\n");
				printf("4. Conflict Management       5 days    15-19 December 2019        50            600       50              25\n");

				do {
					printf("\nWhich course to take?\n");
					scanf("%d", &skills);

					switch (skills)
					{
					case 1:
						course = "<Team building>";
						date = "11-13 December 2019";
						fee = 800;
						fprintf(fptr, "Course = %s\n", course);
						fprintf(fptr, "Date = %s\n", date);
						do {
							printf("\n1. Meal(Vegetarian)\n2. Meal(Non-Vegetarian)\nSelect a Meal Type: ");
							scanf("%f", &mealtype);
							if (mealtype == 1)
							{
								fprintf(fptr, "Meal = Vegetarian\n");
								meal = 75;
								total = fee + adminFee + meal;
							}
							else if (mealtype == 2)
							{
								fprintf(fptr, "Meal = Non-Vegetarian\n");
								meal = 50;
								total = fee + adminFee + meal;
							}
							else
							{
								("Please enter a valid number!");
							}
						} while (mealtype < 1 || mealtype > 2);
						rangeteambuild();
						break;
					case 2:
						course = "<Communications>";
						date = "9-11 December 2019";
						fee = 650;
						fprintf(fptr, "Course = %s\n", course);
						fprintf(fptr, "Date = %s\n", date);
						do {
							printf("\n1. Meal(Vegetarian)\n2. Meal(Non-Vegetarian)\nSelect a Meal Type: ");
							scanf("%f", &mealtype);
							if (mealtype == 1)
							{
								fprintf(fptr, "Meal = Vegetarian\n");
								meal = 50;
								total = fee + adminFee + meal;
							}
							else if (mealtype == 2)
							{
								fprintf(fptr, "Meal = Non-Vegetarian\n");
								meal = 25;
								total = fee + adminFee + meal;
							}
							else
							{
								("Please enter a valid number!");
							}
						} while (mealtype < 1 || mealtype > 2);
						rangecomm();
						break;
					case 3:
						course = "Corporate Career Growth";
						date = "15-17 November 2019";
						fee = 750;
						fprintf(fptr, "Course = %s\n", course);
						fprintf(fptr, "Date = %s\n", date);
						do {
							printf("\n1. Meal(Vegetarian)\n2. Meal(Non-Vegetarian)\nSelect a Meal Type: ");
							scanf("%f", &mealtype);
							if (mealtype == 1)
							{
								fprintf(fptr, "Meal = Vegetarian\n");
								meal = 50;
								total = fee + adminFee + meal;
							}
							else if (mealtype == 2)
							{
								fprintf(fptr, "Meal = Non-Vegetarian\n");
								meal = 25;
								total = fee + adminFee + meal;
							}
							else
							{
								("Please enter a valid number!");
							}
						} while (mealtype < 1 || mealtype > 2);
						rangecorpcargrow();
						break;
					case 4:
						course = "Conflict Management";
						date = "15-19 December 2019";
						fee = 600;
						fprintf(fptr, "course = %s\n", course);
						fprintf(fptr, "date = %s\n", date);
						do {
							printf("\n1. Meal(Vegetarian)\n2. Meal(Non-Vegetarian)\nSelect a Meal Type: ");
							scanf("%f", &mealtype);
							if (mealtype == 1)
							{
								fprintf(fptr, "Meal = Vegetarian\n");
								meal = 50;
								total = fee + adminFee + meal;
							}
							else if (mealtype == 2)
							{
								fprintf(fptr, "Meal = Non-Vegetarian\n");
								meal = 25;
								total = fee + adminFee + meal;
							}
							else
							{
								("Please enter a valid number!");
							}
						} while (mealtype < 1 || mealtype > 2);
						rangeconflictmanage();
						break;
					default:
						printf("\nPLEASE ENTER A VALID NUMBER\n");
						break;
					}
				} while (skills < 1 || skills > 4);
			}
			else if (category == 2)
			{
				fprintf(fptr, "\nCategory= Computing skills\n");
				printf("\n  COMPUTING SKILLS            DAY            DATE              ADMIN FEE        FEE   MEAL(VEGAN)  MEAL(NON-VEGAN)\n");
				printf("5. Software Design           5 days    16-20 November 2019        50            1000      50              25\n");
				printf("6. Web Development           5 days    5-9 October 2019           50            1100      75              50\n");
				printf("7. Cloud Computing           3 days    23-25 December 2019        50            1300      50              25\n");
				printf("8. Mobile Content Design     5 day     5-9 December 2019          50            1200      75              50\n");
				printf("   and Development\n");

				do {
					printf("\nWhich course would you like to take?:\n");
					scanf("%d", &skills);

					switch (skills)
					{
					case 5:
						course = "<Software Design>";
						date = "16-20 November 2019";
						fee = 1000;
						fprintf(fptr, "course = %s\n", course);
						fprintf(fptr, "date = %s\n", date);
						do {
							printf("\n1. Meal(Vegetarian)\n2. Meal(Non-Vegetarian)\nSelect a Meal Type: ");
							scanf("%f", &mealtype);
							if (mealtype == 1)
							{
								fprintf(fptr, "Meal = Vegetarian\n");
								meal = 50;
								total = fee + adminFee + meal;
							}
							else if (mealtype == 2)
							{
								fprintf(fptr, "Meal = Non-Vegetarian\n");
								meal = 25;
								total = fee + adminFee + meal;
							}
							else
							{
								("Please enter a valid number!");
							}
						} while (mealtype < 1 || mealtype > 2);
						rangesoftdes();
						break;
					case 6:
						course = "<Web Development>";
						date = "5-9 October 2019";
						fee = 1100;
						fprintf(fptr, "Course = %s\n", course);
						fprintf(fptr, "Date = %s\n", date);
						do {
							printf("\n1. Meal(Vegetarian)\n2. Meal(Non-Vegetarian)\nSelect a Meal Type: ");
							scanf("%f", &mealtype);
							if (mealtype == 1)
							{
								fprintf(fptr, "Meal = Vegetarian\n");
								meal = 75;
								total = fee + adminFee + meal;
							}
							else if (mealtype == 2)
							{
								fprintf(fptr, "Meal = Non-Vegetarian\n");
								meal = 50;
								total = fee + adminFee + meal;
							}
							else
							{
								("Please enter a valid number!");
							}
						} while (mealtype < 1 || mealtype > 2);
						rangewebdevelop();
						break;
					case 7:
						course = "<Cloud Computing>";
						date = "23 - 25 December 2019";
						fee = 1300;
						fprintf(fptr, "Course = %s\n", course);
						fprintf(fptr, "Date = %s\n", date);
						do {
							printf("\n1. Meal(Vegetarian)\n2. Meal(Non-Vegetarian)\nSelect a Meal Type: ");
							scanf("%f", &mealtype);
							if (mealtype == 1)
							{
								fprintf(fptr, "Meal = Vegetarian\n");
								meal = 50;
								total = fee + adminFee + meal;
							}
							else if (mealtype == 2)
							{
								fprintf(fptr, "Meal = Non-Vegetarian\n");
								meal = 25;
								total = fee + adminFee + meal;
							}
							else
							{
								("Please enter a valid number!");
							}
						} while (mealtype < 1 || mealtype > 2);
						rangecloudcomp();
						break;
					case 8:
						course = "<Mobile Content Design and Development>";
						date = "5 - 9 December 2019";
						fee = 1200;
						fprintf(fptr, "Course = %s\n", course);
						fprintf(fptr, "Date = %s\n", date);

						printf("\n1. Meal(Vegetarian)\n2. Meal(Non-Vegetarian)\nSelect a Meal Type: ");
						scanf("%f", &mealtype);
						do {
							printf("\n1. Meal(Vegetarian)\n2. Meal(Non-Vegetarian)\nSelect a Meal Type: ");
							scanf("%f", &mealtype);
							if (mealtype == 1)
							{
								fprintf(fptr, "Meal = Vegetarian\n");
								meal = 75;
								total = fee + adminFee + meal;
							}
							else if (mealtype == 2)
							{
								fprintf(fptr, "Meal = Non-Vegetarian\n");
								meal = 50;
								total = fee + adminFee + meal;
							}
							else
							{
								("Please enter a valid number!");
							}
						} while (mealtype < 1 || mealtype > 2);
						rangemobdesdev();
						break;
					default:
						printf("\nPLEASE ENTER A VALID NUMBER\n");
						break;
					}
				} while (skills < 5 || skills > 8);
			}
			else
			{
				printf("Please enter a valid Number\n");
			}

		} while (category < 1 || category > 2);

		newTotal += total;
		system("cls");
		printf("The Chosen Course is %s\n", course);
		printf("FEE            RM%.2f\nADMIN FEE      RM%.2f\nMEAL           RM%.2f", fee, adminFee, meal);// details
		printf("\nTHE TOTAL IS  <RM%.2f>\n", total);
		printf("SUM = RM%.2f\n", newTotal);
		fprintf(fptr, "Course Total = RM%.2f\n", total);
		printf("\n**************Payment to be made RM%.2f**************\n", newTotal);// total amount that needed to be paid
		fprintf(fptr, "Total Payment = RM%.2f\n", newTotal);
		printf("\nTo add more course, press 1\nTo pay, press 0\n");
		scanf("%d", &choose);

	} while (choose == 1);

	printf("enter the amount to pay for right now:RM");
	scanf("%f", &pay);
	//system("pause");
	payment();
}
void usercourse()//view participants information
{
	char display;
	int changeCourse = 0;

	printf("\n-----Search for User Info-----");
	printf("\nUsername : ");
	scanf("%s", enteruname);
	strcat(enteruname, ".txt");//enter file name without .txt

	fptr = fopen(enteruname, "r");
	if (fptr == NULL)
	{
		printf("Username not found!!!\n");
		usercourse();
	}
	else
	{
		display = fgetc(fptr);// display all the details
		while (display != EOF)//until end of files
		{
			printf("%c", display);
			display = fgetc(fptr);
		}
		main();
	}
}
//void existcancel()
//{
//	printf("\n-----Cancellation-----");
//	printf("\nUsername : ");
//	scanf("%s", enteruname);
//	strcat(enteruname, ".txt");
//
//	fptr = fopen(enteruname, "r");
//	if (fptr == NULL)
//	{
//		printf("Username not found!!!\n");
//		existcancel();
//	}
//	else
//	{
//		cancel();
//	}
//}
void cancel()//course cancellation
{
	printf("\n----Cancellation----");
	printf("\nEnter Username : ");
	scanf("%s", enteruname);
	strcat(enteruname, ".txt"); //enter file name without .txt

	if (status == 0)
	{
		status = remove(enteruname);
		printf("\t ___________________________________________________________\n");
		printf("\t|\t\tCourse has been Cancelled                   |\n");
		printf("\t|___________________________________________________________|\n");
		main();
	}
	else
	{
		printf("Username not found!!!");
		cancel();
	}
	system("pause");

}
void change()//change of course
{
	printf("\n----Change of Course----");
	printf("\nEnter Username : ");
	scanf("%s", enteruname);
	strcat(enteruname, ".txt"); //enter file name without .txt

	if (status == 0)
	{
		status = remove(enteruname);
		printf("Please enter information again for confirmation\n");
		signup();
	}
	else
	{
		printf("Username not found!!!");
		change();
	}
	system("pause");
}
void payment() // to make a payment after booking
{
	do {
		printf("\nPayment Method");
		printf("\n1.Credit Card\n2.Debit Card\n3.Cash\nEnter <1/2/3>\n");// payment method
		scanf("%d", &paymenttype);

		if (paymenttype == 1)//pay by Credit Card
		{
			printf("\nCard number:");
			scanf("%d", &cardno);
			printf("\nExpiration date:");
			scanf("%d", &expiration);
			printf("\nCVV code: ");
			scanf("%d", &cvv);
			fprintf(fptr, "Credit Card Details");
			fprintf(fptr, "\nPayment method:Credit card\n");
			fprintf(fptr, "Card number: %d\nExpiration date: %d\nCVV code: %d\n", cardno, expiration, cvv);
		}
		else if (paymenttype == 2)//Pay by Debit card
		{
			printf("\nCard number:");
			scanf("%d", &cardno);
			printf("\nExpiration date:");
			scanf("%d", &expiration);
			printf("\nCVV code: ");
			scanf("%d", &cvv);
			fprintf(fptr, "Debit Card Details");
			fprintf(fptr, "\nPayment method:Debit card\n");
			fprintf(fptr, "Card number: %d\nExpiration date: %d\nCVV code: %d\n", cardno, expiration, cvv);// store in text files
		}
		else if (paymenttype == 3)//Pay by cash
		{
			printf("Pay with cash");
			fprintf(fptr, "\nPayment method:Cash");
		}
		else
		{
			printf("\n Please enter a valid Number\n");
		}

	} while (paymenttype < 1 || paymenttype > 3);

	fprintf(fptr, "\nPayment made:RM%.2f\n", pay);
	left = newTotal - pay;
	printf("\nPayment Left:RM%.2f\n", left);
	fprintf(fptr, "\nPayment left:RM%.2f\n", left);
	fprintf(fptr, "_________________________________________\n");
	system("pause");
	exit(0);
	
}
void cashiersystem() // to make a payment what has left
{
	float amount,owed,remain;
	printf("Enter amount still owed: RM");
	scanf("%f",&owed);
	printf("Enter amount to pay: RM");
	scanf("%f", &amount);

	do {
		printf("\nPayment Method");
		printf("\n1.Credit Card\n2.Debit Card\n3.Cash\nEnter <1/2/3>\n");// payment method
		scanf("%d", &paymenttype);

		if (paymenttype == 1)//pay by Credit Card
		{
			printf("\nCard number:");
			scanf("%d", &cardno);
			printf("\nExpiration date:");
			scanf("%d", &expiration);
			printf("\nCVV code: ");
			scanf("%d", &cvv);
			printf( "\nCredit Card Details");
			printf( "\nPayment method:Credit card\n");
			printf( "Card number: %d\nExpiration date: %d\nCVV code: %d\n", cardno, expiration, cvv);
		}
		else if (paymenttype == 2)//Pay by Debit card
		{
			printf("\nCard number:");
			scanf("%d", &cardno);
			printf("\nExpiration date:");
			scanf("%d", &expiration);
			printf("\nCVV code: ");
			scanf("%d", &cvv);
			printf("\nDebit Card Details");
			printf("\nPayment method:Credit card\n");
			printf("Card number: %d\nExpiration date: %d\nCVV code: %d\n", cardno, expiration, cvv);
		}
		else if (paymenttype == 3)//Pay by cash
		{
			printf( "\nPayment method:Cash");
		}
		else
		{
			printf("\n Please enter a valid Number\n");
		}

	} while (paymenttype < 1 || paymenttype > 3);

	remain = owed - amount;
	printf("\nPayment left: RM%.2f\n", remain);

	system("pause");
	exit(0);

}
void finddate()//find course based on date input
{
	int month, nov, dec, findmenu;

	do {
		printf("Course available based on date:");
		printf("\nPlease pick a month\n");
		printf("1. OCTOBER\n2. NOVEMBER\n3. DECEMBER\n");
		scanf("%d", &month);

		if (month == 1)
		{
			printf("\n  COMPUTING SKILLS            DAY            DATE              ADMIN FEE        FEE   MEAL(VEGAN)  MEAL(NON-VEGAN)\n");
			printf("6. Web Development           5 days    5-9 October 2019           50            1100      75              50\n");
			viewwebdevelop();//view the course's available slots

		}
		else if (month == 2)
		{
			do {
				printf("\nPlease pick a day\n");
				printf("1. 15-17 November\n2. 16-20 November\n");
				scanf("%d", &nov);
				if (nov == 1)
				{
					printf("\n  SOFT SKILLS                 DAY            DATE              ADMIN FEE        FEE   MEAL(VEGAN)  MEAL(NON-VEGAN)\n");
					printf("3. Corporate Career Growth   3 days    15-17 November 2019        50            750       50              25\n");
					viewcorpcargrow();
				}
				else if (nov == 2)
				{
					printf("\n  COMPUTING SKILLS            DAY            DATE              ADMIN FEE        FEE   MEAL(VEGAN)  MEAL(NON-VEGAN)\n");
					printf("5. Software Design           5 days    16-20 November 2019        50            1000      50              25\n");
					viewsoftdes();
				}
				else
				{
					printf("\nPlease enter a valid number: ");
				}

			} while (nov < 1 || nov > 2);
		}
		else if (month == 3)
		{
			do {
				printf("\nPlease pick a day\n");
				printf("1. 9-11 December\n2. 11-13 December\n3. 15-19 December\n4. 5-9 December\n5. 23-25 December\n");
				scanf("%d", &dec);
				if (dec == 1)
				{
					printf("\n  SOFT SKILLS                 DAY            DATE              ADMIN FEE        FEE   MEAL(VEGAN)  MEAL(NON-VEGAN)\n");
					printf("2. Communications            3 days     9-11 December 2019        50            650       50              25\n");
					viewcomm();
				}
				else if (dec == 2)
				{
					printf("\n  SOFT SKILLS                 DAY            DATE              ADMIN FEE        FEE   MEAL(VEGAN)  MEAL(NON-VEGAN)\n");
					printf("1. Team building             3 days    11-13 December 2019        50            800       75              50\n");
					viewteambuilding();
				}
				else if (dec == 3)
				{
					printf("\n  SOFT SKILLS                 DAY            DATE              ADMIN FEE        FEE   MEAL(VEGAN)  MEAL(NON-VEGAN)\n");
					printf("4. Conflict Management       5 days    15-19 December 2019        50            600       50              25\n");
					viewconflictmanage();
				}

				else if (dec == 4)
				{
					printf("\n  COMPUTING SKILLS            DAY            DATE              ADMIN FEE        FEE   MEAL(VEGAN)  MEAL(NON-VEGAN)\n");
					printf("8. Mobile Content Design     5 day     5-9 December 2019          50            1200      75              50\n");
					printf("   and Development\n");
					viewmobdesdev();
				}
				else if (dec == 5)
				{
					printf("\n  COMPUTING SKILLS            DAY            DATE              ADMIN FEE        FEE   MEAL(VEGAN)  MEAL(NON-VEGAN)\n");
					printf("7. Cloud Computing           3 days    23-25 December 2019        50            1300      50              25\n");
					viewcloudcomp();
				}
				else
				{
					printf("\nPlease enter a valid number: ");
				}
			} while (dec < 1 || dec > 5);
		}
		else
		{
			printf("\nPlease enter a valid number: ");
		}
	} while (month < 1 || month> 3);

	do {
		printf("\nPress 1 to find another course\nPress 2 for main menu\n");
		scanf("%d", &findmenu);

		if (findmenu == 1)
		{
			finddate();// find another course
		}
		else if (findmenu == 2)
		{
			main();// go to menu
		}
		else
		{
			printf("\nPlease enter a valid number\n");
		}
	} while (findmenu < 1 || findmenu > 2);
}
void rangeteambuild() //subtract a course if the booking has been made
{
	fp = fopen("TeamBuilding.txt", "r");
	if (fp == NULL)
	{
		printf("Unable to open the file\n");
	}
	else
	{
		fscanf(fp, "%d", &capacity);
		capacity = capacity - 1;
		fprintf(fp, "%d", capacity);
	}
	teambuildleft();
}
void teambuildleft() // storing in text file of the number of available slot
{
	fp = fopen("TeamBuilding.txt", "w");
	fprintf(fp, "%d", capacity);
}
void viewteambuilding()// view the availability of the course
{
	fp = fopen("TeamBuilding.txt", "r");
	if (fp == NULL)
	{
		printf("Unable to open the file\n");
	}
	else
	{
		fscanf(fp, "%d", &capacity);
		printf("\t\t\t\t\t============================");
		printf("\n\t\t\t\t\t       %d SLOT(S) LEFT", capacity);
		printf("\n\t\t\t\t\t============================");
	}
}
void rangecomm()
{
	fp = fopen("Communications.txt", "r");
	if (fp == NULL)
	{
		printf("Unable to open the file\n");
	}
	else
	{
		fscanf(fp, "%d", &capacity1);
		capacity1 = capacity1 - 1;
		fprintf(fp, "%d", capacity1);
	}
	commleft();
}
void commleft()
{
	fp = fopen("Communications.txt", "w");
	fprintf(fp, "%d", capacity1);
}
void viewcomm()
{
	fp = fopen("Communications.txt", "r");
	if (fp == NULL)
	{
		printf("Unable to open the file\n");
	}
	else
	{
		fscanf(fp, "%d", &capacity1);
		printf("\t\t\t\t\t============================");
		printf("\n\t\t\t\t\t       %d SLOT(S) LEFT", capacity1);
		printf("\n\t\t\t\t\t============================");
	}
}

void rangecorpcargrow()
{
	fp = fopen("CorporateCareerGrowth.txt", "r");
	if (fp == NULL)
	{
		printf("Unable to open the file\n");
	}
	else
	{
		fscanf(fp, "%d", &capacity2);
		capacity2 = capacity2 - 1;
		fprintf(fp, "%d", capacity2);
	}
	corpcargrowleft();
}
void corpcargrowleft()
{
	fp = fopen("CorporateCareerGrowth.txt", "w");
	fprintf(fp, "%d", capacity2);
}
void viewcorpcargrow()
{
	fp = fopen("CorporateCareerGrowth.txt", "r");
	if (fp == NULL)
	{
		printf("Unable to open the file\n");
	}
	else
	{
		fscanf(fp, "%d", &capacity2);
		printf("\t\t\t\t\t============================");
		printf("\n\t\t\t\t\t       %d SLOT(S) LEFT", capacity2);
		printf("\n\t\t\t\t\t============================");
	}
}

void rangeconflictmanage()
{
	fp = fopen("ConflictManagement.txt", "r");
	if (fp == NULL)
	{
		printf("Unable to open the file\n");
	}
	else
	{
		fscanf(fp, "%d", &capacity3);
		capacity3 = capacity3 - 1;
		fprintf(fp, "%d", capacity3);
	}
	conflictmanageleft();
}
void conflictmanageleft()
{
	fp = fopen("ConflictManagement.txt", "w");
	fprintf(fp, "%d", capacity3);
}
void viewconflictmanage()
{
	fp = fopen("ConflictManagement.txt", "r");
	if (fp == NULL)
	{
		printf("Unable to open the file\n");
	}
	else
	{
		fscanf(fp, "%d", &capacity3);
		printf("\t\t\t\t\t============================");
		printf("\n\t\t\t\t\t       %d SLOT(S) LEFT", capacity3);
		printf("\n\t\t\t\t\t============================");
	}
}

void rangesoftdes()
{
	fp = fopen("SoftwareDesign.txt", "r");
	if (fp == NULL)
	{
		printf("Unable to open the file\n");
	}
	else
	{
		fscanf(fp, "%d", &capacity4);
		capacity4 = capacity4 - 1;
		fprintf(fp, "%d", capacity4);
	}
	softdesleft();
}
void softdesleft()
{
	fp = fopen("SoftwareDesign.txt", "w");
	fprintf(fp, "%d", capacity4);
}
void viewsoftdes()
{
	fp = fopen("SoftwareDesign.txt", "r");
	if (fp == NULL)
	{
		printf("Unable to open the file\n");
	}
	else
	{
		fscanf(fp, "%d", &capacity4);
		printf("\t\t\t\t\t============================");
		printf("\n\t\t\t\t\t       %d SLOT(S) LEFT", capacity4);
		printf("\n\t\t\t\t\t============================");
	}
}

void rangewebdevelop()
{
	fp = fopen("WebDevelopment.txt", "r");
	if (fp == NULL)
	{
		printf("Unable to open the file\n");
	}
	else
	{
		fscanf(fp, "%d", &capacity5);
		capacity5 = capacity5 - 1;
		fprintf(fp, "%d", capacity5);
	}
	webdevelopleft();
}
void webdevelopleft()
{
	fp = fopen("WebDevelopment.txt", "w");
	fprintf(fp, "%d", capacity5);
}
void viewwebdevelop()
{
	fp = fopen("WebDevelopment.txt", "r");
	if (fp == NULL)
	{
		printf("Unable to open the file\n");
	}
	else
	{
		fscanf(fp, "%d", &capacity5);
		printf("\t\t\t\t\t============================");
		printf("\n\t\t\t\t\t       %d SLOT(S) LEFT", capacity5);
		printf("\n\t\t\t\t\t============================");
	}
}

void rangecloudcomp()
{
	fp = fopen("CloudComputing.txt", "r");
	if (fp == NULL)
	{
		printf("Unable to open the file\n");
	}
	else
	{
		fscanf(fp, "%d", &capacity6);
		capacity6 = capacity6 - 1;
		fprintf(fp, "%d", capacity6);
	}
	cloudcompleft();
}
void cloudcompleft()
{
	fp = fopen("CloudComputing.txt", "w");
	fprintf(fp, "%d", capacity6);
}
void viewcloudcomp()
{
	fp = fopen("CloudComputing.txt", "r");
	if (fp == NULL)
	{
		printf("Unable to open the file\n");
	}
	else
	{
		fscanf(fp, "%d", &capacity6);
		printf("\t\t\t\t\t============================");
		printf("\n\t\t\t\t\t       %d SLOT(S) LEFT", capacity6);
		printf("\n\t\t\t\t\t============================");
	}
}
void rangemobdesdev()
{
	fp = fopen("MobileContentDesignDevelopment.txt", "r");
	if (fp == NULL)
	{
		printf("Unable to open the file\n");
	}
	else
	{
		fscanf(fp, "%d", &capacity7);
		capacity7 = capacity7 - 1;
		fprintf(fp, "%d", capacity7);
	}
	mobdesdevleft();
}
void mobdesdevleft()
{
	fp = fopen("MobileContentDesignDevelopment.txt", "w");
	fprintf(fp, "%d", capacity7);
}
void viewmobdesdev()
{
	fp = fopen("MobileContentDesignDevelopment.txt", "r");
	if (fp == NULL)
	{
		printf("Unable to open the file\n");
	}
	else
	{
		fscanf(fp, "%d", &capacity7);
		printf("\t\t\t\t\t============================");
		printf("\n\t\t\t\t\t       %d SLOT(S) LEFT", capacity7);
		printf("\n\t\t\t\t\t============================");
	}
}





