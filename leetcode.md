[TOC]

## 做题注意事项

1. 条件语句if,continue,break和标志位设置

   ```c++
   1.if ..
     if..//多个if并列，一行一行的执行
   2.if,,,
     else if...//分支关系，只执行其中一行
   3.if..
         continue;//满足条件希望跳过后面的程序
   4.if..
         break;//满足条件希望退出当前循环。这种情况一定有循环。
   5.bool a=true;//两种情况都有可能统计结果，但是只想要其中满足要求的一种。
     if(条件A..)
         a=false;
         break;
     if(a&&条件B..)统计结果。//不用if（A）内的内容
   6.bool a=false;//两种情况都有可能统计结果，但是只想要其中满足要求的一种。
     if(条件A..)
         a=true;
         break;
     if(a)统计结果。//只用if（A）内的内容。
       
   ```

12. sort自定义排序规则：

    ```c++
    sort(first,last,cmp);
    first是元素的起始地址（迭代器），last是结束地址，[first,last)左闭右开，cmp是排序的方式，默认从小到大
    自定义排序：
    bool cmp(const int &a,const int &b){
      return b<a;//从大到小排序，默认a<b
    }
    还有重载<和声明比较类
    ```

21. ##### 二叉搜索树：记录前一个结点的技巧

    ```c++
    //左子树所有节点小于中间节点，右子树所有节点大于中间节点，中序遍历之后元素值是升序的，并且没有重复元素。
    验证二叉搜索树，pre的设置！！！
    class Solution {
    public:
     TreeNode* pre = NULL; // 用来记录前一个节点 
        bool isValidBST(TreeNode* root) {
            if (root == NULL) return true;
            bool left = isValidBST(root->left);
    
            if (pre != NULL && pre->val >= root->val) return false;
            pre = root; // 记录前一个节点
    
            bool right = isValidBST(root->right);
            return left && right;
        }
    };
    ```

22. ##### 利用num[i]==num[i-1]的时候注意i>=1,

23. 去重：先搞清楚哪些情况是重复的，然后去重的方法就是

    ```c++
    1、for(int i=0;i<nums.size();i++){//数组
        if(i>0&&nums[i]==nums[i-1])continue;//或者其他操作，看具体题目意思
    }
    2、
    ```

## 类型

### 衡量算法的标准

https://blog.csdn.net/xiaojinIT/article/details/78113947

时间复杂度:

```c++
首先你要知道时间都花在哪里了，
O（f(n)）//f（n）就是程序每个部分执行的次数之和，n就是问题的规模，
    //如果算法的执行时间不随着问题规模n的增加而增长，即使算法中有上千条语句，其执行时间也不过是一个较大的常数。
    一般准测：用常数1取代运行时间中的所有加法常数，f(n)只保留最高阶（当n比较大时相对的），去除最高阶的系数。主要还是要计算出运行次数。
    一般时间复杂度大小：
    O（1）<0(logn)<O(n)<o(nlogn)<o(n**2)<o(n**3)<o(2**n)<o(n!)<o(n**n)
    这只是最坏情况下时间复杂度，也有的是根据平均情况下的时间复杂度
```

空间复杂度：

```c++
  程序所占用的存储空间：
    程序代码本身所占用的存储空间；
    程序中如果需要输入输出数据，也会占用一定的存储空间；
    程序在运行过程中，可能还需要临时申请更多的存储空间。
```



### 内存的四个分区

![image-20210416203755741](C:\Users\小面包\AppData\Roaming\Typora\typora-user-images\image-20210416203755741.png)![image-20210416204751920](C:\Users\小面包\AppData\Roaming\Typora\typora-user-images\image-20210416204751920.png)![image-20210416205313742](C:\Users\小面包\AppData\Roaming\Typora\typora-user-images\image-20210416205313742.png)

### 数组

##### 基本知识

1. 数组在内存中的存储方式：数组是存放在**连续内存空间**上的**相同类型数据**的集合，因为是连续的，所以在插入和删除元素的时候就需要移动其他元素的地址，链表不需要，数组一般通过下标索引获取元素，遍历数组不可避免；一般是内存地址，字符数组和下标。二维数组是一个线性数组存放着其他数组的首地址。

2. 计算十进制转K进制后数字各个位置上的和

   ```c++
   int n;//n是十进制数，转成K进制。
   //将给定的十进制数除以基数K；余数是所求K进制的最低位，先求最低位。第二步，将上一步的商再除以k,余数就是所求K进制的次低位，依次重复直到商为零。
   while(n){
       int sum+=n%k;//先求模，从最低位上相加
       n=/k;//然后继续求得下一步的数
   }
   ```

   

3. 动态数组：new申请

4. 运算先后顺序

   ```c++
   if(num[astr[i]-'a']++)//先num[]再if再++ 
   ```

5. **求数组中的最大元素的下标**：遍历一遍数组，主要就是if条件的内容改变

   ```c++
   int cut=start;//求谁先建立一个数据类型来存储它
   for(int i=start+1;i<end;i++){
              if(nums[i]>nums[cut]){//一个是判断条件
                  cut=i;//一个是根据条件做出动作
               }
           }
   ```

6. 求数组中最大（最小）元素

   ```c++
   int m=INT_MIN;
   for(auto j=mymap.begin();j!=mymap.end();j++){
               if(j->second>m){
                   m=j->second;//如果有最大值，可以及时记录下来，思考这一行代码的作用
               }//直接使用max或者min函数也行
           }
   ```

7. 一个整数求其各个位置上的数字的平方之和

   ```c++
   int getSum(int x){//取余数就是每个位置的数字，通过取整来求剩余位数的数字是多少，每次/10都会从右到左减少一位，%10都会求出这个位置的数字是多少。
           int sum=0;
           while(x){//直到此数为0
               sum+=(x%10)*(x%10);//%取余数
               x/=10;//取整除的数字
           }
           return sum;
       }
   ```

8. 自定义sort函数

   ```c++
   // 比较器函数
   bool compare(参与比较的第一个元素, 参与比较的第二个元素)
   {
       return 参与比较的第一个元素 > 参与比较的第二个元素; // 降序
       // return 参与比较的第一个元素 < 参与比较的第二个元素; 升序
   }
   // sort函数，泛型算法一般都是基于迭代器操作的。
   void sort(排序的首地址, 排序的末地址 + 1, 比较器函数名称);
   ```

9. 有序且有重复数组中元素出现的频率（不占用哈希表内存的方法）

   ```c++
      //有序数组比较相邻两个元素即可
      vector<int>ans,result;
      for(int i=0;i<result.size();i++){
           if(i>0&&result[i]==result[i-1]){//
                      count++;
                  }
                  else{
                      count=1;
                  }
                  if(count==maxcount){//
                      ans.push_back(result[i]);
                  }
                  if(count>maxcount){//
                      maxcount=count;
                      ans.clear();//
                      ans.push_back(result[i]);
                  }
              }
   ```

##### 经典题目

1. 搜索插入位置

   ```c++
   二分法：左闭右闭
   class Solution {
   public:
       int searchInsert(vector<int>& nums, int target) {
           int l=0,r=nums.size()-1;//左闭右闭
           if(nums[0]>target)return 0;
           if(nums[nums.size()-1]<target)return nums.size();
           while(l<=r){
               int mid=l+(r-l)/2;
               if(nums[mid]>target){
                   r=mid-1;
               }
               else if(nums[mid]<target){
                   l=mid+1;
               }
               else return mid;
           }
           return l;
       }
   };
   //暴力法也行
   class Solution {
   public:
       int searchInsert(vector<int>& nums, int target) {
           for(int i=0;i<nums.size();i++){
               if(nums[i]>=target)return i;//相等和大于都替换这个元素的位置，返回位置比较简单，要是返回数组就有点东西了
           }
           return nums.size();
   
       }
   };
   ```

   

2. 移除数组元素

   普通双指针，一个移动，一个满足条件再移动。从前向后遍历还是从后向前遍历根据题意而定。

   ```c++
   class Solution {
   public:
       int removeElement(vector<int>& nums, int val) {
           int i=0,j=0;
           for(i;i<nums.size();i++){
               if(nums[i]==val)continue;
               nums[j++]=nums[i];
           }
           return j;//每次运算之后j都会加1，所以不用返回j+1
       }
   };
   ```

   

3. 长度最小的子数组

   ```c++
   滑动窗口;精髓在于两个指针都在变化，并且一次变化是众多答案中的一个。
   class Solution {
   public:
       int minSubArrayLen(int target, vector<int>& nums) {
           int sum=0;
           int l=0,r=0;
           int result=INT_MAX;
           while(r<=nums.size()){
               if(sum<target){
                   if (r == nums.size())break;//防止溢出，这里反映出代码技巧。直接使用while循环来表达不停的改变更直接！！！
                   sum+=nums[r];
                   r++;
               }else{
                   result=min(result,r-l);
                   sum-=nums[l];
                   l++;
               }
           }
           return result==INT_MAX?0:result;
       }
   };
   // class Solution {
   // public:
   //     int minSubArrayLen(int target, vector<int>& nums) {
   //         int sum=0;
   //         int l=0,r=0;
   //         int result=INT_MAX;
   //         while(r<nums.size()){
   //             sum+=nums[r];
   //             while(sum>=target){//这里是while，因为要不断l的位置可能要不断改变，所以是直到改变到满足条件为止。
   //                 result=min(result,r-l+1);
   //                 sum-=nums[l];
   //                 l++;    // 不断变更l的位置，直到满足条件，肯定在while循环之下
   //             }
   //             r++;
   //         }
   //         return result==INT_MAX?0:result;
   //     }
   // };
   ```

   

4. 螺旋矩阵

   ```c++
   纯模拟，转的时候搞清楚状态，怎么转，转到什么时候停止。其实思考结束代码就体现出来了，但是要搞清楚自己的语言怎么用代码表达处理。
   // class Solution {//n*n相等于特例了
   // public:
   //     vector<vector<int>> generateMatrix(int n) {
   //         vector<vector<int>>result(n,vector<int>(n,0));
   //         int m=1;
   //         for(int s=0,e=n-1;s<=e;s++,e--){
   //             if(s==e)result[s][e]=m++;
   //             for(int i=s;i<=e-1;i++)result[s][i]=m++;
   //             for(int j=s;j<=e-1;j++)result[j][e]=m++;
   //             for(int i=e;i>=s+1;i--)result[e][i]=m++;
   //             for(int j=e;j>=s+1;j--)result[j][s]=m++;
   //         }
   //         return result;
   //     }
   // };
   
   class Solution{//m*n写法
   public:
         vector<vector<int>>generateMatrix(int n){
             vector<vector<int>>result(n,vector<int>(n,0));
             int l=0,r=n-1,s=0,x=n-1;//行和列对应都有初始和终止位置
             int num=1;
             while(num<=n*n){
                 if(num==n*n){
                     result[l][r]=num++;
                     break;
                 }
                 for(int j=l;j<=r-1;j++)result[l][j]=num++;
                 l++;
                 for(int i=s;i<=x-1;i++)result[i][r]=num++;//
                 r--;
                 for(int j=r+1;j>=l;j--)result[x][j]=num++;
                 x--;
                 for(int i=x+1;i>=s+1;i--)result[i][s]=num++;
                 s++;
             }
             return result;
         }
   };
   ```

   

5. 



### 链表

##### 基本知识

对链表的操作有两种，一种设置虚拟头节点进行操作，一种直接在原来链表上操作。

1. 链表的定义：什么是链表，链表是一种通过指针串联在一起的线性结构，每一个节点是由两部分组成，一个是数据域一个是指针域（存放指向下一个节点的指针），最后一个节点的指针域指向null（空指针的意思）。

2. 基本结构：最后一个节点的指针域为null

   ```c++
   //基本结构,结点（包括数据域和指针域）
   template<typename T>//模板表示
   struct ListNode{
       T val;//数据域
       ListNode*next;//指针域
       ListNode(int x):val(x),next(null){}//初始化
       ListNode(const T&d):data(d),next(nullptr){} 
   }
   //单链表，双链表，循环链表
   ```

3. **技巧**：由于在进行链表操作时，尤其是删除节点时，经常会因为对当前节点进行操作而导致内存或 指针出现问题。有两个小技巧可以解决这个问题：

   **一是尽量处理当前节点的下一个节点而非当前 节点本身**，

   **二是建立一个虚拟节点 (dummy node)，使其指向当前链表的头节点，这样即使原链表 所有节点全被删除**，也会有一个 dummy 存在，返回 dummy->next 即可，**记得在创建虚拟节点之后要另外创建一个虚拟头节点进行迭代操作**，因为还要返回虚拟头节点的下一个节点，迭代的时候节点已经改变了。

4. 虚拟头节点的设置：设置虚拟头节点之后，返回这个虚拟头节点的下一个节点，**操作的时候要另外创建一个节点代替虚拟头节点来执行。**切记！！！加入head为创建的虚拟头节点，不要用head=head->next来得到真正的头节点，要另外创建一个节点：auto node=head->next;此时node为真正的头节点。

   ```c++
    ListNode*node=new ListNode(0);//创建虚拟节点（下一步就是让虚拟节点变成虚拟头节点）
    node->next=head;//让虚拟节点指向头节点，成为虚拟头节点，目的是让虚拟节点变成虚拟头节点，改变的是虚拟节点，所以是在左边。
    ListNode*p=node;//在另外一个虚拟头节点上操作。返回最初的虚拟头节点的指针域就是真正的链表头节点了。
   之后在p上操作。
   ```

5. 创建节点

   ```c++
   ListNode*create(int n) {
   	auto dummy = new ListNode(0);
   	auto pre = dummy;
   	for (int i = 0; i < n; i++)
   	{
   		auto p = new ListNode(0);
   		cin >> p->val;
   		pre->next = p;
   		pre = pre->next;
   	}
   	return dummy->next;
   }
   ```

6. 初始化

   ```c++
   MyLinkedList() {//
         Node *head=new Node(0);
         size=0;//链表节点个数
       }
   ```

7. 插入：注意插入要先申请节点。

   ```c++
   1. 先申请一段内存来存储新的结点
   2. p后插入节点
   void Insert(Node<T>*p,const T&data)
   {
       auto tmp=new Node<T>(data);//申请新的内存来存储新结点
       temp->next=p-next;//先把原来p的指针域赋值到新节点的指针域
       p->next=tmp;//再更新p
   }
   ```
   
8. 删除：删除p节点后的q节点。

   ```c++
   两种方式:核心就是将q节点的指针域复制给p节点的指针域，然后删除q节点（想一下先把节点存起来的原因），A指向B。就是A=B。
   void Remove(Node<T>*p)
   {
       if(p==nullptr||p->next==nullptr)
           return;
       auto tmp=p->next->next;//先存起来q后面结点的地址
       delete p->next;//然后删除q，C++中要手动释放这块内存
       p->next=tmp;//再把p和q后面的结点连接起来 
       //auto tmp=p->next;先把节点存起来
       //p->next=p->next->next;直接连接要得到的链表（另外删除节点）
       //delete tmp;删除节点
   }
   ```

9. 修改

10. 遍历

   ```c++
   p=p->next;//更新节点也是一样，记住=改变的是左边的值，更新谁谁肯定在=左边，而链表中A指向B，就是A=B，想想谁在改变。
   ```

11. 打印节点

    最后一个为null，先把特殊的给处理掉

    ```c++
    void print(ListNode* head)
    {
    	while (head)
    	{
    		if (head->next == NULL)//处理节点的下一个节点，先把特殊的给处理掉.处理最后一个节点
    			cout << head->val << "-> NULL";
    		else
    			cout << head->val << "-> ";
    		head = head->next;
    	}
    	cout << endl;
    }
    ```

    

12. ###### 链表和双指针

    ```c++
    //获取链表中倒数第k个结点，普通双指针
    class Solution{
        public:
        ListNode * getKth(ListNode*head,int k)
        {
            ListNode*l=head,*r=head;//初始化l,r都指向头节点
            while(k--)//结束条件，while循环本身条件为true才进入循环
                r=r->next;//右移k个单位
            while(r!=null)//结束条件r指向空
            {
                r=r->next;
                l=l->next;  //左右一起右移
            }   
            return l;
        }
    }
    //获取中间位置的元素，快慢指针
    n为偶数
    class Solution{
        public:
        ListNode*middleNode(ListNode *head)
        {
            ListNode*l=head,*r=head;
            while(r!=null&&r->next!=null)//结束条件，r为0或者-1最终是r=null或者r->next=null
            {
                l=l->next;  
                r=r->next->next;//快指针移动两步，慢指针移动一步
    }
             return l;
    }         
    }
    //环链表
    //是否存在环，一个链表存在环，快慢指针必然相遇
    class Solution{
         public:
         bool hasCycle(ListNode*head)
         {
             ListNode*l=head,r=head;
             while(r!=null)
             {
                 r=r->next;//考虑一个结点的情况
                 if(r!null)
                     r=r->next;//考虑两个结点的情况
                 if(r==l)
                     return true;
                 l=l->next;
    }
             return null;
         }
        
    }
    //反转链表
    class Solution {
    public:
        ListNode* reverseList(ListNode* head) {
            ListNode*pre=nullptr;
            ListNode*cur=head;
            ListNode*tmp;
            while(cur){
                // cur->next=pre;
                // pre=cur;
                // cur=cur->next;这样就是pre和cur的相互赋值了,链表中一般都要多创建一个节点来保存其余部分，因为链表在内存中是分散分布的，要保存起来下一个节点才能找到。同时，赋值的时候要弄清楚谁指向谁，或者谁在改变。原来的，现在的，一般都要重新设置来保存原来的或者现在的。关于链表遍历，一般是l=l->next;如果是双指针，也可能有这种，pre=cur,cur=cur->next；的情况，前提是pre->next=cur;但是要注意是否有指向或者节点改变，有改变不妨重新设置新的节点保存改变前的节点。
                tmp=cur->next;//先保存指向要改变的节点的后面的节点
                cur->next=pre;//当前节点指向改变
                pre=cur;//更新指针
                cur=tmp;//这里是遍历还未访问的节点，所以一定是
            }
            return pre;
        }
    };
    ```

##### 链表经典题目

1. 移除链表元素

   ```c++
   class Solution {
   public:
       ListNode* removeElements(ListNode* head, int val) {
           ListNode*node = new ListNode(0);//创建虚拟节点
   	node->next = head;//虚拟节点变为虚拟头节点
   	auto tmp = node;//在另外一个虚拟头节点上操作
   	while (tmp->next)//迭代的终止条件，就和递归一样，有终止条件，这里只要真实的节点不为空就行，我们关注的就是真实的节点。
   	{
   		if (tmp->next->val == val) {//判断的是当前节点的下一个节点。
   			auto after = tmp->next->next;
   			delete tmp->next;
   			tmp->next = after;
   		}
   		else tmp=tmp->next;//第一次写的是没加else，注意区别，
   	}
   	return node->next;
   
       }
   };
   ```

   

2. 设计链表

   ```c++
   class MyLinkedList {
       private:
           int size;
           Node* head;
   public:
       //定义结构体
       //template<typename T>
       struct Node{
           int val;
           Node*next;
           Node(int x):val(x),next(NULL){}
       };
       /** Initialize your data structure here. */
       MyLinkedList() {//
           head=new Node(0);.//创建虚拟头节点
           size=0;//链表节点个数
       }
       /** Get the value of the index-th node in the linked list. If the index is invalid, return -1. */
       int get(int index) {
           if(index>(size-1)||index<0){
               return -1;
           }
           //Node *cur=new Node(0);
           //head->next=cur;
           Node *cur=head->next;//直接创建虚拟头节点的下一个节点，即直接创建真实的节点。如果已有真实链表头节点，创建一个虚拟节点，让其指向真实链表头节点即可。
           while(index--){
               cur=cur->next;
           }
           return cur->val;
       }
       
       /** Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list. */
       void addAtHead(int val) {
           auto newNode=new Node(val);
           newNode->next=head->next;
           head->next=newNode;
           size++;
       }
       
       /** Append a node of value val to the last element of the linked list. */
       void addAtTail(int val) {
           auto new_node=new Node(val);
           Node*cur=head;
           while(cur->next){//对链表的下一个节点，也就是真实节点进行操作
               cur=cur->next;
           }
           //new_node->next=NULL;
           cur->next=new_node;//
           size++;
       }
       
       /** 在链表中的第 index 个节点之前添加值为 val  的节点。如果 index 等于链表的长度，则该节点将附加到链表的末尾。如果 index 大于链表长度，则不会插入节点。如果index小于0，则在头部插入节点。
   */
       void addAtIndex(int index, int val) {  
           if(size==index){
               addAtTail(val);
           }
           else if(index<0){
               addAtHead(val);
           }
           else if(index>size){
               return ;
           }else{
               auto p=new Node(val);
               auto q=head;
               //index=index-1;
               while(index--){
                   q=q->next;
               }
               p->next=q->next;
               q->next=p;
               size++;
           }
       }
       
       /** Delete the index-th node in the linked list, if the index is valid. */
       void deleteAtIndex(int index) {
           if(index<0||index>(size-1)){
               return ;
           }
           //index=index-1;
           auto cur=head;
           while(index--){
               cur=cur->next;
           }
           auto tmp=cur->next->next;
           delete cur->next;
           cur->next=tmp;
           size--;
       }
   
   };
   ```

   

3. 合并两个排序的链表![image-20210328203340397](C:\Users\小面包\AppData\Roaming\Typora\typora-user-images\image-20210328203340397.png)

   ```c++
   * Definition for singly-linked list.
    * struct ListNode {
    *     int val;
    *     ListNode *next;
    *     ListNode(int x) : val(x), next(NULL) {}
    * };
    */
   class Solution {
   public:
       ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
           ListNode*root=new ListNode(0);
           auto node=root;
           while(l2&&l1){//思路不清晰，代码出错。比较节点的值，小的链接在新建的节点后面，递归可以直接原节点操作。当任何一个链表走到空节点退出，
               if(l1->val>=l2->val){
                   node->next=l2;
                   l2=l2->next;
               }
               else if(l1->val<l2->val){
                   node->next=l1;
                   l1=l1->next;
               }
               node=node->next;
           }//最后不为空的链表要添加到新建的链表的末尾。
           if(!l1)node->next=l2;
           else node->next=l1;
           return root->next;
       }
   };
   ```

   

4. 环形链表2

   ```c++
   这题目我服了
   class Solution {
   public:
   	ListNode *detectCycle(ListNode *head) {
   		ListNode*f=head, *s = head;
   		while (f!=NULL&&f->next!=NULL)//主要是清楚1.判断链表是否有环-环形链表快慢指针必然相遇2.链表环的入口在哪呢？如何结算环的入口。
   		{
   			s = s->next;
   			f = f->next->next;
   			if (s == f) {
   				ListNode*x = head;//头节点一个指针
   				ListNode*z = f;//相遇的节点一个指针，同时走相遇就返回
   				while (x!=z)//
   				{
   					x = x->next;
   					z = z->next;
   				}
   				return z;
   			}
   		}
   		return NULL;
   	}
   };
   ```

   

5. 



### 字符串

1. 输入输出

   ```c++
   cin:使用空白（空格，制表符和换行符）来确定字符结束的位置，这意味着cin在获取字符数组时只读取一个单词。
   cin.getline(name,cnt)//面向行的输入；name为要读取的字符的名称，cnt为要读取的字符的个数。使用空格确定结尾，但是不保留空格。
   cin.get(name,cnt)//并不丢弃空白，而是将其保留在输入队列中
   cin.get()//不带任何参数的get（），可以读取下一个字符，即使是换行符
   getline(cin,str)//
   //输出直接cout,不过题目要看是否需要换行cout<<endl;输出大小写也要注意。
   例子：像这种
       cin>>n;
   cin.getline(name,a);//会读取上一行的换行符，导致出错。
   ```
   
