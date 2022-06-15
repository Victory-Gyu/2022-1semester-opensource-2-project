#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#pragma warning(disable:4996)


#define SIZE   30
#define SAFE_FREE(p) if(p) { free(p); p=NULL; }



typedef struct
{
    char date[30];		// 날짜
    char yesno[30];		// 헬스 유무
    int kg;   // 몸무게
    int bmi;  // bmi
    char body[30];		// 분할 부위
} work; // struct 선언


void menu_print();
void manual();
void insert(work* ptr, int* location);
void healthlist(work* ptr, int* location);


int main(void)
{
    int menu, index = 0;
    char* name = (char*)malloc(sizeof(char) * SIZE);         // 이름 동적 메모리 할당



     // struct동적 메모리 할당
    work* ptr = (char*)malloc(sizeof(work) * SIZE);



    while (1)
    {
        menu_print();
        scanf("%d", &menu);



        switch (menu) // 
        {
        case 0: manual(ptr, &index);  break;
        case 1: insert(ptr, &index);  break;
        case 2: healthlist(ptr, &index);   break;
        case 3: printf("종료합니다.\n\n");    exit(0);
        default: printf("잘못된 입력입니다.\n\n");  break;
        }
    }

    FILE* stream; //파일 포인터를 선언한다.

    stream = fopen("test.txt", "w"); //test.txt를 쓰기용으로 연다.

    fprintf(stream, healthlist);

    fclose(stream); //파일을 닫는다.

    return 0;


    SAFE_FREE(name); // 동적 메모리 해제
    SAFE_FREE(ptr);  // 동적 메모리 해제



    return 0;
}



void menu_print() // 메뉴 출력
{
    printf("\n<몸짱되기 프로젝트 6월버전>\n");
    printf("0. 프로그램 설명 \n");
    printf("1. 정보 입력 \n");
    printf("2. 목록 출력 \n");
    printf("3. 종료 \n");
    printf("번호를 입력하시오: ");
}
void manual()
{
    printf("<<이 프로그램은 헬스를 꾸준히 하기 위해서 만든 프로그램이다.\n");
    printf("헬스를 한 횟수를 시각적으로 확인하여 자극을 받을 수 있다.\n");
    printf("골고루 분할운동을 하고 있는지 확인할 수도 있다.\n이 프로그램은 달마다 갱신된다.지금 버전은 2022 06월 버전이다.\n");
    printf("열심히해서 몸짱되자!\n\n");
}



void insert(work* ptr, int* location) // 데이터 삽입
{
    printf("추가할 정보를 입력하세요\n");

    if (*location < SIZE)
    {
        printf(" 날짜(일): "); scanf(" %s", &ptr[*location].date);
        printf(" 헬스유무(o/x) : "); scanf("%s", &ptr[*location].yesno);      
        printf(" 몸무게 : "); scanf(" %d", &ptr[*location].kg);
        printf(" 분할부위(A:가슴,B:하체,C:등) : "); scanf(" %s", &ptr[*location].body);

        (*location)++;
    }

}





 

void healthlist(work* ptr, int* location) // 데이터 리스트 출력
{


    if (*location > 0)
    {
        printf("                 < 2022 6월 운동일지>\n");
        printf("----------------------------------------------------\n");
        printf(" 날짜(일)   헬스 유무  몸무게(kg)    분할 부위(A:가슴,B:하체,C:등)   \n");
        printf("----------------------------------------------------\n");

        for (int i = 0; i < (*location); ++i)
        {
            printf(" %s      %5s         %5d             %5s \n", ptr[i].date, ptr[i].yesno, ptr[i].kg, ptr[i].body);

        }
        int count = 0;
        int countA = 0;
        int countB = 0;
        int countC = 0;
        for (int i = 0; i < (*location); ++i) {
            if (*ptr[i].yesno == 'o')
            {
                count += 1;
            }

            if (*ptr[i].body == 'A')
            {
                countA += 1;
            }
            else if (*ptr[i].body == 'B')
            {
                countB += 1;
            }
            else if (*ptr[i].body == 'C')
            {
                countC += 1;
            }
           
        }
        printf("<2022.06.%d기준>\n", *location);
        printf("헬스장에 간 횟수: %d\n", count);
        printf("가슴 횟수: %d\n", countA);
        printf("하체 횟수: %d\n", countB);
        printf("등 횟수: %d\n", countC);
    }
}
