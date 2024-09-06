```c
typedef struct 
{
    // 指向栈低的指针变量
    ElemType *base;
    // 指向栈顶的指针变量
    ElemType *top;
    //栈当前可用的最大容量
    int stacksize;
    /* data */
}SqStack;

#define STACKINCREMENT 10
#define STACK_INIT_SIZE 100  // 定义栈的初始大小为100

// 初始化顺序栈的函数
void initStack(sqStack *s) 
{
    // 为栈的 base 分配初始内存，大小为 STACK_INIT_SIZE 个 ElemType 类型的元素
    // malloc()申请空间
    s->base = (ElemType *)malloc(STACK_INIT_SIZE * sizeof(ElemType));

    // 检查内存分配是否成功，如果失败则退出程序
    if (!s->base)
        exit(0);

    // 将栈顶指针初始化为栈底指针，表示栈为空时栈顶与栈底相同
    s->top = s->base;  // 最开始，栈顶就是栈底

    // 设置栈的初始大小为 STACK_INIT_SIZE
    s->stackSize = STACK_INIT_SIZE;
}

#define STACKINCREMENT 10  // 定义栈空间每次扩展的增量为10

void Push(sqStack *s, ElemType e)
{
    // 检查栈是否已满：如果栈顶指针减去栈底指针的值大于等于当前栈的最大容量，说明栈满了
    if (s->top - s->base >= s->stackSize)
    {
        // 扩展栈空间：增加 STACKINCREMENT 个元素的存储空间
        s->base = (ElemType *)realloc(s->base, (s->stackSize + STACKINCREMENT) * sizeof(ElemType));

        // 检查内存分配是否成功，如果失败则退出程序
        if (!s->base)
            exit(0);

        // 更新栈顶指针，指向新的栈顶位置，即扩展后的新内存块的末尾
        s->top = s->base + s->stackSize;

        // 更新栈的最大容量，增加了 STACKINCREMENT 个元素的空间
        s->stackSize = s->stackSize + STACKINCREMENT;
    }

    // 将元素 e 压入栈顶
    *(s->top) = e;

    // 更新栈顶指针，指向下一个空位置
    s->top++;
}
void Pop(sqStack *s, ElemType *e)
{
    // 检查栈是否为空：如果栈顶指针等于栈底指针，说明栈已空
    if (s->top == s->base)  // 栈已空
        return;  // 直接返回，不执行弹出操作

    // 弹出栈顶元素：先将栈顶指针向下移动一位，再将该位置的元素赋值给 e
    *e = *--(s->top);
}

```