2. openjudge基础总结

   ```
   1.char(数字)//简单字符和ASCII码转换
   2.要统计字符出现的个数的时候，可以利用数组当哈希表int a[26]={0};//来充当哈希表，求解s[i]-'a'的相对值就行
   3.数字和字母的字符表示就是s[i]>='0'&&s[i]<='9';s[i]>='a'&&s[i]<='z';
   4.输入一行：cin>>a>>b>>c;
   5.
   ```

   

3. 要统计字符出现的个数的时候，可以利用数组当哈希表

   ```c++
   int a[26]={0};//来充当哈希表，求解s[i]-'a'的相对值就行
   
   ```

4. int转string

   ```c++
   .c++11标准增加了全局函数std::to_string:
   
   string to_string (int val);
   
   string to_string (long val);
   
   string to_string (long long val);
   
   string to_string (unsigned val);
   
   string to_string (unsigned long val);
   
   string to_string (unsigned long long val);
   
   string to_string (float val);
   
   string to_string (double val);
   
   string to_string (long double val);
   
   Example:
   
       // to_string example
       #include <iostream>   // std::cout
       #include <string>     // std::string, std::to_string
        
       int main ()
       {
         std::string pi = "pi is " + std::to_string(3.1415926);
         std::string perfect = std::to_string(1+2+4+7+14) + " is a perfect number";
         std::cout << pi << '\n';
         std::cout << perfect << '\n';
         return 0;
       }
   
   Output:
   
       pi is 3.141593
       28 is a perfect number
   
   2.采用sstream中定义的字符串流对象来实现
   
       ostringstream os; //构造一个输出字符串流，流内容为空 
       int i = 12; 
       os << i; //向输出字符串流中输出int整数i的内容 
       cout << os.str() << endl; //利用字符串流的str函数获取流中的内容 
   ————————————————
   ```

5. string转int

   **可以使用std::stoi/stol/stoll等等函数**

   ```c++
   1.
   Example:
   
       // stoi example
       #include <iostream>   // std::cout
       #include <string>     // std::string, std::stoi
        
       int main ()
       {
         std::string str_dec = "2001, A Space Odyssey";
         std::string str_hex = "40c3";
         std::string str_bin = "-10010110001";
         std::string str_auto = "0x7f";
        
         std::string::size_type sz;   // alias of size_t
        
         int i_dec = std::stoi (str_dec,&sz);
         int i_hex = std::stoi (str_hex,nullptr,16);
         int i_bin = std::stoi (str_bin,nullptr,2);
         int i_auto = std::stoi (str_auto,nullptr,0);
        
         std::cout << str_dec << ": " << i_dec << " and [" << str_dec.substr(sz) << "]\n";
         std::cout << str_hex << ": " << i_hex << '\n';
         std::cout << str_bin << ": " << i_bin << '\n';
         std::cout << str_auto << ": " << i_auto << '\n';
        
         return 0;
       }
   
   Output:
   
       2001, A Space Odyssey: 2001 and [, A Space Odyssey]
       40c3:  16579
       -10010110001: -1201
       0x7f: 127
   
   2.采用标准库中atoi函数,对于其他类型也都有相应的标准库函数，比如浮点型atof(),long型atol()等等
   
       string s = "12"; 
       int a = atoi(s.c_str());
   
   3.采用sstream头文件中定义的字符串流对象来实现转换
   
       istringstream is("12"); //构造输入字符串流，流的内容初始化为“12”的字符串 
       int i; 
       is >> i; //从is流中读入一个int整数存入i中
   
   ```

   


##### 经典题目

1. ![image-20210328210345099](C:\Users\小面包\AppData\Roaming\Typora\typora-user-images\image-20210328210345099.png)

   ```c++
   #include<iostream>
   #include<string>
   #include<stack>
   #include<stdlib.h>
   #include<algorithm>
   using namespace std;
   //映射
   //1.字符和下标的一一对应关系。哈希表或者数组都行。
   //2.如果不是一对一的关系，可以开两个数组或者两个哈希表来同时对应
   
   string a[] = { "a","b","a1" };//a,b建立映射
   int b[] = { 1,2,1 };//不同字符需要对应相同的数字，用这种方式映射。
   int c[7],n;//n记录数组出现的数字单词
   string t;
   int main() {
   	for (int i = 0; i < 6; i++) {//逗号和单词之间有空格
   		cin >> t;
   		for (int j = 0; j < 26; j++) {
   			if (t == a[j]) {//找到了这个单词
   				c[++n] = b[j];//找到这几个数
   				c[n] *= c[n];//每个数要处理下
   				c[n] %= 100;
   			}
   		}
   	}
   	sort(c + 1, c + n + 1);
   	if (n == 0) {//处理限制条件
   		cout << 0;
   		return 0;
   	}
   	cout << c[1];//开头为零就去掉0.前面我们就没考虑0，直接输出就行
   	for (int i = 1; i < n; i++) {
   		if (c[i] < 10) {
   			cout << 0;//我们没考虑0的情况，现在要补上
   		}
   		cout << c[i];
   	}
   }
   ```

   

2. 潜伏者（洛谷）

   ```c++
   #include<iostream>
   #include<string>
   using namespace std;
   string x, y;
   char a[100], b[100];//a是x在下标对应y的关系。x的字符是下标，数值是y中的字符
   int len,cnt;
   //主要是建立的对应关系，
   int main() {
   	memset(a, '?', sizeof(a));//将a后面的sizeof（a）个字节用？替换并返回a
   	memset(b, '?', sizeof(b));
   	cin >> x >> y;
   	len = x.length();
   	for (int i = 0; i < len; i++) {
   		if (a[x[i]] == '?'&&b[y[i]] == '?') {	//如果a,b是空的就可以建立对应关系了
   			a[x[i]] = y[i];//两者都为空建立二者的对应关系
   			b[y[i]] = x[i];
   			cnt++;
   		}
   		else if (a[x[i]] != y[i]) {//两个都不是空的，而且又不对应,就是存在多个对应关系了
   			cout << "Failed";
   			return 0;
   		}
   	}
   	if (cnt < 26) {//26个字母没有完全出现
   		cout << "Failed";
   		return 0;
   	}
   	return 0;
   }
   ```

3. 拼数

   ```c++
   //比较数字中第一个数谁大，第一个相等就比较第二个。利用字典序即可。'0' < '1' < '2' < ... < '9' < 'a' < 'b' < ... < 'z'
   	//字典序：对于两个字符串，大小关系取决于两个字符串从左到右第一个不同字符的 ASCII 值的大小关系。
   #include<iostream>
   #include<string>
   #include<algorithm>
   using namespace std;
   bool cmp(string x, string y) {
   	return  x + y > y + x;
   }
   int main() {
   	int n;
   	cin >> n;
   	string a[30];//字典序把数字声明为字符就行
   	for (int i = 0; i < n; i++) {
   		cin >> a[i];
   	}
   	sort(a + 1, a + n + 1,cmp);//字典序排序会有问题，例如。812，8123，7
   	for (int i = 0; i < n; i++) {
   		cout << a[i];
   	}
   	return 0;
    }
   
   ```
   
   
   
4. 字符串中不同整数的数目![image-20210328203119683](C:\Users\小面包\AppData\Roaming\Typora\typora-user-images\image-20210328203119683.png)

   ```c++
   class Solution {
   public:
       int numDifferentIntegers(string word) {
           unordered_set<string>myhash;
           for(int i=0;i<word.size();i++){
               string str;
               if((word[i]<='9'&&word[i]>'0')||(word[i]=='0'&&!isdigit(word[i+1]))){
                   str+=word[i];//单独考虑0的情况即可。
                   //i++;
                   while(isdigit(word[++i])){//下一个还是数字的话就字符串添加。如果能转换成数字的话就很简单了。
                       str+=word[i];
                       //i++;
                   }
                   myhash.insert(str);
               }
           }
           return myhash.size();
       }
   };
   //区别于输入一个字符串，输出其中的数字  
   
   **标志位的设置和数字组成的字符串转化为数字的方法**。
   string s="abc123def45"
   int res = 0;
   int flag=0;
     for (int i = left; i <= right; i++) {
         if(s[i]>='0'&&s[i]<='9')//只提取数字
               res = res * 10 + (s[i] - '0');//将字符串里的数字整个保存起来,0开头的去掉。包括0的话直接stoi了。
               flag=1;//
           }else if(flag){//想要数字读取结束就放入数组，同时字母直接跳过，最简单就是设置标志位。
         result.push_back(res);
         res=0;
         flag=0;
   }
   ```

   

5. 反转字符串

   ```c++
   class Solution {
   public:
       void reverseString(vector<char>& s) {
           //双指针首尾两端交换
           int l=0;
           int r=s.size()-1;
           while(l<r){
               swap(s[l],s[r]);
               l++;
               r--;
           }
       }
   };
   ```

6. 反转字符串2

   **多参考别人的代码，另外continue和break的用法要善于利用啊！**

   ```c++
   
   class Solution {
   public:
       void reverse(string& s, int start, int end) {
           int offset = (end - start + 1) / 2;
           for (int i = start, j = end; i < start + offset; i++, j--) {
               swap(s[i], s[j]);
           }
       }
       string reverseStr(string s, int k) {
           for (int i = 0; i < s.size(); i += (2 * k)) {
               // 1. 每隔 2k 个字符的前 k 个字符进行反转
               // 2. 剩余字符小于 2k 但大于或等于 k 个，则反转前 k 个字符
               if (i + k <= s.size()) {//精髓啊
                   reverse(s, i, i + k - 1);
                   continue;//只想运行if条件下的，不满足不允行，可以elseif,不过这样貌似更好！！
               }
               // 3. 剩余字符少于 k 个，则将剩余字符全部反转。
               reverse(s, i, s.size() - 1);
           }
           return s;
       }
   };
   自己写的。。
       class Solution {
   public:
       void prereverse(string &s,int l,int r){//反转字符串函数
           while(l<r){
               swap(s[l],s[r]);
               l++;
               r--;
           }
       }
       string reverseStr(string &s, int k) {
           int size=s.size();
           if(size<=k)prereverse(s,0,size-1);
           else if(size>k&&size<=2*k)prereverse(s,0,k-1);
           else if(size>2*k){
               int strcount=size-2*k*(size/(2*k));
               for(int i=0;i<2*k*(size/(2*k));i+=2*k){
                   prereverse(s,i,i+k-1);
               }
               if(strcount<k)prereverse(s,2*k*(size/(2*k)),size-1);
               else if(strcount>=k&&strcount<2*k)prereverse(s,2*k*(size/(2*k)),2*k*(size/(2*k))+k-1);
           }
           return s;
       }
   };
   ```

   

7. 替换空格，

   这题还是挺简单的。**遇到对字符串或者数组做填充或删除的操作时，都要想想从后向前操作怎么样。**因为数组添加和删除是比较麻烦的，O（n）的时间复杂度。而链表就很方便。

   ```c++
   class Solution {
   public:
       string replaceSpace(string s) {
           int count=0;
           for(int i=0;i<s.size();i++){//先统计空格个数
               if(s[i]==' ')count++;
           }
           string newstr(s.size()+2*count,0);//新建字符串
           for(int i=s.size()-1,j=newstr.size()-1;i>=0;i--,j--){//从后向前遍历
               if(s[i]==' '){
                   newstr[j]='0';
                   newstr[j-1]='2';
                   newstr[j-2]='%';
                   j-=2;
                   continue;//else if也行，esle也行。但是continue更有意思，
               }
               newstr[j]=s[i];
           }
           return newstr;
       }
   };
   ```

8. 翻转字符转里的单词

   空格情况给考虑清楚就行。

   ```c++
   class Solution {
   public:
       //先去空格，再反转整个字符串，再反转单词。参考下别人去空格的方式。思想差不多，但是双指针到底，并且中间空格的情况可以和后面的相结合来考虑。另外就是string函数的使用，
       void move(string &s){
           for(int i=0;i<s.size();i++){
               if(s[i]==' ')continue;
               s=s.substr(i,s.size());//这里要将截取的重新赋值，参考人别人双指针到底的方法
               break;
           }
           for(int l=s.size()-1;l>=0;l--){
               if(s[l]==' ')continue;
               s=s.substr(0,l+1);
               break;
           }
           int j=0;
           for(int i=0;i<s.size();i++){
               if(i>=1&&(s[i]==s[i-1]&&s[i]==' '))continue;//不能三个等于一起
               s[j]=s[i];
               j++;
           }
           s.resize(j);//这里resize()是改变从前到后的元素个数。
       }
       void dve(string &s,int l,int r){
           while(l<r){
                swap(s[l],s[r]);
                l++;
                r--;
           }
       }
       string reverseWords(string s) {
           move(s);
           reverse(s.begin(),s.end());
           for(int l=0, r=l;l<=s.size();l++){
               if(s[l]==' '||l==s.size()){
                   dve(s,r,l-1);
                   r=l+1;
               }else continue;
           }
           return s;
       }
   };
   ```

   

9. 左旋转字符串

   **直接双指针或者反转-反转，如果不要求原地改变，通常都可以新建立一个字符串或者数组来存储结果，这样会很方便，相当于辅助数组或者辅助字符串。**

   ```c++
   class Solution {
   public:
       string reverseLeftWords(string s, int n) {
           int size=s.size()-1;//区间边界开闭记住
           int r=size;
           string s1=s;//新建立字符串来存储结果。
           for(int i=n;i<=size;i++){
               s1[i-n]=s[i];
           }
           while(n){
               s1[r]=s[n-1];
               n--;
               r--;
           }
           return s1;
       }
   };
   
   class Solution {
   public:
       void ver(string &s,int l,int r){
           while(l<r){//左闭右闭
               swap(s[l],s[r]);
               l++;
               r--;
           }
       }
       string reverseLeftWords(string s, int n) {
           //反转整个字符串，然后反转两个部分
           reverse(s.begin(),s.end());
           ver(s,0,s.size()-n-1);
           ver(s,s.size()-n,s.size()-1);
           return s;
       }
   };
   
   ```

   

10. KMP是重点！！！经典算法一类。

   ```
   
   ```

   

### 滑动窗口

滑动窗口：在众多选择中选择一个最大的或者最小的数组

精髓：不断更改两个指针的位置来找寻满足条件的值

我定义1次滑动窗口为：j先移动形成窗口满足条件为止，j先停，之后i移动缩小窗口达到满足条件的最小窗口之一

之后在这得到的N个最小窗口中找到一个更小的，就是满足最小条件的窗口。

```c++
模板：一般滑动窗口都是结合哈希表，双指针或者其他数据结构来解决问题的，滑动窗口是这个问题本身。
    //一般都要用到双指针+哈希表map
int l=0;//左
for(int r=0;r<n;r++){
    if()//r继续走的条件或者其他问题
    while(窗口缩小的条件)//一般没给窗口缩小的条件就要自己利用哈希表或者其他方式去找
    {
        if(ans>r-l+1){
            ans=r-l+1;
            result=..
}
        if()//如果有其他需要的条件，这里关注的是L指针
        l++;//窗口缩小
    }
    //或者
    result=....
}
```



### 思想1：双指针

##### 基本知识

双指针是一种思想，是为了更好的解决问题，所谓更好就是时间复杂度和空间复杂度更好。**为什么用双指针，f,s是位于同一端还是两端，f什么时候移动，什么时候停止，怎么移动，s什么时候移动，什么时候停止，怎么移动，**

1. 数组中一个去重方法

   ```c++
   for(int i=0;i<nums.size();i++){
       if(i>0&&nums[i]==nums[i-1])continue;//i表示当前元素
   }
   ```
   
2. 

3. 

   

##### 双指针分类

1. 首尾双指针
2. 同一端双指针（快慢指针）
3. 滑动窗口

##### 经典题目

普通双指针

快慢指针：一个快指针和一个慢指针在一个for循环内完成两个for循环的工作

1. 三数之和

   ```c++
   class Solution {
   public:
       vector<vector<int>> threeSum(vector<int>& nums) {
           vector<vector<int>>result;
           sort(nums.begin(),nums.end());//只考虑元素值，先排序双指针即可。其实用三个变量，一个变量固定，双指针遍历结束再移动这个变量。
           for(int i=0;i<nums.size();i++){
               if(nums[i]>0)return result;//排序之后第一个数大于0，肯定就不是
               //去重,当前的值和前一个重复，就跳过当前值。关注的是当前值。
               if(i>0&&nums[i]==nums[i-1]){
                   continue;
               }
               int l=i+1;
               int r=nums.size()-1;
               while(l<r){
                   if(nums[i]+nums[l]+nums[r]>0){
                       r--;
                   }
                   else if(nums[i]+nums[l]+nums[r]<0){
                       l++;
                   }
                   else{
                       result.push_back({nums[i],nums[l],nums[r]});
                       //去重
                       while(l<r&&nums[l]==nums[l+1])l++;
                       while(l<r&&nums[r]==nums[r-1])r--;
                       r--;
                       l++;
                   }
               }
   
           }
           return result;
       }
   };
   ```

   

2. 四数之和一个道理

   ```c++
   class Solution {
   public:
       vector<vector<int>> fourSum(vector<int>& nums, int target) {
           vector<vector<int>>result;
           if(nums.size()==0)return result;
           sort(nums.begin(),nums.end());
           for(int i=0;i<nums.size();i++){
               if(i>0&&nums[i]==nums[i-1])continue;
               for(int j=i+1;j<nums.size();j++){
                   if(j>i+1&&nums[j]==nums[j-1])continue;
                   int l=j+1;
                   int r=nums.size()-1;
                   while(l<r){
                       if(nums[i]+nums[j]+nums[l]+nums[r]>target){
                           r--;
                       }
                       else if(nums[i]+nums[j]+nums[l]+nums[r]<target){
                           l++;
                       }
                       else{
                           result.push_back({nums[i],nums[j],nums[l],nums[r]});
                           while(l<r&&nums[l]==nums[l+1])l++;
                           while(l<r&&nums[r]==nums[r-1])r--;
                           l++;
                           r--;
                       }
   
                   }
               }
           }
           return result;
       }
   };
   ```

   

3. 



### 思想2：二分查找

##### 基本知识

**实现基础条件：顺序存储，元素有序。**
注意：循环不变量，也就是左闭右闭或者左闭右开，在整个过程中要保持不变
[left,right]以左闭右闭为例，left==right区间依然是有效的，这也是需要注意的一点，

左闭右闭和左闭右开的写法

```
//寻找一个数
//寻找一个区间
//
```

```c++
一般格式：为二分查找
    class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int n = nums.size();
        int left = 0;
        int right = n - 1; // 定义target在左闭右闭的区间里，[left, right] 
        while (left <= right) { // 当left==right，区间[left, right]依然有效
            int middle = left + ((right - left) / 2);// 防止溢出 等同于(left + right)/2
            if (nums[middle] > target) {
                right = middle - 1; // target 在左区间，所以[left, middle - 1]
            } else if (nums[middle] < target) {
                left = middle + 1; // target 在右区间，所以[middle + 1, right]
            } else { // nums[middle] == target
                return middle;
            }
        }
        // 分别处理如下四种情况
        // 目标值在数组所有元素之前  [0, -1]
        // 目标值等于数组中某一个元素  return middle;
        // 目标值插入数组中的位置 [left, right]，return  right + 1
        // 目标值在数组所有元素之后的情况 [left, right]， return right + 1
        return right + 1;//return left；清楚二分的过程，结束条件是left>right;此时left=right+1;画个图自己理解下。
    }
};
```

##### 经典例题

1. 旋转数组的最小数字

   ```c++
   二分和搜索的结合，有重复数字和没有重复数字的区别
   class Solution {
   public:
       int minArray(vector<int>& numbers) {
           int l=0,r=numbers.size()-1;
           while(l<=r){
               int mid=l+(r-l)/2;
               if(numbers[mid]<numbers[r]){
                   r=mid;//这是要看是否可以取到值，本题可以取到这个值，不同于一般的二分
               }
               else if(numbers[mid]>numbers[r]){
                   l=mid+1;
               }
               else{
                   r-=1;//缩小搜索范围，有重复数字，即使r时最小值，也有mid代替。
               }
           }
           return numbers[l];
       }
   };
   ```

   

2. 搜索二维矩阵

   ```c++
   class Solution {
   public:
       bool searchMatrix(vector<vector<int>>& matrix, int target) {
           //二分
           int m=matrix.size();
           int n=matrix[0].size();
           int l=0,r=m*n-1;//二维转成一维
           while(l<=r){
               int mid=l+(r-l)/2;
               int x=matrix[mid/n][mid%n];//一维映射成二维
               if(x==target)return true;
               else if(x>target){
                   r=mid-1;
               }
               else{
                   l=mid+1;
               }
           }
           return false;
       }
   };
   ```

   

3. 



### 思想2+标记法

基本知识

### 哈希表

##### 基本知识

使用：**一般是用来快速判断一个元素是否重复出现或者是否出现在集合里**，set和map的使用，当只考虑一个数的时候就用set，要是既要考虑数又要考虑下标就用map。注意pair的使用，或者**两个变量，一个指向元素，一个指向下标。**

