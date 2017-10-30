```
#include<iostream>
#include<stack>
using namespace std;
int partition(int a[],int left,int right)
{
  int temp=a[right];
  int i=left-1;
  int j=right;
  for(;;)
  {
  while(a[++i]<temp)//从左向右找出第一个不比temp小的值
  {}
  while(a[--j]>temp)//从右向左找出第一个不比temp大的值
  {if(j==left)//若j到达left的位置，说明temp是最小值了
    break;
  }
  if(i<j)
  {
    swap(a[i],a[j]);
  }
  else
    break;
  }
  swap(a[i],a[right]);
  return i;//返回i,使得i左边的数值都比temp小，i右边的数值都比temp大
  
}
void quicksort(int a[],int left,int right)
{//利用堆栈将数组细分，小段进行排列，但每一个小步骤都是使得p左边的是小值，p右边的是大值
  stack<int> t;
  if(left<right)
  {
    int p=partition(a,left,right);
    if(p-1>left)
    {
      t.push(left);
      t.push(p-1);
    }
    if(p+1<right)
    {
      t.push(p+1);
      t.push(right);
    }
    while(!t.empty())
    {
      int r=t.top();
      t.pop();
      int l=t.top();
      t.pop();
      p=partition(a,l,r);
      if(p-1>l)
      {t.push(l);
	t.push(p-1);
      }
      if(p+1<r)
      {
      
	t.push(p+1);
	t.push(r);
      }
    }
  }
}
void arrayprint(int a[],int size)
{
  for(int i=0;i<size;i++)
  {
    cout<<a[i]<<" ";
    
  }
  
}
int main()
{
  int size;
  cout<<"请输入你要测试数组的数组长度：（输入为0时则退出程序）\n";
  cin>>size;
  while(size!=0)
  {int element;
    int *p=new int[size];
    cout<<"请输入你数组中的元素：\n";
    for(int i=0;i<size;i++)
    {
      cin>>element;
      p[i]=element;
      
    }
    quicksort(p,0,size-1);
    cout<<"经过快速排序后将数组按从小到大顺序输出：\n";
    arrayprint(p,size);
    cout<<"\n\n\n";
    cout<<"请输入你要测试数组的数组长度：（输入为0时则退出程序）\n";
    cin>>size;
  }
}

```
