# Data Structures and Algorithm Analysis in C 

## 第一部分 算法初探

### bubble

```c
/* selection_problem_bubble.c */
#include <stdio.h>

void bubble_sort(int [], int); 

int main() {
    int a[] = {33, 42, 17, 14, 23, 89, 25, 100, 99, 8};
    int a_len = sizeof(a) / sizeof(int);
    //int a_len = sizeof(a) / sizeof(a[0]);

    for (int k = 0; k < a_len; k++) {
        printf("%d ", a[k]);
    }
    printf("\n\n");

    bubble_sort(a, a_len);

    for (int k = 0; k < a_len; k++) {
        printf("%d ", a[k]);
    }
    printf("\n\n");
    
    printf("10-3 = %d\n", a[2]);
    printf("\n\n");
}

void bubble_sort(int a[], int len) {
    for (int i = 0; i < len - 1; i++) {
        for(int j = 0; j < len - 1 - i; j++) {
            if (a[j] < a[j + 1]) {
                int temp = a[j];
                a[j] = a[j + 1];
                a[j + 1] = temp;
            }
        }
    }   
}
/*
33 42 17 14 23 89 25 100 99 8 
100 99 89 42 33 25 23 17 14 8 
10-3 = 89
*/
```

### top3

```c
/* selection_problem_strength.c */
#include <stdio.h>

void top3_sort(int []);

int main() {
    int a[] = {33, 42, 17, 14, 23, 89, 25, 100, 99, 8};
    int a_length = sizeof(a) / sizeof(int);
    //int a_length = sizeof(a) / sizeof(a[0]);
    for (int k = 0; k < a_length; k++) {
        printf("%d ", a[k]);
    }
    printf("\n\n");
    
    top3_sort(a);

    for(int i = 3; i < a_length - 1; i++) {
        if (a[i] > a[2]) {
            a[2] = a[i];
            top3_sort(a);
        }
    }
    for (int k = 0; k < a_length; k++) {
        printf("%d ", a[k]);
    }
    printf("\n\n");  
    printf("10-3 = %d", a[2]);
    printf("\n\n");
}

void top3_sort(int a[]) {
    for(int j = 0; j < 2; j++) {
        for (int k = 0; k < 2- j; k++) {
            if (a[j] < a[j + 1]) {
                int temp = a[j];
                a[j] = a[j + 1];
                a[j + 1] = temp;
            }
        }
    }
}
/*
33 42 17 14 23 89 25 100 99 8 
100 99 89 14 23 89 25 100 99 8 
10-3 = 89
*/

```

### gcd

```c
/* gcd.c */
#include <stdio.h>

int gcd(int m, int n);
int main() {
    int i = gcd(45, 18);
    printf("%d\n", i);
}

int gcd(int m, int n) {  
    int rem;
    while (n > 0) {
        rem = m % n;
        m = n;
        n = rem;
    }
    return m;
}
/* 9 */
```

### pow

```c
/*
pow.c
*/
#include <stdio.h>

int p_pow(int x, int n);
int main() {
    int i = p_pow(2, 8);
    printf("%d\n", i);
}

int p_pow(int x, int n) {
    if (n == 0) {
        return 1;
    }
    if (n == 1) {
        return x;
    }
    if (n % 2 == 0) {
        return p_pow(x * x, n / 2);
    } else {
        return p_pow(x * x, n / 2) * x;
    }
}
/* 256 */

```

### binary_search

```c
/*
binary_search.c
*/
#include <stdio.h>

int binary_search(int [], int, int); 

int main() {
    int a[] = {1, 2, 3, 4, 5, 6, 7, 8, 9};
    int i = binary_search(a, 8, 10);
    printf("%d\n", i);
}

int binary_search(int a[], int x, int len) {
    int low, mid, high;
    low = 0;
    high = len - 1;
    while (low <= high) {
        mid = (low + high) / 2;
        if (a[mid] < x) {
            low = mid + 1;
        } else if (a[mid] > x) {
            high = mid - 1;
        } else {
            return mid;
        }
    }
    return -1;
}
/* 7 */
```

### max_sub_sum

```c
/* max_subsequence_sum.c */
#include <stdio.h>

int max_subsequence_sum1(int a[], int len);
int max_subsequence_sum2(int a[], int len);
int max_subsequence_sum3(int a[], int len);
int max_subsequence_sum4(int a[], int len);

int main() {
    int a[] = {4, -3, 5, -2, -1, 2, 6, -2};

    int max_sum1 = max_subsequence_sum1(a, 8);
    printf("%d\n", max_sum1);

    int max_sum2 = max_subsequence_sum2(a, 8);
    printf("%d\n", max_sum2);
    
    int max_sum3 = max_subsequence_sum3(a, 8);
    printf("%d\n", max_sum3);

    int max_sum4 = max_subsequence_sum4(a, 8);
    printf("%d\n", max_sum4);
}


int max_subsequence_sum1(int a[], int len) {

    int this_sum, max_sum;
    max_sum = 0;
    for (int i = 0; i < len; i++) {
        for (int j = i; j < len; j++) {
            this_sum = 0;
            for (int k = i; k <= j; k++) {
                this_sum += a[k];
            }
            if (this_sum > max_sum) {
                max_sum = this_sum;
            }
        }
    }
    return max_sum;
}

int max_subsequence_sum2(int a[], int len) {

    int this_sum, max_sum;
    max_sum = 0;
    for (int i = 0; i < len; i++) {
        this_sum = 0;
        for (int j = i; j < len; j++) {
            this_sum += a[j];

            if (this_sum > max_sum) {
                max_sum = this_sum;
            }

        }
    }
    return max_sum;
}

int max_sub_sum(int [], int, int);
int max_subsequence_sum3(int a[], int len) {
    return max_sub_sum(a, 0, len - 1);
}

int max3(int, int, int);
int max_sub_sum(int a[], int left, int right) {

    int max_left_sum, max_right_sum;
    int max_left_border_sum, max_right_border_sum;
    int left_border_sum, right_border_sum;
    int center, i;

    if (left == right) {
        if(a[left] > 0) {
            return a[left];
        } else {
            return 0;
        }
    }

    center = (left + right) / 2;

    max_left_sum = max_sub_sum(a, left, center);
    max_right_sum = max_sub_sum(a, center+1, right);

    max_left_border_sum = 0;
    left_border_sum = 0;
    
    for (i = center; i >= left; i--) {
        left_border_sum += a[i];
        if (left_border_sum > max_left_border_sum) {
            max_left_border_sum = left_border_sum;
        }
    }

    max_right_border_sum = 0;
    right_border_sum = 0;

    for (i = center + 1; i <= right; i++) {
        right_border_sum += a[i];
        if (right_border_sum > max_right_border_sum) {
            max_right_border_sum = right_border_sum;
        }
    }

    return max3(max_left_sum, max_right_sum, max_left_border_sum + max_right_border_sum);

}

int max3(int a, int b, int c) { 
    int max;
    max = a > b ? a : b;
    max = max > c ? max : c;
    return max;
}

int max_subsequence_sum4(int a[], int len) {

    int this_sum, max_sum;
    this_sum = 0;
    max_sum = 0;
    for (int i = 0; i < len; i++) {
        this_sum += a[i];
        if (this_sum > max_sum) {
            max_sum = this_sum;
        } else if (this_sum < 0) {
            this_sum = 0;
        }
    }
    return max_sum;
}
/* 11 11 11 11*/
```



## 第二部分 链表

### linked_list

```c
/* linked_list.c */
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

// 函数原型声明
// 创建表头
struct Node *createHeaderNode();

// 从表头插入
void insertFirst(struct Node *header, int x);

// 从表尾插入
void insertLast(struct Node *header, int x);

// 查找x，如果没有找到，返回NULL
struct Node *find(struct Node *header, int x);

// 查找位置为position的结点,如果没有找到，返回NULL
struct Node *findKth(struct Node *header, int position);

// 删除第一个值匹配的结点
void delete(struct Node *header, int x);

// 判断表是否为空
bool isEmpty(struct Node *header);

// 表中结点个数
int size(struct Node *header);

void printList(struct Node *header);

struct Node {
    int element;    // node value
    struct Node *next; // next node point
};

int main() {
    
    struct Node *node;
    struct Node *header;

    // 创建表头
    header = createHeaderNode();

    // 判断表是否为空
    printf("List is empty?: %d\n", isEmpty(header));
    printf("================================");
    printf("\n");

    // 从表头插入
    insertFirst(header, 1);
    insertFirst(header, 2);

    printList(header);
    printf("================================");
    printf("\n");

    // 从表尾插入
    insertLast(header, 3);
    insertLast(header, 4);

    printList(header);
    printf("================================");
    printf("\n");

    // 查找结点值为3的结点
    node = find(header, 3);
    if (node == NULL) {
        printf("not find...\n");
    } else {
        printf("find node element: %d\n", node->element);
    }
    printf("================================");
    printf("\n");

    // 查找表中第2个结点
    node = findKth(header, 2);
    if (node == NULL) {
        printf("not find...\n");
    } else {
        printf("find node element: %d\n", node->element);
    }
    printf("================================");
    printf("\n");

    // 删除结点值为3的结点
    delete(header, 3);
    printList(header);
    printf("================================");
    printf("\n");

    // 打印表中结点个数，即表的大小
    printf("List size: %d\n", size(header));
    printf("================================");
    printf("\n");
}


// 创建表头
struct Node *createHeaderNode() {

    struct Node *p;
    p = malloc(sizeof(struct Node));

    if (p == NULL) {
        printf("内存分配失败\n");
        exit(1);
    }

    p->next = NULL;

    return p;
}

// 判断表是否为空
bool isEmpty(struct Node *header) {
    return header->next == NULL;
}

// 从表头插入
void insertFirst(struct Node *header, int x) {

    struct Node *tmp;

    tmp = malloc(sizeof(struct Node));

    if (tmp == NULL) {
        printf("内存不足\n");
        return;
    }

    tmp->element = x; //给结点赋值
    tmp->next = header->next;

    header->next = tmp;

    return;
}

// 从表尾插入
void insertLast(struct Node *header, int x) {
    
    struct Node *p;
    struct Node *tmp;

    tmp = malloc(sizeof(struct Node));

    if (tmp == NULL) {
        printf("内存不足\n");
        return;
    }

    tmp->element = x; //给结点赋值
    tmp->next = NULL;

    p = header;

    while (p->next != NULL) {
        p = p->next;
    }

    p->next = tmp;

    return;
}

// 查找x，如果没有找到，返回NULL
struct Node *find(struct Node *header, int x) {
    
    struct Node *p;

    p = header->next;

    while (p != NULL && p->element != x) {
        p = p->next;
    }

    return p;
}

// 查找位置为position的结点,如果没有找到，返回NULL
struct Node *findKth(struct Node *header, int position) {
    
    int count = 1;
    struct Node *p;

    if (position <= 0) {
        printf("position 不能为负数\n");
        return NULL;
    }

    p = header->next;

    while (p != NULL) {
        if (count == position) {
            return p;
        }

        p = p->next;
        count++;
    }

    return NULL;
}

// 删除第一个值匹配的结点
void delete(struct Node *header, int x) {
    
    struct Node *previous; // 被删除结点的前一个结点的指针
    struct Node *p;

    previous = header;
    p = header->next;

    while (p != NULL) {
        if (p->element == x) {
            previous->next = p->next;
            free(p);
            break;
        } else {
            previous = p;
            p = p->next;
        }
    }
    return;
}

// 表中结点个数
int size(struct Node *header) {

    int count = 0;
    struct Node *p;

    p = header->next;

    while (p != NULL) {
        count++;
        p = p->next;
    }

    return count;
}

// 
void printList(struct Node *header) {
    
    struct Node *p;
    p = header->next;

    while (p != NULL) {
        printf("node element = %d\n", p->element);
        p = p->next;
    }

    return;
}
/*
List is empty?: 1
================================
node element = 2
node element = 1
================================
node element = 2
node element = 1
node element = 3
node element = 4
================================
find node element: 3
================================
find node element: 1
================================
node element = 2
node element = 1
node element = 4
================================
List size: 3
================================
*/
```

