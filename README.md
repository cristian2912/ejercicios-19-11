# Primer punto


**codigo paso a paso**


```
def obtener_digit(num, posicion):
    # esta funcion saca el digito en la posicion que le pasemos
    return (num // (8 ** posicion)) % 8

def radix_sort_octal(lista):
    # primero miramos cual es el numero mas grande para saber cuantas veces tenemos que ordenar
    max_num = max(lista)
    max_posicion = 0
    while max_num > 0:
        max_num //= 8
        max_posicion += 1

    # ahora ordenamos la lista, por cada "posicion" (unidades, decenas, centenas, etc.)
    for pos in range(max_posicion):
        # creamos 8 "buckets" (uno para cada digito posible en octal)
        buckets = [[] for _ in range(8)]

        # metemos los numeros en los "buckets" segun el digito en esa posicion
        for num in lista:
            digit = obtener_digit(num, pos)
            buckets[digit].append(num)

        # reconstruimos la lista con los numeros ordenados por el digito de esa posicion
        lista = []
        for bucket in buckets:
            lista.extend(bucket)

        # imprimimos el estado de la lista despues de ordenar por esta posicion
        print(f"Despues de ordenar por la {pos+1}a posicion (octal): {lista}")

    return lista

# ejemplo de uso
numeros = [72, 35, 15, 9, 100, 60, 21]
# convertimos los numeros a 3 digitos en octal (por ejemplo: 72 -> 072)
numeros_octal = [int(oct(num)[2:].zfill(3), 8) for num in numeros]
print("Lista original:", numeros)
ordenados = radix_sort_octal(numeros_octal)
print("Lista ordenada:", ordenados)
```

**Resultado esperado:**

Lista original: [72, 35, 15, 9, 100, 60, 21]
Despues de ordenar por la 1a posicion (octal): [72, 9, 35, 100, 60, 21, 15]
Despues de ordenar por la 2a posicion (octal): [72, 9, 15, 21, 35, 100, 60]
Despues de ordenar por la 3a posicion (octal): [9, 15, 21, 35, 60, 72, 100]
Lista ordenada: [9, 15, 21, 35, 60, 72, 100]
 
