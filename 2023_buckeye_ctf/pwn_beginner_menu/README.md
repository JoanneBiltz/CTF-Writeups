# Beginner Menu, 408 solves, 40 points)

## Introduction

<p align="left">
  <img height=300 img src=./readme_assets/menu.PNG/>
</p>

For this challenge we get the source and binary of a small application.

```
fgets(buf, 50, stdin);
    if(strcmp(buf, "0\n")==0){
        printf("That's not an option\n");
        exit(0);
    }
    

	if(atoi(buf) ==1){
	    printf(joke[(rand()%5)]);
	    exit(0);
    }
	else if(atoi(buf) == 2){
	    printf(weather[(rand()%5)]);
	    exit(0);
    }
	else if(atoi(buf) ==3){
        while(num!=atoi(guess)){
	        printf("Guess the number I'm thinking of: ");
            fgets(guess, 50, stdin);
            if(atoi(guess)<num){
                printf("Guess higher!\n");
            }
            else if(atoi(guess)>num){
                printf("Guess lower!\n");
            }
        }
	    exit(0);
    }
	else if(atoi(buf)==4){
	    exit(0);
    }
	else if(atoi(buf)>4){
	    printf("That's not an option\n");
	    exit(0);
    }

    print_flag();
```
## Solution

The source is basically a menu structure where the program exits after every choice. At the bottom the flag is printed but for all positive numbers there is a matching branch, so we don't reach the print_flag call. 

<p align="left">
  <img height=300 img src=./readme_assets/game.PNG/>
</p>

Trying out different options we find that negative numbers and letters both give you the flag.

<p align="left">
  <img height=300 img src=./readme_assets/flag.PNG/>
</p>

## Flag

**`bctf{y0u_ARe_sNeaKy}`**