### array_list

```c
/*array_list.c*/
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

#define SIZE 100

// 函数原型声明
// 创建表头
struct List *createList();

// 从表头插入
void insertFirst(struct List *p, int x);

// 从表尾插入
void insertLast(struct List *p, int x);

// 返回x所在数组的脚标
int find(struct List *p, int x);

// 返回position位置上的元素值
int findKth(struct List *p, int position);

// 删除第一个值匹配的结点
void delete(struct List *p, int x);

// 判断表是否为空
bool isEmpty(struct List *p);

// 表中结点个数
int size(struct List *p);

void printList(struct List *p);

struct List {
    int elements[SIZE];    // 表的元素都存储在数组里
    int length;            // 表中元素的长度（即个数），实际存储的有效元素个数
};

int main() {
    
    int index;
    int element;

    // 创建一个空表
    struct List *list = createList();

    // 判断表是否为空
    printf("List is empty?: %d\n", isEmpty(list));
    printf("================================");
    printf("\n");

    // 从表头插入
    insertFirst(list, 1);
    insertFirst(list, 2);

    printList(list);
    printf("================================");
    printf("\n");

    // 从表尾插入
    insertLast(list, 3);
    insertLast(list, 4);

    printList(list);
    printf("================================");
    printf("\n");

    // 查找结点值为3的结点
    index = find(list, 3);
    if (index == -1) {
        printf("not find...\n");
    } else {
        printf("find index element: %d\n", index);
    }
    printf("================================");
    printf("\n");

    // 查找表中第2个结点
    element = findKth(list, 2);
    printf("find element: %d\n", element);
    printf("================================");
    printf("\n");

    // 删除结点值为3的结点
    delete(list, 3);
    printList(list);
    printf("================================");
    printf("\n");

    // 打印表中结点个数，即表的大小
    printf("List size: %d\n", size(list));
    printf("================================");
    printf("\n");
}


// 创建新表
struct List *createList() {

    struct List *p;
    p = malloc(sizeof(struct List));

    p->length = 0;

    return p;
}

// 判断表是否为空
bool isEmpty(struct List *p) {
    return p->length == 0;
}

// 从表头插入
void insertFirst(struct List *p, int x) {
    
    int i;

    if (p->length >= SIZE) {
        printf("表已满\n");
        return;
    }

    for (i = p->length; i > 0; i--) {
        p->elements[i] = p->elements[i - 1];
    }

    p->elements[0] = x;
    p->length++;

    return;
}

// 从表尾插入
void insertLast(struct List *p, int x) {
    
    int len = p->length;
    if (len >= SIZE) {
        printf("表已满\n");
        return;
    }

    p->elements[len] = x;
    p->length++;

    return;
}

// 查找x，如果找到，返回x对应的数组脚标，如果没有找到，返回-1
int find(struct List *p, int x) {
    
    int i;
    for (i = 0; i < p->length; i++) {
        if (p->elements[i] == x) {
            return i;
        }
    }

    return -1;
}

// 查找位置为position的结点,如果没有找到，返回NULL
int findKth(struct List *p, int position) {
    
    if (position <= 0) {
        printf("position 不能为负数\n");
        exit(1);
    }

    if (position > p->length) {
        printf("position  超出表的长度\n");
        exit(1);
    }

    return p->elements[position - 1];
}

// 删除第一个值匹配的结点
void delete(struct List *p, int x) {
    
    int i;

    for (i = 0; i < p->length; i++) {
        if (p->elements[i] == x) {
            for ( ; i < p->length - 1; i++) {
                p->elements[i] = p->elements[i + 1];
            }

            p->length--;
            break;
        }
    }
}

// 表中结点个数
int size(struct List *p) {

    return p->length;
}

// 
void printList(struct List *p) {

    int i;

    for (i = 0; i < p->length; i++) {
        printf("list element is : %d\n", p->elements[i]);
    }
}
/*
List is empty?: 1
================================
list element is : 2
list element is : 1
================================
list element is : 2
list element is : 1
list element is : 3
list element is : 4
================================
find index element: 2
================================
find element: 1
================================
list element is : 2
list element is : 1
list element is : 4
================================
List size: 3
================================
*/
```

### link_list.h

```c
/* link_list.h */
#ifndef _List_H

struct Node;
typedef struct Node *PtrToNode; //给struct Node取一个别名
typedef PtrToNode List;
typedef PtrToNode Position;
typedef int ElementType;

// 创建表头
List makeEmpty();
// 判断表是否为空
int isEmpty(List L);
// 判断是否最后一个
int isLast(List L);

// 查找x，如果没有找到，返回NULL
Position find(List L, ElementType X);
// 查找位置为y的结点,如果没有找到，返回NULL
Position findKth(List L, int y);
// 查找当前结点的前一个位置
Position findPrevious(ElementType X, List L);

// 从表头插入
void insertFirst(List L, int x);
// 从表尾插入
void insertLast(List L, int x);
// 指定位置插入
void insert(ElementType X, List L, ElementType Y);
// 更新element为x的值
void update(ElementType X, ElementType Y,  List L);
// 更新position为x的值
void updateKth(ElementType X, ElementType Y, List L);

// 删除第一个值匹配的结点
void delete(List L, ElementType X);
// 删除表中所有的结点
void deleteList(List L);

Position Header(List L);
Position First(List L);
Position Advance(Position P);
ElementType Retrieve(Position P);
// 表中结点个数
int size(List L);
// 打印表中元素
void printList(List L);
#endif  /* _List_H */

```

### link_list.c

