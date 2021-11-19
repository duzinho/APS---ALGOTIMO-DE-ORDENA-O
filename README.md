# APS---ALGOTIMO-DE-ORDENA-O
#include <stdio.h>
#include <stdbool.h>
#include <time.h>


// ----- BUBBLE SORT -----

void BubbleSort(int *v, int tam){
    int i;

    int a, b, aux;

    for(a = tam -1 ; a>=1 ; a--){
        for(b=0 ; b<a ; b++){
            if(v[b]>v[b+1]){
                aux = v[b];
                v[b] = v[b+1];
                v[b+1] = aux;
            }
        }

    }
}

// ----- QUICK SORT -----

void QuickSort(int *v, int E, int D){
    int i, j, pivot, temp;

    for(i=0 ; i<D ; i++)
        v[i] = v[i];

    if(E < D){
        pivot = E;
        i = E;
        j = D;

    while(i<j){
        while(v[i]<=v[pivot]&&i<D)
            i++;
        while(v[j]>v[pivot])
            j--;
        if(i<j){
            temp = v[i];
            v[i] = v[j];
            v[j] = temp;
        }
    }

    temp = v[pivot];
    v[pivot] = v[j];
    v[j] = temp;
    QuickSort(v, E, j-1);
    QuickSort(v, j+1, D);
    }
}


// ----- INSERTION SORT -----

void InsertionSort(int *v, int tam){

    int i, j, tmp;

        for(i=0;i<tam;i++){
           // printf("\n v[%d]:", i);
            //printf("\n");
            //scanf("%i", &v[i]);
        }

        for(i=1 ; i<5 ; i++){
            tmp = v[i];
            j = i - 1;
            while((j>=0) && (v[j]>tmp)){
                v[j+1] = v[j];
                j = j - 1;
            }
            v[j+1] = tmp;
        }
}


// ----- BINARY INSERTION SORT -----

void BinaryInsertionSort(int a[], int n)
{
    int i, loc, j, k, selected;

    for (i = 1; i < n; ++i)
    {
        j = i - 1;
        selected = a[i];


        loc = BinarySearch(a, selected, 0, j);


        while (j >= loc)
        {
            a[j+1] = a[j];
            j--;
        }
        a[j+1] = selected;
    }
}

int BinarySearch(int a[], int item,
                 int low, int high)
{
    if (high <= low)
        return (item > a[low]) ?
                (low + 1) : low;

    int mid = (low + high) / 2;

    if (item == a[mid])
        return mid + 1;

    if (item > a[mid])
        return BinarySearch(a, item,
                            mid + 1, high);
    return BinarySearch(a, item, low,
                        mid - 1);
}

// ----- SELECTION SORT -----

void SelectionSort(int *v, int tam){
    int vMenor, vAux, vTemp, vTroca;

    for(vAux = 0; vAux < tam-1 ; vAux++){
        vMenor = vAux;
        for(vTemp = vAux + 1 ; vTemp < tam ; vTemp++){
            if(v[vTemp] < v[vMenor]){
                vMenor = vTemp;
            }

            if(vMenor != vAux){
                vTroca = v[vAux];
                v[vAux] = v[vMenor];
                v[vMenor] = vTroca;
            }
        }
    }
}

// ----- HEAP SORT -----

void HeapSort(int a[], int n) {
   int i = n / 2, pai, filho, t;
   while(true) {
      if (i > 0) {
          i--;
          t = a[i];
      } else {
          n--;
          if (n <= 0) return;
          t = a[n];
          a[n] = a[0];
      }
      pai = i;
      filho = i * 2 + 1;
      while (filho < n) {
          if ((filho + 1 < n)  &&  (a[filho + 1] > a[filho]))
              filho++;
          if (a[filho] > t) {
             a[pai] = a[filho];
             pai = filho;
             filho = pai * 2 + 1;
          } else {
             break;
          }
      }
      a[pai] = t;
   }
}


// ----- MERGE SORT -----

void merge(int arr[], int l, int m, int r)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 =  r - m;

    int L[n1], R[n2];

    for (i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (j = 0; j < n2; j++)
        R[j] = arr[m + 1+ j];

    i = 0;
    j = 0;
    k = l;
    while (i < n1 && j < n2)
    {
        if (L[i] <= R[j])
        {
            arr[k] = L[i];
            i++;
        }
        else
        {
            arr[k] = R[j];
            j++;
        }
        k++;
    }

    while (i < n1)
    {
        arr[k] = L[i];
        i++;
        k++;
    }

    while (j < n2)
    {
        arr[k] = R[j];
        j++;
        k++;
    }
}


