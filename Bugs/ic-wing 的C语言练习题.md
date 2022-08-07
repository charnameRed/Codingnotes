# ic-wing 的C语言练习题

## Part 1

### 进制转换

```c
#include<stdio.h>
int convert(int*num, char*output, int length);

int main()
{
    int n,r;
    int i = 0,answer[128] = {0};

    printf("请输入十进制数与希望的进制(最高十六进制)\n");

    while(scanf("%d%d",&n,&r) != EOF)
    {
        if (r < 2 || r > 16)
        {
            printf("输入进制有误\n");
            continue;
        }

        if (n == 0) 
            printf("0\n");
        
        while (n != 0)
        {
            answer[i++] = n%r;
            n /= r;
        }
        
        char output[i];

        convert(answer,output,i);

        printf("%s",output);

        printf("\n");
        
        i = 0;
    }

    return 0;
}

int convert(int*num, char*output, int length)
{
    char elements[16] = {'0','1','2','3','4','5','6','7','8','9','a','b','c','d','e','f'};

    for(int i = 0;i < length;i++)
    {
        output[i] = elements[num[length-i-1]];
    }

    return 0;
}
```

- **问题:** 当输出仅为一位数时, 输出后面会带有其他字符
- **原因:** `char output[]`之后没有空字符`\0`, 导致`output[]`以字符串形式输出时无法检测到终止位.
- **解决方法:**
    1. 将`printf("%s",output)`的直接输出字符串改为逐字符输出;

        ```c
        for (int t = 0; t < i; t++)
        {printf("%c",output[t]);}
        ```

    2. 在定义`output[]`时在末尾插入空字符;

        ```c
        char output[i+1];
        output [i] = '/0';
        ```