```c
/* link_list.c */
#include <stdio.h>
#include <stdlib.h>
#include "link_list.h"


struct Node {
    int element;    // node value
    struct Node *next; // next node point
};

int main() {
    
    // struct Node *node;
    List node;
    // struct Node *header;
    List header;

    // 创建表头
    header = makeEmpty();

    // 判断表是否为空
    if (isEmpty(header)) {
        printf("struct Node is empty ? : Yes\n");
    } else {
        printf("struct Node is empty ? : No\n");
    }

    printf("struct Node is empty ? : %d\n", isEmpty(header));

    printf("================================");
    printf("\n");

    // 从表头插入
    insertFirst(header, 1);
    insertFirst(header, 2);

    printList(header);
    printf("================================");
    printf("\n");

    // 从表尾插入
    insertLast(header, 3);
    insertLast(header, 4);

    printList(header);
    printf("================================");
    printf("\n");

    // 指定位置插入
    insert(5, header, 3); 
    printList(header);
    printf("================================");
    printf("\n");

    // 更新element为1的值为10
    update(1, 10, header);

    // 更新position为1的值为20
    updateKth(1, 20, header); 
                
    // 查找结点值为3的结点
    node = find(header, 3);
    if (node == NULL) {
        printf("not find...\n");
    } else {
        printf("find node element by element: %d\n", node->element);
    }
    printf("================================");
    printf("\n");

    // 查找表中第2个结点
    node = findKth(header, 2);
    if (node == NULL) {
        printf("not find...\n");
    } else {
        printf("find node element by position: %d\n", node->element);
    }
    printf("================================");
    printf("\n");

    // 删除结点值为3的结点
    delete(header, 3);
    printList(header);
    printf("================================");
    printf("\n");

    // 打印表中结点个数，即表的大小
    printf("struct Node size: %d\n", size(header));
    printf("================================");
    printf("\n");
}


// 创建表头
// struct Node *makeEmpty() {
List makeEmpty() {

    // struct Node *p;
    List p;
    p = malloc(sizeof(struct Node));

    if (p == NULL) {
        printf("内存分配失败\n");
        exit(1);
    }

    p->next = NULL;

    return p;
}

// 判断表是否为空
// int isEmpty(struct Node *header) {
int isEmpty(List header) {
    return header->next == NULL;
}

// 判断是否最后一个
int isLast(List L) {
    
}

// 从表头插入
// void insertFirst(struct Node *header, int x) {
void insertFirst(List header, ElementType x) {

    // struct Node *tmp;
    List tmp;

    tmp = malloc(sizeof(struct Node));

    if (tmp == NULL) {
        printf("内存不足\n");
        return;
    }

    tmp->element = x; //给结点赋值
    tmp->next = header->next;

    header->next = tmp;

    return;
}

// 从表尾插入
// void insertLast(struct Node *header, int x) {
void insertLast(List header, ElementType x) {
    
    // struct Node *p;
    // struct Node *tmp;
    List p;
    List tmp;

    tmp = malloc(sizeof(struct Node));

    if (tmp == NULL) {
        printf("内存不足\n");
        return;
    }

    tmp->element = x; //给结点赋值
    tmp->next = NULL;

    p = header;

    while (p->next != NULL) {
        p = p->next;
    }

    p->next = tmp;

    return;
}

// 指定位置插入
void insert(ElementType x, List l, ElementType position) {
    // struct Node *p;
    // struct Node *tmp;
    List tmp;
    List previous;

    if (position <= 0) {
        printf("position 不能为负数\n");
        return;
    }

    tmp = malloc(sizeof(struct Node));

    if (tmp == NULL) {
        printf("内存不足\n");
        return;
    }

    previous = findKth(l, position - 1);
    tmp->element = x; //给结点赋值
    tmp->next = previous->next;
    previous->next = tmp;

    return;
}

// 更新element为x的值为y
void update(ElementType x, ElementType y, List l) {
    
    List tmp;
    tmp = find(l, x);
    tmp->element = y;
}

// 更新position为x的值为y
void updateKth(ElementType x, ElementType y, List l) {

    List tmp;
    tmp = findKth(l, x);
    tmp->element = y;

}
// 查找x，如果没有找到，返回NULL
// struct Node *find(struct Node *header, int x) {
List find(List header, ElementType x) {
    
    // struct Node *p;
    List p;

    p = header->next;

    while (p != NULL && p->element != x) {
        p = p->next;
    }

    return p;
}

// 查找位置为position的结点,如果没有找到，返回NULL
// struct Node *findKth(struct Node *header, int position) {
List findKth(List header, int position) {
    
    int count = 1;
    // struct Node *p;
    List p;

    if (position <= 0) {
        printf("position 不能为负数\n");
        return NULL;
    }

    p = header->next;

    while (p != NULL) {
        if (count == position) {
            return p;
        }

        p = p->next;
        count++;
    }

    return NULL;
}

// 删除第一个值匹配的结点
// void delete(struct Node *header, int x) {
void delete(List header, int x) {
    
    // struct Node *previous; // 被删除结点的前一个结点的指针
    // struct Node *p;
    List previous; // 被删除结点的前一个结点的指针
    List p;

    previous = header;
    p = header->next;

    while (p != NULL) {
        if (p->element == x) {
            previous->next = p->next;
            free(p);
            break;
        } else {
            previous = p;
            p = p->next;
        }
    }
    return;
}

// 表中结点个数
// int size(struct Node *header) {
int size(List header) {

    int count = 0;
    // struct Node *p;
    List p;

    p = header->next;

    while (p != NULL) {
        count++;
        p = p->next;
    }

    return count;
}

// 
// void printList(struct Node *header) {
void printList(List header) {
    
    // struct Node *p;
    List p;
    p = header->next;

    while (p != NULL) {
        printf("printList:node element = %d\n", p->element);
        p = p->next;
    }

    return;
}

/*
struct Node is empty ? : Yes
struct Node is empty ? : 1
================================
printList:node element = 2
printList:node element = 1
================================
printList:node element = 2
printList:node element = 1
printList:node element = 3
printList:node element = 4
================================
printList:node element = 2
printList:node element = 1
printList:node element = 5
printList:node element = 3
printList:node element = 4
================================
find node element by element: 3
================================
find node element by position: 10
================================
printList:node element = 20
printList:node element = 10
printList:node element = 5
printList:node element = 4
================================
struct Node size: 4
================================
*/
```

### double_linked_list

```c
/* double_linked_list.c */
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

// 函数原型声明
// 创建表头
struct Node *createHeaderNode();

// 从表头插入
void insertFirst(struct Node *header, int x);

// 从表尾插入
void insertLast(struct Node *header, int x);

// 查找x，如果没有找到，返回NULL
struct Node *find(struct Node *header, int x);

// 查找位置为position的结点,如果没有找到，返回NULL
struct Node *findKth(struct Node *header, int position);

// 删除第一个值匹配的结点
void delete(struct Node *header, int x);

// 判断表是否为空
bool isEmpty(struct Node *header);

// 表中结点个数
int size(struct Node *header);

void printList(struct Node *header);

struct Node {
    int element;    // node value
    struct Node *previous; // previous node point
    struct Node *next; // next node point
};

int main() {
    
    struct Node *node;
    struct Node *header;

    // 创建表头
    header = createHeaderNode();

    // 判断表是否为空
    printf("List is empty?: %d\n", isEmpty(header));
    printf("================================");
    printf("\n");

    // 从表头插入
    insertFirst(header, 1);
    insertFirst(header, 2);

    printList(header);
    printf("================================");
    printf("\n");

    // 从表尾插入
    insertLast(header, 3);
    insertLast(header, 4);

    printList(header);
    printf("================================");
    printf("\n");

    // 查找结点值为3的结点
    node = find(header, 3);
    if (node == NULL) {
        printf("not find...\n");
    } else {
        printf("find node element: %d\n", node->element);
    }
    printf("================================");
    printf("\n");

    // 查找表中第2个结点
    node = findKth(header, 2);
    if (node == NULL) {
        printf("not find...\n");
    } else {
        printf("find node element: %d\n", node->element);
    }
    printf("================================");
    printf("\n");

    // 删除结点值为3的结点
    delete(header, 3);
    printList(header);
    printf("================================");
    printf("\n");

    // 打印表中结点个数，即表的大小
    printf("List size: %d\n", size(header));
    printf("================================");
    printf("\n");
}


// 创建表头
struct Node *createHeaderNode() {

    struct Node *p;
    p = malloc(sizeof(struct Node));

    if (p == NULL) {
        printf("内存分配失败\n");
        exit(1);
    }
    p->previous = NULL;
    p->next = NULL;
    return p;
}

// 判断表是否为空
bool isEmpty(struct Node *header) {
    return header->next == NULL;
}

// 从表头插入
void insertFirst(struct Node *header, int x) {

    struct Node *tmp;

    tmp = malloc(sizeof(struct Node));

    if (tmp == NULL) {
        printf("内存不足\n");
        return;
    }

    tmp->element = x; //给结点赋值
    tmp->previous = header;
    tmp->next = header->next;

    header->next = tmp;

    return;
}

// 从表尾插入
void insertLast(struct Node *header, int x) {
    
    struct Node *p;
    struct Node *tmp;

    tmp = malloc(sizeof(struct Node));

    if (tmp == NULL) {
        printf("内存不足\n");
        return;
    }

    tmp->element = x; //给结点赋值
    tmp->next = NULL;

    p = header;

    while (p->next != NULL) {
        p = p->next;
    }

    p->next = tmp;
    tmp->previous = p;

    return;
}

// 查找x，如果没有找到，返回NULL
struct Node *find(struct Node *header, int x) {
    
    struct Node *p;

    p = header->next;

    while (p != NULL && p->element != x) {
        p = p->next;
    }

    return p;
}

// 查找位置为position的结点,如果没有找到，返回NULL
struct Node *findKth(struct Node *header, int position) {
    
    int count = 1;
    struct Node *p;

    if (position <= 0) {
        printf("position 不能为负数\n");
        return NULL;
    }

    p = header->next;

    while (p != NULL) {
        if (count == position) {
            return p;
        }

        p = p->next;
        count++;
    }

    return NULL;
}

// 删除第一个值匹配的结点
void delete(struct Node *header, int x) {
    
    struct Node *p;

    p = header->next;

    while (p != NULL) {
        if (p->element == x) {
            p->next->previous = p->previous;
            p->previous->next = p->next;
            free(p);
            break;
        } else {
            p = p->next;
        }
    }
    return;
}

// 表中结点个数
int size(struct Node *header) {

    int count = 0;
    struct Node *p;

    p = header->next;

    while (p != NULL) {
        count++;
        p = p->next;
    }

    return count;
}

// 
void printList(struct Node *header) {
    
    struct Node *p;
    p = header->next;

    while (p != NULL) {
        printf("node element = %d\n", p->element);
        p = p->next;
    }

    return;
}
/*
List is empty?: 1
================================
node element = 2
node element = 1
================================
node element = 2
node element = 1
node element = 3
node element = 4
================================
find node element: 3
================================
find node element: 1
================================
node element = 2
node element = 1
node element = 4
================================
List size: 3
================================
*/
```

## 第三部分 队列

### queue_linked_list