1. 容器的使用：优先考虑unordered_set,如果集合有序就用set，如果要求有序并且有重复数据就用multiset,

   ![图片](https://mmbiz.qpic.cn/mmbiz_png/F1VzfUpxxe4nxvWzKLIMPMARI6WiaMdagsSyX9BibHPKxX4OqujgmzzGy4CPRKI7sictaibiadXvxENh8KHIbjUiaueQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/F1VzfUpxxe4nxvWzKLIMPMARI6WiaMdag5moDNWxGcOot6SRoialwsCSnlX9Sa1Upl0PP6vR50mkaQT5yL2upUcQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)
   
3. 把事物映射到哈希表，一般是映射成哈希表的索引，有可能有哈希碰撞。这时候一般用拉链法和线性探测法牺牲了空间来换取时间，需要使用额外的内存来存放数据

3. 哈希碰撞：不同的关键字有相同的value，解决办法：拉链法：发生冲突的元素被存储在链表中

   线性探测法：

4. 常见的三种哈希结构：数组，set,map

5.     找出现两次的元素：遍历找到重复的就删除。或者哈希表统计元素出现的次数。
       使用集合（set）存储数字其实也可以是map。遍历数组中的每个数字，如果集合中没有该数字，则将该数字加入集合，如果集合中已经有该数字，则将该数字从集合中删除，最后剩下的数字就是只出现一次的数字。

6. 哈希表输出map容器中的键值对，pari类。setkey和value值相等。

   ```c++
   for (auto i = myMap.begin(); i != myMap.end(); ++i) {
         cout << i->first << " " << i->second << endl;
   //哈希表对value排序，要自定义函数，另外排序之后键值对依然是一一对应的，也就是说对value排序，key自动跟上排序。
   ```

7. 哈希表统计key出现的频率：

   ```c++
   map<int,int>mymap;
   for(int i=0;i<result.size();i++){
      mymap[result[i]]++;}
   ```

8. 找出value（频率）最大值：要善于利用pair键值对（排序value也行）

   ```c++
           int m=INT_MIN;
           for(auto j=mymap.begin();j!=mymap.end();j++){
               if(j->second>m){
                   m=j->second;
               }
           }
   ```

9. 对map中的value排序，对key排序是自带的sort就行，value排序要转换为vector来排序

   ```c++
   bool static cmp (const pair<int, int>& a, const pair<int, int>& b) {
       return a.second > b.second; // 按照频率从大到小排序
   }//排序函数
   vector<pair<int, int>> vec(map.begin(), map.end());//map转成vector
   sort(vec.begin(), vec.end(), cmp); // 给频率排个序
   ```

10. 哈希和vector转换

   ```c++
      unordered_set<int> result_set;
      vector<int>nums1;
      vector<int>(result_set.begin(), result_set.end())
      unordered_set<int> nums_set(nums1.begin(), nums1.end());
   ```

11. 字母就26个，一般涉及到字母的，想着用数组代替哈希STL

    ```c++
    int a[26]={0};
    string num;//26个字符任意组成的字符串
    for(auto b:num){
        a[b-'a']++;//b-'a'是拿num中的字符字面值'x'减去26个字符中第一个’a'的字符字面值，得到一个相对的数值，才能在0-26之间，如果是b本身，那他的ASCII值就很大，数组26个元素就不行
    }
    ```

12. 几种常见实现

   ```c++
   //用数组表示哈希表的时候要明确有多少个索引，即有多少个key值
   //value++，//统计数组中每个数字出现的次数
   unordered_map <int,int>umap;
       for(auto i:nums)//基于范围的for循环，需要对元素进行写操作需要声明为引用
       {
           umap[i]++;  //哈希容器中尚未存在以i为key的元素时，自动安插默认以i为key以0为value的新元素，每出现一次同样的key，value就++
   }
   //统计数组中出现多少个数字（重复的不算），加个条件统计所有元素出现一次的个数，重复元素避免两次映射
       for (int i = 0; i < nums1.size(); i++)
   	{
   		if (nums3[nums1[i]] == 0)//这样，重复的元素统计一次就行了
   			nums3[nums1[i]]++;
           
           
   	}
   //标记为value都为1
   for(auto a:arr){
               res[a]=1;//一个数组存储arr中的数和对应坐标并标记为1
           }
   //所有的数据映射哈希表，统计每个字符出现的位置，相同的字符会覆盖。
   for (int i = 0; i < nums.size(); i++) {
   			myhash[nums[i]] = i;//直接数组下标访问就行，这只是便于查找罢了
   		}
   //常用用法，先判断有没有，没有就插入
    if(mySet.find(result)!=mySet.end()){
             return true;}
          else{
               mySet.insert(result);
              //
   if (hash.count(key)) 是查找键为 key 的键值对的个数并返回；
   if (hash[key]) 是判断key对应的value值是否是真，如果key在hash表中不存在，则会先为其创建默认值，比如int的默认值是0，vector<int>的默认值是vector<int>()；
   在C++中，如果想往哈希表中插入一对(key, value)，一般写hash[key] = value；或者insert()
   //如果想查找一个key是否存在，一般有两种写法：
   if (hash.find(key) != hash.end())，说明key存在
   if (hash.count(key) != 0)
   //// 在哈希表（nums1）中存在 且 不在数组ans中
   if(m.count(num) != 0 && find(ans.begin(),ans.end(), num) == ans.end())
            ans.push_back(num);
   ```

##### 哈希表经典题目

1. 数组中出现两次的数字

   ```c++
   //先用的哈希表，空间复杂度太高
   class Solution {
   public:
       vector<int> findDuplicates(vector<int>& nums) {
           vector<int>result;
           unordered_set<int>myhash;
           for(int i=0;i<nums.size();i++){
               if(myhash.find(nums[i])!=myhash.end()){
                   result.push_back(nums[i]);
               }else{
                   myhash.insert(nums[i]);
               }
           }
           return result;
   
       }
   };
   //后来用的双指针，可是要先排序
   class Solution {
   public:
       vector<int> findDuplicates(vector<int>& nums) {
           vector<int>result;
           sort(nums.begin(),nums.end());
           for(int i=0,j=1;j<nums.size();i++,j++){
               if(nums[j]==nums[i]){
                   result.push_back(nums[j]);
               }
           }
           return result;
       }
   };
   //最后原地哈希，但是发现也就这回事！！
   class Solution {
   public:
       vector<int> findDuplicates(vector<int>& nums) {
           vector<int>resultl;
           //原地哈希，数组元素值作为索引
           for(int i=0;i<nums.size();i++){
               int p=abs(nums[i])-1;//数组元素值作为索引,元素值变为负数，要加上abs计算真正的元素值
               nums[p]*=-1;//当前元素作为索引对应的数组中的元素，令其变为负数，如果后面它变为正数了，说明表示为索引的元素出现偶数次了
               if(nums[p]>0)resultl.push_back(abs(nums[i]));
           }
           return resultl;
       }
   };
   ```

2. 存在重复元素2：

   给定一个整数数组和整数K,判断数组中是否存在两个不同的索引i和j，是的nums[i]=nums[j],**并且i和j的差的绝对值至多为K。**

   ```c++
   //首先想了涉及到下标肯定元素不能排序，之后想到哈希表来统计元素出现的个数，但是没办法求得i和j的差值，之后想到了利用无序map来统计元素值和下标。
   //更好的是利用哈希表+滑动窗口
   class Solution {
   public:
       unordered_set<int>myhash;
       bool containsNearbyDuplicate(vector<int>& nums, int k) {
           for(int i=0;i<nums.size();i++){
               if(myhash.find(nums[i])!=myhash.end())return true;
               myhash.insert(nums[i]);
               if(myhash.size()>k){//说明肯定没找到相等的
                   myhash.erase(nums[i-k]);
               }
           }
           return false;
       }
   };
   //或者是元素值当作key,元素下标当作value,区分统计元素个数的哈希表
   class Solution {
   public:
       unordered_map<int,int>myhash;//key为元素值，value为元素下标
       bool containsNearbyDuplicate(vector<int>& nums, int k) {
           for(int i=0;i<nums.size();i++){
               if(myhash.find(nums[i])!=myhash.end()&&i-myhash[nums[i]]<=k)return true;
               myhash[nums[i]]=i;
           }
           return false;
       }
   };
   ```

3. 无重复字符的最长子串

   ```c++
   //一开始用的哈希表+单变量，变量会反复回溯，浪费时间
   class Solution {
   public:
       int lengthOfLongestSubstring(string s) {
           if(s.size()==0)return 0;
           unordered_set<char>myhash;
           int result=1;
           for(int i=0;i<s.size();i++){
               if(myhash.find(s[i])!=myhash.end()){
                   int size=myhash.size();
                   result=max(result,size);
                   myhash.clear();
                   i-=size;
               }
               else{
                   myhash.insert(s[i]);
               }
               int size1=myhash.size();
               result=max(result,size1);
           }
           return result;
       }
   };
   //后来用的哈希表+双指针。需要注意两个问题：1.哈希表用来判断重复数字，涉及到下标和元素就map家族，只涉及下标或者元素一个就用set家族，通过利用find和count函数来判断元素是否重复出现，哈希表中没有就添加，有重复就移除。所以各个STL中函数要会使用2.双指针，滑动窗口有一个窗口形成过程，左指针先不动，右指针一直动（while）到不满足条件为止，然后左指针开始动，之后右指针同样动到不满足条件为止。一直动到什么条件为止。。一定结合while循环。
   class Solution {
   public:
       int lengthOfLongestSubstring(string s) {
           if(s.size()==0)return 0;
           int result=1;
           int n=s.size();
           unordered_set<char>myhash;
           for(int l=0,r=0;l<n;l++){
               while(r<n&&myhash.find(s[r])==myhash.end()){
                   myhash.insert(s[r]);
                   r++;
               }//不同的左指针，右指针都是一直移动到条件限制下。
               myhash.erase(s[l]);//STL中各个函数要熟悉
               result=max(result,r-l);
           }
           return result;
       }
   };
   ```

4. 有效的字母异位词

   ```c++
   class Solution {
   public:
       bool isAnagram(string s, string t) {
           if(s.size()!=t.size())return false;//如果单词长度不相同，肯定就不是
           int a[26]={0};//
           for(int i=0;i<s.size();i++){
               a[s[i]-'a']++;//都是小写字母，数组充当哈希表，计算每个字母相对'a'的位置，类似于位运算，26个位，出现一个相应位置就加1
           }
           for(int i=0;i<t.size();i++){
               a[t[i]-'a']--;//同理，出现一个相应位置减一
           }
           for(int i=0;i<26;i++){
               if(a[i]!=0)return false;//如果是具有相同的字母个数，那就应该每个位都是0，否则就不是
           }
           return true;
       }
   };
   ```

   

5. 两个数组的交集

   ```c++
   class Solution {
   public:
       vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
           unordered_set<int>myhash1,myhash2;//set的特点利用好就行
           for(int i=0;i<nums1.size();i++){
               myhash1.insert(nums1[i]);
           }
           for(int i=0;i<nums2.size();i++){
               if(myhash1.find(nums2[i])!=myhash1.end()){
                   myhash2.insert(nums2[i]);
               }
           }
           return vector<int>(myhash2.begin(),myhash2.end());
       }
   };
   ```

   

6. 快乐数

   ```c++
   快乐数定义为：对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和。
   然后重复这个过程直到这个数变为 1，也可能是 无限循环 但始终变不到 1。
   如果 可以变为  1，那么这个数就是快乐数。
       //主要是无限循环的判断。可以用哈希表统计出现次数，更好的是快慢指针破除循环
       class Solution {
   public:
       int sum(int &x){
           int ans=0;
           while(x){
               ans+=(x%10)*(x%10);
               x/=10;
           }
           return ans;
       }
       bool isHappy(int n) {
           unordered_set<int>myhash;
           while(n!=1){
               n=sum(n);//出现相同的数字就会无限循环
               if(myhash.find(n)!=myhash.end())return false;//循环看哈希表中是否出现相同的数字，出现就直接退出
               else myhash.insert(n);
           }
           return true;
       }
   };
   
   //弗洛伊德循环查找算法-快慢指针
   class Solution {
   public:
       int sum(int x){
           int ans=0;
           while(x){
               ans+=(x%10)*(x%10);
               x/=10;
           }
           return ans;
       }
       bool isHappy(int n) {
           int slow=n;
           int fast=sum(n);//快慢指针
           while(fast!=1&&slow!=fast){
               slow=sum(slow);
               fast=sum(sum(fast));
           }
           return fast==1;
       }
   };
   ```

   

7. 

### 栈和队列

##### 基本知识

1. 栈：后入先出，主要是STL-stack，注意top,pop，push,empty,size等几个方法的使用，注意pop栈长度减一，push栈长度要加一。

2. 队列：queue-先入先出，尾部进入，开头出。同样注意STL的用法。

3. 优先级队列（披着队列外衣的堆）（堆，大/小顶堆）：对队列中所有元素进行排序，**维护所有元素**。优先队列常常用堆（heap）来实现。**堆是一个完全二叉树**，其每个节点的值总是大于等于子 节点的值。实际实现堆时，我们通常用一个数组而不是用指针建立一个树。这是因为堆是完全二 叉树，所以用数组表示时，位置 i 的节点的父节点位置一定为 i/2，而它的两个子节点的位置又一 定分别为 2i 和 2i+1。 以下是堆的实现方法，其中最核心的两个操作是上浮和下沉：如果一个节点比父节点大，那 么需要交换这个两个节点；交换后还可能比它新的父节点大，因此需要不断地进行比较和交换操 作，我们称之为上浮；类似地，如果一个节点比父节小，也需要不断地向下进行比较和交换操作， 我们称之为下沉。如果一个节点有两个子节点，我们总是交换最大的子节点。STL中是priority_queue。**堆是将一组数据按照完全二叉树的存储顺序，将数据存储在一个一维数组中的结构。**
   
   ```c++
   priority_queue默认是大顶堆，
       template <typename T,//存的数值
            typename Container=std::vector<T>,//使用的底层容器
               typename Compare=std::less<T> >//默认元素从大到小
       class priority_queue{
           //......
       }
   还可以手动指定 priority_queue 使用的底层容器以及排序规则，比如：
   int values[]{ 4,1,2,3 };
   std::priority_queue<int, std::deque<int>, std::greater<int>>copy_values(values, values+4);//{1,3,2,4}
   自定义排序的方式：// 时间复杂度：O(nlogk)
   // 空间复杂度：O(n)
   class Solution {
   public:
       // 小顶堆
       class mycomparison {
       public:
           bool operator()(const pair<int, int>& lhs, const pair<int, int>& rhs) {
               return lhs.second > rhs.second;
           }
       };
       vector<int> topKFrequent(vector<int>& nums, int k) {
           // 要统计元素出现频率
           unordered_map<int, int> map; // map<nums[i],对应出现的次数>
           for (int i = 0; i < nums.size(); i++) {
               map[nums[i]]++;
           }
   
           // 对频率排序
           // 定义一个小顶堆，大小为k
           priority_queue<pair<int, int>, vector<pair<int, int>>, mycomparison> pri_que;
           
           // 用固定大小为k的小顶堆，扫面所有频率的数值 
           for (unordered_map<int, int>::iterator it = map.begin(); it != map.end(); it++) {
               pri_que.push(*it);
               if (pri_que.size() > k) { // 如果堆的大小大于了K，则队列弹出，保证堆的大小一直为k
                   pri_que.pop();
               }
        }
   
           // 找出前K个高频元素，因为小顶堆先弹出的是最小的，所以倒叙来输出到数组
           vector<int> result(k);
           for (int i = k - 1; i >= 0; i--) {
               result[i] = pri_que.top().first;
               pri_que.pop();
           }
           return result;
   
       }
   };
   ```
   
   堆有两种结构，一种称为大顶堆，一种称为小顶堆，如下图。
   小顶堆：任意结点的值均小于等于它的左右孩子，并且最小的值位于堆顶，即根节点处。
   大顶堆：任意结点的值均大于等于它的左右孩子，并且最大的值位于堆顶，即根节点处。
   ![image-20210310170844863](C:\Users\小面包\AppData\Roaming\Typora\typora-user-images\image-20210310170844863.png)
   
   ```c++
   //大顶堆为例子
   vector<int> heap;
   // 获得最大值
   void top() {
   return heap[0];
   }
   // 插入任意值：把新的数字放在最后一位，然后上浮
   void push(int k) {
   heap.push_back(k);
   swim(heap.size() - 1);
   }
   // 删除最大值：把最后一个数字挪到开头，然后下沉
   void pop() {
   heap[0] = heap.back();
   heap.pop_back();
   sink(0);
   }
   // 上浮
   void swim(int pos) {
       while (pos > 1 && heap[pos/2] < heap[pos])) {//如果该节点大于其父节点,开始上浮。
   swap(heap[pos/2], heap[pos]);//交换二者
   pos /= 2;//更新节点
   }
   }
   // 下沉
   void sink(int pos) {
   while (2 * pos <= N) {
   int i = 2 * pos;
   if (i < N && heap[i] < heap[i+1]) ++i;//如果左孩子节点小于右孩子，则定位到右孩子
   if (heap[pos] >= heap[i]) break;//如果父节点已经比孩子节点大了，就退出
   swap(heap[pos], heap[i]);//否则交换二者
   pos = i;//更新下一个
   }
   }
   ```
   
4. 单调队列（利用双端队列，单调的性质要自己去写，而优先级队列是做好的数据结构，可以理解为一种思想）：**只需要保证队列中元素是有序的，但是可以并不是所有元素，只维护需要用的元素**。和滑动窗口紧密联系，来维护整个序列中长度为K的区间的最大值或者最小值。**单调队列的长度取决于输入数据的合法性，而优先队列的长度始终与输入数据的数量等同**。而他们的单调性都是单调递减或单调递增。单调队列是使用双端队列（STL-deque）实现的。

5. 单调栈同理单调队列

6. 都是套路，注意基本用法，很多题目都是基本用法变换的。两点需要牢记，一个是如何创建栈和队列，另外一个栈和队列的相互应用，要熟记STL的函数和栈和队列的特性。

##### 经典题目

1. 三合一数组，用数组实现栈

   ~~~c++
    数组创建栈，各种基本知识的运用。三合一面试题目。
   
      ```c++
      class TripleInOne {
      private:
          struct StackInfo//创建栈结构
          {
              int base;//栈底
              int top;//栈顶元素的下一个位置
          };
          int size;//每一个栈的大小
          int* piTripleStack;
          StackInfo* pSI;//
      public:
          TripleInOne(int stackSize) : size(stackSize), piTripleStack(nullptr), pSI(nullptr)
          {
              piTripleStack = new int[3 * size];//创建动态数组，包含三个栈的数组，根据size的修改而改变
              pSI = new StackInfo[3];//创建三个栈，同理因为三个栈的大小相互之间是可以改变的，所以用new创建动态结构。
              for(int i = 0; i < 3; i++)
              {
                  pSI[i].base = i * size;//一开始栈内没有元素，三个栈都固定起始位置
                  pSI[i].top = i * size;
              }
          }
      
          ~TripleInOne()
          {
              delete [] piTripleStack;
              delete [] pSI;
          }
          
          void push(int stackNum, int value) {
              if(pSI[stackNum].top - pSI[stackNum].base == size) return;//栈满了就返回
              else piTripleStack[pSI[stackNum].top++] = value;//栈未满就入栈
          }
          
          int pop(int stackNum) {
              if(isEmpty(stackNum)) return -1;
              else return piTripleStack[--pSI[stackNum].top];//弹出就是栈顶元素减一
          }
          
          int peek(int stackNum) {
              if(isEmpty(stackNum)) return -1;
              else return piTripleStack[pSI[stackNum].top - 1];//top指的是栈顶元素的下一个位置，这里也可以理解为左闭右开！！！
          }
          
          bool isEmpty(int stackNum) {
              return pSI[stackNum].top == pSI[stackNum].base;//空栈就是栈底位置==栈顶
          }
      };
      ```
   ~~~

2. 栈和队列的相互实现，简单

   **利用辅助栈和队列**

   ```
   1.栈实现队列：两个栈，一个栈辅助存储数据，一个栈实现先进先出。输入栈和输出栈
   2.队列实现栈：两个队列，一个队列主打栈的实现，一个队列辅助
   ```

3. 有效的括号：**类似消消乐的匹配问题都可以考虑栈**

   ```c++
   
   class Solution {
   public:
       bool isValid(string s) {
           int size=s.size();
           stack<char>st;
           if(size%2!=0)return false;//
           for(int i=0;i<size;i++){
               if(s[i]=='(')st.push(')');
               else if(s[i]=='[')st.push(']');
               else if(s[i]=='{')st.push('}');
               else if(st.empty()||s[i]!=st.top())return false;//左右必须以正确的顺序闭合，正确顺序就那一种，st.empty()必须在前，栈为空说明上来第一个就是右括号，没法正常闭合，为空的话没法top，要先考虑是否为空。
               else st.pop();
           }
           return st.empty();
       }
   };
   //如果括号或者其他类型多的话，可以用哈希表来存储，官方题解。。
   class Solution {
   public:
       bool isValid(string s) {
           int n = s.size();
           if (n % 2 == 1) {
               return false;
           }
   
           unordered_map<char, char> pairs = {
               {')', '('},
               {']', '['},
               {'}', '{'}
           };
           stack<char> stk;
           for (char ch: s) {
               if (pairs.count(ch)) {
                   if (stk.empty() || stk.top() != pairs[ch]) {
                       return false;
                   }
                   stk.pop();
               }
               else {
                   stk.push(ch);
               }
           }
           return stk.empty();
       }
   };
   ```

4. 删除字符串中的所有相邻重复项

   ```c++
   
   class Solution {
   public:
       string removeDuplicates(string S) {
           stack<char>st;
           int size=S.size();
           // st.push(S[0]);//先入一个元素，
           // for(int i=1;i<size;i++){
           //     if(st.empty()||S[i]!=st.top()){
           //         st.push(S[i]);
           //     }
           //     else st.pop();
           // }
           for(int i=0;i<size;i++){
               if(st.empty()||S[i]!=st.top()){
                   st.push(S[i]);
               }else{
                   st.pop();
               }
           }
           string result;
           while(!st.empty()){
               result+=st.top();
               st.pop();
           }
           reverse(result.begin(),result.end());
           return result;
       }
   };
   class Solution {
   public:
       string removeDuplicates(string S) {
           string stk;
           for (char ch : S) {
               if (!stk.empty() && stk.back() == ch) {
                   stk.pop_back();
               } else {
                   stk.push_back(ch);
               }
           }
           return stk;
       }
   };
   
   ```

   5.逆波兰表达式求值

   ```
   适合用栈操作运算：遇到数字则入栈；遇到算符则取出栈顶两个数字进行计算，并将结果压入栈中
   
   ```

   6.滑动窗口最大值

   单调队列和优先级队列使用的经典！！

   ```c++
   优先级队列的方法
   class Solution {
   public:
       vector<int> maxSlidingWindow(vector<int>& nums, int k) {
           //利用优先级队列，思路：首先要清楚优先级队列是自动排序的，底层实现是堆，STL默认大顶堆，priority_queue。1.优先级队列里面存放数组的元素和下标（存放下标是为了方便判断队首的最大值是否是滑动窗口内的），利用pair同时存放两个元素，默认是以key排序。首先将一个滑动窗口中的元素放进队列，此时放进去队列中的元素自动排序，我们只要放进去队首就是最大值，（也可以一开始不放），之后滑动窗口右移，添加的元素还是直接放进队列中并且自动排序，然后判断队首元素是否是滑动窗口内的元素，这里就是利用下标来判断了，最大值下标在窗口的范围内就不用移除队首元素，否则删除队首元素遍历直到最后一个元素，然后返回最大值的数组
           vector<int>result;
           priority_queue<pair<int,int>>qu;//key为数字，value为下标
           for(int i=0;i<k;i++){
               qu.emplace(nums[i],i);
           }
           result.push_back(qu.top().first);
           for(int i=k;i<nums.size();i++){
               qu.emplace(nums[i],i);
               while(qu.top().second<i-k+1){//这里要是while，因为有很多元素都是在队列中，区别于单调队列只维护了可能成为最大的元素
                   qu.pop();
               }
               result.push_back(qu.top().first);
           }
           return result;
       }
   };
   单调队列：只维护了窗口内的元素！！！
   class Solution {
   public:
       vector<int> maxSlidingWindow(vector<int>& nums, int k) {
           //单调队列，滑动窗口一进一出，正好符合单调队列的特性，两端都可以添加和删除，STL中是deque，但是只是双端队列，单调性要自己去写！！！本题：队列中存访下标，同理方便去除不在窗口内的元素，删除队尾元素来保持单调性，队首元素要确认是否在当前窗口内。这里区别与优先级队列维护整个数组，这里就是维护窗口内的元素罢了（实际只是维护窗口内有可能成为最大值的元素），队列中最多只有k个元素每一个窗口都判断一次，并且队列中也只是该窗口内的部分元素（可能成为最大值的元素），
           deque<int>dequ;//存放下标。
           vector<int>result;
           for(int i=0;i<k;i++){
               while(!dequ.empty()&&nums[i]>nums[dequ.back()]){
                   dequ.pop_back();
               }
               dequ.push_back(i);
           }
           result.push_back(nums[dequ.front()]);
           for(int i=k;i<nums.size();i++){
               while(!dequ.empty()&&nums[i]>nums[dequ.back()]){
                   dequ.pop_back();//去除队尾
               }
               dequ.push_back(i);
               if(dequ.front()<i-k+1){//
                   dequ.pop_front();//去除队首元素
               }
               result.push_back(nums[dequ.front()]);
           }
           return result;
       }
   };
   ```

   7.前K个高频元素

   注意出现次数**前K高**的元素和出现次数**大于K**的元素可不一样！！！

   ```c++
   class Solution {
   public:
       bool static cmp (const pair<int, int>& a, const pair<int, int>& b) {
       return a.second > b.second; // 按照频率从大到小排序
   }//排序函数
       vector<int> topKFrequent(vector<int>& nums, int k) {
           vector<int>result;//是取前K个出现次数高的，不是出现次数大于K的。出现次数前K个和出现次数大于K。
           unordered_map<int,int>myhash;
           for(int i=0;i<nums.size();i++){
               myhash[nums[i]]++;//先统计各个元素出现的次数，然后将出现的次数排序，最后取出前K个出现次数搞得元素。对次数排序，取出元素，就用键值对，pair
           }
           vector<pair<int, int>> vec(myhash.begin(), myhash.end());//map转成vector
           sort(vec.begin(), vec.end(), cmp); // 给频率排个序.要学会如何自定义排序规则。
           for(int i=0;i<k;i++){
               result.push_back(vec[i].first);
           }
           return result;
       }
   };
   也可以对
   class Solution {
   public:
       // 小顶堆
       class mycomparison {
       public:
           bool operator()(const pair<int, int>& lhs, const pair<int, int>& rhs) {
               return lhs.second > rhs.second;
           }
       };
       vector<int> topKFrequent(vector<int>& nums, int k) {
           // 要统计元素出现频率
           unordered_map<int, int> map; // map<nums[i],对应出现的次数>
           for (int i = 0; i < nums.size(); i++) {
               map[nums[i]]++;
           }
   
           // 对频率排序
           // 定义一个小顶堆，大小为k
           priority_queue<pair<int, int>, vector<pair<int, int>>, mycomparison> pri_que;
           
           // 用固定大小为k的小顶堆，所有频率的数值 
           for (unordered_map<int, int>::iterator it = map.begin(); it != map.end(); it++) {
               pri_que.push(*it);
               if (pri_que.size() > k) { // 如果堆的大小大于了K，则队列弹出，保证堆的大小一直为k
                   pri_que.pop();
               }
           }
   
           // 找出前K个高频元素，因为小顶堆先弹出的是最小的，所以倒叙来输出到数组
           vector<int> result(k);
           for (int i = k - 1; i >= 0; i--) {
               result[i] = pri_que.top().first;
               pri_que.pop();
           }
           return result;
   
       }
   };
   
   ```

   8.带有最小值的栈

   ```c++
   一种方法是为每一个元素附带一个当前的最小值，但是在栈非常大时，会使用大量的空间记录最小值。class MinStack {
   private:
       stack<int> Stack;
       stack<int> minStack;
   public:
       /** initialize your data structure here. */
       MinStack() {
   
       }
       
       void push(int x) {
           Stack.push(x);
           if(minStack.empty() || minStack.top() > x){
               minStack.push(x);
           }
           else{
               minStack.push(minStack.top());//给每个元素赋值一个最小值，其实就是当前元素如果大于最小值的话把栈里面的最小值赋值给他。。。
           }
       }
       
       void pop() {
           Stack.pop();
           minStack.pop();
       }
       
       int top() {
           return Stack.top();
       }
       
       int getMin() {
           return minStack.top();
       }
   };
   一种更好的解决办法是将所有的最小值串起来放在一个单独的栈中。
   class MinStack {
   private:
       stack<int> Stack;
       stack<int> minStack;
   public:
       /** initialize your data structure here. */
       MinStack() {
   
       }
       
       void push(int x) {
           Stack.push(x);
           if(minStack.empty() || x <= minStack.top()){
               minStack.push(x);//只维护最小值
           }
       }
       
       void pop() {
           if(Stack.top() == minStack.top()){
               minStack.pop();//只有当主栈弹出到最小值的时候。最小栈才出栈，不然就会为空
           }
           Stack.pop();
       }
       
       int top() {
           return Stack.top();
       }
       
       int getMin() {
           return minStack.top();
       }
   };
   
   ```

   9.

### 二叉树

##### 基本知识

1. 树：节点组成的数据结构

2. 满二叉树：如果一棵二叉树只有度为0和度为2的节点，并且度为零的节点在同一层上

3. 完全（完整）二叉树：完全二叉树的定义如下：在完全二叉树中，除了最底层节点可能没填满外，其余每层节点数都达到最大值，并且最下面一层的节点都集中在该层最左边的若干位置。若最底层为第 h 层，则该层包含 1~ 2h 个节点

4. 二叉搜索树(二叉查找树，二叉排序树，BST):二叉搜索树是有数值的了，**「二叉搜索树是一个有序树」**。

   - **若它的左子树不空，则左子树上所有结点的值均小于它的根结点的值；**
   - **若它的右子树不空，则右子树上所有结点的值均大于它的根结点的值；**
   - **它的左、右子树也分别为二叉排序树**

5. 平衡二叉（搜索）树：又被称为**AVL**（Adelson-Velsky and Landis）树，具有二叉搜索树性质的前提下且具有以下性质：它是一棵空树或它的左右两个子树的高度差的绝对值不超过1，**并且左右两个子树都是一棵平衡二叉树。**

6. 红黑树：

7. 二叉堆（小顶堆和大顶堆）：![image-20210305171340044](C:\Users\小面包\AppData\Roaming\Typora\typora-user-images\image-20210305171340044.png)![image-20210305171355982](C:\Users\小面包\AppData\Roaming\Typora\typora-user-images\image-20210305171355982.png)

8. 二叉树的存储：链表和数组

9. 二叉树的遍历：深度优先和广度优先

10. 二叉树的定义：链式方式，每个节点都是一个对象

    ```c++
    struct TreeNode{
        int val;
        TreeNode *left;
        TreeNode *right;
        TreeNode(int x):val(x),left(null),right(null){}
    };
    ```

11. 创建二叉树的节点

    ```
    TreeNode*node=new TreeNode(元素值);
    ```

12. 二叉树节点的高度和深度：节点深度：指从根节点到该节点的最长简单路径边的条数。节点高度：指从该节点到叶子节点的最长简单路径边的条数。

13. 哈夫曼树：

14. B树：

15. 并查集：

##### 二叉树经典例题

###### 构造二叉树19.20

1. 根据中序和后序遍历序列构造二叉树：**首先要理解后序遍历是左右中，那序列最后一个元素肯定是根节点，先确定根节点，以此根节点为切割点，先去切割中序序列，这样中序就分成中左子树和中右子树，然后再去切割后序序列，后序序列切割点未知，但是和中序序列的左右子树的序列长度肯定是一样的，最后递归处理左右区间就行了**。两点需要注意的，1.切割方式，可以数组vector来保存，也可以使用下标索引2.对应递归函数，参数和返回值要清楚。  1.https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/  2.  https://leetcode-cn.com/problems/maximum-binary-tree/

###### 遍历二叉树（递归+迭代）1.2.3.4.5

1. 前序遍历：**先访问当前节点（cur），然后左右分别再访问其子节点**，根节点肯定第一个被访问。递归注意事项：1.确定递归函数的参数和返回值2，确定终止条件3.确定单层递归的逻辑。要根据题目要求去确定，想一下需要什么，需要的东西起什么作用。迭代方式：递归的底层实现就是栈原理**「递归的实现就是：每一次递归调用都会把函数的局部变量、参数值和返回地址等压入调用栈中」**，然后递归返回的时候，从栈顶弹出上一次递归的各项参数，所以这就是递归为什么可以返回上一层位置的原因。

   ```c++
   附上递归和迭代的代码，熟记
   递归：class Solution {
   public:
       void pre(TreeNode*cur,vector<int>&vec){
           if(cur==0)return ;
           vec.push_back(cur->val);
           pre(cur->left,vec);
           pre(cur->right,vec);
       }
       vector<int> preorderTraversal(TreeNode* root) {
           vector<int>result;
           pre(root,result);
           return result;
       }
   };
   迭代：BFS类型，出栈保存结果，这种首先先保存根节点，根节点首先入栈然后出栈保存。一层一层的考虑，结合左右中的特性。
   class Solution {
   public:
       vector<int> preorderTraversal(TreeNode* root) {
           vector<int>result;
           stack<TreeNode*>st;
           st.push(root);//和DFS的区别，这是首先入栈根节点然后开始循环遍历。
           while(!st.empty()){//栈上来就不是空的了
               TreeNode*node=st.top();
               st.pop();
               if(node!=nullptr)result.push_back(node->val);//
               else continue;//防止node为零，也可以分别加if(node!=null)然后st.push(node->right)，另外，continue跳出当前一个循环，后面的代码只是这一次不执行；然后继续下一次循环。break是直接退出所有循环。
               st.push(node->right);//有可能入栈空节点
               st.push(node->left);
           }
           return result;
       }
   };
   DFS类型，入栈即保存结果。指针node来访问节点，处理节点根据需要保存的结果来使用。
   class Solution {
   public:
       vector<int> preorderTraversal(TreeNode* root) {
           vector<int>result;
           stack<TreeNode*>st;
           TreeNode*cur=root;
           while(!st.empty()||cur!=nullptr){//cur!=null;因为一开始栈就是空的，先用节点不为空来开始遍历，遍历结束节点也是为空.st.empty()栈为空返回true.
               while(cur){
                   st.push(cur);
                   result.push_back(cur->val);
                   cur=cur->left;
               }
               cur=st.top();//左边遍历结束之后开始弹出遍历右边节点，同样判断当前节点的右边节点是否为空来入栈并且保存
               st.pop();
               cur=cur->right;
           }
           return result;
       }
   };
   ```

2. 中序遍历：左中右。迭代的时候注意处理节点和访问节点的过程，和前序遍历不同，DFS出栈保存结果

   ```c++
   递归：
       class Solution {
   public:
       vector<int> inorderTraversal(TreeNode* root) {
           vector<int>result;
           stack<TreeNode*>st;
           TreeNode*node=root;
           while(!st.empty()||node!=nullptr){
               while(node!=nullptr){
                   st.push(node);
                   node=node->left;
               }
               node=st.top();
               st.pop();
               result.push_back(node->val);
               node=node->right;
           }
           return result;
       }
   };
   迭代：DFS思想
   class Solution {
   public:
       vector<int> inorderTraversal(TreeNode* root) {
           vector<int>result;
           stack<TreeNode*>st;
           TreeNode*node=root;
           while(!st.empty()||node!=nullptr){
               while(node!=nullptr){//也可以ifelse
                   st.push(node);
                   node=node->left;
               }
               node=st.top();
               st.pop();
               result.push_back(node->val);
               node=node->right;
           }
           return result;
       }
   };
   ```

   3.后序遍历：左右中，迭代方式可以通过前序中左右-中右左-然后反转，也可以通过辅助指针来记录已经访问过的节点，好清楚左右节点谁返回的根节点，

   ```c++
   class Solution {
   public:
       vector<int> postorderTraversal(TreeNode* root) {
           stack<TreeNode*>st;
           vector<int>result;
           TreeNode*node=root;
           TreeNode*pre=nullptr;//辅助指针，记录已经访问过的节点
           while(!st.empty()||node!=nullptr){
               while(node!=nullptr){
                   st.push(node);
                   node=node->left;
               }
               node=st.top();//取得栈顶节点，开始访问当前节点的右子树，第一次的当前节点就是最左边的节点。
               if(node->right==nullptr||node->right==pre){//右边没有节点或者右边节点已经访问过，直接保存该节点
                   result.push_back(node->val);
                   st.pop();
                   pre=node;////访问过的节点标记
                   node=nullptr;//防止把栈中已经有的节点再次入栈，根据实例情况推出的
               }
               else{//右边节点还未访问过直接访问
                   node=node->right;
               }
           }
           return result;        
       }
   };
   ```

   4.层序遍历：队列实现层序遍历，其中每层的元素个数要添加到数组中，利用循环添加，而循环的次数就是要添加的元素的个数

   ```c++
   class Solution {
   public:
       vector<vector<int>> levelOrder(TreeNode* root) {
           vector<vector<int>>result;
           queue<TreeNode*>qu;
           TreeNode*node=root;
           if(root!=nullptr)qu.push(node);
           while(!qu.empty()){//怎么保存一层的元素呢？肯定要循环添加，怎么循环呢？？循环的时候添加的元素的个数就是循环的次数
              int size=qu.size();//一开始的size要固定，因为后面添加的时候size是在变化的
              vector<int>ans;
               while(size--){//for循环也行。
                   TreeNode*cur=qu.front();
                   qu.pop();
                   ans.push_back(cur->val);
                   if(cur->left)qu.push(cur->left);
                   if(cur->right)qu.push(cur->right);
               }
               result.push_back(ans);
           }
           return result;
       }
   };
   ```

   5.N叉树的层序遍历

   ```c++
   class Solution {
   public:
       vector<vector<int>> levelOrder(Node* root) {
           queue<Node*> que;
           if (root != NULL) que.push(root);
           vector<vector<int>> result;
           while (!que.empty()) {
               int size = que.size();
               vector<int> vec;
               for (int i = 0; i < size; i++) { 
                   Node* node = que.front();
                   que.pop();
                   vec.push_back(node->val);
                   for (int i = 0; i < node->children.size(); i++) { // 将节点孩子加入队列
                       if (node->children[i]) que.push(node->children[i]);
                   }
               }
               result.push_back(vec);
           }
           return result;
   
       }
   };
   ```

###### 修改二叉树6，22

1.翻转二叉树   递归从上向下或者从下向上都行

```c++
递归：注意节点也代表整个树。class Solution {
public:
    void pre(TreeNode*root){
        if(root==nullptr)return ;
        swap(root->left,root->right);//先交换再递归直到叶子节点。
        pre(root->left);
        pre(root->right);
    }
    TreeNode* invertTree(TreeNode* root) {
        pre(root);
        return root;
    }
};
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if (root == nullptr) {
            return nullptr;
        }
        TreeNode* left = invertTree(root->left);//直接递归到叶子节点，然后开始交换
        TreeNode* right = invertTree(root->right);
        root->left = right;
        root->right = left;
        return root;
    }
};
迭代：层序遍历，每层交换下节点就行
    class Solution{
    public:
    TreeNode* invertTree(TreeNode* root) {
        if(root==nullptr)return root;
        queue<TreeNode*>qu;
        TreeNode*node=root;
        qu.push(node);
        while(!qu.empty()){
            int size=qu.size();
            for(int i=0;i<size;i++){
                TreeNode*cur=qu.front();
                qu.pop();
                swap(cur->left,cur->right);
                if(cur->left)qu.push(cur->left);
                if(cur->right)qu.push(cur->right);
            }
        }
        return root;
    }
};
```

2，合并二叉树

```c++
递归：class Solution {
public:
    TreeNode* mergeTrees(TreeNode* root1, TreeNode* root2) {
        //if(root2==nullptr&&root1==nullptr)return root2;
        if(root1==nullptr)return root2;
        if(root2==nullptr)return root1;
        TreeNode*node=new TreeNode(root2->val+root1->val);
        node->left=mergeTrees(root1->left,root2->left);//返回值的问题想一想，
        node->right=mergeTrees(root1->right,root2->right);//
        return node;
    }
};
```

###### 二叉树公共祖先

1. 二叉树的最近公共祖先

   ```c++
   搜索一条边的写法：
   
   if (递归函数(root->left)) return ;
   
   if (递归函数(root->right)) return ;
   
   搜索整个树写法：
   
   left = 递归函数(root->left);
   right = 递归函数(root->right);
   left与right的逻辑处理;
   
   「在递归函数有返回值的情况下：如果要搜索一条边，递归函数返回值不为空的时候，立刻返回，如果搜索整个树，直接用一个变量left、right接住返回值，这个left、right后序还有逻辑处理的需要，也就是后序遍历中处理中间节点的逻辑（也是回溯）
   
       递归：class Solution {
   public:
   //1.x要是p,q的祖先，2.x的深度要尽可能大（高度小就是离叶子节点近或者离根节点远），从上向下找到的节点（公共祖先）不一定是深度最大的，但是从小向上找到的节点一定是高度最小的。这样就是后序遍历。另外，x如何是q和p的祖先？1.x的左子树找到q,右子树找到p；或者x的左子树找到p，右子树找到q；或者在左子树或者右子树里面，这时在非空的子树找到的第一个节点就是p或者q，也就是公共祖先2.x是p或者q，此时一定直接返回x就行,这是左右子树都不为空但是还是在同一个左子树或者同一个右子树中，在第一行就包括了，因为如果只在一个子树中，那么另外一个子树遍历结束也是空，或者可以直接看作空。
       TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
           if(root==NULL||root==q||root==p)return root;
           TreeNode*lefttree=lowestCommonAncestor(root->left,p,q);
           TreeNode*righttree=lowestCommonAncestor(root->right,p,q);
           if(lefttree&&righttree)return root;
           if(lefttree==NULL)return righttree;
           if(righttree==NULL)return lefttree;
           return NULL;
       }
   };
   ```

   

###### 二叉树匹配问题

1. 检查子树

   ```c++
   /**
    * Definition for a binary tree node.
    * struct TreeNode {
    *     int val;
    *     TreeNode *left;
    *     TreeNode *right;
    *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
    * };
    */
   class Solution {
   public:
       //当已经在A中找到B根节点
       bool dfs(TreeNode*A,TreeNode*B){
           //递归-首先是终止条件
           if(A==NULL&&B==NULL){//先把都为空的条件列出来，
               return true;
           }
           if(A==NULL||B==NULL){//默认一个为空一个不为空了，都为空的已经先判断了
               return false;
           }
           if(A->val==B->val){//都不为空就比较二者是否相等，相等就返回继续比较下一个节点.虽然已经确定根节点但是要看后序的节点是否相等。
              return true;
           }else {
               return false;
           }
           return dfs(A->left,B->left)&&dfs(A->right,B->right);
       }
   
       //但是首先要知道如何在A中找到一个B，主函数就是在A中找到和B相等的节点
       bool checkSubTree(TreeNode* t1, TreeNode* t2) {
           if(t1==NULL)return false;
           //如果首节点就相等，比较后序的节点
           //如果首节点不相等，就比较A的左子树或者右子树的节点是否有节点和B的根节点相等
           return dfs(t1,t2)||checkSubTree(t1->left,t2)||checkSubTree(t1->right,t2);
   
       }
   };
   ```

   

2. 树的子结构

   ```c++
   /**
    * Definition for a binary tree node.
    * struct TreeNode {
    *     int val;
    *     TreeNode *left;
    *     TreeNode *right;
    *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
    * };
    */
   class Solution {
   public:
   //当已经在A中找到和B相同的节点C时
       bool dfs(TreeNode*C,TreeNode*B){
           //递归-终止条件.考虑下一个节点来写终止条件的代码
           if(B==NULL)return true;
           //默认B已经不是空集了
           if(C==NULL||C->val!=B->val)return false;
           //如果节点值相等就继续同时遍历AB两棵树，A左对应B左，A右对应B右
           return dfs(C->left,B->left)&&dfs(C->right,B->right);
       }
       bool isSubStructure(TreeNode* A, TreeNode* B) {
           if(A==NULL||B==NULL)return false;
           //要知道如何在A中找和B相等的节点。首先根节点相等的话直接继续比较就行，否则在A的左子树找，找不到就再在A的右子树找
           return dfs(A,B)||isSubStructure(A->left,B)||isSubStructure(A->right,B);
       }
   };
   ```

   

3. 

###### 二叉树的属性8.9.10.11.12.13.15.16.17.18

1. **对称二叉树：首先考虑空节点，之后也比较简单**

   ```c++
   递归：
   class Solution {
   public:
       bool tree(TreeNode*l,TreeNode*r){
           if(l==nullptr&&r==nullptr)return true;
           if((l==nullptr&&r!=nullptr)||(l!=nullptr&&r==nullptr))return false;
           return (l->val==r->val)&&tree(l->left,r->right)&&tree(l->right,r->left);
       }
       bool isSymmetric(TreeNode* root) {
           return tree(root->left,root->right);
       }
   };
   迭代：使用队列
       class Solution {
   public:
       bool isSymmetric(TreeNode* root) {
           queue<TreeNode*>qu;//类似BFS，层序遍历，先入队列节点
           qu.push(root->left);
           qu.push(root->right);
           while(!qu.empty()){//先入直接考虑队列不为空，
               TreeNode*l=qu.front();
               qu.pop();
               TreeNode*r=qu.front();
               qu.pop();
               //if(l==nullptr&&r==nullptr)continue;
               if(!l&&!r)continue;
               // if((l==nullptr&&r!=nullptr)||(l!=nullptr&&r==nullptr))return false;
               // if(l!=nullptr&&r!=nullptr&&(l->val!=r->val))return false;
               if(!l||!r||l->val!=r->val)return false;
               qu.push(l->left);
               qu.push(r->right);
               qu.push(l->right);
               qu.push(r->left);
           }
           return true;
       }
   };
   迭代：使用栈
       
   ```

2. 二叉树的最大深度：

   ```c++
   递归：代码的逻辑其实是求的根节点的高度，而根节点的高度就是这颗树的最大深度，所以才可以使用后序遍历。」
       先求左子树的深度，再求右子树的深度，最后取最大的，N叉树同理，对第二层的所有子树进行比较
   class Solution {
   public:
       int maxDepth(TreeNode* root) {
           if(root==nullptr)return 0;
           int leftmax=maxDepth(root->left);
           int rightmax=maxDepth(root->right);
           return 1+max(leftmax,rightmax);
       }
   };
   其实应该这样：class Solution {
   public:
       int result;
       void getDepth(TreeNode* node, int depth) {
           result = depth > result ? depth : result; // 中
   
           if (node->left == NULL && node->right == NULL) return ;
   
           if (node->left) { // 左
               depth++;    // 深度+1
               getDepth(node->left, depth);
               depth--;    // 回溯，深度-1
           }
           if (node->right) { // 右
               depth++;    // 深度+1
               getDepth(node->right, depth);
               depth--;    // 回溯，深度-1
           }
           return ;
       }
       int maxDepth(TreeNode* root) {
           result = 0;
           if (root == 0) return result;
           getDepth(root, 1);
           return result;
       }
   };
   迭代:就是求其有多少层，关键是a加在什么地方，要知道大循环一次就是结束一层。
   class Solution {
   public:
       int maxDepth(TreeNode* root) {
           int a=0;
           if(root==nullptr)return 0;
           queue<TreeNode*>qu;
           qu.push(root);
           while(!qu.empty()){
               int size=qu.size();
               a+=1;//看有多少层就是size归0重置了几次
               while(size--){
                   //if(size==0)a+=1;
                   TreeNode*node=qu.front();
                   qu.pop();
                   if(node->left)qu.push(node->left);
                   if(node->right)qu.push(node->right);
               }
           }
           return a;
       }
   };
   ```

   3.二叉树的最小深度：注意和最大深度的区别，有在同一侧的特殊情况。

   ```c++
   递归：注意到特殊情况，而最大深度不用考虑，因为是返回最大的值。
   class Solution {
   public:
       int minDepth(TreeNode* root) {
           if(root==nullptr)return 0;
           if(root->left==nullptr)return minDepth(root->right)+1;
           if(root->right==nullptr)return minDepth(root->left)+1;
           return min(minDepth(root->left),minDepth(root->right))+1;
       }
   };
   迭代：注意是叶子节点才是满足条件的。
       class Solution {
   public:
       int minDepth(TreeNode* root) {
           if(root==nullptr)return 0;
           queue<TreeNode*>qu;
           qu.push(root);
           int result=0;
           while(!qu.empty()){
               int size=qu.size();
               result+=1;
               for(int i=0;i<size;i++){
                   TreeNode*node=qu.front();
                   qu.pop();
                   if(node->left)qu.push(node->left);
                   if(node->right)qu.push(node->right);
                   if(node->left==nullptr&&node->right==nullptr)return result;//利用return的特性，如果是找到答案直接返回答案。也可以设计标记，当遇到叶子节点标记，并且退出当前循环。另外，退出大循环直接if（flag==1）break；
               }
           }
           return result;
       }
   };
   ```

   4.完全二叉树的节点：

   ```c++
   递归:不就等于左子树节点+右子树+1（根节点）
   class Solution {
   public:
       int countNodes(TreeNode* root) {
           if(root==nullptr)return 0;
           int leftnode=countNodes(root->left);
           int rightnode=countNodes(root->right);
           return leftnode+rightnode+1;
       }
   };
   迭代：class Solution {
   public:
       int countNodes(TreeNode* root) {
           if(root==nullptr)return 0;
           queue<TreeNode*>qu;
           qu.push(root);
           int sum=0;
           while(!qu.empty()){
               int size=qu.size();
               sum+=size;//就是求每层的个数之和，每层的个数就是size的数值。
               for(int i=0;i<size;i++){
                   TreeNode*node=qu.front();
                   qu.pop();
                   //sum++;或者统计每个节点的个数也行
                   if(node->left)qu.push(node->left);
                   if(node->right)qu.push(node->right);
               }
           }
           return sum;
       }
   };
   ```

   5**.平衡二叉树：**

   ```c++
   递归：自顶向下递归
       class Solution {
   public:
       int h(TreeNode*root){
           if(root==nullptr)return 0;
           else{
               return max(h(root->left),h(root->right))+1;
           }
       }
       bool isBalanced(TreeNode* root) {
           if(root==nullptr)return true;
           else{
               return isBalanced(root->left)&&isBalanced(root->right)&&(abs(h(root->left)-h(root->right))<=1);
           }
       }
   };
   自底向上递归:如果当前传入节点为根节点的二叉树已经不是二叉平衡树了，还返回高度的话就没有意义了。
   所以如果已经不是二叉平衡树了，可以返回-1 来标记已经不符合平衡树的规则了。
   class Solution {
   public:
       int height(TreeNode* root) {
           if (root == NULL) {
               return 0;
           }
           int leftHeight = height(root->left);
           int rightHeight = height(root->right);
           if (leftHeight == -1 || rightHeight == -1 || abs(leftHeight - rightHeight) > 1) {
               return -1;
           } else {
               return max(leftHeight, rightHeight) + 1;
           }
       }
   
       bool isBalanced(TreeNode* root) {
           return height(root) >= 0;
       }
   };
   ```

   6**.二叉树的所有路径：**

   ```c++
   递归：关注当前节点和当前节点的孩子，如果当前节点不为零，并且其左右孩子都为零，就是叶子节点，加入结果，否则递归计算。
   class Solution {
   public:
       void pre(TreeNode*root,string path,vector<string>&result){
           if(root!=nullptr){
               path+=to_string(root->val);
               if(root->left==nullptr&&root->right==nullptr){
                   result.push_back(path);
                   //return ;
               }else{
                   pre(root->left,path+"->",result);//这题例子先执行这个
                   pre(root->right,path+"->",result);
                   
               }
           }
       }
       vector<string> binaryTreePaths(TreeNode* root) {
           vector<string>result;
           pre(root,"",result);
           return result;
       }
   };
   递归：
   class Solution {
   private:
   
       void traversal(TreeNode* cur, string path, vector<string>& result) {
           path += to_string(cur->val); // 中
           if (cur->left == NULL && cur->right == NULL) {
               result.push_back(path);
               return;
           }
           if (cur->left) traversal(cur->left, path + "->", result); // 左
           if (cur->right) traversal(cur->right, path + "->", result); // 右
       }
   
   public:
       vector<string> binaryTreePaths(TreeNode* root) {
           vector<string> result;
           string path;
           if (root == NULL) return result;
           traversal(root, path, result);
           return result;
   
       }
   };
   迭代：两个队列分别存储路径和结果
       
   
   ```

   7.二叉树左叶子之和：

   ```c++
   递归:左叶子定义：一个节点的左节点并且这个左节点为叶子节点（隐含该节点不为零），然后遍历就行
   class Solution {
   public:
       void pre(TreeNode*root,int&sum){
           if(root==NULL)return;
           if(root->left!=NULL&&root->left->left==NULL&&root->left->right==NULL){
               sum+=root->left->val;
               //return ;//
           }
           if(root->left)pre(root->left,sum);//遍历的时候注意节点不为零
           if(root->right)pre(root->right,sum);
       }
       int sumOfLeftLeaves(TreeNode* root) {
           int result=0;
           pre(root,result);
           return result;
       }
   };
   //或者用带返回值的函数
   class Solution {
   public:
       int sumOfLeftLeaves(TreeNode* root) {
           if (root == NULL) return 0;
   
           int leftValue = sumOfLeftLeaves(root->left);    // 左
           int rightValue = sumOfLeftLeaves(root->right);  // 右
                                                           // 中
           int midValue = 0;
           if (root->left && !root->left->left && !root->left->right) { // 中
               midValue = root->left->val;
           }
           int sum = midValue + leftValue + rightValue;
           return sum;
       }
   };
   //或者总的叶子节点减去右边的叶子节点
   class Solution {
   public:
       void pre(TreeNode*root,int &sum){
           if(root->left==NULL&&root->right==NULL){
               sum+=root->val;
               return;
           }
           if(root->left)pre(root->left,sum);
           if(root->right){
               pre(root->right,sum);
               if(root->right->left==NULL&&root->right->right==NULL){
                   sum-=root->right->val;
               }
           }
       }
       int sumOfLeftLeaves(TreeNode* root) {
           if(root==NULL)return 0;
           if(root->left==NULL&&root->right==NULL)return 0;
           int result=0;
           pre(root,result);
           return result;
       }
   //迭代同理
       class Solution {
   public:
       int sumOfLeftLeaves(TreeNode* root) {
           queue<TreeNode*>qu;
           if(root==NULL)return 0;
           int result=0;
           qu.push(root);
           while(!qu.empty()){
               TreeNode*node=qu.front();
               qu.pop();
               if(node->left!=NULL&&node->left->left==NULL&&node->left->right==NULL){
                   result+=node->left->val;
               }
               if(node->left)qu.push(node->left);
               if(node->right)qu.push(node->right);
           }
           return result;
       }
   };
   ```

   8.二叉树路径之和

   ```c++
   递归：根节点到当前节点的和为val，然后当前节点到叶子节点的值就为sum-val。
   class Solution {
   public:
       bool hasPathSum(TreeNode *root, int sum) {
           if (root == nullptr) {
               return false;
           }
           if (root->left == nullptr && root->right == nullptr) {
               return sum == root->val;
           }
           return hasPathSum(root->left, sum - root->val) ||
                  hasPathSum(root->right, sum - root->val);
       }
   };
   或者求所有路径然后再选择。
   
   ```

###### 构造二叉搜索树-二叉搜索树中序遍历是升序的。

1. 将有序数组转换为二叉搜索树：

   ```c++
   取中间元素已经是平衡的了，不用在比较高度。
   class Solution {
   public:
       TreeNode*ctree(vector<int>&nums,int i,int j){
           if(i>j){
               return NULL;
           }
           int mid=(i+j)/2;
           TreeNode*node=new TreeNode(nums[mid]);
           node->left=ctree(nums,i,mid-1);
           node->right=ctree(nums,mid+1,j);
           return node;
       }
       TreeNode* sortedArrayToBST(vector<int>& nums) {
           return ctree(nums,0,nums.size()-1);
       }
   };
   ```

###### 修改二叉搜索树

1. 二叉搜索树的插入

   二叉搜索树的特性：节点数值：左<中<右；中序遍历有序

   ```c++
   递归:看当前节点的数值和插入的数值的大小，其实思想是一样的，另外就是当遇到空节点时插入节点（新生成节点）要连接到父节点才行。root->left=in(root->left);
   class Solution {
   public:
       TreeNode* insertIntoBST(TreeNode* root, int val) {
           if(root==nullptr)return new TreeNode(val);
           if(root->val>val){
               root->left=insertIntoBST(root->left,val);//新生成节点连接父节点。结合边界条件，融合到这一句话内。
           }
           if(root->val<val){
               root->right=insertIntoBST(root->right,val);
           }
           return root;
       }
   };
   迭代：class Solution {
   public:
       TreeNode* insertIntoBST(TreeNode* root, int val) {
           if(root==nullptr)return new TreeNode(val);
           TreeNode*node=root;//在node上操作，遍历节点会改变root的值
           while(node){//迭代肯定要有循环
               if(node->val>val){
               if(node->left==nullptr){
                   node->left=new TreeNode(val);
                   break;
               }
               else{
                   node=node->left;
               }
           }
           if(node->val<val){
               if(node->right==nullptr){
                   node->right=new TreeNode(val);
                   break;
               }
               else{
                   node=node->right;
               }
           }
   
           }
           return root;
       }
   };
   
   ```

2. 删除二叉搜索树的节点

   ```c++
   考虑各种情况，删除节点涉及结构调整。
   class Solution {
   public:
       TreeNode* deleteNode(TreeNode* root, int key) {
           if(root==nullptr){return root;}
           if(root->val==key){
               if(root->left!=nullptr&&root->right==nullptr){
                   root=root->left;
                   return root;
               }
               if(root->right!=nullptr&&root->left==nullptr){
                   root=root->right;
                   return root;
               }
               if(root->left==nullptr&&root->right==nullptr){
                   root=nullptr;
                   return root;
               }
               if(root->left&&root->right){//将左子树节点放在右子树最下面左孩子的左孩子上
                   TreeNode *cur=root->right;
                   while(cur->left!=nullptr){
                       cur=cur->left;
                   }
                   cur->left=root->left;
                   TreeNode*ans=root;//root要在赋值前删除，先保存一下root,然后赋值，然后删除
                   root=root->right;
                   delete ans;
                   return root;
               }
           }
           if(root->val>key){
               root->left=deleteNode(root->left,key);//赋值都是从右向左看，这样就理解返回的节点和父节点建立的关系了。
           }
           if(root->val<key){
               root->right=deleteNode(root->right,key);
           }
           return root;
       }
   };
   ```

   

3. **修剪二叉搜索树：深刻理解递归的经典题目！**

   ```c++
   递归：从谁递归看返回值从哪返回，递归和回溯同时存在，注意实际的遍历过程。返回值切记！！！
   class Solution {
   public:
       TreeNode* trimBST(TreeNode* root, int low, int high) {
           if (root == nullptr ) return nullptr;
           if (root->val < low) {
               TreeNode* right = trimBST(root->right, low, high); // 寻找符合区间[low, high]的节点
               return right;
           }
           if (root->val > high) {
               TreeNode* left = trimBST(root->left, low, high); // 寻找符合区间[low, high]的节点
               return left;
           }
           root->left = trimBST(root->left, low, high); // root->left接入符合条件的左孩子
           root->right = trimBST(root->right, low, high); // root->right接入符合条件的右孩子
           return root;
       }
   };
   迭代：迭代是题目的直观体现
    class Solution {
   public:
       TreeNode* trimBST(TreeNode* root, int low, int high) {
           if(root==nullptr)return root;
           while(root&&(root->val<low||root->val>high)){
               if(root->val<low)root=root->right;
               if(root->val>high)root=root->left;
           }//确保根节点在范围内，那就左子树找小于low的，右子树找大于low的
           auto l=root;//所有左子树都小于根节点，所以只看左子树的左子树就行
           while(l&&l->left){
               if(l->left->val<low)l->left=l->left->right;
               else{
                   l=l->left;
               }
           }
           auto r=root;////右子树同理
           while(r&&r->right){
               if(r->right->val>high)r->right=r->right->left;
               else{
                   r=r->right;
               }
           }
           return root;
       }
   };
   ```

   

###### 二叉搜索树的属性

1. 二叉搜索树中的搜索： **迭代：注意if和else if的区别，多个if是并列，if+else if+else 是分枝。本题root继续执行会改变，注意别搞错了。**

   ```c++
   递归：return 的使用
   class Solution {
   public:
       TreeNode* searchBST(TreeNode* root, int val) {
           if(root==nullptr)return root;
           if(root->val==val)return root;
           if(root->val>val){
               auto l=searchBST(root->left,val);
               return l;//这里需要return的原因是找到就返回该节点，并不是要找树的所有节点，注意遍历整棵树和遍历到找到的节点就停的区别。
           }
           if(root->val<val){
               auto r=searchBST(root->right,val);
               return r;
           }
           return nullptr;
       }
   };
   迭代：注意if和else if的区别，多个if是并列，if+else if+else 是分枝。本题root继续执行会改变，注意别搞错了。
   class Solution {
   public:
       TreeNode* searchBST(TreeNode* root, int val) {
           while (root != NULL) {
               if (root->val > val) root = root->left;
               else if (root->val < val) root = root->right;
               else return root;
           }
           return NULL;
       }
   };
   ```

   2.**验证二叉搜索树：就是看这棵树的中序遍历是不是升序的！！！**另外要清楚是左子树的所有节点都小于根节点，右子树的所有节点都大于根节点。易错点。如何判断都小于都大于，遍历比较数值即可。

   ```c++
   错误递归：这只是比较了当前一棵树的节点大小，并没有包含子树所有的节点都小于根节点
       class Solution {
   public:
       bool isValidBST(TreeNode* root) {
           if(root==nullptr)return true;
           if(root->left){//这只是比较了当前一棵树的节点大小，并没有包含子树所有的节点都小于根节点
               if(root->val>root->left->val){
                    isValidBST(root->left);//没找到就继续遍历，找到了就返回false.
               }else return false;
           }
           if(root->right){
               if(root->val<root->right->val){
                    isValidBST(root->right);
               }else return false;
           }
           return true;
       }
   };
   正确递归：class Solution {
   public:
       TreeNode* pre = NULL; // 用来记录前一个节点 
       bool isValidBST(TreeNode* root) {
           if (root == NULL) return true;
           bool left = isValidBST(root->left);
   
           if (pre != NULL && pre->val >= root->val) return false;
           pre = root; // 记录前一个节点
   
           bool right = isValidBST(root->right);
           return left && right;
       }
   };
   
   class Solution {
   public:
       long long maxVal = LONG_MIN; // 因为后台测试数据中有int最小值
       bool isValidBST(TreeNode* root) {
           if (root == NULL) return true;
   
           bool left = isValidBST(root->left);
           // 中序遍历，验证遍历的元素是不是从小到大
           if (maxVal < root->val) maxVal = root->val;
           else return false;
           bool right = isValidBST(root->right);
   
           return left && right;
       }
   };
   迭代也行
   ```

   3.二叉搜索树的最小绝对差，涉及到二叉搜索树的最值，差值之类的都要先考虑下是否有序，可以直接转成数组计算，另外就是递归过程中使用双指针来计算！！

   ```c++
   中序递归：
   class Solution {
   public:
       int result=INT_MAX;
       TreeNode*pre=NULL;//记录前一个节点，当前节点改变之前把当前节点先记录下来。
       void mid(TreeNode*root){
           if(root==NULL)return;
           mid(root->left);
           if(pre){
               result=min(result,root->val-pre->val);}
           pre=root;////
           mid(root->right);
       }
       int getMinimumDifference(TreeNode* root) {
           mid(root);
           return result;
       }
   };
   ```

   4.二叉搜索树的众数

   ```c++
   模拟一下，也不难：class Solution {
   public:
       vector<int>result;
       vector<int>ans;
       void mid(TreeNode*root){
           if(root==NULL){return ;}
           mid(root->left);
           result.push_back(root->val);
           mid(root->right);
       }
       vector<int> findMode(TreeNode* root) {
           mid(root);
           int count=1;
           int maxcount=0;
           // if(result.size()==1){return result;}
           for(int i=0;i<result.size();i++){
               if(i>0&&result[i]==result[i-1]){//这里利用了二叉搜索树的特性，中序遍历是有序的
                   count++;
               }
               else{
                   count=1;
               }
               if(count==maxcount){
                   ans.push_back(result[i]);
               }
               if(count>maxcount){
                   maxcount=count;
                   ans.clear();
                   ans.push_back(result[i]);
               }
           }
           return ans;
       }
   };
   //统计两次，暴力解法了，不过这种解法对于求二叉树的公共祖先也是可以的
   class Solution {
   public:
       vector<int>result;
       vector<int>ans;
       void mid(TreeNode*root){
           if(root==NULL){return ;}
           mid(root->left);
           result.push_back(root->val);
           mid(root->right);
       }
       vector<int> findMode(TreeNode* root) {
           mid(root);
           map<int,int>mymap;
           for(int i=0;i<result.size();i++){
               mymap[result[i]]++;
           }
           int m=INT_MIN;//这里也可以对map中的value数值进行排序，
           for(auto j=mymap.begin();j!=mymap.end();j++){
               if(j->second>m){
                   m=j->second;
               }
           }
           for(auto j=mymap.begin();j!=mymap.end();j++){
               if(j->second==m){
                   ans.push_back(j->first);
               }
           }
           return ans;
       }
   };
   
   利用双指针来计算，不用遍历先把元素放到数组中了，直接在遍历的过程中开始比较、统计
    class Solution {
   private:
       int maxCount; // 最大频率
       int count; // 统计频率
       TreeNode* pre;
       vector<int> result;
       void searchBST(TreeNode* cur) {
           if (cur == NULL) return ;
   
           searchBST(cur->left);       // 左
                                       // 中
           if (pre == NULL) { // 第一个节点
               count = 1;
           } else if (pre->val == cur->val) { // 与前一个节点数值相同
               count++;
           } else { // 与前一个节点数值不同
               count = 1;
           }
           pre = cur; // 更新上一个节点
   
           if (count == maxCount) { // 如果和最大值相同，放进result中
               result.push_back(cur->val);
           }
   
           if (count > maxCount) { // 如果计数大于最大值频率
               maxCount = count;   // 更新最大频率
               result.clear();     // 很关键的一步，不要忘记清空result，之前result里的元素都失效了
               result.push_back(cur->val);
           }
   
           searchBST(cur->right);      // 右
           return ;
       }
   
   public:
       vector<int> findMode(TreeNode* root) {
           count = 0; 
           maxCount = 0;
           TreeNode* pre = NULL; // 记录前一个节点
           result.clear();
   
           searchBST(root);
           return result;
       }
   };
   ```

   5.二叉搜索树转化为累加树

   ```c++
   class Solution {
   public:
       int sum=0;
       TreeNode* convertBST(TreeNode* root) {
           if(root!=nullptr){
               convertBST(root->right);//无返回值？？最终有返回值就行
               sum+=root->val;
               root->val=sum;
               convertBST(root->left);
           }
           return root;
       }
   };
   //二者是一样的，一个先把节点为空确定然后返回，另外一个先把节点不为空进行循环，节点为空自然也是返回。写代码的方式不同，要多练习！！
   class Solution {
   public:
       int pre=0;////注意是只改变数值，不改变节点位置
       void mid(TreeNode*root){//void还是非void要看是否要遍历整棵树，还是到哪里就停止
           if(root==nullptr)return ;
           mid(root->right);
           root->val+=pre;//归
           pre=root->val;
           mid(root->left);
       }
       TreeNode* convertBST(TreeNode* root) {//确定了反中序遍历，但是代码没写对！！
           if(root==nullptr)return root;
           mid(root);
           return root;
       }
   };
   ```

   

###### 二叉搜索树的公共祖先

**区分二叉树的公共祖先，特别是递归写法，一个在没有约束条件下递归整棵树，一个是在约束条件下递归到满足条件的就返回。**

```c++
递归：区分二叉树的公共祖先，特别是递归写法，一个在没有约束条件下递归整棵树，一个是在约束条件下递归到满足条件的就返回。
class Solution {
private:
    TreeNode* traversal(TreeNode* cur, TreeNode* p, TreeNode* q) {
        if (cur == NULL) return cur;
                                                        // 中
        if (cur->val > p->val && cur->val > q->val) {   // 左，加了判断条件的递归不会遍历整棵树了，直接返回，出栈的时候出的是一开始返回的值。
            TreeNode* left = traversal(cur->left, p, q);
            if (left != NULL) {
                return left;
            }
        }

        if (cur->val < p->val && cur->val < q->val) {   // 右
            TreeNode* right = traversal(cur->right, p, q);
            if (right != NULL) {
                return right;
            }
        }
        return cur;
    }
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        return traversal(root, p, q);
    }
};

迭代：class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        while(root) {
            if (root->val > p->val && root->val > q->val) {
                root = root->left;
            } else if (root->val < p->val && root->val < q->val) {
                root = root->right;
            } else return root;
        }
        return NULL;
    }
};

//也可以找路径来判断，学习一下程序，搜索树可以这样，普通二叉树就不行，普通二叉树不知道每个节点的数值
class Solution {
public:
    vector<TreeNode*> getPath(TreeNode* root, TreeNode* target) {
        vector<TreeNode*> path;
        TreeNode* node = root;
        while (node != target) {
            path.push_back(node);
            if (target->val < node->val) {
                node = node->left;
            }
            else {
                node = node->right;
            }
        }
        path.push_back(node);
        return path;
    }

    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        vector<TreeNode*> path_p = getPath(root, p);
        vector<TreeNode*> path_q = getPath(root, q);
        TreeNode* ancestor;
        for (int i = 0; i < path_p.size() && i < path_q.size(); ++i) {
            if (path_p[i] == path_q[i]) {
                ancestor = path_p[i];
            }
            else {
                break;//最后一个不相同的就是公共祖先，
            }
        }
        return ancestor;
    }
};


```



### 回溯

##### 基本知识

1. 如何理解回溯？：穷举方式的一种，就是一种搜索方式，列出所有可能，然后选出我们想要的答案。又称为试探法，常用于需要记录节点状态的深度优先搜索。

2. 回溯一般可以解决如下几种问题：**组合问题：N个数里面按一定规则找出k个数的集合**
   **排列问题：N个数按一定规则全排列，有几种排列方式**。组合不强调元素顺序，而排列强调元素顺序。
   **切割问题：一个字符串按一定规则有几种切割方式**
   **子集问题：一个N个数的集合里有多少符合条件的子集**
   **棋盘问题：N皇后，解数独等等**。

3. 如何用回溯法解决问题：都可以抽象为树形结构，在搜索到某一节点的时候，如果我们发现目前的节点（及 其子节点）并不是需求目标时，我们回退到原来的节点继续搜索，并且把在目前节点修改的状态 还原。这样的好处是我们可以始终只对图的总状态进行修改，而非每次遍历时新建一个图来储存 状态。在具体的写法上，它与普通的深度优先搜索一样，都有 [修改当前节点状态]→[递归子节 点] 的步骤，只是多了回溯的步骤，变成了 [修改当前节点状态]→[递归子节点]→[回改当前节点 状态]。模板

   ```
   回溯方法的模板：
   ```

   

   



##### 经典例题

### 思想3：分治

##### 基本知识

### 编程技巧：递归

##### 基本知识

1. 如何理解递归？

   递归百科解释：程序调用自身的**编程技巧**称为递归（ recursion）。递归做为一种[算法](https://link.zhihu.com/?target=https%3A//baike.baidu.com/item/%E7%AE%97%E6%B3%95)在[程序设计语言](https://link.zhihu.com/?target=https%3A//baike.baidu.com/item/%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1%E8%AF%AD%E8%A8%80)中广泛应用。 一个过程或[函数](https://link.zhihu.com/?target=https%3A//baike.baidu.com/item/%E5%87%BD%E6%95%B0)在其定义或说明中有直接或间接调用自身的一种方法，**它通常把一个大型复杂的问题层层转化为一个与原问题相似的规模较小的问题来求解**，递归策略只需少量的程序就可描述出解题过程所需要的多次重复计算，大大地减少了程序的代码量。递归的能力在于用有限的[语句](https://link.zhihu.com/?target=https%3A//baike.baidu.com/item/%E8%AF%AD%E5%8F%A5)来定义对象的[无限集合](https://link.zhihu.com/?target=https%3A//baike.baidu.com/item/%E6%97%A0%E9%99%90%E9%9B%86%E5%90%88)。一般来说，**递归需要有边界条件、递归前进段和递归返回段。当边界条件不满足时，递归前进；当边界条件满足时，递归返回。。迭代是从前往后计算的，而递归则是先从后往前推，然后再由前往后计算，有“递”又有“归”。**

2. 递归的运行时间计算

   ：画出递归树，递归算法运行时间=节点数=调用的次数

   ![image-20210223082421596](C:\Users\zpp\AppData\Roaming\Typora\typora-user-images\image-20210223082421596.png)

3. 递归三要素

   1.定义递归函数：这个函数干什么是你自己定义的，参数和返回值根据实际问题确定。确定哪些参数是递归的过程中需要处理的，那么就在递归函数里加上这个参数， 并且还要明确每次递归的返回值是什么进而确定递归函数的返回类型。

   2.寻找结束条件：找出参数为多少时递归结束，之后返回结果。此时注意，必须能够根据这个找出的参数的值直接能知道函数的结果才行。

   3.找函数的等价关系式：找原函数的等价关系式来不断缩小参数的范围。确定每一层递归需要处理的信息。在这里也就会重复调用自己来实现递归的过程。

4. 解题思路：首先要明白递归的解就是基于子问题的解构建的，通常只需要在f(n-1)的解中加入、移除某些东西或者稍作修改就能算出f(n)。将问题分解为子问题最常用三种方式

   ```
   1.自底向上的递归
   从解决问题的简单情况入手，例如列表中只有一个元素时，然后再解决两个元素等等的情况，关键在于如何基于上一种情况的答案（或者前面所有情况）得出后一种情况的解。
   2.自上而下的递归
   尝试着把变量为N的情况分解为子问题的解，要注意分解的子问题之间是否有重叠。
   3.数据分割的递归
   像二分查找，归并排序。
   ```

##### 递归和迭代

递归算法极其耗空间。每次递归调用都会增加一层新的方法入栈，简而言之，如果递归深 度为 n，那么最少占用 O(n)的空间。 鉴于此，用迭代实现递归算法往往更好。所有的递归都可以用迭代实现，只不过有时会让 代码超级复杂。所以有了递归算法之后，不要急于实现。先问问自己用迭代实现难不难，也可 以和面试官讨论该如何权衡。

##### 经典题目



### 思想3+：贪心

##### 基本知识

如何理解贪心：每一步互相不影响，每一步选择最优的即可。

DP：先寻找子问题的最优解，然后在其中进行选择，要求解所有可能的子问题。

贪心：首先做出一次贪心选择（在当时看起来是最优的选择），然后求解选出的子问题**，从而不必费心求解所有可能的子问题。**

1. 遍历数组：环形和一般型

   ```c++
   for循环适合从头到尾的遍历，而while循环适合模拟环形遍历，关于环形遍历，参考以下程序，怎么找环？数组num，找起点。参考贪心134加油站题目
   for(int i=0;i<num.size();i++){
       int index=(i+1)%num.size();//精髓
       while(index!=i){//index是一直变换的，知道和出发点相等
           index=(index+1)%num.size();
   }
   }
   ```

2. 

   
   

##### 贪心经典例题

###### 分配问题

1. 分发饼干

   ```c++
   //一种贪心策略是大尺寸的优先对应胃口值大的孩子，
   class Solution {
   public:
       int findContentChildren(vector<int>& g, vector<int>& s) {
           //贪心-最终目标是尽可能满足越多数量的孩子，那饼干就要充分利用，大尺寸的对应胃口大的，小尺寸的对应胃口小的
           sort(g.begin(),g.end());
           sort(s.begin(),s.end());
           int count=0;
           int j=s.size()-1;
           for(int i=g.size()-1;i>=0;i--){
               if(j>=0&&s[j]>=g[i]){
                   count++;
                   j--;
               }
           }
           return count;
       }
   };
   //或者给最小胃口值的孩子分配最小的能喂饱的饼干。把大于等于这个孩子饥饿度的、并且大小最小的饼干给这个孩子。
   class Solution {
   public:
       int findContentChildren(vector<int>& g, vector<int>& s) {
           sort(g.begin(),g.end());
           sort(s.begin(),s.end());
           int l=0,r=0;
           while(l<g.size()&&r<s.size()){//
               if(g[l]<=s[r])l++;
               r++;
           }
           return l;
       }
   };
   ```

2. 数列分段

   ```c++
   #include<iostream>
   #include<string>
   #include<algorithm>
   using namespace std;
   int n, m, a,s,cnt=1;
   int main() {
   	cin >> n >> m;
   	while (n--) {
   		cin >> a;
   		if (s + a <= m) {//分成最小的组，呢就尽量在满足条件下用更多的数，
   			s += a;
   		}
   		else
   		{
   			s = a;
   			cnt++;
   		}
   	}
   	cout << cnt;
   	return  0;
   }
   ```

3. 纪念品分组

   ```c++
   #include<iostream>
   #include<string>
   #include<algorithm>
   using namespace std;
   int w, n,cnt, a[30010];
   int main() {
   	cin >> w;
   	cin>>n;
   	for (int i = 0; i < n; i++) {
   		cin >> a[i];
   	}
   	sort(a, a + n);//分组数量为最小，就是尽可能分成两组，让大的和小的一组。
   	int l = 0, r = n - 1;
   	while (l <= r) {
   		if (a[l] + a[r] <= w) {
   			cnt++;
   			l++;
   			r--;
   		}
   		else {
   			r--;
   			cnt++;
   		}
   	}
   	cout << cnt;
   	return  0;
   }
   ```

4. 

   

   


###### 序列问题

1. 摆动序列

   ```c++
   class Solution {
   public:
       int wiggleMaxLength(vector<int>& nums) {
           if(nums.size()==0)return 0;
           int pre=0;
           int cur=0;
           int count=1;//
           for(int i=1;i<nums.size();i++){
               cur=nums[i]-nums[i-1];//cur每次随着i的变化在更新
               if(pre>=0&&cur<0||pre<=0&&cur>0){//可能的情况考虑到
                   count++;
                   pre=cur;
               }
           }
           return count;
       }
   };
   ```

   

###### 子序列问题

1. 最长子序和

   ```
   
   ```

   

###### 股票问题



### 思想5：动态规划

##### 基本知识

1. 如何理解动态规划？

   DP一般是用来求问题的**最优解**的方法，是穷举方法的优化；**关键要理解现在的选择可能会影响后面的选择；**这种问题穷举搜索也可以，但是效率很低，通过找到问题中有重复的地方，也就是重叠子问题，来用DP解决。

   DP解决这种问题的方式就是通过找到**最优的子结构**，求每个阶段的最优状态，最后每个阶段的最优状态贪心组合即可。关于无后效性是指我们只关心子问题的最优，而不关心这个子问题的最优是如何得来的。通过重叠子问题和最优子结构来求出状态转移方程，其次就是遍历顺序和初始化的问题了，这也是需要认真思考的。

   由于动态规划解决的问题多数有重叠子问题这个特点，为减少重复计算，对每一个子问题只解一次，将其不同阶段的不同状态保存在一个二维数组（或者一维数组）中。随后如果再次需要此问题的解 ，只需要查找保存的值即可。动态规划算法，不需要反复计算前面步骤的值，这也是动态规划的优势。

2. 说一下最优子结构和重叠子问题。

   最优子结构：**如果一个问题的最优解包含其子问题的最优解，就称此问题具有最优子结构性质。**

   重叠子问题：**问题的递归算法会反复的求解相同的子问题，而不是一直生成新的子问题**。DP是对每个子问题求解一次，将解放入一个表中，当再次需要这个子问题时直接查表，每次查表的时间未常量时间。
   
   **分治算法求解的问题通常在递归的每一步都生成全新的子问题**。
   
3. 什么样的问题能使用DP解决？

   在面试过程中如果是求一个问题的最优解（通常是最大值或者最小值），并且该问题能够分解成若干个子问题，并且子问题之间有重叠的更小子问题，就可以考虑用动态规划来解决这个问题。

4. 算法实现的步骤

   1、创建一个一维数组或者二维数组，保存每一个子问题的结果，具体创建一维数组还是二维数组看题目而定，基本上如果题目中给出的是一个一维数组进行操作，就可以只创建一个一维数组，如果题目中给出了两个一维数组进行操作或者两种不同类型的变量值，比如背包问题中的不同物体的体积与总体积，找零钱问题中的不同面值零钱与总钱数，这样就需要创建一个二维数组。注：需要创建二维数组的解法，都可以创建一个一维数组运用滚动数组的方式来解决，即一位数组中的值不停的变化，后面会详细叙述。

   2、设置数组边界值，一维数组就是设置第一个数字，二维数组就是设置第一行跟第一列的值，特别的滚动一维数组是要设置整个数组的值，然后根据后面不同的数据加进来变化成不同的值。

   3、找出状态转换方程，也就是说找到每个状态跟他上一个状态的关系，根据状态转化方程写出代码。

   4、返回需要的值，一般是一维数组的最后一个或者二维数组的最右下角。

5. 暴力搜索-DP记忆化搜索-DP递推

   ![image-20210223082750856](C:\Users\zpp\AppData\Roaming\Typora\typora-user-images\image-20210223082750856.png)![image-20210223091508992](C:\Users\zpp\AppData\Roaming\Typora\typora-user-images\image-20210223091508992.png)

   

6. 滚动数组：

##### 经典例题

**//首先确定要使用搜索（动态规划）来解决，然后确定原问题的最优解涉及多少个子问题，再然后在确定最优解使用哪些子问题时，我们需要考察多少种选择，之后看每种选择（每个点）又有几种情况。从而确定最终的状态方程。**（**自底向上**，先考虑子问题每个点的选择（每个点的情况），然后写出状态转移方程）**可以从上到下分析**（递归）

**运行时间：我们可以用子问题的总数和每个子问题需要多少种选择这两个因素的乘积来粗略分析动态规划的运行时间。**

###### 简单一维数组

**举列子从特殊到一般**，正常分析都是自上到下的，DP是自下到上。

1. 爬台阶

   ```c++
   1、举例子（）
   2.可以分解为多少个子问题
   3.每个子问题有一种选择，起始点固定（只有自底向上的DP这样考虑，递归或者自顶向上就直接考虑原问题涉及多少个子问题，每个子问题有几种选择来分析）
   4.每个点有两种选择，跳一个还是两个
   //递归，会超时，但是分析还是从上到下分析，DP直接从下到上来做
       class Solution {
   public:
       int climbStairs(int n) {
           if(n==0||n==1)return 1;
           if(n==2)return 2;
           return climbStairs(n-1)+climbStairs(n-2);
       }
   };
   //DP
       class Solution {
   public:
       int climbStairs(int n) {
           vector<int>dp(n+1);
           dp[0]=1;
           dp[1]=1;
           for(int i=2;i<=n;i++){
               dp[i]=dp[i-1]+dp[i-2];
           }
           return dp[n];
       }
   };
   ```
   
   
   
2. 打家劫舍

   ```c++
   // class Solution {
   // public:
   //     int rob(vector<int>& nums) {
   //         int n=nums.size();
   //         if(n<1)return 0;
   //         if(n==1)return nums[0];
   //         vector<int>dp(n);
   //         dp[0]=nums[0];
   //         dp[1]=max(nums[1],dp[0]);
   //         for(int i=2;i<n;i++){
   //             dp[i]=max(dp[i-1],dp[i-2]+nums[i]);//每种选择有几种情况==这间房（这个点）偷还是不偷？
   //         }
   //         return dp[n-1];
   //     }
   // };
   //状态压缩。
   class Solution {
   public:
       int rob(vector<int>& nums) {
           int n=nums.size();
           if(n<1)return 0;
           if(n==1)return nums[0];
           int p=nums[0];
           int q=max(nums[0],nums[1]);
           if(n==2)return q;
           int s=0;
           for(int i=2;i<n;i++){
               s=max(p+nums[i],q);
               p=q;
               q=s;
           }
           return s;
       }
   };
   
   ```

   

3. 打家劫舍2，环形数组

   ```c++
   class Solution {
   public:
       int rob(vector<int>& nums) {
           int n=nums.size();
           int result=0;
           vector<int>dp(n);
           vector<int>dp1(n);
           if(n==1)return nums[0];
           int flag=1;//第一个偷
           if(flag==1){
               dp[0]=nums[0];//限定了第一个偷还是不偷，每一步都紧扣DP[i]的定义来判断初始条件！！
               dp[1]=nums[0];
               for(int i=2;i<n-1;i++){
                   dp[i]=max(dp[i-1],dp[i-2]+nums[i]);
               }
               flag=0;
           }
           if(flag==0){
               dp1[0]=0;//每一步取最优
               dp1[1]=nums[1];
               for(int i=2;i<n;i++){
                   dp1[i]=max(dp1[i-1],dp1[i-2]+nums[i]);
               }
           }
           result=max(dp[n-2],dp1[n-1]);
           return result;
       }
   };
   ```

   

4. 等差数列

   ```c++
   class Solution {
   public:
       int numberOfArithmeticSlices(vector<int>& nums) {
           int n=nums.size();
           vector<int>dp(n,0);//以i结尾的子数组数量
           int sum=0;
           for(int i=2;i<n;i++){
               if(nums[i]-nums[i-1]==nums[i-1]-nums[i-2]){
                   dp[i]=dp[i-1]+1;
                   sum+=dp[i];
               }
           }
           return sum;
       }
   };
   ```

   

###### 简单二维数组

1. 最小路径和

   ```c++
   class Solution {
   public:
       int minPathSum(vector<vector<int>>& grid) {
           //DP或者DFS
           int m=grid.size();
           int n=grid[0].size();
           vector<vector<int>>dp(m,vector<int>(n,0));
           for(int i=0;i<m;i++){
               for(int j=0;j<n;j++){
                   if(i==0&&j==0){//矩阵的各种情况
                       dp[i][j]=grid[i][j];
                   }
                   else if(i==0){
                       dp[i][j]=dp[i][j-1]+grid[i][j];
                   }
                   else if(j==0){
                       dp[i][j]=dp[i-1][j]+grid[i][j];
                   }
                   else{
                       dp[i][j]=min(dp[i][j-1],dp[i-1][j])+grid[i][j];
                   }
               }
           }
           return dp[m-1][n-1];
       }
   };
   ```

   

2. 0-1矩阵

   ```c++
   //自上向下分析，自下向上写代码。BFS也可。
   class Solution {
   public:
       vector<vector<int>> updateMatrix(vector<vector<int>>& matrix) {
           int m = matrix.size(), n = matrix[0].size();
           // 初始化动态规划的数组，所有的距离值都设置为一个很大的数
           vector<vector<int>> dist(m, vector<int>(n, INT_MAX / 2));
           // 如果 (i, j) 的元素为 0，那么距离为 0
           for (int i = 0; i < m; ++i) {
               for (int j = 0; j < n; ++j) {
                   if (matrix[i][j] == 0) {
                       dist[i][j] = 0;
                   }
               }
           }
           // 只有 水平向左移动 和 竖直向上移动，注意动态规划的计算顺序
           for (int i = 0; i < m; ++i) {
               for (int j = 0; j < n; ++j) {
                   if (i - 1 >= 0) {
                       dist[i][j] = min(dist[i][j], dist[i - 1][j] + 1);
                   }
                   if (j - 1 >= 0) {
                       dist[i][j] = min(dist[i][j], dist[i][j - 1] + 1);
                   }
               }
           }
           // 只有 水平向右移动 和 竖直向下移动，注意动态规划的计算顺序
           for (int i = m - 1; i >= 0; --i) {
               for (int j = n - 1; j >= 0; --j) {
                   if (i + 1 < m) {
                       dist[i][j] = min(dist[i][j], dist[i + 1][j] + 1);
                   }
                   if (j + 1 < n) {
                       dist[i][j] = min(dist[i][j], dist[i][j + 1] + 1);
                   }
               }
           }
           return dist;
       }
   };
   
   
   
   ```

   

3. 最大正方形

   ```
   
   ```

   



###### 切割类问题

分割类型题，**动态规划的状态转移方程通常并不依赖相邻的位置，而是依赖于满足分割条件的位置**

1. 整数拆分

   ```c++
   //我们通常自底向上的使用最优子结构，也就是说首先求得子问题的最优解，然后求原问题的最优解。也即是求解原问题的过程中需要在涉及的子问题中做出选择，选出能得到原问题最优解的子问题，原问题最优解的代价一般就是子问题最优解的代价和此次选择直接产生的代价，
   ////使用最优子结构，首先需要在涉及的子问题（状态）中做出选择（dp[i]），其次需要计算此次子问题当拥有最优解时付出的代价（确定使用哪些子问题，我们需要考虑怎样的选择，这次选择又会产生哪些相关问题。）通过组合选择之后的相关问题的最优解，并在所有的可能的子问题中选取最优的，构成原问题的最优解。本题：在每个子问题中，数字可以有j个选择，当选出一个j时，此时认为选择是最优的，后面需要考虑这次选择会后面又会产生哪些问题。3层套娃。例如：i-j不分就是最大，或者继续分是最大。然后取两者之间的最大值。就是max(j*dp[i-j],j*(i-j)
               }
           }
   class Solution {
   public:
       int cuttingRope(int n) {
           vector<int>dp(n+1);//dp[i]:分解数字i得到的最大乘积。切割问题：原问题分解成多少子问题。
           dp[2]=1;//初始化
           for(int i=2;i<=n;i++){//原问题分解成多少子问题，在这些子问题中选取最优的
               for(int j=2;j<=i;j++){//每种子问题又有多少种选择，假设当前一种选择就是最优的（无后效性），选择之后又会有哪些子子问题发生（每个选择（每个点）有几种情况）。
                   dp[i]=max(dp[i],max(j*dp[i-j],j*(i-j)));
           return dp[n];
       }
   };
   ```

   

2. 完全平方和

   ```c++
   class Solution {
   public:
       int numSquares(int n) {
           vector<int>dp(n+1,INT_MAX);
           dp[0]=0;
           for(int i=1;i<=n;i++){
               for(int j=1;j*j<=i;j++){
                   dp[i]=min(dp[i],dp[i-j*j]+1);
               }
           }
           return dp[n];
   
       }
   };
   ```

   

3. 解码方式

   ```c++
   //每种可能情况的考虑
   class Solution {
   public:
       int numDecodings(string s) {
           int n=s.size();
           if(s[0]=='0')return 0;
           if(n==1)return 1;
           //初始化
           vector<int>dp(n);
           dp[0]=1;
           if(s[1]=='0'){
               if(s[0]=='1'||s[0]=='2')dp[1]=1;
               else dp[1]=0;
           }
           else{
               if(s[0]=='1'||(s[0]=='2'&&s[1]>='1'&&s[1]<='6'))dp[1]=2;
               else if(s[0]=='2'&&s[0]>='7')dp[1]=1;
               else dp[1]=1;
           }
           for(int i=2;i<n;i++){
               if(s[i]=='0'){
                   if(s[i-1]=='1'||s[i-1]=='2')dp[i]=dp[i-2];
                   else return 0;
               }
               else{
                   if(s[i-1]=='1'){
                       dp[i]=dp[i-1]+dp[i-2];
                   }
                   else if(s[i-1]=='2'&&s[i]>='1'&&s[i]<='6'){
                       dp[i]=dp[i-1]+dp[i-2];
                   }
                   else{
                       dp[i]=dp[i-1];
                   }
               }
           }
           return dp[n-1];
       }
   };
   ```

   

4. 单词拆分

   ```
   
   ```

   

###### 子序列问题

1. 最长递增子序列（二分查找）

   ![image-20210429145219184](C:\Users\小面包\AppData\Roaming\Typora\typora-user-images\image-20210429145219184.png)

   ```c++
   class Solution {
   public:
       int lengthOfLIS(vector<int>& nums) {
           int n=nums.size();
           int max_len=0;
           vector<int>dp(n,1);
           for(int i=0;i<n;i++){
               for(int j=0;j<i;j++){
                   if(nums[i]>nums[j]){//递增子序列的条件，满足条件才能DP
                       dp[i]=max(dp[i],dp[j]+1);//dp[i]=dp[j]+1;区别在每次对dp[i]的赋值我们都要选最大的才行
                   }
               }
               max_len=max(dp[i],max_len);//选出dp数组中最大的数,可以打印出DP数组看看里面的数
           }
           return dp[n-1];
       }
   };
   //二分 做法
   class Solution {
   public:
       int find(int x,int l,int r,vector<int>&b){
           while(l<=r){
               int mid=l+(r-l)/2;
               if(x>b[mid])l=mid+1;
               else r=mid-1;
           }
           return l;
       }
       int lengthOfLIS(vector<int>& nums) {
           int n=nums.size();
           vector<int>dp(n,0);
           int j=0;
           int len=0;
           dp[0]=nums[0];
           for(int i=1;i<n;i++){
               if(nums[i]>dp[len]){
                   dp[++len]=nums[i];
               }
               else{
                   j=find(nums[i],0,len-1,dp);
                   dp[j]=nums[i];
               }
           }
           return len+1;
       }
   };
   ```

   

2. 最长公共子序列

   ```c++
   class Solution {
   public:
       int longestCommonSubsequence(string &text1, string &text2) {
           int m=text1.size();
           int n=text2.size();
           vector<vector<int>>dp(m+1,vector<int>(n+1));//这里定义元素为i，j，即dp[i][j]为s1的前i个字符,s2的前j个字符形成的最长公共子序列的长度。
           for(int i=0;i<m;i++)dp[i][0]=0;
           for(int j=0;j<n;j++)dp[0][j]=0;
           for(int i=1;i<=m;i++){
               for(int j=1;j<=n;j++){//数组从下标1开始，字符串从下标0开始的，所以是text[i-1]
                   if(text1[i-1]==text2[j-1])dp[i][j]=dp[i-1][j-1]+1;
                   else{
                       dp[i][j]=max(dp[i-1][j],dp[i][j-1]);
                   }
               }
           }
           return dp[m][n];
       }
   };
   ```

   

3. 最长公共子串

   ![image-20210428213237053](C:\Users\小面包\AppData\Roaming\Typora\typora-user-images\image-20210428213237053.png)

   ```c++
   //公共子串：连续相等
   //公共子序列：连续不一定相等
   class Solution {
   public:
       int findLength(vector<int>& nums1, vector<int>& nums2) {
           int m=nums1.size();
           int n=nums2.size();
           int ans=-1;
           vector<vector<int>>dp(m+1,vector<int>(n+1,0));
           //dp[i][j]为以a[i]和b[j]为结尾的公共子串的长度
           for(int i=0;i<m;i++)dp[i][0]=0;
           for(int j=0;j<n;j++)dp[0][j]=0;
           for(int i=1;i<=m;i++){
               for(int j=1;j<=n;j++){
                   if(nums1[i-1]==nums2[j-1]){//我们从一开始计算公共数组长度，但是数组中的元素还是从下标0开始。这样也方便初始化dp[i][0]和dp[0][j]为0.
                       dp[i][j]=dp[i-1][j-1]+1;
                   }
                   else{
                       dp[i][j]=0;
                   }
                   if(ans<dp[i][j]){
                       ans=dp[i][j];
                   }
               }
           }
           return ans;
   
       }
   };
   ```

   

4. 

###### 背包问题

![image-20210415160209454](C:\Users\小面包\AppData\Roaming\Typora\typora-user-images\image-20210415160209454.png)

1. 分割等和子集

   ```c++
   class Solution {
   public:
       bool canPartition(vector<int>& nums) {
           int size=nums.size();
           if(size<2)return false;
           //先考虑一些情况
           int sum=accumulate(nums.begin(),nums.end(),0);//accumulate计算容器的和
           int max_num=*max_element(nums.begin(),nums.end());//*min_element返回容器中的最小值
           if(sum%2!=0)return false;
           if(max_num>sum/2)return false;
           vector<vector<int>>dp(size,vector<int>(sum/2+1,0));
           for (int i = 0; i < size; i++) {
               dp[i][0] = 1;//j==0意味着选取的数的和为0，不选就是为0，所以是正确的
           }
           //dp[0][nums[0]] = 1;
           for(int i=1;i<size;i++){
               for(int j=1;j<=sum/2;j++){
                   if(j<nums[i])dp[i][j]=dp[i-1][j];//背包问题，当前选取的数大于要=的数了，就跳过这个数
                   else{
                       dp[i][j]=dp[i-1][j-nums[i]]|dp[i-1][j];//背包问题，当前i选取了这个数，那就是选取的数的和等于j-nums[i]就行了。
                   }
               }
           }
           return dp[size-1][sum/2];
       }
   };
   ```

   

2. 

###### 股票问题





### 图论

##### 基本知识

##### DFS+回溯模板

```c++
void dfs()//参数用来表示状态，根据需要添加。一般什么变化就把什么设置成参数
{  
    if(到达终点状态)  
    {  
        ...//根据题意添加  
        return;  
    }  
    if(越界或者是不合法状态)  
        return;  
    if(特殊状态)//剪枝
        return ;
    for(扩展方式)  //统计所有的可能结果，行参数
    {  
        if(扩展方式所达到状态合法)  //所有可能结果中找满足条件的
        {  
            修改操作;//根据题意来添加  
            标记；  
            dfs()； //列参数 
            (还原标记)；
            (不是覆盖结果的话就回溯修改的操作)；vector添加和一般数组覆盖。
            //是否还原标记根据题意  
            //如果加上（还原标记）就是 回溯法 
        }  
    }  
```



##### 经典例题

1. 全排列

   ```c++
   class Solution {
   public:
       vector<vector<int>>result;//统计最终结果
       vector<int>ans;//统计每个结果
       void dfs(vector<int>& nums,vector<bool>&vis){//vis来标记元素已经访问过
           if(nums.size()==ans.size()){//满足条件就添加到结果中，返回
               result.push_back(ans);
               return;
           }
           for(int i=0;i<nums.size();i++){//包含所有情况
               if(!vis[i]){//如果满足条件
                   ans.push_back(nums[i]);//先添加元素
                   vis[i]=1;//然后标记已经访问过
                   dfs(nums,vis);//开始递归
                   ans.pop_back();//退出这个元素，同时消除访问标记。回溯。不会覆盖要回溯，如果是输出数字，覆盖之后不用回溯
                   vis[i]=0;
               }
           }
       }
       vector<vector<int>> permute(vector<int>& nums) {
           vector<bool>vis(nums.size(),0);
           dfs(nums,vis);
           return result;
       }
   };
   
   //输入输出
   //int n;
   //vector<bool>vis(20, 0);
   //int result[20];//记录选了谁
   //
   //void pr() {
   //	for (int i = 1; i <= n; i++) {
   //		cout << setw(5) << result[i];
   //	}
   //	cout << endl;
   //}
   //void dfs(int x) {
   //	if (x>n) {//满足条件输出
   //		pr();
   //	}
   //	for (int i = 1; i <=n; i++) {//理论上要连接所有的数
   //		if (!vis[i]) {//排除掉不满足条件的
   //			result[x] = i;//选的数输出到结果,直接赋值后面会覆盖，不用再回溯
   //			vis[i] = 1;//选了这个数就标记它已经选过了
   //			dfs(x + 1);//下一层
   //			vis[i] = 0;//回溯
   //		}
   //	}
   //}
   //
   //int main() {
   //	cin >> n;
   //	dfs(1);
   //}
   ```

   

2. N皇后

   ```c++
   class Solution {
   public:
       vector<vector<string>>result;
       bool color[100];//列
       bool u[100];//斜线左
       bool v[100];//斜线右
       void dfs(int x,int n,vector<string>&ans){
           if(x==n){
               result.push_back(ans);
               return;
           }
           for(int i=0;i<n;i++){
               if(!color[i]&&!u[x-i+n]&&!v[x+i]){
                   color[i]=1;
                   u[x-i+n]=1;
                   v[x+i]=1;
                   ans[x][i]='Q';
                   dfs(x+1,n,ans);
                   ans[x][i]='.';
                   color[i]=0;
                   u[x-i+n]=0;
                   v[x+i]=0;
               }
           }
       }
   
       vector<vector<string>> solveNQueens(int n) {
           vector<string>ans(n,string(n,'.'));//一维数组中是个长度为n的字符串
           dfs(0,n,ans);
           return result;
       }
   };
   
   //输入输出
   #include<iostream>
   #include<algorithm>
   using namespace std;
   int n;
   int cnt=0;//统计输出的行数
   bool lie[40];
   bool u[40];
   bool v[40];
   int result[20];
   
   void pr() {
   	for (int i = 1; i <= n; i++) {//控制输出每行的元素
   		cout << result[i] << " ";//
   	}
   	cout << endl;//一行输出结束开始换行
   }
   void dfs(int x) {//位置X,行
   	if (x == n + 1) {//终止条件，到达第n+1行
   		cnt++;
   		if(cnt<=3)pr();//满足条件一行一行的输出，控制输出每一行,另外要求只输出前三行
   		return;
   	}
   	for (int i = 1; i <= n; i++) {//i是列
   		if (!lie[i] && !u[x - i + n] && !v[x + i]) {
   			lie[i] = 1;//访问过的标记
   			u[x - i + n]=1;
   			v[x + i] = 1;
   			result[x] = i;//统计每行的结果
   			dfs(x + 1);//下一行
   			lie[i] = 0;//回溯
   			u[x - i + n] = 0;
   			v[x + i] = 0;
   		}
   	}
   }
   int main() {
   	cin >> n;
   	dfs(1);
   	cout << cnt;
   	return 0;
   }
   ```

3. 迷宫

   ```c++
   int n, m, t, sx, sy, fx, fy;//要求的输入
   bool vis[10][10];//计算有没有被访问过，没被访问过就是0
   bool mp[10][10];//看是否有障碍，无障碍就是0
   int xx[] = { 1,0,-1,0 };//四个方向，上下左右
   int yy[] = { 0,-1,0,1 };//
   int cnt = 0;
   
   void dfs(int x,int y) {
   	if (x == fx && y == fy) {//找到终点
   		cnt++;//返回路径总数即可
   		return;
   	}
   	for (int i = 0; i < 4; i++) {//四个方向
   		int dx = xx[i] + x;//下一步的方向，先包含所有的，下面开始判断真正可以去的
   		int dy = yy[i] + y;
   		if (dx >= 1 && dx <= n && dy >= 1 && dy <= m && !vis[dx][dy] && !mp[dx][dy]) {
   			//不能出界+访问过了+遇见障碍
   			vis[dx][dy] = 1;//访问过标记
   			dfs(dx, dy);
   			vis[dx][dy] = 0;//回溯
   		}
   	}
   }
   int main() {
   	cin >> n >> m >> t >> sx >> sy >> fx >> fy;
   	while (t--) {//读入障碍点
   		int x, y;
   		cin >> x >> y;
   		mp[x][y]=1;//有障碍就是1
   	}
   	vis[sx][sy] = 1;//第一个位置被访问就标记下,起始位置固定，之后不会再撤销
   	dfs(sx,sy);//从初始点开始搜索,参数要包含位置信息，如果要包含其他信息，再加入参数也行，例如走的步数。
   	cout << cnt;
   	return 0;
   }
   
   ```

   

4. 单词搜索

   ```c++
   //和迷宫区别就是迷宫是初始位置确定为一个，本题是初始位置可能是矩阵中的每一个元素。
   class Solution {
   public:
       int xx[4]={1,0,-1,0};
       int yy[4]={0,-1,0,1};
       bool result=false;
       bool dfs(int x,int y,vector<vector<bool>>& vis,vector<vector<char>>& board, string word,int k){
           if(board[x][y]!=word[k]){//先找一开始和字符串相同的第一个字母，第一个不相同直接退出，相同的话四个方向开始找，同理找第二个和字符串第二个相同的
               return false;
           }
           else if(word.size()-1==k){//如果遍历到最后一个都相同，就返回true，这里程序默认board[x][y]==word[k]，和else ..if..相同。
               return true;
           }
           int n = board.size();
   		int m = board[0].size();
           //vis[x][y] = 1;
           for(int i=0;i<4;i++){//四个方向上行走
               int dx = xx[i] + x;//
   			int dy = yy[i] + y;
   			if (dx >= 0 && dx <n &&dy >= 0 && dy <m && !vis[dx][dy]) {
   				vis[dx][dy] = 1;
   				bool flag=dfs(dx, dy, vis,board,word,k+1);
                   if(flag){//找到就返回，就是最节省时间的。
                       result=true;
                       break;
                   }
                   vis[dx][dy] = 0;
   			}
           }
           //vis[x][y]=0;这样就不用单独考虑初始位置了，直接包含了。
           return result;
   
       }
       bool exist(vector<vector<char>>& board, string word) {
   		int h = board.size();
   		int t = board[0].size();
           vector<vector<bool>> vis(h,vector<bool>(t));
           for(int i=0;i<h;i++){
               for(int j=0;j<t;j++){//和迷宫的区别就是这里没固定初始位置，矩阵中所有的位置都可能是初始位置，所以要遍历每一个位置当坐初始位置
                  if(board[i][j]==word[0]){//同理，如果找到了就是开始标记，同时开始往下搜
                      vis[i][j]=1;
                      bool a= dfs(i,j,vis,board,word,0);
                      if(a){
                          return true;
                      }
                      else{//这个为初始位置后面可能没找到，这时候这个位置就要取消标记。一种简单做法就是，在搜索前考虑所有情况
                          vis[i][j]=0;
                      }
                  }
            }
           }
           return false;
       }
   };
   ```

   

5. 单词方阵

   ```c++
   #include<iostream>
   #include<vector>
   using namespace std;
   
   const int p = 110;
   bool vis[p][p];
   int n;
   vector< vector<char> >a(110, vector<char>(110));//或者char a[110][110];
   int xx[] = { 1,1,1,0,0,-1,-1,-1 };//八个方向。pari实现也可
   int yy[] = { 1,0,-1,1,-1,1,0,-1};
   string yz = "yizhong";
   void dfs(int x, int y) {
   	for (int i = 0; i < 8; i++) {//每个方向，
   		int flag = 1;
   		for (int j = 0; j < 7; j++) {//固定字符串yz
   			int dx = x + j * xx[i];
   			int dy = y + j * yy[i];
   			if (dx<0||dx>n-1||dy<0||dy>n-1|| yz[j] != a[dx][dy]) {//每个方向上字符yz第j个位置上,另外考虑边界
   				flag = 0;//不符合条件为出边界和不相等
   				break;//退出当前一个方向的循环
   			}//判断一个数列是否完全相同的时候，先判断它们是否有不同，有一个不同就可以判断了。如果限制条件较少的话，也可以直接根据约束来找相同，然后continue，然后else或者直接输出。
   		}
   		if (flag) {
   			for (int j = 0; j < 7; j++) {//固定字符串yz
   				int dx = x + j * xx[i];
   				int dy = y + j * yy[i];
   				vis[dx][dy] = 1;//如果相等就标记为1
   		    }
   	    }
   
       }
   
   }
   int main(){
   	cin >> n;
   	for (int i = 0; i < n; i++) {//矩阵输入
   		for (int j = 0; j < n; j++) {
   			cin >> a[i][j];
   		}
   	}
   	for (int i = 0; i < n; i++) {//双重循环来找出初始点
   		for (int j = 0; j < n; j++) {
   			if (a[i][j] == 'y') {//初始点正确的话就开始搜
   				dfs(i, j);
   			}
   		}
   	}
   	for (int i = 0; i < n; i++) {//输出
   		for (int j = 0; j < n; j++) {
   			if (!vis[i][j]) {//根据输出的特点来看，满足什么条件输出什么东西，
   				cout << "*";//这里如果每个方向上有字母不相等，就输出*
   			}
   			else {
   				cout << a[i][j];
   			}
   		}
   		cout << endl;//换行
   	}
   	return 0;
   }
   ```

   

6. 单词接龙

   ```c++
   //字符串操作和搜索结合，主要字符串操作部分
   #include<iostream>
   #include<string>
   using namespace std;
   int n，ans;
   string s[22];
   char a;
   int vis[22];
   void dfs(string x,int size){//上一个字符串，能拼接出来的长度
       ans=max(ans,size);//找最长的
       for(int i=0;i<n;i++){//先枚举可能出现的节点
           int p=1,flag=0;//重叠部分.一个重合最好，不然就继续找其他单词看有没有重合两个的，三个的等
           int la=x.size(),lb=s[i].size();//string本身就是一个容器
           while(p<min(la,lb)){//并且还不能完全重合，不能是包含关系
              if(x.substr(la-p)==s[i].substr(0,p)&&vis[2]<2){//找两个字符串之间是否有相同的部分，最长的就是首尾一个就相等，否则继续找下去。substr（l,r）//迭代器操作
                  vis[i]++;//每个单词使用两次
                  dfs(s[i],m+lb-p);//如果找到了就标记下或者找到了继续搜索,上一个单词就是现在的s[i]；
                  vis[i]--;
                  break;//找到了就退出继续找下一个
              }
               p++;
   }
          // if(flag){
               
               //dfs(s[i],m+lb-p);
   //}
          
   }
       
   }
   int main(){
       cin>>n;
       for(int i=0;i<n;i++){
           cin>>s[i];
   }
       cin>>a;
       for(int i=0;i<n;i++){
           if(s[i][0]==a){//先找出第一个单词
               vis[i]++;//从第一个开始用了就标记下
               dfs(s[i],s[i].size())； //从第一个单词开始搜索 
               vis[i]--;
   }
   }
       cout<<ans;
       return 0;
   }
   ```

7. 

##### BFS模板

分层搜索，当队头节点出队时，扩展其子节点入队。**队列是其结构基础**。相关的点入队，使用完毕出队。

从某个点开始，先搜索跟这个点连接的所有节点，这个点先入队，之后跟这个点连接的所有点入队之后，这个点出队，依次类推。

###### 经典例题 洛谷

1. 填涂颜色

   ```c++
   #include<iostream>
   #include<queue>
   using namespace std;
   int xx[]={0,-1,0,1};//搜索的方向
   int yy[]={1,0,-1,0};
   int mp[35][35];//存储图,矩阵元素
   bool vis[35][35];//看是否访问过
   int n;
   int main(){
       cin>>n;
       for(int i=1;i<=n;i++){//外层建立一层假想的元素
           for(int j=1;j<=n;j++){
               cin>>mp[i][j];
           }
   }
       //只是将外圈0访问一遍标记，输出做出数值改变
       queue<int>x;//点的纵坐标和横坐标
       queue<int>y;
       x.push(0);y.push(0);//从第一个点开始
       vis[0][0]=1;//访问过的记录
       while(!x.empty()){//X已经是不空的了
           for(int i=0;i<4;i++){//相关的点就是周围四个方向的点
               int dx=x.front()+xx[i];
               int dy=y.front()+yy[i];
               if(dx>=0&&dx<n+1&&dy>=0&&dy<=n+1&&mp[dx][dy]==0&&!vis[dx][dy]){
                   x.push(dx);
                   y.push(dy);
                   vis[dx][dy]=1;
   }
               
               
   }
           x.pop();
           y.pop();
   }
       //点没被访问过，而且为0，就输出2
       for(int i=1;i<=n;i++){
           for(int j=1;j<=n;j++){
               if(mp[i][j]==0&&vis[i][j]==0){
                   cout<<2;
                   
   }
               else{
                   cout<<mp[i][j];
   }
   }
   }
       
       return 0;
   }
   ```

   

2. P1443马的遍历（最少要走几步）![image-20210418211022126](C:\Users\小面包\AppData\Roaming\Typora\typora-user-images\image-20210418211022126.png)

   马的跳法就是他要走的方式。同样是马当前的坐标先入队，马相关的点走完了就弹出这个点，除了马的坐标还要有马跳了几次。

   ```c++
   #include<iostream>
   #include<queue>
   #include<cstring>
   #include<iomanip>//stew
   using namespace std;
   int xx[]={2,2,1,1,-1,-1,-2,-2};//马跳的方向
   int yy[]={1,-1,2,-2,3,-2,1,-1};
   int n,m,sx,sy;
   int mp[410][410];//本身也有记录是否访问的作用
   struct Node{
       int x,y,s;//行列的坐标以及走了几步
   }
   int main(){
       cin>>n>>m>>sx>>sy;
       for(int i=1;i<=n;i++){
           for(int j=1;j<=m;j++){
               mp[i][j]=-1;//先初始化
   }
   }
       //memset(mp,-1,sizeof(mp));
       queue<Node>Q;
       //压入第一个元素
      // Node t;//
      // t.x=sx;t.y=sy;t.s=0;
      // Q.push(t);
       Q.push((Node){sx,sy,0});//直接强制转换也行
       //cout<<Q.front().x;
       mp[sx][sy]=0;//一样访问了就标记
       while(!Q.empty()){
           for(int i=0;i<8;i++){
               int dx=xx[i]+Q.front().x;
               int dy=yy[i]+Q.front().y;
               if(dx>=1&&dx<=n&&dy>=1&&dy<=m&&mp[dx][dy]==-1){
                   Q.push((Node){dx,dy,Q.front().s+1});
                   mp[dx][dy]=Q.front().s+1;//存储这个数
                   
                   
   }
   }
           Q.pop();
   }
       for(int i=1;i<=n;i++){
           for(int j=1;j<=m;j++){
               cout<<left<<setw(5)mp[i][j]<<" ";
   }//setw(5)设置宽度5，左对齐
           cout<<endl;
       }
       
       return 0;
   }
   ```

   

3. 

### 排序

##### 选择排序

###### 思想

关键是**选择**，就是不断地从未排序的元素中选择最大（或最小，或者最符合题意的元素）放入已经排好序的元素集合中。每一个元素都需要和他下一个元素作为首元素的集合中的所有元素比较，然后交换。

###### 代码

```c++
void selection_sort(vector<int>&nums,int n){
    for(int i=0;i<n-1;i++){//只需要比较到最后一个元素的前一个元素，不然会溢出
        int minIndex=i;//默认第一个元素为最小的元素，我们关注下标
        for(int j=i+1;j<n;j++){//在未排序的数组中找最小的元素，每次比较一个元素都需要再找一遍，比较麻烦
            if(nums[j]>nums[i])minIndex=j;
            }
        swap(nums[minIndex],nums[i]);//交换最小值和无序区间的第一个元素
}
}
//时间复杂度：内层循环O（n*n），外层O（n）。不稳定排序。
//空间复杂度：O（1）；
```

##### 插入排序

###### 思想

适用处理**数据量比较少或者部分有序**的数据。

先假定第一个元素是已经排好序的，后面元素是未排序的，然后把把未排序的一个一个插入到有序的集合中，如何插入呢：把**有序集合从后向前扫一遍**，找到合适的位置插入。和选择排序区别就是只需要比较有序集合中的元素，先根据元素大小找到插入位置，然后插入到比这个元素大的位置上。

###### 代码

```c++
void insertion_sort(vector<int>&nums,int n){
    for(int i=1;i<n;i++){
        insert(nums,i);
}
}
void insert(vector<int>&nums,int i){
    int presert=nums[i];//构建临时变量来保存要插入的元素
    for(int j=i-1;j>=0&&nums[j]>preinsert;j--){
        nums[j+1]=nums[j];//比待插元素大的元素后移，空出位置
    }
    nums[j+1]=presert;//插入元素，j先减一了。只是遍历有序数组中的元素，直到每个未排序的元素找到合适的位置
}
//时间复杂度：O（n*n）;比较稳定（元素相等不会进行移动，只会）
//空间复杂度：
```



##### 冒泡排序

###### 思想

**一个无序序列，每一次两两比较选出较大的（小的），确定序列中最大的元素，这是一次选出最大的，然后对剩下的n-1个元素再继续用同样的方法选择出最大的，直到剩下最后一个元素。**和插入，选择相同的是都需要针对每个元素，不同的是这里是要进行n-1次元素的选择最大，每一次选择最大都经过一个冒泡排序。比较简单的排序，效率不高。

###### 代码

```c++
void bubblesort(vector<int>&nums,int n){
    bool swapped;
    for(int i=1;i<n;i++){
        swapped=false;
        for(int j=1;j<n-i+1;j++){
            if(nums[j]>nums[j-1]){//可能一直比较，但不用交换，所以优化可以设置一个标记来判断有没有交换
                swap(nums[j],nums[j-1]);
                swapped=ture;
}
}
        if(!swapped)break;//如果一直没有交换的话，说明序列就已经是排好序的，直接退出就行
}
}
//时间复杂度：O（n*n）
```

##### 希尔排序

###### 思想

先根据间隔进行分组，让数组中间隔为h的元素有序，采用的是插入排序的方式。间隔一开始可以是整个数组长度的一半，然后调整间隔，让间隔一直缩小，直到间隔为1，此时数组中任意间隔为1的元素都是有序的，整个数组就是有序的了。相对于插入排序，多了个间隔的选取。

###### 代码

##### 归并排序

###### 思想

采用了**分治**（**所谓分而治之就是把一个复杂庞大的问题分解成一个个小的问题去解决**）的思想，比较适合用于处理大规模的数据，但是比较消耗内存。

就是将待排序的数**分**成两半后排序（**治**），然后再将这两个排好序的序列**合**成一个有序序列。分治：不断地分未排序的数组，一直分到只有一个元素的时候，这个时候就不用治了，开始合了，合并：不断地取出两个有序数组中比较小的那一个放在一个辅助数组中（通过比较）,直到把两个数组中的元素取完。

###### 代码

```c++
void mergesort(vector<int>&nums,vector<int>&temp,int left,int right){
    if(left==right)return;
    if(left<right){
        int mid=left+(right-left)/2;
        mergesort(nums,temp,left,center); //分左    
        mergesort(nums,temp,center+1,right);//分右
        merge(nums,temp,left,center,right);//合并
}
}

void merge(vector<int>&nums,vector<int>&temp,int left,int center,int right){
    int i=left,j=center+1;
    for(int k=left;k<=right;k++){
        if(i>center)temp[k]=nums[j++];//都已经是排好序的数组了，如果一边取完，直接把另外一个添加到数组中
        else if(j>right)temp[k]=nums[i++];
        else if(nums[i]<=nums[j])temp[k]=nums[i++];
        else temp[k]=nums[j++];
}
}
    for(int k=left;k<=right;k++){//先把子数组合并到辅助数组，然后把有序的数组复制到原数组中
        nums[k]=temp[k];
}
//时间复杂度：O（nlogn），稳定排序

```

##### 快速排序

###### 思想

递归分治的思想。首先选取一个主元，通过主元把数组分成两部分，把一个大的数组通过主元**分割成**两个小部分的数组，接下来递归处理这两个小部分的数组，直到数组中只有一个或者零个元素。关键是分割的方式：双指针单向调整或者双向调整。

###### 代码

```c++
分割：单向分割
void quicksort(vector<int>nums,int l,int r){
    int center;
    if(l<r){
        center=partion(nums,l,r);//根据主元分割成两个基本排序的数组
        quicksort(nums,l,center-1);//分别对这两个数组以相同的方式处理，分治：每个子问题都是变化的
        quicksort(nums,center+1,r);
        
}
}
int partion(vector<int>nums,int l,int r){
    int key=nums[r];//选取最后一个元素作为主元
    for(int i=l;i<right;i++){//双指针操作，都指向第一个元素，通过一个指针来遍历元素
        if(nums[i]<key){//如果这个指针小于主元就交换这个指针和另外一个指针指向的元素，同时两个指针都++
            swap(nums[i],nums[l]);
            l++;
}
}
    swap(nums[i],key);//把主元放到边界位置

}
分割操作：双向调整
    int parition(vector<int>nums,int l,int r){
    int key=nums[l];
    int fast=l+1,last=r;
    while(true){
        while(fast<last&&nums[fast]<=key)fast++;
        while(fast<last&&nums[last]>=key)last--;
        if(fast>=last)break;
        swap(nums[last],nums[fast]);
}
    //swap(nums[r],nums[l]);//key为什么不行？一种已经排好序的情况会有问题？--交换key值的话，只是和key交换了，但是没有交换数组中的主元。注意值传递和引用传递。所以要直接交换数组中的值，或者用赋值的操作。
        //nums[l]=nums[r];
        //nums[r]=key;
    swap(nums[fast],nums[l]);
    return fast;
}   
//平均时间复杂度0（nlongn），最坏哦（n*n）,每次主元左边的元素个数都是零个。这样需要分割n次,每次分割整理时间复杂度为O（n）;//交换之后会破坏稳定性
//所以一般使用快排可以先打乱数组。
```

##### 堆排序

###### 思想

1.通过依次删除堆顶元素放入一个数组里，就是一个有序数组了。前提是一定是二叉堆。

2.不用辅助数组也行，因为堆本身也是用一个数组存储的，删除的根节点依次放进堆数组的最后。这**相当于**把堆顶的元素和堆尾部的元素进行交换，然后再通过下沉（上浮）的方式把二叉树恢复成二叉堆。

###### 代码

```c++
//下沉，节点下沉有一个假设前提，就是该节点以下的非叶节点已经完成了堆排序。所以每次下沉只需检查交换后的节点是否需要继续调整。也是因为这个原因，构建大顶堆时需要从最后一个非叶节点开始构建
class Solution {
public:
	void sink(vector<int>&a, int i, int heapSize) {
		int l = 2 * i + 1;//元素从零开始
		while (l <heapSize) {
			//如果右孩子存在并且大于左孩子，就定位到右孩子
			if (l+1< heapSize&&a[l] < a[l + 1])++l;
			//如果父节点已经大于子节点了，
			if (a[i] >= a[l])break;
			swap(a[i], a[l]);//也可以这里单向赋值，要先记录父节点，之后再将父节点赋值给子节点
			i = l;
			l = 2 * i + 1;
		}
        //
	}
	//建立大顶堆
	void buildMaxHeap(vector<int>&a, int heapSize) {
		for (int i = (heapSize-2) / 2; i >= 0; --i) {//从最后一个非叶子节点开始向上构建
			sink(a, i, heapSize);
		}
	}
	int findKthLargest(vector<int>& nums, int k) {//求解数组中第K个最大的元素，堆排序，建立一个大顶堆，之后依次删除k-1个根节点就是第k大的节点了
		int size = nums.size();
		buildMaxHeap(nums, size);
		for (int i = nums.size()-1; i >= nums.size() - k+1 ; i--) {
			swap(nums[i], nums[0]);//先交换最后一个元素和根节点，然后根节点下沉就行
			sink(nums, 0, i);//长度已经减一了，下面依次减一了。
		}
		return nums[0];
	}
};
```



##### 计数排序

###### 思想

取值范围不是很大的情况下时间复杂度比快排好，是一种根据在数组下标上操作的一种排序方式。原理：数组下标范围就是元素值的范围，下标对应的值是元素出现的次数。（如果是稀疏的数或者数值范围太大这种方式弊端很大）。然后输出数组下标即可，另外下标对应的值是多少数组下标就输出多少次，结果就是排序好的。

###### 代码

```

```



##### 桶排序

###### 思想



###### 代码

##### 基数排序

###### 思想

###### 代码



###### 经典例题

1. 在一个未排序的数组中，找到第K个大的数字

   ```c++
   //快排
   class Solution {
   public:
       int quicksort(vector<int>&nums,int l,int r){
           int i=l+1;//找主元
           //int j=r;
           int key=nums[l];
           while(true){//双向指针操作
               while(i<=r&&nums[i]<=key)i++;
               while(i<=r&&nums[r]>=key)r--;
               if(i>=r)break;
               swap(nums[i],nums[r]);
           }
           //swap(nums[r],nums[l]);//key为什么不行？一种已经排好序的情况会有问题？--交换key值的话，只是和key交换了，但是没有交换数组中的主元。注意值传递和引用传递。所以要直接交换数组中的值，或者用赋值的操作。
           nums[l]=nums[r];
           nums[r]=key;
           return r;
       }
       int findKthLargest(vector<int>& nums, int k) {
           int target=nums.size()-k;
           int l=0,r=nums.size()-1;
           while(l<r){
               int mid=quicksort(nums,l,r);
               if(mid==target)return nums[mid];
               if(mid>target){
                   r=mid-1;
               }
               else{
                   l=mid+1;
               }
   
           }
           return nums[l];
       }
   };
   //堆排序
   //下沉，节点下沉有一个假设前提，就是该节点以下的非叶节点已经完成了堆排序。所以每次下沉只需检查交换后的节点是否需要继续调整。也是因为这个原因，构建大顶堆时需要从最后一个非叶节点开始构建
   class Solution {
   public:
   	void sink(vector<int>&a, int i, int heapSize) {
   		int l = 2 * i + 1;//元素从零开始
   		while (l <heapSize) {
   			//如果右孩子存在并且大于左孩子，就定位到右孩子
   			if (l+1< heapSize&&a[l] < a[l + 1])++l;
   			//如果父节点已经大于子节点了，
   			if (a[i] >= a[l])break;
   			swap(a[i], a[l]);//也可以这里单向赋值，要先记录父节点，之后再将父节点赋值给子节点
   			i = l;
   			l = 2 * i + 1;
   		}
           //
   	}
   	//建立大顶堆
   	void buildMaxHeap(vector<int>&a, int heapSize) {
   		for (int i = (heapSize-2) / 2; i >= 0; --i) {//从最后一个非叶子节点开始向上构建
   			sink(a, i, heapSize);
   		}
   	}
   	int findKthLargest(vector<int>& nums, int k) {//求解数组中第K个最大的元素，堆排序，建立一个大顶堆，之后依次删除k-1个根节点就是第k大的节点了
   		int size = nums.size();
   		buildMaxHeap(nums, size);
   		for (int i = nums.size()-1; i >= nums.size() - k+1 ; i--) {
   			swap(nums[i], nums[0]);//先交换最后一个元素和根节点，然后根节点下沉就行
   			sink(nums, 0, i);//长度已经减一了，下面依次减一了。
   		}
   		return nums[0];
   	}
   };
   ```

   

2. 最小的K个数

   ```
   
   ```

   

### 数论

##### 基本知识

1. **快速幂**：求x的n次方。一般是通过循环将n个x乘起来。时间复杂度o(n),快速幂法为二分法的一个应用，可以将时间复杂度降至log2n:

##### 经典例题

1. 数值的整数次方

   实现pow(x,n),计算x的n次幂。

   ```c++
   class Solution {
   public:
       double myPow(double x, int n) {
           double result=1;
           if(n==0)return 1;//注意n的各种情况
           if(n==1)return x;
           long b=n;//考虑负数的情况
           if(b<0){
               x=1/x;
               b=-b;
           }
           while(b){
               if(b&1){//二进制最后一位是否为1（也就是这个数是偶数还是奇数），二进制最后一位为1，肯定是奇数，最后一位为零，肯定是偶数
                   result*=x;//奇数就多乘个x
               }
               x*=x;//b为偶数直接平方
               b>>=1;//右移一位，相当于/2。这里是看/2一共多少次，奇数多乘x，偶数直接平方。例如10：10为偶数，5为奇数，2为偶数，1为奇数。总共四次，2323.为x的（2+3+2+3）次方。
           }
           return result;
       }
   };
   ```

   

2. 

### 位运算

##### 基本知识

1. 位运算只能在整数上操作
2. 异或^:相同位不同为1，相同为0。**一般位判断相同或者不同用异或。**。**任何数和本身异或都是0，任何数和0异或都是其本身**。**X^X=0;X^0=X;**
3. 与&：相同位都为1才为1，有一个不为1就是0；**0、1和1位与都是本身。**即判断当前位是0还是1和1与就行。**并且异或，与和或的结果也就是1或0**
4. 或|：相同位有一个为1就是1
5. 取反~：
6. 位左移<<:将二进制位全部左移若干位，高位丢弃，低位补0；
7. 位算术右移>>:将二进制位全部右移若干位，对无符号数，高位补0，有符号数，各编译器处理方式不同。有的补符号位，（算术右移）有的补0（逻辑右移）
8. 熟悉简单的运算，二进制十进制十六进制和八进制之间的关系
9. 二进制补码和负数：![image-20210314160910270](C:\Users\小面包\AppData\Roaming\Typora\typora-user-images\image-20210314160910270.png)![image-20210314160927647](C:\Users\小面包\AppData\Roaming\Typora\typora-user-images\image-20210314160927647.png)
10. 
11. 
12. 

##### 常用位操作

1. **遍历**：一个整数n，从右向左遍历它，即n=n>>1;检索整数n最右边的位：n&1；另外注意优先级，不清楚的就先加上括号吧！！
2. **判断奇偶**：和1与。(x&1)==1等价于X%2==1,奇数（最后一位肯定为1）；(x&1)==0等价于X%2==0，偶数（最后一位肯定为零）；
3. x&=(x-1):把二进制的X的最低位的1给变成0；
4. X&-x:得到最低位的1；
5. X&（~x）:为0
6. 获取X的第n位的值：（x>>n）&1;
7. 获取X的第n位的幂值：x&(1<<n);
8. 检查一个数是否是2的幂：X>0andx&(x-1)==0;

##### 经典例题

1. 汉明距离：这两个数字对应二进制位不同的位置的数目。

   ```c++
   //先异或，然后求出1的个数。利用异或相同位相等为0，不等为1，然后通过移位来判断各个位置的数字。class Solution {
   public:
       int hammingDistance(int x, int y) {
           int diff=x^y,ans=0;
           while(diff){//迭代判断
               ans+=diff&1;//与的运算
               diff>>=1;//diff=diff>>1;
           }
           return ans;
       }
   };
   ```

   

2. 颠倒二进制位（递增，递减两种思想）

   ```c++
   1.检索一个整数n最右边的位可以通过n&1；2.颠倒就是0到31的位置，可以直接左移位数，3.要检索二进制的没一位就要遍历，
   class Solution {
   public:
       uint32_t reverseBits(uint32_t n) {
           int result=0,bit=31;
           while(bit>=0){//以n为结束条件也可以，
               result+=(n&1)<<bit;//先确定好总共的位数，然后最后一位直接左移到第一位，
               n>>=1;//n一直右移的话最终为零
               bit-=1;
           }
           return result;
       }
   };
   class Solution {
   public:
       uint32_t reverseBits(uint32_t n) {
           int result=0;//能否理解为符号位?
           for(int i=0;i<32;i++){//
               result<<=1;//确定符号位之后开始左移给n的最低位留出空间，和上一种方法相比，第一种是先确定左移位数，直接赋值到这一位就行，可以理解为一开始确定最终位数，然后低贱。这种方法是递增位数，一开始从0开始，逐渐递增到需要满足的位数。
               result+=n&1;//把n的最低位赋值给result的最高位，
               n>>=1;//n右移，循环
           }
           return result;
       }
   };
   ```

   

3. 只出现一次的数字

   ```c++
   class Solution {
   public:
       int singleNumber(vector<int>& nums) {
           int result=0;
           for(const int &num:nums){
               result^=num;//遍历过程中，任何数和本身异或都是0.任何数和0异或都是本身。以0为初始值直接异或每个元素即可，最后剩下的肯定就是只出现一次的数字
           }
           return result;
       }
   };
   ```

   

4. 4的幂

   ```c++
   //普通解法
   class Solution {
   public:
       bool isPowerOfFour(int n) {
           for(int i=0;i<16;i++){
               if(n==pow(4,i))return true;//pow(x,y)返回x的y次幂。
           }
           return false;
       }
   };
   
   //位运算
   再来一次也做不出来
       class Solution {//先判断是不是2的幂，和全奇数为与，这个数是4的幂的话那就是2的偶数幂，2的偶数幂位与全奇数位等于0.
   public:
       bool isPowerOfFour(int n) {
           return n>0&&!(n&(n-1))&&!(n&0xaaaaaaaa);
       }//要看是不是都是真，
   };(101010...10)2​ 用十六进制表示为 ：(0xaaaaaaaa)16​。
   ```

   

5. 最大单词长度乘积

   ```c++
   //比较两个字母串是否有公共子母的方式。不同的条件下指向程序，但是条件又不方便写出来，可以直接用标志位标记下。也可以if..continue.但是没有if条件结合continue使用的时候，一般都是设置标志位。
   class Solution {
   public:
       int maxProduct(vector<string>& words) {//遍历每个单词，比较两个字母串之间是否有公共字母，没有更新最大值
           int result=0;
           bool a[1000][26]={false};//每个单词中的每个字母
           //统计每个单词中出现的字母
           for(int i=0;i<words.size();i++){
               for(int j=0;j<words[i].size();j++){
                   a[i][words[i][j]-'a']=true;//出现就是true//
               }
           }
           for(int i=0;i<words.size()-1;i++){
               for(int j=i+1;j<words.size();j++){
                   bool b=true;//避免计算重复字符的长度乘积
                   for(int k=0;k<26;k++){//判断两个字母串是否有公共字母
                       if(a[i][k]&&a[j][k]){//有就退出，后面程序不希望执行，可以放在里面for循环内，但是多次计算，这时候可以设置标志位，退出标志和下面希望程序执行标志，两种状态即可。
                           b=false;
                           break;
                       }
                   }
                   if(b&&result<words[i].size()*words[j].size())
                           result=words[i].size()*words[j].size();
   
               }
           }
           return result;
       }
   };
   class Solution {
   public:
   	bool cmp(string s1, string s2) {//两个单词不含有公共字母是前提条件，一行代码实现不了的话记得另外设置一个函数
   		for (int i = 0; i < s1.size(); i++) {
   			if (s2.find(s1[i]) != -1)return false;
   		}
   		return true;
   	}
   	int maxProduct(vector<string>& words) {
   		int max_result = 0;
   		for (int i = 0; i < words.size(); i++) {
   			for (int j = i + 1; j < words.size(); j++) {
   				if (cmp(words[i], words[j])) {
   					if (max_result < (words[i].size()*words[j].size())) {
   						max_result = (words[i].size()*words[j].size());
   					}
   				}
   			}
   		}
   		return max_result;
   	}
   };
   //位运算
   class Solution {
   public:
       int maxProduct(vector<string>& words) {
           unordered_map<int,int>myhash;//key为单词的位掩码，value为该位掩码对应的最大长度的字母串
           int result=0;
           for(const string word:words){
               //统计
               int mask=0,size=word.size();
               for(const char c:word){//计算一个单词的位掩码：遍历这个单词，先计算每个字母在位掩码中的位置n=(int)c-'a;然后将第n位的掩码设置为1（m=1<<n）;这时候每个字母的掩码都设置好了。然后利用或运算，合并到单词中，mask|=m;
                   mask|=1<<(c-'a');
               }
               myhash[mask]=max(myhash[mask],size);//可能是不同的单词具有相同的位掩码，例如a和aaaaaa，只要保存相同位掩码对应最大长度的字母串就行。
               for(auto [h_mask,h_len]:myhash){//哈希表中单词两两比较，这里代码经过优化，一般是外面建立两个for循环重新比较，这里是比较当前哈希表中的所有单词，每个单词都经过两两比较。
                   if(!(mask&h_mask)){//有重复的就是位与运算为1；
                       result=max(result,h_len*size);
                   }
               }
           }
           return result;
       }
   };
   ```

6. 比特位计数

   ```
   
   ```

   

7. 

### 高级数据结构

##### 二叉堆

###### 介绍

二叉堆是一种特殊的堆，具有完全二叉树的特性，堆中任何一个父节点的值都大于等于它左右孩子节点的值（最大堆），或者小于等于它左右孩子节点的值（最小堆）。

###### 插入一个节点



```c++
//插入的时候我们把新节点插入到完全二叉树的最后一个位置，之后再来调整。调整的原则是：让新插入的节点与它的父节点进行比较，如果新结点小于父节点，则让新节点上浮，即和父节点交换位置。上浮之后继续和他的父节点进行比较，直到父节点的值小于等于该节点，才停止上浮，即插入结束。
void swim(int i,vector<int>&a){//i=size-1;二叉树的最后一个位置
    while(i>0&&a[i]>a[i/2]){
        swap(a[i],a[i/2]);
        i/=2;
}
    
}
//插入
void push(int k,vector<int>&a){
    a.push_back(k);//先把新的数字放在最后一位，然后上浮
    swim(a.size()-1);
}

```

###### 删除一个节点（删除一个根节点）

删除和插入一样，删除的时候首先我们要马上恢复它具有完全二叉树的特性，之后再做调整。

```c++
//把根节点删除之后，用二叉堆的最后一个元素顶替上来，然后再进行调整恢复。调整的规则采用下沉的策略：让根节点和左右孩子节点比较，如果左右孩子小于根节点的值就让根节点下沉，
//删除就是相当于把最后一个元素赋值给根元素之后，然后对根元素执行下沉操作。
```

###### 构建一个二叉堆

构建：就是给你一个无序的完全二叉树，然后把他构建成二叉堆

方法：我们可以让所有非叶子节点一次下沉，是从下向上开始下沉，不是从根节点开始下沉。

```

```



##### 红黑树

##### B树

##### 跳跃列表



### 经典算法

### KMP

原理：

1. 详解https://www.cnblogs.com/tangzhengyue/p/4315393.html，https://www.bilibili.com/video/BV1L441147wB?from=search&seid=7857849543620439605，https://mp.weixin.qq.com/s/Gk9FKZ9_FSWLEkdGrkecyg，https://www.cnblogs.com/smile233/p/8134614.html

   ```c++
   经典问题
       暴力双指针
       class Solution {
   public:
   	int strStr(string haystack, string needle) {
   		int i = 0, j = 0;
   		while (i<haystack.size()&&j<needle.size())
   		{
   			if (haystack[i]==needle[j])
   			{
   				i++;
   				j++;
   			}
   			else
   			{
   				i = i - j + 1;//注意i的回溯就行
   				j = 0;
   			}
   		}
   		if (j>=needle.size())
   		{
   			return i-j;
   		}
   		return -1;
   	}
   };
   //    
   class Solution {
   public:
   	void getnext(int *next,string &T) {
   		int j= 0;//k是模式串遍历到的位置，也是模式串后缀的最后一个元素，
   		int k = -1;//k是当模式串和主串中元素不匹配时，j要回溯到的下一个位置的值，就是next[j]的值
   		next[0] = -1;
   		while (j<T.size()-1)
   		{
   			if (k==-1||T[j]==T[k])//
   			{
   				j++;
   				k++;
   				next[j] = k;//由next[j+1]=next[j]+1而来，也就是现在next数组更新，本来next[j]就是等于k的，如果是前后缀匹配好的下一个字符前后缀不匹配的话就是next[j+1]=k+1;也就是next[++j]=++k;
   			}
   			else
   			{
   				k = next[k];//k位置失配回退到next[k],可以理解：后缀是主串，前缀是子串，和KMP中j位置不匹配就回退到next[j]的意思一样。或者是现在已经T[k]!=T[j]了,那我们就去找短一点的最长相等的前后缀，j找最大相等的前后缀是回退到next[j]位置,同理k位置上不匹配去找最长相等前后缀就是回退到next[k],所以就是k=next[k]。
   			}
   		}
   	}
   	int strStr(string haystack, string needle) {
   		if (needle.size()==0)
   		{
   			return 0;
   		}
   		int i = 0, j = 0;
   		int *next = new int[needle.size()];
   		getnext(next, needle);
   		while (i<haystack.size()&&j<int(needle.size()))
   		{
   			if (j==-1||haystack[i]==needle[j])
   			{
   				i++;
   				j++;
   			}
   			else
   			{
   				j = next[j];//next就是当模式串T的指针j在主串S的某个位置与主串不匹配时，下一次指针j应该从T的哪个位置与主串进行匹配,j位置失配回退到next[j]
   			}
   		}
   		if (j==needle.size())
   		{
   			return i-j;
   		}
   		else
   		{
   			return -1;
   		}
   	}
   };
   ```

##### 补充知识

###### 数组的前缀、后缀和差分

https://blog.csdn.net/weixin_45629285/article/details/111146240

1. 一维数组前缀和

   定义：预处理O（n）S[i]就是数组a[0...i]的值。s[i]=a[1]+a[2]+a[3]+..a[i];

   查询：O(1):s[r]-s[l-1].求l到r之间的数组和

   a[l]+a[l+1]+...a[r]=s[r]-s[l-1];

   ```c++
   #include<iostream>
   #include<vector>
   #include<map>
   #include<unordered_map>
   using namespace std;
   int n, m;
   const int N = 100010;
   int a[N], s[N];
   int main() {
   	cin >> n >> m;
   	for (int i = 0; i < n; i++) {
   		cin >> a[i];
   	}
   	for (int i = 0; i < n; i++) {
   		s[i] = s[i - 1] + a[i];//预处理
   	}
   	while (m--)
   	{
   		int l, r;
   		cin >> l >> r;
   		cout << s[r] - s[l - 1];//直接使用，也可以写个函数
   	}
   	return 0;
   }
   ```

2. 二维数组前缀和

3. 一维差分数组

   ![image-20210425144710559](C:\Users\小面包\AppData\Roaming\Typora\typora-user-images\image-20210425144710559.png)

   ```
   
   ```

4. 二维差分

   



