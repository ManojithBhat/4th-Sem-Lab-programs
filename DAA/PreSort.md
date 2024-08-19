# Pre Sorting 


### code 

In separate file named mergeSort.h write the code for mergeSort which will be used as a library to call mergeSort function.
``` c
#include <stdio.h>
#include <stdlib.h>

#define N 32000

void merge(int arr[], int low, int mid, int high) {     
    
    int left = low;
    int right = mid + 1;
    
    int temp[high - low + 1];
    int k = 0;

    while (left <= mid && right <= high) {
        if (arr[left] <= arr[right]) {
            temp[k++] = arr[left++];
        } else {
            temp[k++] = arr[right++];
        }
    }

    while (left <= mid) {
        temp[k++] = arr[left++];
    }

    while (right <= high) {
        temp[k++] = arr[right++];
    }

    for (int i = low; i <= high; i++) {
        arr[i] = temp[i - low];
    }

}

void MergeSort(int arr[], int low, int end) {
    if (low >= end) return;
    int mid = (low + end) / 2;
    MergeSort(arr, low, mid);
    MergeSort(arr, mid + 1, end);
    merge(arr, low, mid, end);
}

```

### code  
file from where mergeSort function will be called
``` c
#include<stdio.h>
#include "mergeSort.h"

void main(){
    printf("Enter the number of elements\n");
    int size;
    scanf("%d",&size);
    int arr[size];
    for (int i=0;i<size;i++){
        printf("Enter element %d : \t",i+1);
        scanf("%d",&arr[i]);
    }
    MergeSort(arr,0,size-1);
    int i=0;
    for(i=0;i<size-1;i++){
        if(arr[i] == arr[i+1]){
            printf("Array is not Unique\n");
            break;
        }
    }
    if(i == size-1){
        printf("Array is Unique\n");
    }
}

```
