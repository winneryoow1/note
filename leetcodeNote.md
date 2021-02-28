

#### 1、两数之和

```c
//1、给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值的那两个整数，并返回它们的数组下标。
#include <stdio.h>

int* twoSum(int* nums, int numSize, int target,  int* resultSize)
{
    int i,j;
    int *a = (int *)malloc(sizeof(int) * 2);
    for(i=0; i<numSize - 1; i++)
    {
        for(j=i+1; j<numSize; j++)
        {
            if(nums[i] + nums[j] == target)
            {
               a[0] = i;
               a[1] = j;
            }
               
        }
    }
    *resultSize = 2;
    return a;
}
```

```c
//2、给定一个已按照升序排列的整数数组numbers，请你从数组中找出两个数满足相加之和等于目标数target 
int* twoSum(int* numbers, int numbersSize, int target, int* returnSize){
   int *returnNUM = (int *)malloc(sizeof(int) * 2);
    int low = 0, high = numbersSize - 1;
    //二分法，用low和high分别向中间移动
    while(numbers[low] + numbers[high] != target)
    {
        if(numbers[low] + numbers[high] > target)
          high--;
        else 
          low++;
    }
        if(numbers[low] + numbers[high] == target)
        {
            returnNUM[0] = low+1;
            returnNUM[1] = high+1;
        }
    *returnSize = 2;
    return returnNUM;
}
```







#### 二、整数反转

```c
/* 
 1、给你一个 32 位的有符号整数 x ，返回 x 中每位上的数字反转后的结果。
如果反转后整数超过32位的有符号整数的范围 [−231,  231 − 1] ，就返回 0 
*/
int reverse(int x){
   long result=0,i;
   while(x!=0)
   {
      i = x % 10;
      result = result*10 + i;
      x /= 10;
   }
  return result>MAX_INT || result<MIN_INT ? 0:result;
}
```

##### tip: c语言中如何提取二进制数中的某一位?

* num % 2——取出二进制的最后一位

* num / 2——右移去掉二进制的最后一位

```c
//2、颠倒给定的 32 位无符号整数的二进制位
uint32_t reverseBits(uint32_t n) {
    uint32_t result=0, count=0;
    while(count < 32)
    {
        result = result * 2 + n % 2;
        n /= 2;
        count++;
    }
    return result;
}
```



##### 补充：位1的个数

```c
//编写一个函数，输入是一个无符号整数（以二进制串的形式），返回其二进制表达式中数字位数为 '1' 的个数
int hammingWeight(uint32_t n) {
    int count=0, num=0;
    while(count < 32)
    {
      if(n % 2 == 1)
        num++;
      n /= 2;
      count++;
    }
    return num;
}
```







#### 三、回文

```c
/*
1、给你一个整数 x ，如果 x 是一个回文整数，返回 true ；否则，返回 false 。
回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。例如，121 是回文，而 123 不是。
*/
bool isPalindrome(int x){
    long result = 0, n = x;
    while(x)
    {
        result = result * 10 + x % 10;
        x /= 10;
    }
    if(n >= 0 && result == n)
      return 1;
    else
      return 0;
}
```

```c
//2、判断一个链表是否为回文链表
//最简单的方法就是将链表的值复制到数组列表中，再使用双指针法判断。
/*
一共为两个步骤：
复制链表值到数组列表中。
使用双指针法判断是否为回文
*/
bool isPalindrome(struct ListNode* head){
   int arr[50001];
   int i=0, low, high;
   while(head != NULL)
   {
       arr[i++] = head->val;
       head = head -> next;
   }
   for(low=0, high=i-1;low<high; low++, high--)
   {
       if(arr[low] != arr[high])
         return false;
   }
   return true;

}
```

```c
//3、给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写
bool isPalindrome(char * s){
    int len = strlen(s);
   int i,j, k=0;
    for(i=0,j=0; i<len; i++)
    {
       if(s[i]>='0' && s[i]<='9' || s[i]>='a' && s[i]<='z')
            s[j++] = s[i];
       if(s[i]>='A' && s[i]<='Z')
            s[j++] = s[i]+32;
    }
    j--;
    while(k<j)
    {
        if(s[k] == s[j])
        {
               j--;
               k++;
        }
        else
           return false;
    }
    return true;
}
//tip:重新覆盖，不要重新定义一个新的数组（大小不确定，很容易出错）
```







