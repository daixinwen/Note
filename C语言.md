[toc]



# 排序算法

## 冒泡排序

依次比较相邻两个数,若前一个数比后一个数大,则交换两个数组,直到最后一个元素,此时最后一个数为最大数;
接着从头开始重复相同的操作,直到倒数第二个元素即次最大数;依次类推,如同水中水泡,依次将最大数浮出水面;
注意:n个元素,要进行n-1次外层循环,每一次内层循环要进行n-1-j次,外层循环控制比较多少次冒泡,内层循环控
制每次冒泡需要进行多少次两两比较;

时间复杂度: O(N 2 ) 稳定性: 稳定

```c
for(i = 0; i < len - 1; i++)
{
    for(j = 0; j < len - 1 - i; j++)
    {
        if(data[j] < data[j + 1])
        {
            tmp = data[j];
            data[j] = data[j + 1];
            data[j + 1] = tmp;
        }
    }
}
```



## 选择排序:

第一个元素依次与后面所有的元素比较,若后面的元素比第一个元素小,则交换位置;
第二个元素依次与后面所有的元素比较,若后面的元素比第二个元素小,则交换位置;
依次类推,直到倒数第二个元素;
注意:只有前n-1个数需要与后面的比较大小

时间复杂度: O(N 2 ) 稳定性: 稳定

```c
for(i = 0; i < len - 1; i++)
{
    for(j = i + 1; j < len; j++)
    {
        if(data[i] < data[j])
        {
            tmp = data[i];
            data[i] = data[j];
            data[j] = tmp;
        }
    }
}
```



## 快速排序

思想:
1第begin个元素作为基准保存到临时变量中;
2第end个元素与基准相比较,大于基准则end--,直到小于基准的元素出现,小于基准则将第end个元素赋值
给第begin个元素;
3第begin个元素与基准相比较,小于基准则begin++,直到大于基准的元素出现,大于基准则将第begin个元
素复制给end;
4当end>=begin的时候,将保存在临时变量中的基准赋值给第begin/end个元素;
以上步骤完成功能,将小于基准的元素放大基准的左边,大于基准的数子放到基准的右边;
用递归的思想分别将左边的元素和右边的元素完成上述的操作。
时间复杂度: O(NlogN)
稳定性: 不稳定

```c
void quick_sort(int* data, int begin, int end)
{
    int tmp = data[begin];
    if(begin >= end)
    {
   	 return;
    }
    while(end > begin)
    {
    	while(data[end] < tmp && end > begin)
        {
       		end--;
        }
    	data[begin] = data[end];
    	while(data[begin] > tmp && end > begin)
        {
   			begin++;
    	}
    	data[end] = data[begin];
    }
    data[begin] = tmp;
    quick_sort(data, 0, begin - 1);
    quick_sort(data, begin + 1, end);
    return;
}
```



## 插入排序

思想:
1选择第一个元素作为一个有序的序列,第二个元素到最后一个元素作为无序序列;
2依次将无序的序列插入到 有序序列的合适的位置中,使之成为一个元素个数加1的有序序列;
对于基本有序或者小规模的数据,效率十分高效
注意:
共有n-1个无序序列,故需要进行n-1次插入;
每次插入时,有序序列个数位i个;
时间复杂度: O(N 2 )
稳定性: 稳定

```c
void insert_sort(int* data, int len)
{
    int i = 0;
    int j = 0;
    int tmp = 0;
    for(i = 1; i < len; i++)
    {
    	tmp = data[i];
    	j = i - 1;
    	while(j >= 0 && tmp < data[j])
    	{
    		data[j + 1] = data[j];
    		j--;
    	}
    	if(j != (i - 1))
    	{
    		data[j + 1] = tmp;
    	}
    }
}
```



## 折半插入排序:

插入排序的基本操作时在一个有序表中进行查找插入的,查找用折半查找来实现,叫做折半插入
排序。折半查找的思想如下:

```c
while(low <= high)
{
    mid = (low + high) / 2;
    if(tmp > data[mid])
    {
    	low = mid + 1;
    }
    else
    {
   		high = mid - 1;
    }
}
```



## 希尔排序:

又称缩小增量排序,属于插入排序类的方法,但是在时间效率上比插入排序有较大的改善。
对于插入排序来说,当n很小或者序列基本有序时,插入排序效率比较高,希尔排序就是从这两
点出发进行改进得到的一种插入排序方法
其基本思想方法:先将待排序列分割成若干个子序列分别进行直接插入排序,待整个序列中的记
录基本有序时,再对全体进行依次直接插入排序。
代码没怎么看懂,难受

```c
void shell_sort(int* data, int len)
{
    int gap = 1;
    int i = 0;
    int j = 0;
    int tmp = 0;
    while (gap < len/4)
    {
    	gap = gap * 4 + 1;
    }
    while (gap > 0)
    {
    	for (i = gap; i < len; i++)
    	{
    		tmp = data[i];
        	j = i - gap;
    		while (j >= 0 && data[j] > tmp)
    		{
    			data[j + gap] = data[j];
    			j -= gap;
    		}
    		data[j + gap] = tmp;
    	}
    	gap = (int) (gap / 4);
    }
    return ;
}
```



## 归并排序:

思想:







# 解耦-回调



# 可变参数



# 数组与指针