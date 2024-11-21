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

# Explicación

Paso 1: Ordenando por la unidad (1ª posición en octal)
Cuando ordenamos los números por las unidades, lo que estamos haciendo es agruparlos según el último dígito en su representación octal (por ejemplo, 72 en octal es 72, y 100 es 144). Esto es lo que ocurre:

72 (octal 72) → dígitos de unidades es2
35 (octal 43) → dígitos de unidades es3
15 (octal 17) → dígitos de unidades es7
9 (octal 11) → dígitos de unidades es1
100 (octal 144) → dígitos de unidades es4
60 (octal 74) → dígitos de unidades es4
21 (octal 25) → dígitos de unidades es5
Después de ordenar por las unidades:

Salida esperada :[72, 9, 35, 100, 60, 21, 15]

Paso 2: Ordenando por la decena (2ª posición en octal)
Ahora, ordenamos por el siguiente dígito (la decena), y para eso, tratamos los números como si fueran de 3 dígitos:

72 (octal 72) → dígito de decenas es7
9 (octal 11) → dígito de decenas es1
35 (octal 43) → dígito de decenas es4
100 (octal 144) → dígito de decenas es4
60 (octal 74) → dígito de decenas es7
21 (octal 25) → dígito de decenas es2
15 (octal 17) → dígito de decenas es1
Después de ordenar por las decenas:

Salida esperada :[72, 9, 15, 21, 35, 100, 60]

Paso 3: Ordenando por la centena (3ª posición en octal)
Finalmente, ordenamos por la centena:

72 (octal 72) → dígitos de centenas es0
9 (octal 11) → dígito de centenas es0
15 (octal 17) → dígitos de centenas es0
21 (octal 25) → dígito de centenas es0
35 (octal 43) → dígitos de centenas es0
100 (octal 144) → dígitos de centenas es1
60 (octal 74) → dígitos de centenas es0
Después de ordenar por las centenas:

Salida esperada :[9, 15, 21, 35, 60, 72, 100]


![image](https://github.com/user-attachments/assets/4f9c033b-6b29-4639-aae9-c89c72e4f638)