#### 四、罗马数字转整数

```c
int romanToInt(char * s){
    //1、建立数字与字符的对应关系
    //2、找规律：若罗马数字中小的数字在大的数字的右边，则加；否则(那六种情况)，就减
    //借鉴思路
    int result = 0;
    while(*s)
    {
        switch(*s++)
        {
            case 'I': result += (*s == 'V'|| *s == 'X') ? -1:1;
                 break;
            case 'V': result += 5;
                 break;
            case 'X': result += (*s == 'L' || *s == 'C') ? -10:10;
                 break;
            case 'L': result += 50;
                 break;
            case 'C': result += (*s == 'D' || *s == 'M') ? -100:100;
                 break;
            case 'D': result += 500;
                 break;
            case 'M': result += 1000;
                 break;

        }
    }
   return result;
}
```







#### 五、合并有序

```c
//1、将两个升序链表合并为一个新的升序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 
struct ListNode* mergeTwoLists(struct ListNode* l1, struct ListNode* l2){
     struct ListNode* l3 = (struct ListNode*)malloc(sizeof(struct ListNode));
     l3 -> next = NULL;
     struct ListNode* p = l1;
     struct ListNode* q = l2;
     struct ListNode* s = l3;
     while(p && q)
     {
       if(p->val <= q->val)
       {
          s->next = p;
          s = p;
          p = p->next;
       }
       else{
           s->next = q;
           s = q;
           q = q->next;
       }
     }
     if(p) s->next = p;
     if(q) s->next = q;
     return l3->next;
}
```

```c
/*
2、给你两个有序整数数组 nums1 和 nums2，请你将 nums2 合并到 nums1 中，使 nums1 成为一个有序数组。
初始化 nums1 和 nums2 的元素数量分别为 m 和 n 。你可以假设 nums1 的空间大小等于 m + n，这样它就有足够的空间保存来自 nums2 的元素。
*/
void merge(int* nums1, int nums1Size, int m, int* nums2, int nums2Size, int n){
      int i=m-1, j=n-1, p=m+n-1;
      while(i>=0 && j>=0)
     {
        if(nums1[i] >= nums2[j])
           nums1[p--] = nums1[i--];
      else
         nums1[p--] = nums2[j--];
       }
      while(j>=0) //nums1的原元素全部比nums2小
         nums1[p--] = nums2[j--];
}
```

```c++
//3、给你一个按非递减顺序排序的整数数组 nums，返回 每个数字的平方组成的新数组，要求也按非递减顺序排序
//方法一：采用c++内置函数
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        for(int i=0; i<nums.size(); i++)
          nums[i] *= nums[i];
        sort(nums.begin(), nums.end());
        return nums;   
    }
};


//方法二:用一个新的数组来存放
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        vector<int> result(nums.size());
        int len = result.size() - 1;
        int low=0, high=nums.size()-1,i;
        while(low <= high) //双指针法
      {
         if(nums[low] * nums[low] < nums[high] * nums[high])
         {
            result[len--] = nums[high] * nums[high];
            high--;
         }
          else
         {
            result[len--] = nums[low] * nums[low];
            low++;
         }
     }
    return result;
    }
};
```







#### 六、删除目标项

```c
//1、给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度
//法一：
int removeDuplicates(int* nums, int numsSize){
    int fast=1, low=0;
    if(!numsSize)
      return 0;
    while(fast<numsSize)
    {
        if(nums[fast] != nums[low])
           nums[++low] = nums[fast];
        fast++;
    }
    return low+1;
}


//法二：双指针    
int removeDuplicates(int* nums, int numsSize){
      int* numNew = nums+1;
      int count = 1;
      if(!numsSize)
        return 0;
    for(int i=1; i<numsSize; i++)
    {
        if(*(numNew) != *(nums))
        {
             nums++;
            *(nums) = *(numNew);
            count++;
        }
            numNew++;  
    }
    return count;
}
```

