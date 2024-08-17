# N Queens Problem 

### Code 

``` c
#include<stdio.h>
int count = 0;

int canPlace(int r,int c,int n,char board[n][n]){
    int row = r,col = c;
    //check for row above
    while(row>=0){
        if(board[row][c] == 'Q') return 0;
        row--;
    }

    row = r,col = c;
    //check for right diagnol
    while(row>=0 && col<n){
        if(board[row][col]=='Q') return 0;
        row--;
        col++;
    }

    row = r,col = c;
    //check for left diagnol
    while(row>=0 && col>=0){
        if(board[row][col]=='Q') return 0;
        row--;
        col--;
    }

    return 1;
}

void nqueens(int row,int n,char board[n][n]){
    if(row == n){
        count++;
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                printf("%c\t",board[i][j]);
            }
            printf("\n");
        }
        
        printf("\n");
        return;
    }

    for(int i=0;i<n;i++){
        if(canPlace(row,i,n,board)==1){
            board[row][i] = 'Q';
            nqueens(row+1,n,board);
            board[row][i] = '.';
        }
    }
    return;
}

int main(){
    int n;
    printf("Enter n (no of queens):\n ");
    scanf("%d", &n);
   
    if(n==2 || n==3)
        printf("Solution does not exist.");
    else{
        char board[n][n];
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                board[i][j] = '.';
            }
        }
        nqueens(0,n,board);
        printf("Total number of solutions: %d\n", count);
    }
    return 0;
}

```

### output 

```bash
Enter n (no of queens): 6
 .	Q	.	.	.	.	
.	.	.	Q	.	.	
.	.	.	.	.	Q	
Q	.	.	.	.	.	
.	.	Q	.	.	.	
.	.	.	.	Q	.	

.	.	Q	.	.	.	
.	.	.	.	.	Q	
.	Q	.	.	.	.	
.	.	.	.	Q	.	
Q	.	.	.	.	.	
.	.	.	Q	.	.	

.	.	.	Q	.	.	
Q	.	.	.	.	.	
.	.	.	.	Q	.	
.	Q	.	.	.	.	
.	.	.	.	.	Q	
.	.	Q	.	.	.	

.	.	.	.	Q	.	
.	.	Q	.	.	.	
Q	.	.	.	.	.	
.	.	.	.	.	Q	
.	.	.	Q	.	.	
.	Q	.	.	.	.	

Total number of solutions: 4


``
