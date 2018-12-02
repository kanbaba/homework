1.snake_move.c  

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

    
    