void MergeSort(int arr[], int l, int r)
{
    if (l < r)
    {

        int m = l+(r-l)/2;


        MergeSort(arr, l, m);
        MergeSort(arr, m+1, r);

        merge(arr, l, m, r);
    }
}


void printArray(int A[], int size)
{
    int i;
    for (i=0; i < size; i++)
        printf("%d ", A[i]);
    printf("\n");
}


// ----- BUCKET SORT -----

struct bucket
{
    int count;
    int* value;
};

int compareIntegers(const void* first, const void* second)
{
    int x = *((int*)first), y =  *((int*)second);
    if (x == y)
    {
        return 0;
    }
    else if (x < y)
    {
        return -1;
    }
    else
    {
        return 1;
    }
}

void BucketSort(int array[],int n)
{
    struct bucket buckets[3];
    int i, j, k;
    for (i = 0; i < 3; i++)
    {
        buckets[i].count = 0;
        buckets[i].value = (int*)malloc(sizeof(int) * n);
    }

    for (i = 0; i < n; i++)
    {
        if (array[i] < 0)
        {
            buckets[0].value[buckets[0].count++] = array[i];
        }
        else if (array[i] > 10)
        {
            buckets[2].value[buckets[2].count++] = array[i];
        }
        else
        {
            buckets[1].value[buckets[1].count++] = array[i];
        }
    }
    for (k = 0, i = 0; i < 3; i++)
    {

        qsort(buckets[i].value, buckets[i].count, sizeof(int), &compareIntegers);
        for (j = 0; j < buckets[i].count; j++)
        {
            array[k + j] = buckets[i].value[j];
        }
        k += buckets[i].count;
        free(buckets[i].value);
    }
}


void imprimeVetor(int *v, int tam){
    int i;
        for(i=0;i<tam;i++)
           printf("\nv[%d]: %d", i,v[i]);

}


int main(int argc, char *argv[])
{
    int i, tam;

    printf("Digite o tamanho do vetor: ");
    scanf("%d", &tam);
    int vetor[tam];

    printf("\n");


    for(i = 0; i < tam; i++)
    {
        vetor[i] = rand() % 100;
    }


    clock_t begin;
    clock_t end;

    begin = clock();
    BubbleSort(vetor, tam);
    end = clock();
    printf("Tempo da Execucao BubbleSort: %f seconds\n", (double)(end - begin) / CLOCKS_PER_SEC);

  //  imprimeVetor(vetor, tam);

    begin = clock();
    InsertionSort(vetor, tam);
    end = clock();
    printf("Tempo da Execucao InsertionSort: %f seconds\n", (double)(end - begin) / CLOCKS_PER_SEC);

    begin = clock();
    QuickSort(vetor, 0, tam);
    end = clock();
    printf("Tempo da Execucao QuickSort: %f seconds\n", (double)(end - begin) / CLOCKS_PER_SEC);

    begin = clock();
    BinaryInsertionSort(vetor, tam);
    end = clock();
    printf("Tempo da Execucao BinaryInsertionSort: %f seconds\n", (double)(end - begin) / CLOCKS_PER_SEC);


    begin = clock();
    SelectionSort(vetor, tam);
    end = clock();
    printf("Tempo da Execucao SelectinSort: %f seconds\n", (double)(end - begin) / CLOCKS_PER_SEC);

    begin = clock();
    HeapSort(vetor, tam);
    end = clock();
    printf("Tempo da Execucao HeapSort: %f seconds\n", (double)(end - begin) / CLOCKS_PER_SEC);

    begin = clock();
    MergeSort(vetor, 0, tam);
    end = clock();
    printf("Tempo da Execucao MergeSort: %f seconds\n", (double)(end - begin) / CLOCKS_PER_SEC);


    begin = clock();

    BucketSort(vetor, tam);
    end = clock();
    printf("Tempo da Execucao BucketSort: %f seconds\n", (double)(end - begin) / CLOCKS_PER_SEC );

    free(vetor);

    system("pause");
    return 0;
}


