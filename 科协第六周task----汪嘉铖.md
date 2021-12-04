### 科协第六周task----汪嘉铖

#### malloc（）

##### 1.通过malloc()函数接受一个参数：所需的内存字节数，它会自动找到合适的空闲内存块，并返回动态分配内存块的首字节地址，因此可以把它的该地址赋值给一个指针变量，并使用指针访问这块内存，malloc()的范围类型一般被定义成char类型的指针；

例如

```
double* ptd;
ptd = (double*)malloc(30*sizeof(double));
//相当于double ptd[30];
划出一片内存来给指针赋值
```

通过这样的方法创建数组，可以在程序运行时选择数组的大小和分配内存



#### 结构体指针的->运算符

结构指针：

```
struct date{
	int day;
	int month;
	int year;
};				//定义了一个struct date 类型的结构体
struct date today;
struct date *pDate = &today;
//这样表示创建一个 指向struct date类型的指针*pDate 
  它指向的地址是&today
*pDate ->day;		//即today.day
*pDate ->month = 1;	//即today.month = 1;
```



#### 链表

通过创建结构体，成员包含值和指针，让这个指针指向另一个结构体，将多个结构体以指针的形式相连，组成链表

```
typedef struct node{
	int value;
	struct node *next;
}Node;

int number;
Node*head = NULL;

do{
	scanf("%d",&number);
	if(number!=-1){
	
		//创建一个新的部分
		Node*new = (Node*)malloc(sizeof(Node));
		new->value = number;
		new->next = NULL;
		
		//找到链表最后的位置
		Node*last = head;
		if(last){  	//如果头指针的地址不为NULL
			while(lase->next){
				lase=last->next;}
			//链接
			last->next = new;}
			
		else{		//如果头指针的地址为NULL
		head = new;
		}
		
	}
}while(number!=-1);

```



#### Leetcode：

##### 344：反转字符串

```
void exchange(char*a,char*b){
    char t = *a;
    *a = *b;
    *b = t;
}

void reverseString(char* s, int sSize){
char* p=s+sSize-1;
int a = 0;
int b = sSize-1;
for(;a<b;a++,b--){
    exchange(s+a,s+b);
    }
}
```





##### 371两整数之和

```
int getSum(int a, int b)
{
    return log(exp(a) * exp(b));
}
```





##### 1两数之和

```
int* twoSum(int* nums, int numsSize, int target, int* returnSize) {
    int q = 0;
    *returnSize = 2;
    int *result=NULL;
    int* b = nums+1;
    int* p = nums;
    for (int i = 0; i < numsSize; ) {
        for (int j = i + 1; j < numsSize; b++,j++) {
            if (*p + *b == target)
              { q = 1;
                break;}
        }
        if(q)break;
        p++,i++;
        b = p + 1;
    }
    result = (int*)malloc(2 * sizeof(int));
    result[0] = (int)(p - nums);
    result[1] = (int)(b - nums);
    return result;
}
```





##### 35搜索插入位置

```
int searchInsert(int* nums, int numsSize, int target){
int*p=nums;
for(int i = 0;i<numsSize;i++){
if(*p==target)break;
else if(*p<target)p++;
}
return((int)(p-nums));
}
```





##### 15三数之和

```
int** threeSum(int* nums, int numsSize, int* returnSize, int** returnColumnSizes){
    int p = 0;
    int q = 1;
    int max[5000];
    int min[5000];

    //
    int** result = NULL;
    result = (int **)malloc(sizeof(int *) * 5000);
    *returnColumnSizes = (int*)malloc(sizeof(int*) * 5000);

    /*
    for(int i=0; i<100; i++)
    {
        result[i] = (int *)malloc(sizeof(int) * (10));//分配每个指针所指向的数组，再计算列
    }
*/
//

for(int i = 0;i<numsSize-2;i++){

    for(int j = i+1;j<numsSize-1;j++){

        for(int k = j+1;k<numsSize;k++){

            if(nums[i]+nums[j]+nums[k]==0){

            max[p]=nums[i];
            if(max[p]<nums[j])max[p]=nums[j];
            if(max[p]<nums[k])max[p]=nums[k];

             min[p]=nums[i];
            if(min[p]>nums[j])min[p]=nums[j];
            if(min[p]>nums[k])min[p]=nums[k];

            //
            result[p] = (int*)malloc(sizeof(int) * 3);//给单组答案空间申请空间，三数，就是3
                (*returnColumnSizes)[p] = 3;//给单组答案显示空间申请空间，三数，就是3
            //
            for(int l = 0;l<p;l++){
                if(max[p]==max[l])
                if(min[p]==min[l])
                q = 0;}
                
            if(q){
            result[p][0] = nums[i];
            result[p][1] = nums[j];
            result[p][2] = nums[k];
            p++;}

            }
            q = 1;
        }

    }

}
    *returnSize = p;
    return result;
}
```





##### 206反转链表

```
struct ListNode* reverseList(struct ListNode* head){
struct ListNode*last=head;
struct ListNode*p = head;
struct ListNode*q = head;
int a;
while(last != NULL&&last->next){last = last->next;}
//找到链表的最后一个节点
if(head == NULL){
    return head;
}
//如果头节点为null则直接返回
for(;p!=NULL && p->next != last && p!= last;){
    
    a = last->val;			//交换val值
    last->val = p->val;
    p->val = a;

    for(;q!=NULL;){			//找到last的上一个节点
    if(last!=NULL&&q!=NULL&&q->next == last){
    last = q;				//last返回上一个节点
    break;
    }
    q = q->next;
    }
    q = p->next;
    p = p->next;			//p节点到下一个节点
}
    a = last->val;
    last->val = p->val;
    p->val = a;
return head;
}
```

