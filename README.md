# memory-game
# It is a memory game where you show a string of numbers and memorize and input the numbers! If you succeed 2 times, the number string displayed will increase one by one, and you have to enter the numbers by jumping with a space when entering them! 숫자열을 보여주고 그 숫자를 기억해서 입력하는 메모리 게임이다! 2회 성공하면 보여주는 숫자열이 하나씩 늘어나고 입력할때 숫자들을 스페이스로 뛰어서 입력해야 한다!
# c program
#include <stdio.h>
#include <ctype.h>
#include <stdlib.h>
#include <time.h>
#define TRUE 1
#define FALSE 0
int main(void){
	char game='Y';
	int correct=TRUE;
	int counter=0;
	int sl=0;
	int i=0;
	long seed=0; //초깃값  
	int number=0;
	long now=0;
	long time_t=0;
	printf("기억력게임입니다!");
	printf("화면에 보이는 숫자를 입력해주세요!\n 행운을 빌어요^^");
	scanf("%c",&game);
	do{
		correct=TRUE;
		counter=0;
	    sl=2;
	    time_t=clock();
	    while(correct){
	    	sl+=counter++%2==0; //2회 성공할때마다 숫자열을 한자리 증가시킴  
	    	seed=time(NULL);
	    	now=clock(); //숫자열 보여주기 시작한 시간 기록  
	    	srand((int)seed); //임의의 숫자열 초기화  
	    	for(i=1;i<=sl;i++){
	    		printf("%d",rand()%10);
			}
			for(;clock()-now<CLOCKS_PER_SEC;);
			printf("\r"); //해의 맨처음으로 이동  
			for(i=1;i<=sl;i++){
				printf(" ");
			}
			if(counter==1){
				printf("\n반드시 스페이스바로 구분해서 숫자쓰기\n");
			}
			else{
				printf("\r");
			}
			srand((int)seed);
			for(i=1;i<=sl;i++){
				scanf("%d",&number);
				if(number!=rand()%10){
					correct=FALSE;
					break;
				}
			}
			printf("%s\n",correct?"맞다!":"틀리다!");
		}
	time_t=(clock()-time_t)/CLOCKS_PER_SEC;
	printf("\n\n%d점 획득",--counter*100/time_t);
  fflush(stdin);
	printf("\n다시도전하시겠습니까?(y/n)");
	scanf("%c",&game); //fflush(stdin)이 있어야 입력 0 -->입력버퍼를 지움
}while(toupper(game)=='Y'); //toupper()는 소문자를 대문자로 변경  
}
#result--> 기억력게임입니다!  화면에 보이는 숫자를 입력해주세요! 행운을 빌어요^^ 반드시 스페이스바로 구분해서 숫자쓰기 6 9 2
맞다!  3 5 7 맞다! 6 0 9 7 맞다! 5 5 0 5 맞다! 2 1 7 0 3 맞다! 5 3 2 5 9 틀리다!    15점 획득! 다시도전하시겠습니까?(y/n) 