```c
/* queue_linked_list.c */
#include <stdio.h>
#include <stdlib.h>

struct QueueNode;
typedef struct QueueNode *Queue;

Queue create_queue(int max_elements);

int is_empty(Queue q);

void make_empty(Queue q);

void en_queue(int x, Queue q); // 入队
void de_queue(Queue q); // 出队

int front(Queue q);
int front_and_dequeue(Queue q);

void print_queue(Queue q);

struct QueueNode {
    int element;  
    Queue next;  
};

int main() {
    
    int val;
    Queue q;

    // 创建队列
    q = create_queue(5);

    // 入队
    en_queue(1, q);
    en_queue(2, q);
    en_queue(3, q);
    en_queue(4, q);
    en_queue(5, q);

    // 打印队列
    print_queue(q);
    printf("===========\n");

    // 出队
    de_queue(q);
    de_queue(q);

    print_queue(q);
    printf("===========\n");

    en_queue(9, q);

    print_queue(q);
    printf("===========\n");

    // 获取队头元素
    val = front(q);
    printf("front element is : %d\n", val);
    print_queue(q);
    printf("===========\n");

    // 获取队头元素并删除
    val = front_and_dequeue(q);
    printf("front element is : %d\n", val);
    print_queue(q);
    printf("===========\n");

    return 0;
}

Queue create_queue(int max_elements) {
    
    Queue q;
    q = malloc(sizeof(struct QueueNode));
    if (q == NULL) {
        printf("Out of space\n");
        return NULL;
    }
    
    q->next = NULL;

    return q;
}

// 判断队列是否空
int is_empty(Queue q) {
    
    return q->next == NULL;
}

// 清空队列
void make_empty(Queue q) {

    q->next = NULL;
}

void en_queue(int x, Queue q) { // 队尾入队,linked_list.firstInsert

    Queue tmp;
    tmp = malloc(sizeof(struct QueueNode));

    if (tmp == NULL) {
        printf("内存不足\n");
        return;
    }

    tmp->element = x; //给结点赋值
    tmp->next = q->next;

    q->next = tmp;

    return;
}

void de_queue(Queue q) { // 队头出队,linked_list.lastDelete
    
    Queue previous;
    Queue tmp;

    previous = q;
    tmp = q->next; 

    while (tmp != NULL) {
        if (tmp->next == NULL) {
            previous->next = NULL;
            free(tmp);
            break;
        } else {
            previous = tmp;
            tmp = tmp->next;
        }
    }
}

// 获取表头元素值
int front(Queue q) {
    
    if (is_empty(q)) {
        printf("empty queue\n");
        return 0;
    } else {
        return q->next->element;
    }
}


int front_and_dequeue(Queue q) {

    int element;
    Queue tmp;
    tmp = q->next;

    if (is_empty(q)) {
        printf("empty queue\n");
        return 0;
    } else {
        element = q->next->element;
        q->next = tmp->next;
        free(tmp);
    }
    return element;
}

// 打印队列中的元素
void print_queue(Queue q) {

    Queue tmp;
    tmp = q->next;

    while (tmp != NULL) {
        printf("node element = %d\n", tmp->element);
        tmp = tmp->next;
    }

    return;
}
/*
node element = 5
node element = 4
node element = 3
node element = 2
node element = 1
===========
node element = 5
node element = 4
node element = 3
===========
node element = 9
node element = 5
node element = 4
node element = 3
===========
front element is : 9
node element = 9
node element = 5
node element = 4
node element = 3
===========
front element is : 9
node element = 5
node element = 4
node element = 3
===========
*/
```

### queue_array

```c
/* queue_array.c */
#include <stdio.h>
#include <stdlib.h>

struct QueueRecord;
typedef struct QueueRecord *Queue;

Queue create_queue(int max_elements);

int is_empty(Queue q);
int is_full(Queue q);

void dispose_queue(Queue q); // 释放队列内存空间

void make_empty(Queue q);

void en_queue(int x, Queue q); // 入队
void de_queue(Queue q); // 出队

int succ(int index, Queue q);  // 循环数组的脚标计算

int front(Queue q);
int front_and_dequeue(Queue q);

void print_queue(Queue q);

struct QueueRecord {
    int capacity;   // 队列容量
    int size;   // 队列有效数据的大小
    int front;  // 队列头的脚标
    int rear;   // 队列尾的脚标
    int *arr;   // 指针，指向数组首元素的地址（即数组地址）
};

int main() {
    
    int val;
    Queue q;

    // 创建队列
    q = create_queue(5);

    // 入队
    en_queue(1, q);
    en_queue(2, q);
    en_queue(3, q);
    en_queue(4, q);
    en_queue(5, q);

    // 打印队列
    print_queue(q);
    printf("===========\n");

    // 出队
    de_queue(q);
    de_queue(q);

    print_queue(q);
    printf("===========\n");

    en_queue(9, q);

    print_queue(q);
    printf("===========\n");

    // 获取队头元素
    val = front(q);
    printf("front element is : %d\n", val);
    printf("===========\n");

    // 释放队列
    dispose_queue(q);

    return 0;
}

Queue create_queue(int max_elements) {
    
    Queue q;
    q = malloc(sizeof(struct QueueRecord));
    if (q == NULL) {
        printf("Out of space\n");
        return NULL;
    }
    
    q->arr = malloc(sizeof(int) * max_elements);
    if (q->arr == NULL) {
        printf("Out of space\n");
        return NULL;
    }

    q->capacity = max_elements;
    make_empty(q);

    return q;
}

// 判断队列是否空
int is_empty(Queue q) {
    
    return q->size == 0;
}

// 判读队列是否满
int is_full(Queue q) {

    return q->size == q->capacity;
}

void dispose_queue(Queue q) { // 释放队列内存空间

    if (q != NULL) {
        free(q->arr);
        free(q);
    }
}

// 清空队列
void make_empty(Queue q) {

    q->size = 0;
    q->front = 1;
    q->rear = 0;
}

void en_queue(int x, Queue q) { // 队尾入队

    if (is_full(q)) {
        printf("full queue!\n");
        return;
    } else {
        q->size++;
        q->rear = succ(q->rear, q);
        q->arr[q->rear] = x;
    }
}

void de_queue(Queue q) { // 队头出队
    
    if (is_empty(q)) {
        printf("empty queue\n");
        return;
    } else {
        q->size--;
        q->front = succ(q->front, q);
    }
}

int succ(int index, Queue q) {  // 循环数组的脚标计算
    index++;
    return index % q->capacity;
}

// 获取表头元素值
int front(Queue q) {
    
    if (is_empty(q)) {
        printf("empty queue\n");
        return 0;
    } else {
        return q->arr[q->front];
    }
}

int front_and_dequeue(Queue q) {

    int element;

    if (is_empty(q)) {
        printf("empty queue\n");
        return 0;
    } else {
        element = q->arr[q->front];
        q->size--;
        q->front = succ(q->front, q);
    }
    return element;
}

// 打印队列中的元素
void print_queue(Queue q) {

    int i;
    int front = q->front;
    int rear = q->rear;
    int size = q->size;
    int capacity = q->capacity;

    for (i = front; i < front + size; i++) {
        printf("queue elment is : %d\n", q->arr[i % capacity]);
    }
}
/*
queue elment is : 1
queue elment is : 2
queue elment is : 3
queue elment is : 4
queue elment is : 5
===========
queue elment is : 3
queue elment is : 4
queue elment is : 5
===========
queue elment is : 3
queue elment is : 4
queue elment is : 5
queue elment is : 9
===========
front element is : 3
===========
*/
```

## 第四部分 栈

### stack_linked_list

```c
/* stack_linked_list.c */
#include <stdio.h>
#include <stdlib.h>

struct Node;
typedef struct Node *PtrToNode;
typedef PtrToNode Stack;

Stack create_stack();

int is_empty(Stack s);
void dispose_stack(Stack s);
void make_empty(Stack s);

void push(int x, Stack s);
int top(Stack s);
void pop(Stack s);

struct Node {
    int element;
    struct Node *next;
};

int main() {
    
    int val;
    Stack s;
    // 创建一个栈
    s = create_stack();

    // 压栈
    push(5, s);
    push(2, s);

    // 显示栈中元素
    dispose_stack(s);
    printf("====================\n");

    // 查看栈顶元素
    val = top(s);
    printf("top val is : %d\n", val);
    printf("====================\n");

    // 栈顶元素出栈
    pop(s);
    val = top(s);
    printf("top val is : %d\n", val);
    printf("====================\n");

    push(6, s);
    push(7, s);
    dispose_stack(s);
    printf("====================\n");
    
    // 清空栈
    make_empty(s);
    printf("stack is empty : %d\n", is_empty(s));
    printf("====================\n");
}

Stack create_stack() {

    Stack s;
    s = malloc(sizeof(struct Node));
    if (s == NULL) {
        printf("Out of space\n");
        return NULL;
    }
    s->next = NULL;
    return s;
}

int is_empty(Stack s) {

    return s->next == NULL;
}
void dispose_stack(Stack s) {

    Stack tmp;
    tmp = s->next;
    while (tmp != NULL) {
        printf("Element is : %d\n", tmp->element);
        tmp = tmp->next;
    }
    
}

void make_empty(Stack s) {

    if (s == NULL) {
        printf("Must use create_stack first.\n");
        return;
    } else {
        while (!is_empty) {
            pop(s);
        }
    }
}

void push(int x, Stack s) {

    Stack tmp;
    tmp = malloc(sizeof(struct Node));
    if (tmp == NULL) {
        printf("Out of space!\n");
        return;
    } else {
        tmp->element = x;
        tmp->next = s->next;
        s->next = tmp;
    }
}

int top(Stack s) {
    
    if (!is_empty(s)) {
        return s->next->element;
    }

    printf("empty stack\n");
    return 0;
}

void pop(Stack s) {

    Stack tmp;
    if (is_empty(s)) {
        printf("empty stack!\n");
        return;
    } 
    tmp = s->next;
    s->next = s->next->next;
    free(tmp);
    
}
/*
Element is : 2
Element is : 5
====================
top val is : 2
====================
top val is : 5
====================
Element is : 7
Element is : 6
Element is : 5
====================
stack is empty : 0
====================
*/
```

### stack_array

