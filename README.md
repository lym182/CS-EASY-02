# 2024090914025-李伊眉-CS-02
## 学习心得与路径
- 心得：这半个月被狠狠洗礼，还是之前高估自己了，以为能很快解决，国庆特种兵旅游七天归来后才开始看题（甚至还有闲心去练舞我的天。。）仔细一看要学的超级超级多，而开始熬夜补，最忙的一周平均每天两点半睡七点起，学到崩溃，，，没想到停了其他的事，一堆意外事件接踵而至，一次次耗费我大量的时间，一点开群发现交题截至时间提前（天塌了...）反反复复写，结果怎么都不对，最后两天发现两个大的题目题目全看错，又紧急改，，，改到现在才终于能交了。这半个月真是太让人难崩了，有种磨练赶ddl能力的感觉，同时也让我体会到在时间紧的情况下该怎么以平静的心态去处理种种突发情况，也是体会到了高三都没有的待遇--周末去图书馆自习，有一种奇妙的充实感，真好，又学会了好多东西。
- 路径：B站，问朋友
## 问题回答
1. 在相同的时间内访问到线性表中的任意一个元素；顺序表。

2. 指针是存储另一个变量内存地址的变量；*指针变量名；指针变量的大小不是固定的，它取决于所使用的操作系统和编译器。在32位系统中，指针变量的大小为4 个字节；在64位系统中，指针变量的大小为8个字节。
3.
   一、数组
 - 当需要存储一组具有相同数据类型的元素，且元素数量已知并且相对固定时，数组非常适用。
 - 当需要随机访问元素时，数组效率很高，因为可以通过下标直接定位到元素，时间复杂度为O(1)。

   二、链表
 - 当数据的数量不确定，需要频繁地进行插入和删除操作时，链表比较适用。
 - 链表可以有效地利用分散的内存空间，不像数组需要连续的大块内存。

   三、栈
 - 函数调用和表达式求值是栈的典型应用场景。
 - 回溯问题中，栈可以用来记录状态以便回溯。

   四、队列
 - 当需要按照先进先出的顺序处理数据时，队列非常适用。
 - 模拟排队场景，如银行排队叫号系统、打印机任务队列等。

   五、树
 - 层次化的数据组织。
 - 高效的搜索和排序。
  
   六、图
 - 表示复杂的关系网络。
 - 解决各种图论问题。

