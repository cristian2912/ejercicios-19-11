# Primer punto

**usando radix sort y counting sort**

**codigo:**

**codigo saltandonos el paso a paso:**

```
#include <stdio.h>
#include <stdlib.h>

#define BASE 8 // base octal

// funcion para contar y ordenar los elementos por digitos
void countingSort(int arr[], int n, int exp) {
    int output[n];
    int count[BASE] = {0};

    // contar los digitos en la posicion actual
    for (int i = 0; i < n; i++) {
        int digit = (arr[i] / exp) % BASE;
        count[digit]++;
    }

    // ajustar los indices para que representen las posiciones correctas
    for (int i = 1; i < BASE; i++) {
        count[i] += count[i - 1];
    }

    // construir el arreglo ordenado usando los indices
    for (int i = n - 1; i >= 0; i--) {
        int digit = (arr[i] / exp) % BASE;
        output[count[digit] - 1] = arr[i];
        count[digit]--;
    }

    // copiar el resultado de vuelta al arreglo original
    for (int i = 0; i < n; i++) {
        arr[i] = output[i];
    }
}

// funcion principal del radix sort
void radixSort(int arr[], int n) {
    // buscar el maximo para saber cuantos digitos tiene
    int max = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] > max) {
            max = arr[i];
        }
    }

    // ordenar para cada digito desde el menos significativo
    for (int exp = 1; max / exp > 0; exp *= BASE) {
        countingSort(arr, n, exp);
    }
}

int main() {
    int arr[] = {75, 56, 17, 34, 10, 64, 7, 120};
    int n = sizeof(arr) / sizeof(arr[0]);

    // imprimir el arreglo original
    printf("arreglo original:\n");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");

    // ordenar el arreglo
    radixSort(arr, n);

    // imprimir el arreglo ordenado
    printf("arreglo ordenado:\n");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");

    return 0;
}
```