```c
/* stack_array.c */
#include <stdio.h>
#include <stdlib.h>

#define EMPTY_TOS -1
#define MIN_STACK_SIZE 5
struct StackRecord;
typedef struct StackRecord *Stack;
typedef int ElementType;

int is_empty(Stack s);
int is_full(Stack s);
Stack create_stack(int max_elements);
void dispose_stack(Stack s);
void make_empty(Stack s);
void push(ElementType x, Stack s);
ElementType top(Stack s);
void pop(Stack s);
ElementType top_and_pop(Stack s);
void print_stack(Stack s);

struct StackRecord {
    int capacity;   // 栈的容量
    int top_of_stack; // 栈顶脚标
    ElementType *arr; // 数组首元素地址
};

int main() {
    int val;
    Stack s;
    // 创建一个栈
    s = create_stack(10);

    // 压栈
    push(5, s);
    push(2, s);

    // 显示栈中元素
    print_stack(s);
    printf("====================\n");

    // 查看栈顶元素
    val = top(s);
    printf("top val is : %d\n", val);
    printf("====================\n");

    // 栈顶元素出栈
    pop(s);
    val = top(s);
    printf("top val is : %d\n", val);
    printf("====================\n");

    push(6, s);
    push(7, s);
    print_stack(s);
    printf("====================\n");
    
    // 清空栈
    make_empty(s);
    printf("stack is empty : %d\n", is_empty(s));
    printf("====================\n");

    // 释放栈
    dispose_stack(s);
}

Stack create_stack(int max_elements) {

    Stack s;
    if (max_elements < MIN_STACK_SIZE) {
        printf("stack size is to small!\n");
        return NULL;
    }

    s = malloc(sizeof(struct StackRecord));
    if (s == NULL) {
        printf("Out of space!\n");
        return NULL;
    }

    s->arr = malloc(sizeof(ElementType) * max_elements);
    if (s->arr == NULL) {
        printf("Out of space!\n");
        return NULL;
    }

    s->capacity = max_elements;
    s->top_of_stack = EMPTY_TOS;

    return s;
}

int is_empty(Stack s) {

    return s->top_of_stack == EMPTY_TOS;
}

int is_full(Stack s) {

    return s->capacity == s->top_of_stack + 1;
}

void dispose_stack(Stack s) {

    if (s != NULL) {
        free(s->arr);
        free(s);
    }
}

void make_empty(Stack s) {

    s->top_of_stack = EMPTY_TOS;
}

void push(ElementType x, Stack s) {
    
    if (is_full(s)) {
        printf("full stack.\n");
        return;
    } else {
        s->arr[++s->top_of_stack] = x;
    }
}

int top(Stack s) {
    
    if (!is_empty(s)) {
        return s->arr[s->top_of_stack];
    }

    printf("empty stack\n");
    return 0;
}

void pop(Stack s) {

    Stack tmp;
    if (is_empty(s)) {
        printf("empty stack!\n");
        return;
    } else { 
        s->top_of_stack--;
    }
    
}

ElementType top_and_pop(Stack s) {
    
    if(!is_empty(s)) {
        return s->arr[s->top_of_stack--];
    }

    printf("empty stack\n");
    return 0;
}
void print_stack(Stack s) {
    
    for (int i = 0; i < s->top_of_stack + 1; i++) {
        printf("stack elements is : %d\n", s->arr[i]);
    }
}
/*
stack elements is : 5
stack elements is : 2
====================
top val is : 2
====================
top val is : 5
====================
stack elements is : 5
stack elements is : 6
stack elements is : 7
====================
stack is empty : 1
====================
*/
```

## 第五部分 树

### tree_info

```c
// 树的节点说明
typedef struct TreeNode *PtrToNode;
typedef int element;

struct TreeNode {
    ElementType Element;
    PtrToNode FirstChild;   // 指向第一个孩子节点
    PtrToNode NextSibling;  // 指向兄弟的节点
}

// 二叉树的节点说明
typedef struct TreeNode *PtrToNode;
typedef PtrToNode Tree;
typedef int element;

struct TreeNode {
    ElementType Element;
    Tree Left;
    Tree Right;
}

// 树的遍历
/*
先序遍历：先处理根节点，再处理左节点，最后处理右节点    (根->左->右)
中序遍历：先处理左节点，再处理中节点，最后处理右节点    (左->根->右) 
后续遍历：先处理左节点，再处理有节点，最后处理中节点    (左->右->根 )
*/
```

### binary_tree

```c
/* binary_search_tree.h */
#ifndef _Tree_H

struct TreeNode;
typedef struct TreeNode *Position; //给struct Node取一个别名
typedef struct TreeNode *SearchTree; //给struct Node取一个别名
typedef int ElementType;

// 创建表头
SearchTree make_empty(SearchTree T);

// 查找x，如果没有找到，返回NULL
Position find(ElementType X, SearchTree T);

Position find_min(SearchTree T);
Position find_max(SearchTree T);

SearchTree insert_tree(ElementType X, SearchTree T);
SearchTree delete_tree(ElementType X, SearchTree T);

void print_tree(SearchTree T);
int is_binary_tree(SearchTree T);
#endif  /* _Tree_H */

/* binary_search_tree.c */
#include <stdio.h>
#include <stdlib.h>
#include "binary_search_tree.h"

struct TreeNode {
    ElementType element;
    SearchTree left;
    SearchTree right;
};

int main() {

    SearchTree min;
    SearchTree max;
    SearchTree node;
    SearchTree root;

    root = insert_tree(6, NULL);
    insert_tree(4, root);
    insert_tree(3, root);
    insert_tree(2, root);
    insert_tree(1, root);
    insert_tree(8, root);

    printf("is binary tree ? 1 yes 2 no : %d\n", is_binary_tree(root));

    print_tree(root);
    printf("=============\n");

    node = find(4, root);
    printf("find node element is : %d\n", node->element);
    printf("=============\n");

    min = find_min(root);
    printf("min node element is : %d\n", min->element);
    printf("=============\n");

    max = find_max(root);
    printf("max node element is : %d\n", max->element);
    printf("=============\n");
    
    delete_tree(2, root);
    printf("delete_tree(2, root)\n");
    print_tree(root);
    printf("=============\n");

    make_empty(root);
    print_tree(root);
}
// 清空树
SearchTree make_empty(SearchTree t) {
    
    if (t) {
        make_empty(t->left);
        make_empty(t->right);
        free(t);
    }
    return NULL;
}

// 查找x，如果没有找到，返回NULL
Position find(ElementType x, SearchTree t) {

    if (t == NULL) {
        return NULL;
    }

    if (x < t->element) {
        return find(x, t->left);
    } else if (x > t->element) {
        return find(x, t->right);
    } else {
        return t;
    }
}

Position find_min(SearchTree t) {

    if (t == NULL) {
        return NULL;
    } else if (t->left == NULL){
        return t;
    } else {
        return find_min(t->left);
    }
}

Position find_max(SearchTree t) {

    if (t != NULL) {
        while (t->right != NULL) {
            t = t->right;
        }
    }

    return t;
}

SearchTree insert_tree(ElementType x, SearchTree t) {
    
    if (t == NULL) {
        t = malloc(sizeof(struct TreeNode));
        if (t == NULL) {
            printf("Out of space!\n");
            return NULL;
        } else {
            t->element = x;
            t->left = NULL;
            t->right = NULL;
        }
    } else if (x < t->element) {
        t->left = insert_tree(x, t->left);
    } else if (x > t->element) {
        t->right = insert_tree(x, t->right);
    } else {
        return t;
    }
}

SearchTree delete_tree(ElementType x, SearchTree t) {

    Position tmp;

    if (t == NULL) {
        printf("Empty Tree!\n");
        return NULL;
    } else if (x < t->element) {
        t->left = delete_tree(x, t->left);
    } else if (x > t->element) {
        t->right = delete_tree(x, t->left);
    } else if (t->left && t->right) {
        tmp = find_min(t->right);
        t->element = tmp->element;
        t->right = delete_tree(t->element, t->right);
    } else {
        tmp = t;
        if (t->left == NULL) {
            t = t->right;
        } else if (t->right == NULL) {
            t = t->left;
        }
        free(tmp);
    }

    return t;
}

// 使用中序遍历，打印树中元素
void print_tree(SearchTree t) {

    if (t == NULL) {
        printf("Empty Tree!\n");
        return;
    }

    // 打印左子树
    if (t->left != NULL) {
        print_tree(t->left);
    } 

    // 打印根节点
    printf("tree element is : %d\n", t->element);

    // 打印右子树
    if (t->right != NULL) {
        print_tree(t->right);
    }
}

int is_binary_tree(SearchTree t) {

    if (t == NULL) {
        return 1;
    }

    if (t->left && find_min(t)->element >= t->element) {
        return 0;
    }

    if (t->right && find_max(t)->element <= t->element) {
        return 0;
    }

    if (is_binary_tree(t->left) && is_binary_tree(t->right)) {
        return 1;
    }
}
/*
is binary tree ? 1 yes 2 no : 1
tree element is : 1
tree element is : 2
tree element is : 3
tree element is : 4
tree element is : 6
tree element is : 8
=============
find node element is : 4
=============
min node element is : 1
=============
max node element is : 8
=============
delete_tree(2, root)
tree element is : 1
tree element is : 3
tree element is : 4
tree element is : 6
tree element is : 8
=============
tree element is : 6
tree element is : -676248832
tree element is : 6
tree element is : -676248960
*/
```

### avl_tree

