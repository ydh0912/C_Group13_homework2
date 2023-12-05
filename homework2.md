#define _CRT_SECURE_NO_WARNINGS

#include <stdio.h>
#include <string.h>

#define MAX_BOOKS 5
#define MAX_TITLE_LENGTH 50
#define MAX_AUTHOR_LENGTH 30
#define MAX_PRESS_LENGTH 30
#define MAX_PAGE_LENGTH 5
#define MAX_PRICE_LENGTH 30
struct Book {
	char title[MAX_TITLE_LENGTH];
	char author[MAX_AUTHOR_LENGTH];
	char press[MAX_PRESS_LENGTH];
	char page[MAX_PAGE_LENGTH];
	char price[MAX_PRICE_LENGTH];
	char borrowStatus[12];
};

struct Book books[MAX_BOOKS];

void printBookList();
void searchBook();
void borrowBook();
void returnBook();

int main() {
	strcpy(books[0].title, "Truth");
	strcpy(books[0].author, "John");
	strcpy(books[0].press, "Century");
	strcpy(books[0].page, "300");
	strcpy(books[0].price, "20000");
	strcpy(books[0].borrowStatus, "available");

	strcpy(books[1].title, "Love");
	strcpy(books[1].author, "Paul");
	strcpy(books[1].press, "Goods");
	strcpy(books[1].page, "200");
	strcpy(books[1].price, "15000");
	strcpy(books[1].borrowStatus, "available");

	strcpy(books[2].title, "Joy");
	strcpy(books[2].author, "James");
	strcpy(books[2].press, "Cookie");
	strcpy(books[2].page, "250");
	strcpy(books[2].price, "18000");
	strcpy(books[2].borrowStatus, "available");

	strcpy(books[3].title, "Thanks");
	strcpy(books[3].author, "Mark");
	strcpy(books[3].press, "Saejong");
	strcpy(books[3].page, "240");
	strcpy(books[3].price, "21000");
	strcpy(books[3].borrowStatus, "available");

	strcpy(books[4].title, "God");
	strcpy(books[4].author, "Johnson");
	strcpy(books[4].press, "Jungjo");
	strcpy(books[4].page, "450");
	strcpy(books[4].price, "35000");
	strcpy(books[4].borrowStatus, "available");


	int choice;

	do {
		printf("\n[도서목록] [검색] [대출] [반납] [종료]\n");
		printf("메뉴를 선택하세요: ");
		scanf("%d", &choice);

		switch (choice) {
		case 1:
			printBookList();
			break;
		case 2:
			searchBook();
			break;
		case 3:
			borrowBook();
			break;
		case 4:
			returnBook();
			break;
		case 5:
			printf("프로그램을 종료합니다.\n");
			break;
		default:
			printf("잘못된 선택입니다. 다시 선택하세요.\n");
		}

	} while (choice != 5);

	return 0;
}

void printBookList() {
	printf("\nTitle\tAuthors\tPress\tPage\tPrice\tBorrow\n");
	printf("-----\t-------\t-----\t----\t-----\t------\n");

	for (int i = 0; i < MAX_BOOKS; i++) {
		printf("%s\t%s\t%s\t%s\t%s\t%s\n", books[i].title, books[i].author,
			books[i].press, books[i].page, books[i].price, books[i].borrowStatus);
	}
}

void searchBook() {
	char searchTitle[MAX_TITLE_LENGTH];
	int found = 0;

	printf("검색할 도서를 입력하세요: ");
	scanf("%s", searchTitle);

	for (int i = 0; i < MAX_BOOKS; i++) {
		if (_stricmp(books[i].title, searchTitle) == 0) {
			printf("\nTitle\tAuthors\tPress\tPage\tPrice\tBorrow\n");
			printf("-----\t-------\t-----\t----\t-----\t------\n");
			printf("%s\t%s\t%s\t%d\t%d\t%s\n", books[i].title, books[i].author,
				books[i].press, books[i].page, books[i].price, books[i].borrowStatus);
			found = 1;
			break;
		}
	}

	if (!found) {
		printf("해당 도서를 보유하고 있지 않습니다.\n");
	}
}

void borrowBook() {
	char borrowTitle[MAX_TITLE_LENGTH];
	int found = 0;

	printf("대출할 도서를 입력하세요: ");
	scanf("%s", borrowTitle);

	for (int i = 0; i < MAX_BOOKS; i++) {
		if (_stricmp(books[i].title, borrowTitle) == 0) {
			if (_stricmp(books[i].borrowStatus, "available") == 0) {
				printf("대출되었습니다.\n");
				strcpy(books[i].borrowStatus, "borrowing");
			}
			else {
				printf("대출 중이라 대출할 수 없습니다.\n");
			}
			found = 1;
			break;
		}
	}

	if (!found) {
		printf("해당 도서를 보유하고 있지 않습니다.\n");
	}
}

void returnBook() {
	char returnTitle[MAX_TITLE_LENGTH];
	int found = 0;

	printf("반납할 도서를 입력하세요: ");
	scanf("%s", returnTitle);

	for (int i = 0; i < MAX_BOOKS; i++) {
		if (_stricmp(books[i].title, returnTitle) == 0) {
			if (_stricmp(books[i].borrowStatus, "borrowing") == 0) {
				printf("책이 반납되었습니다.\n");
				strcpy(books[i].borrowStatus, "available");
			}
			else {
				printf("대출되지 않은 책입니다.\n");
			}
			found = 1;
			break;
		}
	}

	if (!found) {
		printf("해당 도서를 보유하고 있지 않습니다.\n");
	}
}
