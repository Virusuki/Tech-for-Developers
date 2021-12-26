## C언어 기반 자료구조 & 알고리즘 practics
<br>

###연결리스트를 사용하여 스택의 삽입, 삭제 알고리즘 구현
=============================================================================
- 단일 연결

```
#include <stdio.h>
#include <malloc.h>

typedef struct _node
{
	int key;
	struct _node *next;
} node;

node *head, *tail;

void init_stack(void)
{
	head = (node*)malloc(sizeof(node));
	tail = (node*)malloc(sizeof(node));
	head->next = tail;
	tail->next = tail;
}

void clear_stack(void)
{
	node *t, *s;
	t = head->next;
	while(t != tail)
	{
		s = t;
		t = t->next;
		free(s);
	}
	head->next = tail;
}

int push(int k)
{
	node *t;
	if ((t = (node*)malloc(sizeof(node))) == NULL)
	{
		printf("\n Out of memory...");
		return -1;
	}
	t->key = k;
	t->next = head->next;
	head->next = t;
	return k;
}

int pop(void)
{
	node *t;
	int i;
	if (head->next == tail)
	{
		printf("\n Stack underflow");
		return -1;
	}
	t = head->next;
	i = t->key;
	head->next = t->next;
	free(t);
	return i;
}

void print_stack(void)
{
	node *t;
	t = head->next;
	printf("\n Stack contents : Top ----> Bottom\n");
	while(t != tail)
	{
		printf("%-6d", t->key);
		t = t->next;
	}
}

void main(void)
{
	int i;
	init_stack();
	
	printf("\nPush 5, 4, 7, 8, 2, 1");
	push(5);
	push(4);
	push(7);
	push(8);
	push(2);
	push(1);
	print_stack();
	
	printf("\Pop");
	i = pop();
	print_stack();
	printf("\n popping value is %d", i);
	
	printf("\nPush 3, 2, 5, 7, 2");
	push(3);
	push(2);
	push(5);
	push(7);
	push(2);
	print_stack();
	
	printf("\nPush 3");
	push(3);
	print_stack();
	
	printf("\nInitialize stack");
	clear_stack();
	print_stack();
	
	printf("\nNow stack is empty, pop");
	i = pop();
	print_stack();
	printf("\n popping value is %d", i);
}	
```

- 다음과 같이 결과는 무엇인가?
```
x = 0, y = 1, z = 2;
printf("%d", --x&&--y||--z);   답:  1
printf("%d %d %d", x, y, z);   답: -1 0 1
  
x = 0, y = 1, z = 2;
  
printf("%d", --x||--y&&--z);   답:  1
printf("%d %d %d", x, y, z);   답: -1 1 2
```
<br>
- 다음과 같이 결과는 무엇인가? (garbage)

```
int x;

void main(void)
{
  int x;
  printf("%d", x++);     답: garbage
  func();           답: x = garbage, y = 0
  {
    int x;  
    printf("%d", x++);   답: garbage
    {
      extern int x;   
      printf("%d", x++); 답: 0
    }
    func();         답: x = garbage, y = 1
    printf("%d", x++);   답: x = garbage
  }
}
  
void func(void)
{
  int x;
  static int y;
  printf("%d", x++);
  printf("%d", y++);
}
```


- main의 명령행 매개변수를 이용하여 단어수를 알아내는 함수를 만들기
```
#include <stdio.h>
#include <stdlib.h>
#define IN 1
#define OUT 0

void main(int argc, char *argv[])
{
   
int word_count = 0, state = OUT;
char c;
FILE *fp;
  
if (argc > 1)
{
  if ((fp = fopen(argv[1], "r")) == NULL)
  {
    printf("%s can't open.\n", argv[1]);
    exit(1);
  }
   
  while ((c = fgetc(fp)) != EOF)
  {
     if (c == ' ' || c == '\n' || c == '\t')
     state = OUT;
     else
    {
      state = IN;
      ++word_count;
    }
  }
  printf(" Word number = %d\n", word_count);
  fclose(fp);
  }
  else
  {
   printf("Wrong Input...retry!!!\n");
   exit(1);
  }
}
```

- 한개의 배열을 이용하여 이중 스택을 구현하고 최적의 삽입, 삭제 알고리즘 구현

```
#include <stdio.h>
#include <stdlib.h>
#define MEMORY 10

static int stack[MEMORY];
int top1 = 0;
int top2 = MEMORY-1;

void add(int, int);
int deleted(int);

void main(void)
{
  int result;
  add(1, 10);
  result = deleted(1);
  printf("스택 1에서 빼낸 값 %d \n", result);
  
  add(2, 20);
  result = deleted(2);
  printf("스택2 에서 빼낸 값 %d \n", result);
}

void add(int i, int item)
{
  if (top1 == top2)
  {
    printf("stack full\n");
    exit(1);
  }
  if (i==1)
   stack[top1++] = item;
  else
   stack[top2--] = item;
}

int deleted(int i)
{
  if (i==1)
  {
    if (top1 <= 0)
    {
      printf("stack empty\n");
      exit(1);
    }
   return stack[--top1];
  }  
  else
  {
    if (top2 >= MEMORY-1)
    {
      printf("stack empty\n");
      exit(1);
    }
   return stack[++top2];
  }
}
```

- macro(#define...)

```
#include <stdio.h>
#define SWAP(x,y) {int temp; temp=x; x=y; y=temp;}
void main()
{
  int a, b;
  scanf("%d %d", &a, &b);
  SWAP(a, b);
  printf("a = %d b = %d\n", a, b);
}
```

- 문자열(str)을 float형으로 바꿔주는 함수 myatof(str)를 구현!
예시) "-23.1" ---> -23.1
```
#include <stdio.h>

float myatof(char *);
void main()
{
  char a[10] = "-23.12";
  float result;
  result = myatof(a);
  printf("%lf\n", result);
	
  getch();
}
	
float myatof(char *str)
{
  float i = 1, result = 0;	//결과 값
  int sign = 1	// 부호표시
  char in;
		
  if (*str == '-')	//음수라면 m을 -1로 세팅
  {
    sign = -1;
    str++;
  }
		
  while((in = *str++) != '.' || (in = i) == NULL))	// 소수점 만나기.
    result = (result*10.0) + (in - '0');
    while((in = *str++) != NULL)	// 소수점 이후의 계산.
    {
       i *= 0.1;			// 소수점 이후에는 0.1을 곱한다.
       result = result + (in - '0')*i;
    }
			
    return sign * result;		//부호 계산하여 리턴시킨다.
}

```