```c
/* avl_tree.h */
#ifndef _AvlTree_H

struct AvlTreeNode;
typedef struct AvlTreeNode *Position; //给struct Node取一个别名
typedef struct AvlTreeNode *AvlTree; //给struct Node取一个别名
typedef int ElementType;

// 创建表头
AvlTree make_empty(AvlTree T);

static int get_height(Position P);
// 查找x，如果没有找到，返回NULL
Position find(ElementType X, AvlTree T);

Position find_min(AvlTree T);
Position find_max(AvlTree T);

int max (int a, int b);

static Position single_rotate_with_left(Position k2);
static Position single_rotate_with_right(Position k2);
static Position double_rotate_with_left(Position k3);
static Position double_rotate_with_right(Position k3);

AvlTree insert_tree(ElementType X, AvlTree T);
AvlTree delete_tree(ElementType X, AvlTree T);

void print_tree(AvlTree T);

#endif  /* _AvlTree_H */

/* avl_tree.c */
#include <stdio.h>
#include <stdlib.h>
#include "avl_tree.h"

struct AvlTreeNode {
    ElementType element;
    AvlTree left;
    AvlTree right;
    int height;
};

int main() {
    AvlTree min;
    AvlTree max;
    AvlTree node;
    AvlTree root;
    root = insert_tree(6, NULL);
    root = insert_tree(4, root);
    root = insert_tree(3, root);
    root = insert_tree(2, root);
    root = insert_tree(1, root);
    root = insert_tree(8, root);
    printf("root node is : %d\n", root -> element);
    print_tree(root);
    printf("=============\n");

    node = find(4, root);
    printf("find node element is : %d\n", node->element);
    printf("=============\n");

    min = find_min(root);
    printf("min node element is : %d\n", min->element);
    printf("=============\n");

    max = find_max(root);
    printf("max node element is : %d\n", max->element);
    printf("=============\n");

    delete_tree(3, root);
    printf("root node is : %d\n", root -> element);
    print_tree(root);
    printf("=============\n");
}


static int get_height(Position p) {

    if (p == NULL) {
        return -1;
    } else {
        return p->height;
    }
}

// 查找x，如果没有找到，返回NULL
Position find(ElementType x, AvlTree t) {

    if (t == NULL) {
        return NULL;
    }

    if (x < t->element) {
        return find(x, t->left);
    } else if (x > t->element) {
        return find(x, t->right);
    } else {
        return t;
    }
}

Position find_min(AvlTree t) {

    if (t == NULL) {
        return NULL;
    } else if (t->left == NULL){
        return t;
    } else {
        return find_min(t->left);
    }
}

Position find_max(AvlTree t) {

    if (t != NULL) {
        while (t->right != NULL) {
            t = t->right;
        }
    }

    return t;
}

int max (int a, int b) {
    return a > b ? a : b;
}
/* This function can be called only if k2 has a left child */
/* Perform a rotate between a node (k2) and its left child */
/* Update heights, then return new root */

Position single_rotate_with_left(Position k2) {
    
    Position k1;
    k1 = k2->left;
    k2->left = k1->right;
    k1->right = k2;

    k2->height = max(get_height(k2->left), get_height(k2->right)) + 1;
    k1->height = max(get_height(k1->left), k2->height) + 1;
    return k1;  /* new root */
}

static Position single_rotate_with_right(Position k2) {

    Position k1;
    k1 = k2->right;
    k2->right = k1->left;
    k1->left = k2;

    k2->height = max(get_height(k2->left), get_height(k2->right)) + 1;
    k1->height = max(get_height(k1->right), k2->height) + 1;

    return k1;  /* new root */
}

/* This function can be called only if k3 has a left */
/* child and k3's left child has a right child */
/* Do the left-right double rotation */
/* Update heights, then return new root */

static Position double_rotate_with_left(Position k3) {
    
    /* Rotate between k1 and k2 */
    k3->left = single_rotate_with_right(k3->left);

    /* Rotate between k3 and k2 */
    return single_rotate_with_left(k3);
}

static Position double_rotate_with_right(Position k3) {

    /* Rotate between k1 and k2 */
    k3->left = single_rotate_with_left(k3->right);

    /* Rotate between k3 and k2 */
    return single_rotate_with_right(k3);
}

AvlTree insert_tree(ElementType x, AvlTree t) {
    if (t == NULL) {
        /* Create and return a one-node tree */
        t = malloc(sizeof(struct AvlTreeNode));
        if (t == NULL) {
            printf("Out of space!!!\n");
        } else {
            t->element  = x;
            t->height = 0;
            t->left = NULL;
            t->right = NULL;
        }
    } else if (x < t->element) {
        t->left = insert_tree(x, t->left);
        if (get_height(t->left) - get_height(t->right) == 2) {
            if (x < t->left->element) {
                t = single_rotate_with_left(t);
            } else {
                t = double_rotate_with_left(t);
            }
        }
        
    } else if (x > t->element) {
        t->right = insert_tree(x, t->right);
        if (get_height(t->right) - get_height(t->left) == 2) {
            if (x > t->right->element) {
                t = single_rotate_with_right(t);
            } else {
                t = double_rotate_with_right(t);
            }
        }
    } 
    /* else x is in the tree already; we'll do nothing */

    t->height = max(get_height(t->left), get_height(t->right)) + 1;
    return t;
}

AvlTree delete_tree(ElementType x, AvlTree t) {
    
    Position tmp;
    if (t == NULL) {
        printf("empty tree!!\n");
        return NULL;
    } else if (x < t->element) {
        t->left = delete_tree(x, t->left);
    } else if (x > t->element) {
        t->right = delete_tree(x, t->right);
    } else if (t->left != NULL && t->right != NULL) {
        tmp = find_min(t->right);
        t->element = tmp->element;
        t->right = delete_tree(t->element, t->right);
    } else {
        tmp = t;
        if (t->left == NULL) {
            t = t->right;
        } else if (t->right == NULL) {
            t = t->left;
        }
        free(tmp);
    }
    return t;
}

void print_tree(AvlTree t) {

    if (t == NULL) {
        printf("Empty Tree!\n");
        return;
    }

    // 打印左子树
    if (t->left != NULL) {
        print_tree(t->left);
    }

    // 打印根节点
    printf("tree element is : %d\n", t->element);

    // 打印右子树
    if (t->right != NULL) {
        print_tree(t->right);
    }
}
/*
root node is : 4
tree element is : 1
tree element is : 2
tree element is : 3
tree element is : 4
tree element is : 6
tree element is : 8
=============
find node element is : 4
=============
min node element is : 1
=============
max node element is : 8
=============
root node is : 4
tree element is : 1
tree element is : 2
tree element is : 4
tree element is : 6
tree element is : 8
=============
*/
```

## 第六部分 哈希

### hash_separate_chaining

```c
/* hash_separate_chaining.h */
#ifndef _HashSep_H

typedef int ElementType;
struct ListNode;
typedef struct ListNode *Position;
typedef Position List;

struct HashTbl;
typedef struct HashTbl *HashTable;

int is_prime(int num);    // 是否是一个素数 
int next_prime(int num);    // 返回下一个素数 

int hash(ElementType key, int table_size);

HashTable initialize_table(int table_size);

void destroy_table(HashTable h);

Position find_element(ElementType key, HashTable h);

void insert_table(ElementType key, HashTable h);
int delete_table(ElementType key, HashTable h);
void print_table(HashTable h);

#endif  /* _HashSep_H */

/* hash_separate_chaining.c */
#include <stdio.h>
#include <stdlib.h>
#include "hash_separate_chaining.h"

#define MIN_TABLE_SIZE 5


struct ListNode {
    ElementType element;
    Position next;
};

struct HashTbl {
    int table_size;
    List *the_lists;
};

int main() {
    
    Position p;
    HashTable table;

    table = initialize_table(10);

    insert_table(19, table);
    insert_table(18, table);
    insert_table(17, table);
    insert_table(9, table);
    insert_table(8, table);
    insert_table(7, table);
    insert_table(10, table);
    insert_table(11, table);
    insert_table(3, table);
    print_table(table);
    printf("================\n");
    
    p = find_element(19, table);
    printf("find_element(19, table): %d\n", p->element);
    printf("================\n");

    delete_table(3, table);
    print_table(table);
    printf("================\n");

    destroy_table(table);
    if (table->the_lists[0] == NULL) {
        print_table(table);
    } else {
        printf("table is empty!\n");
    }
    printf("================\n");
    
}

int is_prime(int num) {   // 是否是一个素数 
    
    for (int i = 2; i * i < num +1; i++) {
        if (num % i == 0) {
            return 0;
        }
    }
    return 1;
}

int next_prime(int num) { // 返回下一个素数

    while(1 == 1) {
        if (is_prime(num)) {
            return num;
        } else {
            num++;
        }
    }
}

int hash(ElementType key, int table_size) { // 简单散列函数
    
    return key % table_size;
}

HashTable initialize_table(int table_size) {
    
    HashTable h;
    int i;

    if (table_size < MIN_TABLE_SIZE) {
        printf("Table size too small!\n");
        return NULL;
    }

    /* Allocate table */
    h = malloc(sizeof(struct HashTbl));

    if (h == NULL) {
        printf("Out of space!\n");
        return NULL;
    }

    h->table_size = next_prime(table_size);

    /* Allocate array of lists */
    h->the_lists = malloc(h->table_size * sizeof(List));

    if (h->the_lists == NULL) {
        printf("Out of space!\n");
        return NULL;
    }

    /* Allocate list header */
    for (i = 0; i < h->table_size; i++) {
        h->the_lists[i] = malloc(sizeof(struct ListNode));

        if (h->the_lists[i] == NULL) {
            printf("Out of space!\n");
            return NULL;
        } else {
            h->the_lists[i]->next == NULL;
        }
    }
    return h;
}

void destroy_table(HashTable h) { // 销毁散列表
    
    Position p, q;
    List l;

    int i;
    for (i = 0; i < h->table_size; i++) {
        l = h->the_lists[i];
        p = l->next;

        while(p) {
            q = p->next;
            free(p);
            p = NULL;
            /*
            if (!q) {
                free(p);
                p = NULL;
            } else {
                free(p);
                p = q;
            }
            
            */
        }
    }
}

Position find_element(ElementType key, HashTable h) {
    
    Position p;
    List l;

    l = h->the_lists[hash(key, h->table_size)];
    p = l->next;

    while(p != NULL && p->element != key) {
        p = p->next;
    }
    return p;
}

void insert_table(ElementType key, HashTable h) {
    
    Position pos, new_cell;
    List l;

    pos = find_element(key, h);
    if (pos == NULL) {
        new_cell = malloc(sizeof(struct ListNode));
        if (new_cell == NULL) {
            printf("Out of space!!!\n");
            return;
        } else {
            l = h->the_lists[hash(key, h->table_size)];
            new_cell->next = l->next;
            new_cell->element = key;
            l->next = new_cell;
        }
    }
}

int delete_table(ElementType key, HashTable h) {

    Position pos, previous;

    previous = h->the_lists[hash(key, h->table_size)];
    pos = h->the_lists[hash(key, h->table_size)]->next;

    while (pos != NULL) {
        if (pos->element == key) {
            previous->next = pos->next;
            free(pos);
            break;
        } else {
            previous = pos;
            pos = pos->next;
        }
    }
    return 1;
}

void print_table(HashTable h) {
    
    Position p;
    List l;

    for (int i = 0; i < h->table_size; i++) {
        l = h->the_lists[i];
        p = l->next;
        printf("下标 %d: ", i);
        
        while (p != NULL) {
            printf("%d ", p->element);
            p = p->next;
        }
    printf("\n");
    }
}
/*
下标 0: 11 
下标 1: 
下标 2: 
下标 3: 3 
下标 4: 
下标 5: 
下标 6: 17 
下标 7: 7 18 
下标 8: 8 19 
下标 9: 9 
下标 10: 10 
================
find_element(19, table): 19
================
下标 0: 11 
下标 1: 
下标 2: 
下标 3: 
下标 4: 
下标 5: 
下标 6: 17 
下标 7: 7 18 
下标 8: 8 19 
下标 9: 9 
下标 10: 10 
================
table is empty!
================
*/
```

