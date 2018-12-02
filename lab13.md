# 贪吃蛇编程

- [贪吃蛇编程](#贪吃蛇编程)  
    - [贪吃蛇全部程序](#贪吃蛇全部程序)  
    - [任务程序](#任务程序)   
        - [1.snake_move.c](#1snake_movec)  
        - [2.snake_eat.c](#2snake_eatc)  

### 贪吃蛇全部程序
    #include <stdio.h>
    #include <stdlib.h>
    #include <time.h>

    #define SNAKE_MAX_LENGTH 20
    #define SNAKE_HEAD 'H'
    #define SNAKE_BODY 'X'
    #define BLANK_CELL ' '
    #define SNAKE_FOOD '$'
    #define WALL_CELL '*'

    void snakeMove(int,int);//移动蛇
    void put_money(void);//放食物 
    void output(void);//输出图形框
    int gameover(void);//判断游戏是否结束

    //初始状态 
	char map[12][13]=
	{"************",
	"*XXXXH     *",
	"*          *",
	"*          *",
	"*          *",
	"*          *",
	"*          *",
	"*          *",
	"*          *",
	"*          *",
	"*          *",
	"************"};

    //初始化蛇身位置（横着是X，竖着是Y） 
	int snakeY[SNAKE_MAX_LENGTH]={5,4,3,2,1};
	int snakeX[SNAKE_MAX_LENGTH]={1,1,1,1,1};
	int snakeLength=5;
    //定义食物的位置 
	int moneyX;
	int moneyY; 
    //添加一个flag，判断食物是否需要一个食物 
	int flag=1; 
	
    int main()
    {
	    printf("欢迎来到贪吃蛇游戏\n");
	    printf("请把输入方式调为英语小写字母形式，方便游戏的进行\n");
	    printf("愉快的开始您的游戏吧！\n"); 
	
	    //打印出原始的图像 
	    output();
	
	    //默认向右移动 
	    char ch='d';
	
	    while(1)
	    {
		    //放下一个食物
		     put_money();
		
		    //根据输入的数据让蛇移动 
		    switch(ch)
		    {
		    	case 'a':
			    	snakeMove(0,-1);
			    	break;
			    case 'w':
			    	snakeMove(-1,0);
			    	break;
			    case 's':
			    	snakeMove(1,0);
			    	break;
			    case 'd':
			    	snakeMove(0,1);
			    	break;
		    }
		
		    //从键盘输入 
		    ch=getchar();
		
		    //判断游戏是否结束
		    int close=gameover(); 
		    if(close)
		    {
			    break;
		    }
	    }
	 
	    return 0;
        } 

    //实现打印图案的函数 
    void output(void)
    {
	    //打印出二维数组 
	    for(int i=0;i<12;i++)
	    {
		    for(int j=0;j<12;j++)
		    {
			    printf("%c",map[i][j]);
		    }
		    printf("\n"); 
	    }
    }

    //实现放食物的函数  
    void put_money(void)
    {
	    //随机产生食物
	    while(flag)
	    {
		    moneyX=rand()%10+1;
		    moneyY=rand()%10+1;
		
		    if(map[moneyX][moneyY]==' ')
		    {
			    flag=0; 
		    }
	    }
	
	    map[moneyX][moneyY]=SNAKE_FOOD;
    } 
 
    //实现移动蛇的函数 
    void snakeMove(int x,int y)
    {
	    //保存蛇最后一块的位置 
	    int tempX,tempY;
	    tempX=snakeX[snakeLength-1];
	    tempY=snakeY[snakeLength-1];
	
	    //重新计算蛇整个身体的位置
	    for(int i=snakeLength-1;i>0;i--)
	    {
		    snakeX[i]=snakeX[i-1];
		    snakeY[i]=snakeY[i-1];
	    } 
	    snakeX[0] += x;
	    snakeY[0] += y;
	
	    //当头出现的位置有食物时 
	    if(snakeX[0]==moneyX&&snakeY[0]==moneyY)
	    {
		    //把flag改成1，意味着食物被吃掉，需要一个新的食物
		    flag=1;
		    snakeLength++;
		    snakeX[snakeLength-1]=tempX;
		    snakeY[snakeLength-1]=tempY;
	    } 
	    //若没有食物 ,把蛇的最后一个位置变成空格 
	    else
	    {
		    map[tempX][tempY]=BLANK_CELL;
	    }
	
	    //把蛇的位置全部变成对应的符号 
	    map[snakeX[0]][snakeY[0]]=SNAKE_HEAD;
	    for(int i=1;i<snakeLength;i++)
	    {
		    map[snakeX[i]][snakeY[i]]=SNAKE_BODY;
	    } 
	
	    //输出图像
	    output(); 
        }

    //实现判断游戏结束的条件 
    int gameover(void)
    {
	    int flag1=0;
	
	    //如果蛇的长度达到20，结束 
	    if(snakeLength==20)
	    {
		    flag1=1;
	    }
	
	    //如果蛇撞到墙，结束 
	    if(snakeX[0]==0||snakeX[0]==12||snakeY[0]==0||snakeY[0]==12)
	    {
		    flag1=1;
	    } 
	
	    //如果蛇撞到自己，结束 
	    for(int i=1;i<snakeLength;i++)
	    {
		    if(snakeX[0]==snakeX[i]&&snakeY[0]==snakeY[i])
		    {
			    flag1=1;
		    }
	    }
	
	    //打印游戏结束 
	    if(flag1)
	    {
		    printf("Game over!!\n");
		    printf("Good Game!!\n");
		    printf("你还要再来一局吗？金主！！\n");
		    return 1;
	    }
	
	    return 0;
    }

### 任务程序
#### 1.snake_move.c  

    //实现移动蛇的函数 
    void snakeMove(int x,int y)
    {
	//保存蛇最后一块的位置 
	int tempX,tempY;
	tempX=snakeX[snakeLength-1];
	tempY=snakeY[snakeLength-1];
	
	//重新计算蛇整个身体的位置
	for(int i=snakeLength-1;i>0;i--)
	{
		snakeX[i]=snakeX[i-1];
		snakeY[i]=snakeY[i-1];
	} 
	snakeX[0] += x;
	snakeY[0] += y;
	
	//当头出现的位置有食物时 
	if(snakeX[0]==moneyX&&snakeY[0]==moneyY)
	{
		//把flag改成1，意味着食物被吃掉，需要一个新的食物
		flag=1;
		snakeLength++;
		snakeX[snakeLength-1]=tempX;
		snakeY[snakeLength-1]=tempY;
	} 
	//若没有食物 ,把蛇的最后一个位置变成空格 
	else
	{
		map[tempX][tempY]=BLANK_CELL;
	}
	
	//把蛇的位置全部变成对应的符号 
	map[snakeX[0]][snakeY[0]]=SNAKE_HEAD;
	for(int i=1;i<snakeLength;i++)
	{
		map[snakeX[i]][snakeY[i]]=SNAKE_BODY;
	} 
	
	//输出图像
	output(); 
    }


#### 2.snake_eat.c

    //实现判断游戏结束的条件 
    int gameover(void)
    {
	int flag1=0;
	
	//如果蛇的长度达到20，结束 
	if(snakeLength==20)
	{
		flag1=1;
	}
	
	//如果蛇撞到墙，结束 
	if(snakeX[0]==0||snakeX[0]==12||snakeY[0]==0||snakeY[0]==12)
	{
		flag1=1;
	} 
	
	//如果蛇撞到自己，结束 
	for(int i=1;i<snakeLength;i++)
	{
		if(snakeX[0]==snakeX[i]&&snakeY[0]==snakeY[i])
		{
			flag1=1;
		}
	}
	
	//打印游戏结束 
	if(flag1)
	{
		printf("Game over!!\n");
		printf("Good Game!!\n");
		printf("你还要再来一局吗？金主！！\n");
		return 1;
	}

