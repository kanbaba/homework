# 智能蛇实验报告

在做完贪吃蛇之后，竟然要做智能蛇。。。  
有那么一点点的难受，不过还好潘老师给出了伪代码。接下来，就开始快乐吧。。

第一步，头文件。  

    #include<stdio.h>
    #include<conio.h>
    #include<stdlib.h>
    #include<time.h>
    #include<math.h>
然后我们需要进行一定的初始化。  

    #define WALL_CELL *
    #define SNAKE_HEAD H
    #define SNAKE_BODY X
    #define SNAKE_FOOD $
    #define SNAKE_MAX_LENGTH 20
    int snake_index = 4;//当前蛇尾数组下标
    int fail = 0;//判断是否失败
    int snake_x[SNAKE_MAX_LENGTH] = {5,4,3,2,1};
    int snake_y[SNAKE_MAX_LENGTH] = {1,1,1,1,1};
    int have_food = 0;//判断是否输出食物
    int distance[4] = {0};
    char movable[4] = {'W','S','A','D'};
    int Fx = 0,Fy = 0;

    //图阵
    char map[12][12] =
    {
    "************",
    "*XXXXH     *",
    "*          *",
    "*      *   *",
    "*          *",
    "*    *     *",
    "*          *",
    "*      *   *",
    "*   *      *",
    "*          *",
    "*          *",
    "************"
    };

根据伪代码，我们要先**输出字符阵**，因此首先写一个函数用来输出字符阵：    
我想给这个函数命名：output  
实现它：

    void output()
    {
        int i,j;

        system("cls");//每次输出，我们都要清屏，因此我们调用system函数

        for(i= 0;i<12;i++)
        {
            for(j=0;j<12;j++)
                printf("%c",map[i][j]);
            printf("\n");
        }
    }

根据伪代码，接下来我们需要写出**游戏结束时的做法**：  
给这个函数命名： gameover  
实现它：  

    void gameover()
    {
        printf("gameover\n");
    }

接下来我们要处理时间，**让蛇每过一段时间自己移动**：  
我们要利用time()函数来实现这个功能:
命名一个函数：dentime
实现它：

    void dentime()
    {
        int start,end;
        
        start=time(NULL);
        end=time(NULL);
        while(end-start<4/snake_index) 
        {
            end=time(NULL);
        }
    }
    
这样的话，到合适的时间就会自己进行下一步。

接下来我们要**找到贪吃蛇向哪里走才是最好的**：
我们命名一个函数：wherego
实现它：

    char wherego()
    {
        int i;
        int count= 4;

        //我们用distance这个数组来记录蛇头位置与食物之间的距离 
        distance[0]=abs(snake_y[0]-1-Fy)+abs(snake_x[0]-Fx);
        distance[1]=abs(snake_y[0]+1-Fy)+abs(snake_x[0]-Fx);
        distance[2]=abs(snake_y[0]-Fy)+abs(snake_x[0]-1-Fx);
        distance[3]=abs(snake_y[0]-Fy)+abs(snake_x[0]+1-Fx);

        while(count--)
        {
            i=min_xiabiao(distance);

            //假如不能移动，我们就换上第二小的方向
            if(!notmove(i))
            {
                distance[i]=9999;
                i=min_xiabiao(distance);
            }
        }

    return movable[i];  
    }

在上述函数中，我们引用了另外两个函数：min_xiabiao和notmove  
min_xiabiao是为了计算distance数组中**距离最近的方向**  
notmove是为了**判断是否能向这个方向走**，假如能，就返回一，加入不能，就返回0  

实现它们：

    int min_xiabiao(int distance[])
    {
        int i=0,temp=9999,j=0;

        for(i=0;i<4;i++)
        {
            if(temp>distance[i] ) 
            {
                temp=distance[i];
                j=i;
            }
        }
    return j;
    }

    int notmove(int i)
    {
        int dx=0,dy=0;

        //根据最小方向，判断蛇头坐标的变化
        if(i==0) 
            dy=-1;
        else if(i==1) 
            dy=1;
        else if(i==2) 
            dx=-1;
        else 
            dx=1;

        //根据蛇头坐标的变化，判断是否能够移动
        if(dy)
        {
            if(map[snake_y[0]+dy][snake_x[0]]=='X') 
                return 0;
            else if(map[snake_y[0]+dy][snake_x[0]]=='*')       
                return 0;
            else 
                return 1;
        }
        else
        {
            if(map[snake_y[0]][snake_x[0]+dx]=='*') 
                return 0;
            else if(map[snake_y[0]][snake_x[0]+dx]=='X')        
                return 0;
            else 
                return 1;
        }
    }

接下来利用贪吃蛇的代码，**让智能蛇移动**：  
我命名一个函数：movesnake  
实现它：  

    void movesnake(int sx , int sy)
    {
        int i,tempx,tempy;
        map[snake_y[snake_index]][snake_x[snake_index]]=' ';
        tempx = snake_x[snake_index];
        tempy = snake_y[snake_index];//记录新生成的尾巴的位置

        for(i=snake_index;i>0;i--)
        {
            snake_x[i] = snake_x[i-1];
            snake_y[i] = snake_y[i-1];
            map[snake_y[i]][snake_x[i]]='X';
        }

        if(sx==0)
        {
            snake_y[0]=snake_y[0]+sy;
        }
        else 
            snake_x[0]=snake_x[0]+sx;

        if(map[snake_y[0]][snake_x[0]]=='$') 
        {
            have_food = 0;
            snake_index++;
            snake_x[snake_index] = tempx;
            snake_y[snake_index] = tempy;
        }

        if(map[snake_y[0]][snake_x[0]]=='*'||map[snake_y[0]][snake_x[0]]=='X') 
            fail = 1;

        map[snake_y[0]][snake_x[0]] = 'H';
    }

我们还要用贪吃蛇中的函数实现**随机产生食物**：  
命名一个函数：put_money
实现它： 

    void put_money()
    {
        int i,j,k;
        int have_food=0;

        while(!have_food)
        {
            for(k=0;k<1000;k++)
            {
                i=rand()%11+1;
                j=rand()%11+1;

                if(map[i][j]==' ') 
                {
                    map[i][j]='$';
                    have_food=1;
                    Fx=j;
                    Fy=i;
                    break;
                }
            }
        }
    }

接下来我们写出主函数：  

    int main()
    {
        char ch;

        output();

        while(1)
        {
            put_money();
            ch=wherego();
            dentime();//我看到过好像可以用空语句延时

            if(ch=='W') 
                movesnake(0,-1);
            else if(ch=='S') 
                movesnake(0,1);
            else if(ch=='A') 
                movesnake(-1,0);
            else if(ch=='D') 
                movesnake(1,0);
            else 
                break;

            if(fail)
            {
                gameover();
                break;
            }
            output();

            if(snake_index==SNAKE_MAX_LENGTH-1) 
            {
                printf("winning!\n");  
                printf("您真棒！\n");
                printf("再来一局吧！\n")；
                break;
            }
        }
    }


ok  
这就是一个神奇的智能蛇！！！