## 第七部分 堆

### binary_heap

```c
/* binary_heap.h */
#ifndef _BinHeap_H

typedef int ElementType;

typedef struct HeapStruct *PriorityQueue;

PriorityQueue initialize_heap(int max_elements);

void destroy_heap(PriorityQueue h);

void make_empty(PriorityQueue h);

void insert_heap(ElementType x, PriorityQueue h);

ElementType delete_min(PriorityQueue h);

ElementType find_min(PriorityQueue h);

int is_empty(PriorityQueue h);

int is_full(PriorityQueue h);

void print_heap(PriorityQueue h);

#endif  /* _BinHeap_H */

/* binary_heap.c */
#include <stdio.h>
#include <stdlib.h>
#include "binary_heap.h"

#define Min_PQSize 5
#define Min_Data -1

struct HeapStruct {

    int capacity;
    int size;
    ElementType *elements;
};

int main() {
    
    PriorityQueue pq;
    int min;

    pq = initialize_heap(20);
    insert_heap(7, pq);
    min = find_min(pq);
    print_heap(pq);
    printf("min = %d\n", min);
    printf("====================\n");

    for (int i = 10; i < 20; i = i + 2) {
        insert_heap(i, pq);
    }
    delete_min(pq);

    min = find_min(pq);
    print_heap(pq);
    printf("min = %d\n", min);
    printf("====================\n");

    insert_heap(5, pq);
    min = find_min(pq);
    print_heap(pq);
    printf("min = %d\n", min);
    printf("====================\n");

    insert_heap(9, pq);
    print_heap(pq);
    min = find_min(pq);
    printf("min = %d\n", min);
    printf("====================\n");

    insert_heap(6, pq);
    print_heap(pq);
    min = find_min(pq);
    printf("min = %d\n", min);
    printf("====================\n");

    make_empty(pq);    
    print_heap(pq);
    min = find_min(pq);
    printf("min = %d\n", min);
    printf("====================\n");

}

PriorityQueue initialize_heap(int max_elements) {
    
    PriorityQueue h;

    if (max_elements < Min_PQSize) {
        printf("PriourtyQueue size is too small\n");
        return NULL;
    }

    h = malloc(sizeof(struct HeapStruct));

    if (h == NULL) {
        printf("Out of space!!!\n");
        return NULL;
    }
    
    h->elements = malloc(sizeof(ElementType) * (max_elements + 1));

    if (h->elements == NULL) {
        printf("Out of space!!!\n");
        return NULL;
    }

    h->capacity = max_elements;
    h->size = 0;
    h->elements[0] = Min_Data;

    return h;
}

void destroy_heap(PriorityQueue h) {
}

void make_empty(PriorityQueue h) {

    h->size = 0;
}

void insert_heap(ElementType x, PriorityQueue h) {

    int i;
    if (is_full(h)) {
        printf("PriorityQueue is full\n");
        exit(0);
    }

    for (i = ++h->size; h->elements[i/2] > x; i/=2) {
        h->elements[i] = h->elements[i/2];
    }

    h->elements[i] = x;
}

ElementType delete_min(PriorityQueue h) {
    
    int i, child;
    ElementType min_element, last_element;

    if (is_empty(h)) {
        printf("Heap is empty!!!\n");
        return h->elements[0];
    } 

    min_element = h->elements[1];
    last_element = h->elements[h->size--];

    for (i = 1; i * 2 <= h->size; i = child) {
        child = i * 2;

        if (child != h->size && h->elements[child + 1] < h->elements[child]) {
            child++;
        }

        if (last_element > h->elements[child]) {
            h->elements[i] = h->elements[child];
        } else {
            break;
        }
    }

    h->elements[i] = last_element;

    return min_element;
}

ElementType find_min(PriorityQueue h) {
    
    if (is_empty(h)) {
        printf("Heap is empty!!!\n");
        return 0;
    } else {
        return h->elements[1];
    }
}

int is_empty(PriorityQueue h) {

    return h->size == 0;
}

int is_full(PriorityQueue h) {

    return h->size == h->capacity;
}

void print_heap(PriorityQueue h) {

    if (is_empty(h)) {
        printf("The heap is empty!!!\n");
        exit(0);
    } else {
        printf("PQ Elements is: ");
        for (int i = 1; i <= h->size; i++) {
            printf("%d ", h->elements[i]);
        }
        printf("\n");
    }
}

/*
PQ Elements is: 7 
min = 7
====================
PQ Elements is: 10 14 12 18 16 
min = 10
====================
PQ Elements is: 5 14 10 18 16 12 
min = 5
====================
PQ Elements is: 5 14 9 18 16 12 10 
min = 5
====================
PQ Elements is: 5 6 9 14 16 12 10 18 
min = 5
====================
The heap is empty!!!
*/
```

## 第八部分 排序

### insertion_sort

```c
/* insertion_sort.c */
#include <stdio.h>

void insertion_sort(int [], int); 
void print_array(int [], int);

int main() {

    int a[] = {9, 8, 1, 4, 3, 2, 5, 7, 6, 0};
    printf("before sort:\n");
    print_array(a, 10);

    printf("after sort:\n");
    insertion_sort(a, 10);
    print_array(a, 10);

}

void insertion_sort(int arr[], int n) {
    
    int p;
    int i;
    int tmp;

    for (p = 1; p < n; p++) {
        tmp = arr[p];
        for (i = p; i > 0 && arr[i - 1] > tmp; i--) {
            arr[i] = arr[i - 1];
        }
        arr[i] = tmp;
    }
}

void print_array(int arr[], int len) {
    
    for (int i = 0; i < len; i++) {
        printf("array element is: %d\n", arr[i]);
    }
    printf("=====================\n");
}
/*
before sort:
array element is: 9
array element is: 8
array element is: 1
array element is: 4
array element is: 3
array element is: 2
array element is: 5
array element is: 7
array element is: 6
array element is: 0
=====================
after sort:
array element is: 0
array element is: 1
array element is: 2
array element is: 3
array element is: 4
array element is: 5
array element is: 6
array element is: 7
array element is: 8
array element is: 9
=====================
*/
```

### shell_sort

```c
/* shell_sort.c */
#include <stdio.h>

void shell_sort(int [], int); 
void print_array(int [], int);

int main() {

    int a[] = {9, 8, 1, 4, 3, 2, 5, 7, 6, 0};
    printf("before sort:\n");
    print_array(a, 10);

    printf("after sort:\n");
    shell_sort(a, 10);
    print_array(a, 10);

}

void shell_sort(int arr[], int n) {
    
    int i, j, increment;
    int tmp;

    for (increment = n / 2; increment > 0; increment /= 2) {
        for (i = increment; i < n; i++) {
            tmp = arr[i];
            for (j = i; j >= increment; j -= increment) {
                if (tmp < arr[j - increment]) {
                    arr[j] = arr[j - increment];
                } else {
                    break;
                }
            }
            arr[j] = tmp;
        }
        printf("===============\n");
    }
}

void print_array(int arr[], int len) {
    
    for (int i = 0; i < len; i++) {
        printf("array element is: %d\n", arr[i]);
    }
    printf("=====================\n");
}

/*
before sort:
array element is: 9
array element is: 8
array element is: 1
array element is: 4
array element is: 3
array element is: 2
array element is: 5
array element is: 7
array element is: 6
array element is: 0
=====================
after sort:
===============
===============
===============
array element is: 0
array element is: 1
array element is: 2
array element is: 3
array element is: 4
array element is: 5
array element is: 6
array element is: 7
array element is: 8
array element is: 9
=====================
*/
```

### merge_sort

```c
/* merge_sort.c */
#include <stdio.h>
#include <stdlib.h>

typedef int ElementType;

void merge_sort(ElementType arr[], int n);
void m_sort(ElementType arr[], ElementType tmp_arr[], int left, int right); 
void merge(ElementType arr[], ElementType tmp_arr[], int lpos, int rpos, int right_end);
void print_array(int [], int);

int main() {

    int a[] = {9, 8, 1, 4, 3, 2, 5, 7, 6, 0};
    printf("before sort:\n");
    print_array(a, 10);

    printf("after sort:\n");
    merge_sort(a, 10);
    print_array(a, 10);
}

// 递归 分治法
void m_sort(ElementType arr[], ElementType tmp_arr[], int left, int right) {
    
    int center;

    if (left < right) {
        center = (left + right) / 2;
        m_sort(arr, tmp_arr, left, center);
        m_sort(arr, tmp_arr, center + 1, right);
        merge(arr, tmp_arr, left, center + 1, right);
    }
}

void merge_sort(ElementType arr[], int n) {
    
    ElementType *tmp_arr;

    tmp_arr = malloc(n * sizeof(ElementType));

    if (tmp_arr != NULL) {
        m_sort(arr, tmp_arr, 0, n-1);
        free(tmp_arr);
    } else {
        printf("No space for tmp array!!!\n");
    }
}

/* lpos = start of left half, rpos = start of right half */
void merge(ElementType arr[], ElementType tmp_arr[], int lpos, int rpos, int right_end) {

    int i, left_end, num_elements, tmp_pos;

    left_end = rpos - 1;
    tmp_pos = lpos;
    num_elements = right_end - lpos + 1;

    /* main loop */
    while (lpos <= left_end && rpos <= right_end) {
        if (arr[lpos] <= arr[rpos]) {
            tmp_arr[tmp_pos++] = arr[lpos++];
        } else {
            tmp_arr[tmp_pos++] = arr[rpos++];
        }
    }

    while (lpos <= left_end) { /* copy rest of first half */
        tmp_arr[tmp_pos++] = arr[lpos++];
    }

    while (rpos <= right_end) { /* copy rest of second half */
        tmp_arr[tmp_pos++] = arr[rpos++];
    }

    /* copy tmp_arr back */
    for (i = 0; i < num_elements; i++, right_end--) {
        arr[right_end] = tmp_arr[right_end];
    }
}

void print_array(int arr[], int len) {
    
    for (int i = 0; i < len; i++) {
        printf("array element is: %d\n", arr[i]);
    }
    printf("=====================\n");
}
/*
before sort:
array element is: 9
array element is: 8
array element is: 1
array element is: 4
array element is: 3
array element is: 2
array element is: 5
array element is: 7
array element is: 6
array element is: 0
=====================
after sort:
array element is: 0
array element is: 1
array element is: 2
array element is: 3
array element is: 4
array element is: 5
array element is: 6
array element is: 7
array element is: 8
array element is: 9
=====================
*/
```