```c
/*
2、给你一个数组nums和一个值val，你需要原地移除所有数值等于val的元素，并返回移除后数组的新长度。
不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并原地修改输入数组。
元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素
*/
int removeElement(int* nums, int numsSize, int val){
   int i,j=0;
   for(i=0; i<numsSize; i++)
   {
       if(nums[i] != val)
       {
           nums[j++] = nums[i];
       }
   }
   return j;
}
//不要想太多，直接用覆盖法就很方便！！！
```

```c
//3、删除链表中等于给定值 val 的所有节点
struct ListNode* removeElements(struct ListNode* head, int val){
     struct ListNode* p;
     struct ListNode* pre = head;
     if(!head)
       return NULL;
     while(head != NULL && head->val == val)
       head = head->next;
     while(pre != NULL)
     {
         p = pre->next;
         if(p != NULL && p->val == val)
         {
             pre->next = p->next;
              free(p);
         }
         else
           pre = pre->next;
    }
    free(pre);
    return head;
}
```

```c
//4、移动零：给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序
void moveZeroes(int* nums, int numsSize){
    int i,j,count=0;
    for(i=0,j=0; i<numsSize; i++)
    {
        if(nums[i] != 0)
        {
           nums[j++] = nums[i];
           count++;
        }
    }
    for(i=count; i<numsSize; i++)
      nums[i] = 0;
}
```

```c
//5、请编写一个函数，使其可以删除某个链表中给定的（非末尾）节点。传入函数的唯一参数为 要被删除的节点
//如何让自己在世界上消失，但又不死？ —— 将自己完全变成另一个人，再杀了那个人就行了
void deleteNode(struct ListNode* node) {
    struct ListNode* p = node->next;
    int temp;
    temp = node->val;
    node->val = p->val;
    p->val = temp;
    node->next = p->next;
    free(p);
}
```







#### 七、查找子字符串

```c
/*
1、实现 strStr()：给定一个 haystack字符串和一个needle字符串，在haystack字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回-1
*/
int strStr(char * haystack, char * needle){
        int len = strlen(needle);
            int i,j,k;
    if(len == 0)
       return 0;
    for(i=0; haystack[i] != '\0'; i++)
    {
        for(j=i,k=0; j<len+i; j++,k++)
        {
            if(haystack[j] != needle[k])
             break;
        }
        if(k == len)
         return i;
    }
    return -1;
}
//思想:遍历整个数组，每次都以子字符串的长度为单位进行查找
```

```c
/*
2、重复的子字符串：给定一个非空的字符串，判断它是否可以由它的一个子串重复多次构成。给定的字符串只含有小写英文字母，并且长度不超过10000
*/
bool repeatedSubstringPattern(char * s){
//列举字符串的重复长度i，然后从j=i开始每次都验证s[j] == s[j-i]
    int len = strlen(s);
    int i,j;
     for(i=1; i<=len/2; i++)
     {
         if(len % i == 0)
         {
             for(j=i; j<len; j++)
              {
                  if(s[j] != s[j-i])
                    break;
             }
         }
         if(j==len)
           return true;
     }
     return false;
}
```







#### 八、二分法搜索位置

```c
/*
1、搜索插入位置：给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置
*/
int searchInsert(int* nums, int numsSize, int target){
   int i;
    for(i=0; i<numsSize; i++)
    {
      if(nums[i] >= target)
         return i;
    }
   return numsSize;
}
```

```c
/*
2、第一个错误的版本：假设你有 n 个版本 [1, 2, ..., n]，你想找出导致之后所有版本出错的第一个错误的版本。通过调用 bool isBadVersion(version) 接口来判断版本号 version 是否在单元测试中出错。
*/
int firstBadVersion(int n) {
    int i=n;
    while(i>=1 && isBadVersion(i))
       i--;
    return i+1;
}

//二分法
int firstBadVersion(int n) {
      long low=1,high=n, mid;
        while(low <= high)
        {
            mid = (low+high)/2;
            if(!isBadVersion(mid))
               low = mid+1;
            else
              high = mid-1;
        }
        return low; 
}
```

