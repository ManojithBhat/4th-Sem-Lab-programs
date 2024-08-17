# Sub Set Problem 

### code 

``` c
#include<stdio.h>
#define MAX 10
int s[MAX],vis[MAX];
int d;
void sumofsub(int currSum, int ind, int remSum){
    //mark the current element as visited 
    vis[ind] = 1;
    //check is the currSum ( that is till now, excluding curr element ) is equal to d
    if(currSum + s[ind] == d){
        //print the solution
        for(int i = 1;i<=ind;i++){
            if(vis[i]==1)
                printf("%d\t",s[i]);}
        printf("\n");
    }
    else if(currSum + s[ind] + s[ind+1] <= d){
        //if the sum + currElement does not lead to the d so we pick this element,
        //we add another condition, we take it only if we could take the next element
        sumofsub(currSum + s[ind],ind+1,remSum - s[ind]);
    }

    //Notpick condition is that we remove the curr element and check for 2 condition before proceeding 
    if((currSum + remSum - s[ind] >= d) && (currSum + s[ind+1]<=d)){
        vis[ind] = 0;
        sumofsub(currSum,ind+1,remSum-s[ind]); //we need to subtract from remSum
    }
}
int main(){
    int i,n,sum=0;
    printf("Enter size of the array: ");
    scanf("%d",&n);
    printf("\n Enter the elements in increasing order : \n");
    for(i=1;i<=n;i++){
        scanf("%d",&s[i]);
        sum=sum + s[i];
    }
    
    printf("\n Enter the subset sum value: ");
    scanf("%d",&d);

    if (sum <d|| s[1] > d)
        printf("n No subset possible");
    else{
        sumofsub(0,1,sum);
    }
}

```


### Output 

``` bash

Enter size of the array: 5

 Enter the elements in increasing order : 
1 2 3 4 5

 Enter the subset sum value: 8
1	2	5	
1	3	4	
3	5


```