4.邻接矩阵和邻接表
## 代码
```
#include <stdio.h>
#include <stdlib.h>
//栈数据类型
typedef int STDataType;
//声明一个栈结构体
typedef struct Stack{
    char* a;//动态数组
    STDataType top;//栈顶
    STDataType capacity;//容量
}ST;
//声明一个节点结构体
struct node{
    int data;
    struct node* next;
};
//创建新节点
struct node* create_newnode(int data);
//创建直型链表
struct node* create_straightlist(int length);
//打印直型链表
void print_straightlist(struct node* head);
//打印环形链表
void print_circularlist(struct node* head);
//释放空间
void free_straightlist(struct node** head);
//H操作
void front_insert(struct node** head,int data);
//T操作
void back_insert(struct node* head,int data);
//D操作
void del(struct node** head,int location);
//C操作
void circulate(struct node* head);
//把数据为3的节点设为头节点
void head_value(struct node** head,int data);
//每次游戏移动头节点
void head_move(struct node** head,struct node* nextnode);
//初始化
void Stack_in_it(ST* ps);
//入栈
void STPush(ST* ps, int i, char secrect[]);
//出栈
void STPop(ST* ps);


int main(void){
    int length = 1;
    struct node* list = create_straightlist(length);
    back_insert(list,1);
    back_insert(list,1);
    back_insert(list,1);
    front_insert(&list,1);
    front_insert(&list,2);
    front_insert(&list,3);
    back_insert(list,1);
    back_insert(list,3);
    back_insert(list,1);
    del(&list,9);
    front_insert(&list,1);
    front_insert(&list,2);
    front_insert(&list,1);
    back_insert(list,2);
    back_insert(list,2);
    back_insert(list,2);
    front_insert(&list,2);
    front_insert(&list,1);
    front_insert(&list,2);
    del(&list,1);
    front_insert(&list,1);
    front_insert(&list,2);
    front_insert(&list,2);
    back_insert(list,1);
    back_insert(list,2);
    back_insert(list,2);
    del(&list,23);
    back_insert(list,2);
    back_insert(list,1);
    back_insert(list,1);
    back_insert(list,2);
    back_insert(list,2);
    back_insert(list,2);
    front_insert(&list,1);
    front_insert(&list,2);
    front_insert(&list,1);
    front_insert(&list,1);
    front_insert(&list,1);
    front_insert(&list,1);
    circulate(list);
    print_circularlist(list);
    printf("\n");
    int number = 34;
    int arr[50] = {0};
    //将3所在节点设为头节点
    head_value(&list,3);
    //检查
    if(list == NULL){
        return 0;
    }
    //第N轮移动N-1次
    for(int i = 0;i <number; i++){
        struct node* goal = list;
        for(int j = 0; j < i; j++){
            goal = goal->next;
        }
        //将每次删除的数依次存入数组
        arr[i] = goal->data;
        //打印每次被删除的数据
        printf("Round %d: %d\n",i+1,goal->data);
        //将所删节点前后链接
        struct node* nextnode = goal->next;
        //先判断是否删去头节点，若不判断则若释放头节点后面传入list后无法对链表进行操作
        if(goal == list){
            list = nextnode;
        }
        struct node* prev = list;
        while (prev->next != goal){
            prev = prev->next;
        }
            prev->next = nextnode;
        //释放目标节点并移动头节点
        free(goal);
        head_move(&list,nextnode);
    }
    //解密过程
    int i = 0;
    ST ps;
    Stack_in_it(&ps);
    char secret[] = "kiglnmrmeiahenrteof4ardar";
    for (int j = 1; j <= 34; j++)
    {   
        //判断奇数位还是偶数位
        switch (j % 2)
        {
        case 1:
            for (int m = 0; m < arr[j - 1]; m++,i++)
            {
                
               STPush(&ps, i, secret);
               
            }
            break;
        case 0:
            for (int k = 0; k < arr[j - 1]; k++)
            {
                STPop(&ps);
            }
            break;
        
        }
    }
    printf("\n");
    free_straightlist(&list);
    system("pause");
    return 0;
}
//创建新节点
struct node* create_newnode(int data){
    struct node* newnode = (struct node*)malloc(sizeof(struct node));
    newnode->data = data;
    newnode->next = NULL;
    return newnode;
}
//创建直型链表
struct node* create_straightlist(int length){
    if (length <= 0){
        return NULL;
    }
    struct node* head = create_newnode(1);
    struct node* temp = head;
    temp->next = NULL;
    return head;
}
//打印直型链表
void print_straightlist(struct node* head){
    if (head == NULL){
        printf("链表为空");
        return;
    }
    struct node* temp = head;
    do{
        printf("%d->",temp->data);
        temp = temp->next;
    }while(temp != NULL);
    printf("NULL");
}
//打印环形链表
void print_circularlist(struct node* head){
    if (head == NULL ){
        printf("你的链表为空");
        return;
    }
    struct node* temp = head;
    do{
        printf("%d->",temp->data);
        temp = temp->next;
    }while(temp != head);
}
//释放空间
void free_straightlist(struct node** head){
    struct node* current = * head;
    do{
        struct node* bridge = current->next;
        free(current);
        current = bridge;
    }while(current != NULL);
    * head = NULL;
}
//H操作
void front_insert(struct node** head,int data){
    struct node* newnode = create_newnode(data);
    newnode->data = data;
    newnode->next = *head;
    *head = newnode;
}
//T操作
void back_insert(struct node* head,int data){
    struct node* newnode = create_newnode(data);
    newnode->data = data;
    newnode->next = NULL;
    if(head == NULL){
        head = newnode;
    }
    else{
        struct node* last_node = head;
        while(last_node->next != NULL){
            last_node = last_node->next;
        }
        last_node->next = newnode;
    }
}
//D操作
void del(struct node** head,int location){
    if (*head == NULL){
        return;
    }
    else if(location > 1 ){
        struct node* goal = *head;
        struct node* temp = *head;
        for (int i = 0; i < location-2; i++){
            temp = temp->next;
        }
        goal = temp->next;
        struct node* bridge = goal->next;
        free(goal);
        temp->next = bridge;
    }
    else if(location ==1){
        struct node* newnode = *head;
        *head = (*head)->next;
        free(newnode);
        return;
    }
    else{
        return;
    }
}
//C操作
void circulate(struct node* head){
    if (head == NULL){
        return;
    }
    else{
        struct node* last_node = head;
        while(last_node->next != NULL){
            last_node = last_node->next; 
        }
        last_node->next = head;
    }
}
//把数据为3的节点设为头节点
void head_value(struct node** head,int data){
    struct node* temp = *head;
    do{
        temp = temp->next;
    }while(temp->data != data);
    *head = temp;
}
//每次游戏移动头节点
void head_move(struct node** head,struct node* nextnode){
    struct node* temp = *head;
    do{
        temp = temp->next;
    }while(temp != nextnode);
    *head = temp;
}
//初始化
void Stack_in_it(ST* ps){
    ps->a =(char*)malloc(sizeof(char) * 26);
    ps->top = 0;
    ps->capacity = 26;
}
//入栈
void STPush(ST* ps, int i, char secret[]){
    ps->a[ps->top] = secret[i];
    ps->top++;
}
//出栈并输出结果
void STPop(ST* ps){
    if(ps->top == 0){
        return;
    }
    printf("%c",ps->a[ps->top - 1]);
    ps->top--;
}
```