### heap_sort

```c
/* heap_sort.c */
#include <stdio.h>

#define left_child(i) (2 * (i) + 1) // 宏函数

typedef int ElementType;

void percolate_down(ElementType [], int, int);
void heap_sort(ElementType [], int); 
void swap(int *, int *); 
void print_array(int [], int); 

int main() {

    int a[] = {9, 8, 1, 4, 3, 2, 5, 7, 6, 0};
    printf("before sort:\n");
    print_array(a, 10);

    printf("after sort:\n");
    heap_sort(a, 10);
    print_array(a, 10);
}

/* 下沉，构造堆 */
void percolate_down(ElementType arr[], int i, int n) {
    
    int child;
    ElementType tmp;

    for (tmp = arr[i]; left_child(i) < n; i = child) {

        child = left_child(i);

        if (child != n - 1 && arr[child + 1] > arr[child]) {
            child++;
        }

        if (tmp < arr[child]) {
            arr[i] = arr[child];
        } else {
            break;
        }
    }
    arr[i] = tmp;
}

/* 堆排序逻辑 */
void heap_sort(ElementType arr[], int n) {
    
    int i;
    for (i = n / 2; i >= 0; i--) { /* build heap */
        percolate_down(arr, i, n);
    }

    for (i = n - 1; i > 0; i--) {
        swap(&arr[0], &arr[i]); /* delete max */ 
        percolate_down(arr, 0, i);
    }

}

void swap(int *px, int *py) {

    int tmp;
    tmp = *px;
    *px = *py;
    *py = tmp;
}

void print_array(int arr[], int len) {
    
    for (int i = 0; i < len; i++) {
        printf("array element is: %d\n", arr[i]);
    }
    printf("=====================\n");
}
/*
before sort:
array element is: 9
array element is: 8
array element is: 1
array element is: 4
array element is: 3
array element is: 2
array element is: 5
array element is: 7
array element is: 6
array element is: 0
=====================
after sort:
array element is: 0
array element is: 1
array element is: 2
array element is: 3
array element is: 4
array element is: 5
array element is: 6
array element is: 7
array element is: 8
array element is: 9
=====================
*/
```

### quick_sort

```c
/* quick_sort.c */
#include <stdio.h>

#define Cutoff (3)

typedef int ElementType;

ElementType median3(ElementType arr[], int left, int right); 

void quick_sort(ElementType arr[], int n); 
void q_sort(ElementType arr[], int left, int right); 

void insertion_sort(int [], int); 
void print_array(int [], int);
void swap(int *px, int *py); 

int main() {
    int a[] = {9, 8, 1, 4, 3, 2, 5, 7, 6, 0};
    printf("before sort:\n");
    print_array(a, 10);

    printf("after sort:\n");
    quick_sort(a, 10);
    print_array(a, 10);
}

void quick_sort(ElementType arr[], int n) {

    q_sort(arr, 0, n - 1);
}

/* Return median of left, center, and right */
/* Order these and hide the pivot */
ElementType median3(ElementType arr[], int left, int right) {

    int center = (left + right) / 2;

    if (arr[left] > arr[center]) {
        swap(&arr[left], &arr[center]);
    }

    if (arr[left] > arr[right]) {
        swap(&arr[left], &arr[right]);
    }

    if (arr[center] > arr[right]) {
        swap(&arr[center], &arr[right]);
    }

    swap(&arr[center], &arr[right -1]); /* Hide pivot */

    return arr[right - 1];/* Return pivot */
}

void q_sort(ElementType arr[], int left, int right) {
    
    int i, j;
    ElementType pivot;

    if (left + Cutoff <= right) {
        pivot = median3(arr, left, right);

        i = left;
        j = right - 1;

        for( ; ; ) {

            while (arr[++i] < pivot) { printf("i => arr[%d] = %d\n", i, arr[i]);}
            while (arr[--j] > pivot) {printf("j => arr[%d] = %d\n", j, arr[j]);}

            if (i < j) {
                swap(&arr[i], &arr[j]);
            } else {
                break;
            }
        }
        swap(&arr[i], &arr[right - 1]); /* Restore pivot */

        q_sort(arr, left, i - 1);
        q_sort(arr, i + 1, right);
    } else { /* Do an insertion sort on the subarray */
        // arr + left 数组首元素地址移动
        insertion_sort(arr + left, right - left + 1);
    }
}

void insertion_sort(int arr[], int n) {
    
    int p;
    int i;
    int tmp;

    for (p = 1; p < n; p++) {
        tmp = arr[p];
        for (i = p; i > 0 && arr[i - 1] > tmp; i--) {
            arr[i] = arr[i - 1];
        }
        arr[i] = tmp;
    }
}

void print_array(int arr[], int len) {
    
    for (int i = 0; i < len; i++) {
        printf("array element is: %d\n", arr[i]);
    }
    printf("=====================\n");
}


void swap(int *px, int *py) {

    int tmp;
    tmp = *px;
    *px = *py;
    *py = tmp;
}
/*
before sort:
array element is: 9
array element is: 8
array element is: 1
array element is: 4
array element is: 3
array element is: 2
array element is: 5
array element is: 7
array element is: 6
array element is: 0
=====================
after sort:
j => arr[7] = 7
j => arr[6] = 5
i => arr[2] = 1
j => arr[4] = 6
j => arr[3] = 4
j => arr[7] = 7
array element is: 0
array element is: 1
array element is: 2
array element is: 3
array element is: 4
array element is: 5
array element is: 6
array element is: 7
array element is: 8
array element is: 9
=====================
*/
```

### quick_select_sort

```c
/* quick_select_sosrt.c */
#include <stdio.h>

#define Cutoff (3)

typedef int ElementType;

ElementType median3(ElementType arr[], int left, int right); 

void quick_select_sort(ElementType arr[], int k, int n); 
void q_select_sort(ElementType arr[], int k, int left, int right); 

void insertion_sort(int [], int); 
void print_array(int [], int);
void swap(int *px, int *py); 

int main() {
    int a[] = {9, 8, 1, 4, 3, 2, 5, 7, 6, 0};
    printf("before sort:\n");
    print_array(a, 10);

    printf("after sort:\n");
    quick_select_sort(a, 4, 10);
    print_array(a, 10);
}

void quick_select_sort(ElementType arr[], int k, int n) {

    q_select_sort(arr, k, 0, n - 1);
}

/* Return median of left, center, and right */
/* Order these and hide the pivot */
ElementType median3(ElementType arr[], int left, int right) {

    int center = (left + right) / 2;

    if (arr[left] > arr[center]) {
        swap(&arr[left], &arr[center]);
    }

    if (arr[left] > arr[right]) {
        swap(&arr[left], &arr[right]);
    }

    if (arr[center] > arr[right]) {
        swap(&arr[center], &arr[right]);
    }

    swap(&arr[center], &arr[right -1]); /* Hide pivot */

    return arr[right - 1];/* Return pivot */
}

void q_select_sort(ElementType arr[], int k, int left, int right) {
    
    int i, j;
    ElementType pivot;

    if (left + Cutoff <= right) {
        pivot = median3(arr, left, right);

        i = left;
        j = right - 1;

        for( ; ; ) {

            while (arr[++i] < pivot) { printf("i => arr[%d] = %d\n", i, arr[i]);}
            while (arr[--j] > pivot) {printf("j => arr[%d] = %d\n", j, arr[j]);}

            if (i < j) {
                swap(&arr[i], &arr[j]);
            } else {
                break;
            }
        }
        swap(&arr[i], &arr[right - 1]); /* Restore pivot */

        if (k <= i) {
            q_select_sort(arr, k, left, i - 1);
        } else if (k > i + 1) {
            q_select_sort(arr, k, i + 1, right);
        }
    } else { /* Do an insertion sort on the subarray */
        // arr + left 数组首元素地址移动
        insertion_sort(arr + left, right - left + 1);
    }
}

void insertion_sort(int arr[], int n) {
    
    int p;
    int i;
    int tmp;

    for (p = 1; p < n; p++) {
        tmp = arr[p];
        for (i = p; i > 0 && arr[i - 1] > tmp; i--) {
            arr[i] = arr[i - 1];
        }
        arr[i] = tmp;
    }
}

void print_array(int arr[], int len) {
    
    for (int i = 0; i < len; i++) {
        printf("array element is: %d\n", arr[i]);
    }
    printf("=====================\n");
}


void swap(int *px, int *py) {

    int tmp;
    tmp = *px;
    *px = *py;
    *py = tmp;
}
/*
before sort:
array element is: 9
array element is: 8
array element is: 1
array element is: 4
array element is: 3
array element is: 2
array element is: 5
array element is: 7
array element is: 6
array element is: 0
=====================
after sort:
j => arr[7] = 7
j => arr[6] = 5
i => arr[2] = 1
j => arr[4] = 6
j => arr[3] = 4
array element is: 0
array element is: 2
array element is: 1
array element is: 3
array element is: 6
array element is: 8
array element is: 5
array element is: 7
array element is: 4
array element is: 9
=====================
*/
```

