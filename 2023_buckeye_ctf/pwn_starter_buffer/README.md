# Starter Buffer, 326 solves, 60 points)

## Introduction

<p align="left">
  <img height=300 img src=./readme_assets/starter-challenge.PNG/>
</p>

We are given an executable named buffer and a c program called starter-buffer.

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void print_flag(void) {
    FILE* fp = fopen("flag.txt", "r");
    char flag[100];
    fgets(flag, sizeof(flag), fp);
    puts(flag);
}

int main(void) {
    // Ignore me
    setbuf(stdout, NULL);

    int flag = 0xaabdcdee;
    char buf[50] = {0};
	printf("Enter your favorite number: ");
	fgets(buf, 0x50, stdin);

    if(flag == 0x45454545){
        print_flag();
    }
    else{
        printf("Too bad! The flag is 0x%x\n", flag);
    }

    return 0;
}
```

## Solution

Looking at the code we see we have to make the flag equal ***`flag == 0x45454545`***.

Through trial and error I got the flag using a long string of **`E`**s. This would have been much easier if I had looked to see what letter **`0x45454545`** converted to.

<p align="left">
  <img height=400 img src=./readme_assets/buffer.PNG/>
</p>

<p align="left">
  <img height=300 img src=./readme_assets/buffer2.PNG/>
</p>

## Flag

**`bctf{wHy_WriTe_OveR_mY_V@lUeS}`**