```c
/*
3、猜数字游戏的规则如下：每轮游戏，我都会从 1 到 n 随机选择一个数字。请你猜选出的是哪个数字。如果你猜错了，我会告诉你，你猜测的数字比我选出的数字是大了还是小了。
你可以通过调用一个预先定义好的接口 int guess(int num) 来获取猜测结果，返回值一共有 3 种可能的情况（-1，1 或 0）：
-1：我选出的数字比你猜的数字小 pick < num
1：我选出的数字比你猜的数字大 pick > num
0：我选出的数字和你猜的数字一样。恭喜！你猜对了！pick == num
*/
int guessNumber(int n){
    long pick,low=1, high=n;
    while(low <= high && guess(pick)!=0)
    {
        pick = (low+high)/2;
        if(guess(pick) == -1)
          high = pick-1;
        else
           low = pick+1;
    }
    return pick;
}
```







#### 九、实现数学函数

```c
//1、实现 pow(x, n) ，即计算 x 的 n 次幂函数（即，x^n）
double dealPow(double x, long n) //递归计算（不断分解为小问题）
{
    if(n==1)
    return x;
    if(n % 2 != 0)
    {
        double des = dealPow(x, n/2);
        return des*x*des;
    }
    else
    {
        double des = dealPow(x, n/2);
        return des*des;
    }
}
double myPow(double x, long n){
    if(n==0 || x==1)
      return 1;
    if(n<0)
      return 1 / dealPow(x, fabs(n));
    return dealPow(x, n);
     
}
```

```c
//2、x的平方根
/*实现 int sqrt(int x) 函数。计算并返回 x 的平方根，其中 x 是非负整数。由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去*/
//经典二分法
int mySqrt(int x){ 
    int low=0, high=x;
    int mid,result=0;
    while(low <= high)
    {
        mid = low + (high - low) / 2;
         if((long long)mid*mid <= x)
        {
           result = mid;
           low = mid+1;
        }
        else
         high = mid-1;
    }
    return result;
}
```

```c
//3、有效的完全平方数
//给定一个正整数 num，编写一个函数，如果 num 是一个完全平方数，则返回 True，否则返回 False。
//经典二分法
bool isPerfectSquare(int num){
   int low=0, high=num;
   int mid;
   while(low <= high)
   {
       mid = (low+high)/2;
       if((long long)mid*mid == num)
         return true;
       else if((long long)mid*mid < num)
         low = mid+1;
       else
         high = mid-1;
   }
     return false;
}
```

```c
//4、平方数之和
//给定一个非负整数 c ，你要判断是否存在两个整数 a 和 b，使得 a2 + b2 = c
//经典二分法
bool judgeSquareSum(long c){
    long low=0, high=sqrt(c);
    while(low <= high)
    {
        if(low*low + high*high == c)
          return true;
        else if(low*low + high*high > c)
           high = high-1;
        else
          low = low+1;
    }
    return false;
}
```







#### 十、最大子序和

```c
/*
1、给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和
*/
int maxSubArray(int* nums, int numsSize){
   int i;
   int sum=0, max=-3276888;
   for(i=0; i<numsSize; i++)
   {
       if(sum < 0)
        sum = 0;//若前面的值为负，则清零重新开始累加
      sum += nums[i];
       if(sum > max)
         max = sum;
   }
   return max;
}

//如果前面的数是负值，那么加上当前的值，肯定会更小，那么我们抛弃前面的值，直接从当前值开始就行了。
//如果前面的数是正值，那么加上当前的值，有可能变小，有可能变大，这要看当前的值是负数还是正数
```

```c
//2、买卖股票的最佳时机
int maxProfit(int* prices, int pricesSize){
//记录【今天之前买入的最小值】
//计算【今天之前最小值买入，今天卖出的获利】，也即【今天卖出的最大获利】
//比较【每天的最大获利】，取最大值即可
    int min=0,max=0,i,profit=0,sum=0;
    for(i=1; i<pricesSize; i++)
    {
        if(prices[i] < prices[min])
          min=i;
        sum=prices[i]-prices[min];
        if(sum>profit)
         profit=sum;
    }
  
    return profit;
}
```

