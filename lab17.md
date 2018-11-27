# 排序算法 

- [排序算法](#排序算法)
    - [排序](#排序)            
		- [冒泡排序](#冒泡排序)            
		- [鸡尾酒排序](#鸡尾酒排序)            
		- [选择排序](#选择排序)            
		- [插入排序](#插入排序)            
		- [快速排序](#快速排序)            
		- [梳排序](#梳排序)            
		- [希尔排序](#希尔排序)            
		- [归并排序](#归并排序)            
		- [桶排序](#桶排序)            
		- [计数排序](#计数排序)            
		- [基数排序](#基数排序)            
		- [堆排序](#堆排序)            
		- [猴子排序](#猴子排序)    
	- [引用](#引用)

## 排序



#### 冒泡排序  
![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fxk941h3pyg307s06ldhe.jpg)  

这张动态图简洁的表示了什么是冒泡排序。  

冒泡排序是龟速三巨头之首，核心是“冒泡”，通过每个元素与其他剩余元素的比较，依次把最小的元素冒出来，达到排序的目的。  

冒牌排序运用两个for循环实现了整个排序过程。  

第一个for循环：控制排序轮数。  
第二个for循环：控制每一轮比较的每一个步骤。  

代码：（懒得一个符号一个符号的敲，附上一个知乎大佬的[帖子链接][1]）  

#### 鸡尾酒排序  

鸡尾酒排序就是对冒泡排序的一个改进。  
它与冒牌排序之间的区别在于冒泡排序只从前面向后一个个比交，而鸡尾酒排序可以还会从后往前一个个比较。  
鸡尾酒排序会得到比冒泡排序好一点点的性能，假如是一个随机的数串，鸡尾酒排序可能比冒泡排序好不到哪里去。  

加一张动图：
[鸡尾酒排序动图](https://baike.baidu.com/pic/%E9%B8%A1%E5%B0%BE%E9%85%92%E6%8E%92%E5%BA%8F/7515196/0/79f0f736afc3793166033f22eac4b74543a91155)  

看了上面那个动图之后，那个红色的条条从左到右，从右到左。而在冒泡排序中，这个条条只会从左到右。  

代码的话，还是给个链接（[鸡尾酒排序算法解析与代码](https://zhuanlan.zhihu.com/p/42870222)）  

#### 选择排序  
现在轮到龟速三巨头第二的选择排序登场了。  
选择排序其实个人感觉和冒牌排序差不多。  
冒牌排序是比大小，比一次数字换一次位置。选择排序是比大小，一直比，把需要提到前面的数字记录下来，比完一轮，到最后再换位置，一轮只换一次位置。   
给张形象的动图： 
![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fxk9v4yoxpg30800800st.jpg)

和冒牌排序的比一下你就会发现，冒泡排序的点是一点点的滑到中间的，选择排序的是直接消失跳到中间。  

#### 插入排序  
先把龟速三巨头最后一个——插入排序说了吧。  

插入排序就是在插入啊.....   

插入排序首先要把第一个元素当作排序后的一个数组。假如第二个元素大于第一个，那么就保持不动（从小到大），假如第二个元素小，就移到前面去。这样两个元素就再次形成了一个有序数组。以此类推，无限循环。  
给张动态图：![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fxka5bbgzyg307s06lq5y.jpg)  

看图中的点，是不是每个元素都找到了自己应该在的位置后逐渐合在一起形成了一条线。这就是他们的插入。   

代码：  

    void insert_sort(int *array,unsigned int n)
    {
        int i,j;
        int temp;

        for(i=1;i<n;i++)
        {
            temp=*(array+i);
            for(j=i;j>0&&*(array+j-1)>temp;j--)
            {
                 *(array+j)=*(array+j-1);
            }
            *(array+j)=temp;
        }
    }


#### 快速排序  
讲完了龟速三巨头，我们讲点快的————快速排序。  

快速排序是一个什么样的算法呢？很简单的，是一个听起来就很快的算法，也确实快。  

快速排序利用了递归的算法，二分的思想。  
快速排序就是把一个元素作为基准，把比它大的，比它小的，分成两个序列。在两个序列中做相同操作，直到完成排序。  

举个栗子：
让我们来假设一下，有这样一个序列：  
3 1 4 5 2  
我们怎么让它来排序呢？  
首先，我们把2放到中间，把比它大的3 4 5分到后面的序列，把比它小的1放到前面的序列.3 4 5继续执行这个操作，4为基准，3和5就分开了。

如果对于这个过程大家理解不了， 那我用一下知乎大佬的图片吧：  
![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fxkalfhq8fj30o00d6my8.jpg)  

总的来说，快速排序只有三步：  
1.在这个序列中取一个数a（这里我们取序列最后的一个元素值作为a）  
2.将序列分为比a大的部分和比a小的部分以及元素a  
3.循环进行1.2两个步骤直到序列中的元素个数为1  

动图一张：  
![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fxkanlx2ryg307s05ytay.jpg)    

（看得懂吗？看不懂没关系，看懂就好了。要是实在看不懂也没事，反正我看懂了）

代码：  

    #include <stdio.h>

    int Partition(int *a, int begin, int end)
    {
	    int f = a[end];	//获得中间值 
	    int num_min_f = begin-1;	//小于中间值的数目，数组的下标从0计算，所以这里取-1
	    int i; 
	    for(i = begin; i<=end; i++)
        {
		    if(a[i] < f)
            {
			    //捕捉到一个小于f的值
			    num_min_f++;
			    //交换 
			    int temp;
			    temp = a[i];
			    a[i] = a[num_min_f];
			    a[num_min_f] = temp;
		    }
	    } 

	    //这样前num_min_f个树都比f小[0,num_min_f-1]
	    num_min_f++;
	    //a[num_min_f]的值设为中间值 
	    a[end] = a[num_min_f];
	    a[num_min_f] = f;
	    //坐标小于num_min_f的值小于等于中间值，大于num_min_f的值大于中间值 
	    return num_min_f;
    }
    //快速排序 
    void quickSort(int *a, int begin, int end)
    {
	    if(begin <= end)
        {
		    //将原序列分为比a小的序列，a，比a大的序列 
		    int mid = Partition(a, begin, end);	//获得中间值a的位置 
		    quickSort(a, begin, mid-1);	//前一半
		    quickSort(a, mid+1, end);  //后一半 
	    }
    }

    int main()
    {
	    int a[10] = {2, 5, 4, 3, 1, 15, 3, 35, 21, 12};
	    quickSort(a, 0, 9);
	    int i;
	    for(i = 0; i < 10; i++)
        {
	    	printf("%d ", a[i]);
	    }
	    return 0;
    } 

比较复杂，看不懂我说的也可以去看[知乎大佬——超爱学习的帖子](https://zhuanlan.zhihu.com/p/46238008
)反正我也是看了他的才会这个。  

#### 梳排序  

我觉得我还可以说个梳排序。  
梳排序是改良自冒泡排序和插入排序的一种算法。

简单的来说，冒泡排序是相邻两项比较最后得到最小的往前冒泡。而梳排序不是相邻两项，相比较的两项之间的项数逐渐减小，直到减为1，之后减为1的时候相当于一轮冒泡排序。  

经过发明者精密的计算，每次间隔递减1.3是最合理的。1.3叫做递减率。 
假如不明白什么是递减率，我给个[梳排序递减率](https://blog.csdn.net/u010647471/article/details/50170825)的链接，大家自己看，绝对能懂。  

动图在你看了递减率后特别容易明白，也会加深你对梳排序的理解：  
![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fxkb7us1avg307h0757pw.jpg)  

代码：

	void comb_sort(int* data, int n)
	{
		const double shrink = 1.25;
		int i, delta = n, noswap = 0;
		while(!noswap)
		{
			for(noswap = 1, i = 0; i + delta < n; i++)
				if(data[i] > data[i + delta])
				{
					data[i] ^= data[i + delta];
					data[i + delta] ^= data[i];
					data[i] ^= data[i + delta];
					noswap = 0;
				}

			if(delta > 1)
			{
				delta /= shrink;
				noswap = 0;
			}
		}
	}  

（代码可能不好懂，原理还是容易明白的，你可以看明白原理自己写代码）  

#### 希尔排序  
梳排序和希尔排序有个共同点，就是对增量进行缩减，所以我们现在来说希尔排序。  

希尔排序是对插入排序的一个极大优化。

插入排序最大的缺点在哪里？每次只能把数据前进一位。但它也有一个巨大的有点，就是把元素线性排列，有序性很高。  

希尔排序继承了插入排序的优点，抛弃了它的缺点。它是怎么实现的呢？

对于一组无序的数组：
首先，希尔排序对元素进行分组（假设元素有n个），希尔排序会首先分成n/2组，这样每组只有两个元素。因为是无序的，元素需要插入，但是每组元素个数少，因此插入时移动的位置少。等到元素个数多的时候，数组经过之前的排序，有序性增加，所以移动的位置也不会很多。这样就克服了插入排序的缺点，得到很好的效率提升。  

从直观上看希尔排序：  
就是把数列进行分组(不停使用插入排序)，直至从宏观上看起来有序，最后插入排序起来就容易了(无须多次移位或交换)。  

然后就是增量的问题：增量记为d=n/2，每轮都会用d/2，当d=1时结束.（比如n=9，第一次4，第二次2，第三次1）  

给个例子吧：  
现在我们有一个数组，该数组有6个元素  
int[] arrays = {2, 5, 1, 3, 4, 6};  
排序前：  
将该数组看成三个（arrays.length/2)数组，分别是:{2,3},{5,4},{1,6}  
第一趟排序：  
对三个数组分别进行**插入排序**，因此我们三个数组得到的结果为{2,3},{4,5},{1,6}  
此时数组是这样子的：{2, 4, 1, 3, 5, 6}  
第二趟排序：  
增量减少了，上面增量是3，此时增量应该为1了，因此把{2, 4, 1, 3, 5, 6}看成一个数组(从宏观上是有序的了)，对其进行**插入排序**  

ps：每一次都是插入排序

附动图两张：  
这张很帅，但是达不到我想要的效果，我是没咋看懂。好像是哪个变成黄色的就和前面的比较吧。  
![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fxkdd110uug307p09kgsu.jpg)  

附一张我能看懂的  
![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fxkdf0yws1g30ih0821kx.jpg)  

代码，也给两个吧：  
第一个是易于理解的（可以直接看第二个，假如理解就不用管这个）

	#include <stdio.h>
	#include <math.h>

	#define MAXNUM 10
 
	void main()
	{
    	void shellSort(int array[],int n,int t);//t为排序趟数
    	int array[MAXNUM],i;
    	for(i=0;i<MAXNUM;i++)
        scanf("%d",&array[i]);
    	shellSort(array,MAXNUM,(int)(log(MAXNUM+1)/log(2)));//排序趟数应为log2(n+1)的整数部分
    	for(i=0;i<MAXNUM;i++)
       		printf("%d ",array[i]);
    	printf("\n");
	}
 
	//根据当前增量进行插入排序
	void shellInsert(int array[],int n,int dk)
	{
    	int i,j,temp;
    	for(i=dk;i<n;i++)//分别向每组的有序区域插入
    	{
        	temp=array[i];
        	for(j=i-dk;(j>=i%dk)&&array[j]>temp;j-=dk)//比较与记录后移同时进行
            	array[j+dk]=array[j];
        	if(j!=i-dk)
            	array[j+dk]=temp;//插入
    	}
	}
 
	//计算Hibbard增量
	int dkHibbard(int t,int k)
	{
   		return (int)(pow(2,t-k+1)-1);
	}
 
	//希尔排序
	void shellSort(int array[],int n,int t)
	{
    	void shellInsert(int array[],int n,int dk);
    	int i;
    	for(i=1;i<=t;i++)
        	shellInsert(array,n,dkHibbard(t,i));
	}
 
	//此写法便于理解，实际应用时应将上述三个函数写成一个函数。

第二个是我们平常写题用的（方便的很）  

	void shellSort(int[] arrays) 
	{
        //增量每次都/2
        for (int step = arrays.length / 2; step > 0; step /= 2) 
		{
            //从增量那组开始进行插入排序，直至完毕
            for (int i = step; i < arrays.length; i++) 
			{

                int j = i;
                int temp = arrays[j];

                // j - step 就是代表与它同组隔壁的元素
                while (j - step >= 0 && arrays[j - step] > temp) 
				{
                    arrays[j] = arrays[j - step];
                    j = j - step;
                }
                arrays[j] = temp;
            }
        }
    } 

《c程序设计语言》上也有一个希尔排序的代码：

	（这可是我一个符号一个符号打出来的）
	void shellsort(int v[],int n)
	{
		int gap,i,j,temp;

		for(gap=n/2;gap>0;gap/=2)
			for(i=gap;i<n;i++)
				for(j=i-gap;j>=0 && v[j]>v[j+gap]; j-=gap)
				{
					temp=v[j];
					v[j]=v[j+gap];
					v[j+gap]=temp;
				}
	}

#### 归并排序  
归并排序也运用了递归，和快速排序有那么一丢丢的差不多。说一下吧。  

归并排序使用了分治法，很简单：  
把长度为n的输入序列分成两个长度为n/2的子序列；  
对这两个子序列分别采用归并排序；  
将两个排序好的子序列合并成一个最终的排序序列。   

看起来理解不了，其实只需要一个动态图：
![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fxkdsy1jvhg30mj0e1qcv.jpg)  

宏观看一下效果：  
![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fxkdux5mthg307s06l0st.jpg)  

懂了吗？不懂还有静态图：![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fxke3zkjfuj30fe07c0t6.jpg)  



然后再给个代码：

归并排序的代码：  

	void Msort(int *a, int begin, int end)
	{
 		if(end > begin)
		{ //序列中元素数目大于1
 		//二分序列，时间复杂度为O(logn) 
 		int mid = (begin+end)/2; //取中间值 
 		Msort(a, begin, mid); //对前一半递归排序 
 		Msort(a, mid+1, end); //对后一半递归排序 
 		Merge(a, begin, mid, end); //将两个排序好的序列合并成为一个有序的序列 
 		}
	}

合并两个有序序列代码：  

	void Merge(int *a, int begin, int mid, int end)
	{
		 //申请临时空间 
 		int *b = (int *)malloc(sizeof(int)*(end - begin + 1)); 
 		int i,j;

 		//赋值 
 		for(i = begin, j = 0; i<=end; i++, j++)
		{
 			b[j] = a[i];
 		}

 		 //合并两个有序链表，时间复杂度为O(n) 
 		 int k = begin;
 		 for(i=begin, j=mid+1; i<=mid&&j<=end; )
		 {
			if(b[i-begin] <= b[j-begin])
			{
 				a[k++] = b[i-begin];//b[0]=a[begin]
				i++;
			}
			else
			{
				a[k++] = b[j-begin];
				j++;
			}
		 }

 		 //这两个只会执行其中一个，因为只有一个序列没有被完全遍历 
 		 while(i <= mid)
		 { 
 			a[k++] = b[i-begin];
 			i++;
 		 }
 		 while(j <= end)
		 {
 			a[k++] = b[j-begin];
 			j++;
 		 } 

 		 //释放临时空间 
 		 free(b); 
	}


最后的整体代码：  

	#include <stdio.h>
	#include <stdlib.h>
	#include <malloc.h>
	void Merge(int *a, int begin, int mid, int end)
	{
 		//申请临时空间 
 		int *b = (int *)malloc(sizeof(int)*(end - begin + 1)); 
 		int i,j;
 		//赋值 
 		for(i = begin, j = 0; i<=end; i++, j++)
		{
 			b[j] = a[i];
 		}

 		//合并两个有序链表，时间复杂度为O(n) 
		int k = begin;
 		for(i=begin, j=mid+1; i<=mid&&j<=end; )
		{
 			if(b[i-begin] <= b[j-begin])
			{
 				a[k++] = b[i-begin];
 				i++;
 			}
			else
			{
 				a[k++] = b[j-begin];
 				j++;
 			}
 		}

 		//这两个只会执行其中一个，因为只有一个序列没有被完全遍历 
 		while(i <= mid)
		{ 
 			a[k++] = b[i-begin];
 			i++;
 		}
 		while(j <= end)
		{
 		a[k++] = b[j-begin];
 		j++;
 		} 

 		//释放临时空间 
 		free(b); 
	}

	void Msort(int *a, int begin, int end)
	{
 		if(end > begin)
		{
 			//二分序列，时间复杂度为O(logn) 
 			int mid = (begin+end)/2; //取中间值 
 			Msort(a, begin, mid); //对前一半递归排序 
 			Msort(a, mid+1, end); //对后一半递归排序 
 			Merge(a, begin, mid, end); //将两个排序好的序列合并成为一个有序的序列 
 		}
	}
 
	int main()
	{
 		int a[10] = {2, 5, 4, 3, 1, 15, 3, 35, 21, 12};
 		Msort(a, 0, 9);
 		int i;
 		for(i = 0; i < 10; i++)
		{
 			printf("%d ", a[i]);
 		}
		return 0;
	}  


记住这串代码，你就学会并且理解了归并排序。  

嫌我说的不清楚的，请拜读这位[知乎大佬的帖子](https://zhuanlan.zhihu.com/p/46438037),不过这次我不是看了这个才懂得。  

#### 桶排序  

桶排序就比较好理解了，你把数据分类，每一类都是一个桶，然后把数据放到桶里。桶是有一定顺序的，所以只需要把每个桶内的数据都进行排序，再按照桶的顺序进行输出，就可以达到排序的目的。  

总结一下，大致4步：  
设置一个定量的数组当作空桶；  
遍历输入数据，并且把数据一个一个放到对应的桶里去；  
对每个不是空的桶进行排序；  
从不是空的桶里把排好序的数据拼接起来。   

示意图：  
![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fxkeldmhv0j30c308a0ti.jpg)  

代码：  
我没找到太好的代码。这样吧，给一个大佬博客的链接，大家有兴趣直接学习。大佬的代码要事例的，还是自己去看比较好。  
[桶排序初级阶段学习](https://blog.csdn.net/YinhJiang/article/details/80397415
)

#### 计数排序  

在桶排序的基础上，说一下计数排序，这个很简单，但是适用范围比较窄。你可能用过，但是没听说过这个名字。  

比如对一列数进行排序。这列数字有10000个0，10000个3，10000个5，10000个7，10000个9.你会怎么处理？  

假如是我，规定一个数组buf[10]={0}，统计这些数字，出现0，buf[0]++，以此类推。最后再按顺序输出相应数目的0，3，5，7，9.

真的方便。适用于数字数目少，重复次数多的数列。多了就不大好用了。  
不给动图和代码了，简单。 

#### 基数排序  

还有一个和计数排序听起来差不多的排序算法——基数排序。  

直接上动图，一看就懂：![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fxkexec1bag30s40fydky.jpg)  

代码：  
[基数排序代码及讲解](https://zhuanlan.zhihu.com/p/26702524)  
明人不说暗话，这个里面有详细的基数排序代码及讲解。  
基数排序虽然易于理解，但是代码有点长。  

上面那个链接里面还有计数排序与基数排序的比较。 

#### 堆排序  

说实话吧，这个我到现在还没有理解是个什么情况，也写不出来什么道道。。。。。  

这样吧，我先给个我看的[大佬帖子](https://zhuanlan.zhihu.com/p/46680658)  

里面不但有讲解，还有代码，还有图示，特别好。  

但是它没有动图。。。  

恰好我有：
![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fxkf9pyzuvg30f70a4u0x.jpg)  

我还有一张看起来特别酷的：  
![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fxkf90iauxg307s05ydn6.jpg)


#### 猴子排序  

最后说个特别好玩的排序——猴子排序。  
不对，是所有排序算法中的至尊程序，拥有这最低的复杂度。O(N)！它突破了最优复杂度的界限。  

简单的来说，就是随机把无序数组排序，如果正好有序，就结束。

233333333，给个视频自己感受：  

图9就是这个王者算法!(严肃脸):[带有猴子算法的视频的大佬的帖子](https://zhuanlan.zhihu.com/p/38157591
)


来个正常的视频：[算法比较](https://zhuanlan.zhihu.com/p/34421623
)  

## 引用  

引用了很多知乎大佬的帖子，我就不一一说了，侵权歉删。

[1]:https://www.zhihu.com/question/20063815/answer/307255236