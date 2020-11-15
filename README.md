# Projek SO - Kelompok 6
|Nama|NIM|
|-----|------|
|Alfian Arief Santoso | G64180061 |
|Muhammad Rayhan Adyatma | G64180064 |
|Muhammad Khoiru Tobi Albertino| G64180065 |
|Muhammad Faris Waliyuddin | G64180067|

-------------

## Topik 17 : Multithread Sekuens Fibonacci
### Programming Problem
The Fibonacci sequence is the series of numbers 0, 1, 1, 2, 3, 5, 8, .... Formally, it can be expressed as: fib0 = 0, fib1 = 1, fibn = fibn−1 + fibn−2. Write a multithreaded program that generates the Fibonacci sequence. This program should work as follows: On the command line, the user will enter the number of Fibonacci numbers that the program is to generate. The program will then create a separate thread that will generate the Fibonacci numbers, placing the sequence in data that can be shared by the threads (an array is probably the most convenient data structure). When the thread finishes execution, the parent thread will output the sequence generated by the child thread. Because the parent thread cannot begin outputting the Fibonacci sequence until the child thread finishes, the parent thread will have to wait for the child thread to finish. Use the techniques described in Section 4.4 to meet this requirement.

### Implementasi Algoritme
```sh
#include <stdio.h>
#include <pthread.h>
#include <stdlib.h>

int N,count=2;

void *fibonacci(void *arg){
	int *A = (int*)arg;				// cast void* --> int*
	int i;
	
	for(i = 0; i <= N; i++){
		A[i] = A[i-1] + A[i-2]; 
	}
	pthread_exit(NULL);
}

int main(){
	pthread_t child;
	scanf("%d",&N);
	
	int A[N+2], i;
	A[0] = 0; 
	A[1] = 1; 
	
	//Thread child memproses bilangan fibonacci
	pthread_create(&child, NULL, fibonacci, &A[2]);
	pthread_join(child, NULL);

	//Thread parent mencetak baris fibonacci
	for (i=1; i<N; i++){
		printf("%d, ",A[i]);
	}
	printf("%d\n",A[N]);
	
	return 0;
}
```