```c
/*
变形：
给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。
设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）
*/
int maxProfit(int* prices, int pricesSize){
    int i, profits=0;
    for(i=0; i<pricesSize-1; i++)
    {
        if(prices[i] < prices[i+1])
            profits += prices[i+1] - prices[i];
    }
     return profits; 
}
//因为交易次数不受限，如果可以把所有的上坡全部收集到，一定是利益最大化的
/*不要整块的去看，而是把整体利润拆为每天的利润。使用贪心算法：只收集每天的正利润，最后稳稳的就是最大利润了。*/
```







#### 十一、最后一个单词的长度

```c
/*
给你一个字符串 s，由若干单词组成，单词之间用空格隔开。返回字符串中最后一个单词的长度。如果不存在最后一个单词，请返回 0
*/
int lengthOfLastWord(char * s){
    //灵活运用加减法（长串-短串）
     int i;
     int len = strlen(s)-1, count;
     while(len>=0 && s[len] == ' ')
        --len;
     count = len;
     while(len>=0 && s[len] != ' ')
        --len;
     return count-len;
}
```







#### 十二、加一/求和

```java
//1、给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。
class Solution {
    public int[] plusOne(int[] digits) {
         int len = digits.length;
         int i;
         for(i=len-1; i>=0; i--)
         {
            digits[i]++;
            digits[i] = digits[i] % 10;
            if(digits[i] != 0)
              return digits;
         }
        digits = new int[len+1];
         digits[0] = 1;
         return digits;
    }
}
/* 
只要+1求余数，余数不等于0，说明没有进位，直接返回。如果余数等于0，说明有进位，遍历前一个数字，加1再求余数，以此循环。如果for循环都遍历完了，说明最高位也有进位，则重新建立一个数组，初始化为0，将第一位设置为1就可以了，因为，99、999之类的数字加一为100、1000 
*/
```

```c
//2、给你两个二进制字符串，返回它们的和（用二进制表示）。输入为非空字符串且只包含数字1和0
char * addBinary(char * a, char * b){
    int alen=strlen(a);
    int blen=strlen(b);
    int binary=0;
    int len;
    len=alen>blen?alen:blen;
    int anum,bnum,sum;
    char* s=(char*) malloc ((len+2) * sizeof(char));
    s[len+1]='\0';
    for(--alen,--blen;len>=0;alen--,blen--,len--){
        if(alen<0) //少的位补0
           anum=0;
        else
           anum=a[alen]-'0';
        if(blen<0)
           bnum=0;
        else
           bnum=b[blen]-'0';
        sum=anum+bnum+binary;
        //binary=sum/2;
        s[len]='0'+sum%2;
        if(sum >= 2)
          binary = 1;
        else
          binary = 0;
    }
    if(s[0]=='0')
    return &s[1];
    else return &s[0];
}
//每次加上进位——前一次结果传过来的
```

```c
/*
3、对于非负整数X而言，X的数组形式是每位数字按从左到右的顺序形成的数组。例如，如果X=1231，那么其数组形式为 [1,2,3,1]。
给定非负整数 X 的数组形式 A，返回整数 X+K 的数组形式
*/
int* addToArrayForm(int* A, int ASize, int K, int* returnSize){
       int * result =  malloc(sizeof(int) * fmax(10, ASize + 1));
       *returnSize = 0;
       int i, temp, sum=0;
       for(--ASize; ASize>=0; ASize--)
       {
          sum = A[ASize] + K%10;
           K /= 10;
         if (sum >= 10) {
            K++; //进位放到K中
            sum %= 10;
          }
         result[(*returnSize)++] = sum % 10;
         //bit = sum / 10;
       }
       for(; K>0; K/=10)
         result[(*returnSize)++] = K%10;
       for(i=0; i<(*returnSize)/2; i++) //反转
       {
           temp = result[i];
           result[i] = result[(*returnSize)-i-1];
           result[(*returnSize)-i-1] = temp;
       }
        
       return result;
}
```

```c
//4、给定两个字符串形式的非负整数 num1 和num2 ，计算它们的和
char * addStrings(char * num1, char * num2){
     int len1 = strlen(num1)-1;
     int len2 = strlen(num2)-1;
    char * s = (char*)malloc(sizeof(char) * (fmax(len1, len2) + 3));
     int len=0, add=0, sum=0, anum, bnum, temp,i;
     while(len1>=0 || len2>=0 || add != 0) //保证只有进位时仍然能加
     {
        anum = len1 < 0 ? 0 : num1[len1]-'0';
        bnum = len2 < 0 ? 0 : num2[len2]-'0';
        sum = anum + bnum + add;
        s[len++] = sum % 10 + '0';
        add = sum/10;
        len1--;
        len2--;
     }
     for(i=0; i<len/2; i++)
     {
        temp = s[i];
        s[i] = s[len-i-1];
        s[len-1-i] = temp;
     }
     s[len++] = 0;
     return s;
}
```







#### 十二、删除链表重复元素

```c
//1、给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次
struct ListNode* deleteDuplicates(struct ListNode* head){
    struct ListNode*p = head;
    struct ListNode*q = head;
    while(p != NULL)
    {
        //用q试探，如果与p所指的值不相等则让p->next指向q
        if(p->val != q->val) 
        {
            p->next = q;
            p=q;
        }
        q=q->next;
        if(q==NULL)
        {
            p->next = NULL;
            return head;
        }
     }
     return head;
}
```

```c
//2、给定一个排序链表，删除所有含有重复数字的节点，只保留原始链表中没有重复出现的数字
//输入: 1->2->3->3->4->4->5   输出: 1->2->5
struct ListNode* deleteDuplicates(struct ListNode* head){
    if(head==NULL)
      return NULL;
  struct ListNode*s = malloc(sizeof(struct ListNode));
   s->next = head;
   struct ListNode* pre=s;
   struct ListNode* p=head;
   while(p != NULL && p->next != NULL)
   {
       //碰到相等的元素就一直向后走
       while(p != NULL && p->next != NULL && p->val == p->next->val)
          p=p->next;
       //间隔多个相同元素
       if(pre->next != p)
          pre->next = p->next;
       else
          pre=p;
       p=p->next;
   }
    return s->next;
}
```







#### 十三、二叉树的应用

```c
/*
1、相同的树：给你两棵二叉树的根节点 p 和 q ，编写一个函数来检验这两棵树是否相同。如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。
*/
bool isSameTree(struct TreeNode* p, struct TreeNode* q){
    int flag1, flag2;
     if(p == NULL && q == NULL)
       return true;
     else if(p == NULL || q == NULL)
       return false;
     else
      {
          if(p->val != q->val)
             return false;
           else{
                flag1 = isSameTree(p->left, q->left);
                flag2 = isSameTree(p->right, q->right);
                return flag1 && flag2;
           }
      }
      return flag1 && flag2;
}
//先判断错的
```

```c
//2、对称二叉树：给定一个二叉树，检查它是否是镜像对称的
//镜像比较-双指针
bool Judge(struct TreeNode* p,struct TreeNode* q){
   if(p == NULL && q == NULL)
     return true;
   else if(p== NULL || q == NULL || p->val != q->val)
     return false;
   else
     return Judge(p->left, q->right) && Judge(p->right, q->left);
}

bool isSymmetric(struct TreeNode* root){
    return Judge(root, root);
}
```

```c
/*
3、给定一个二叉树，找出其最大深度。二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。
说明: 叶子节点是指没有子节点的节点给定一个二叉树，找出其最大深度。
*/
int maxDepth(struct TreeNode* root){
   if(root == NULL)
     return 0;
   else
   {
       int len1 = maxDepth(root->left);
       int len2 = maxDepth(root->right);
       return len1 > len2 ? len1+1:len2+1;
   }
}
```

