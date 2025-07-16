# reto 12 
1. Desarrollar un algoritmo que imprima de manera ascendente los valores (todos del mismo tipo) de un diccionario.
```python

mi_diccionario = {
    "a": 50,
    "b": 20,
    "c": 80,
    "d": 10
}

valores_ordenados = sorted(mi_diccionario.values())

print("Valores del diccionario en orden ascendente:")
for valor in valores_ordenados:
    print(valor)
```
2. Desarrollar una función que reciba dos diccionarios como parámetros y los mezcle, es decir, que se construya un nuevo diccionario con las llaves de los dos diccionarios; si hay una clave repetida en ambos diccionarios, se debe asignar el valor que tenga la clave en el primer diccionario.

```python

def mezclar_diccionarios(dict1, dict2):
   
    combinado = dict2.copy()
 
    combinado.update(dict1)

    return combinado
```
3. Cree un programa que lea de un archivo con dicho JSON y:

+ Imprima los nombres completos (nombre y apellidos) de las personas que practican el deporte ingresado por el usuario.
+ Imprima los nombres completos (nombre y apellidos) de las personas que estén en un rango de edades dado por el usuario.

```python
import json

# Leer el archivo JSON
with open('personas.json', 'r', encoding='utf-8') as archivo:
    personas = json.load(archivo)

# Función para imprimir nombres completos según deporte
def buscar_por_deporte(deporte):
    print(f"\nPersonas que practican {deporte}:")
    encontrado = False
    for persona in personas.values():
        if deporte in persona["deportes"]:
            print(f"- {persona['nombres']} {persona['apellidos']}")
            encontrado = True
    if not encontrado:
        print("Ninguna persona practica ese deporte.")

# Función para imprimir nombres completos según rango de edad
def buscar_por_rango_edad(min_edad, max_edad):
    print(f"\nPersonas entre {min_edad} y {max_edad} años:")
    encontrado = False
    for persona in personas.values():
        if min_edad <= persona["edad"] <= max_edad:
            print(f"- {persona['nombres']} {persona['apellidos']}")
            encontrado = True
    if not encontrado:
        print("Ninguna persona está en ese rango de edad.")

# Menú de opciones
while True:
    print("\n--- Menú ---")
    print("1. Buscar por deporte")
    print("2. Buscar por rango de edad")
    print("0. Salir")
    opcion = input("Seleccione una opción: ")

    if opcion == "1":
        deporte_input = input("Ingrese el deporte a buscar: ").strip()
        buscar_por_deporte(deporte_input)
    elif opcion == "2":
        try:
            min_edad = int(input("Edad mínima: "))
            max_edad = int(input("Edad máxima: "))
            buscar_por_rango_edad(min_edad, max_edad)
        except ValueError:
            print("Por favor ingrese edades válidas.")
    elif opcion == "0":
        print("Fin del programa.")
        break
    else:
        print("Opción no válida.")
```
4. A través de un programa conectese a al menos 3 API's , obtenga el JSON, imprimalo y extraiga los pares de llave : valor.

```python
import requests

# Función para mostrar pares clave:valor de un JSON (solo nivel superior)
def mostrar_claves_valores(json_data):
    for clave, valor in json_data.items():
        print(f"{clave} : {valor}")
    print("-" * 40)

# 1. API de usuario aleatorio
print("\n🔹 API 1: Random User (https://randomuser.me/api/)")
respuesta1 = requests.get("https://randomuser.me/api/")
json1 = respuesta1.json()
print("JSON completo:")
print(json1)
print("\nPares clave:valor (nivel superior):")
mostrar_claves_valores(json1)

# 2. API de Pokémon
print("\n🔹 API 2: PokéAPI (https://pokeapi.co/api/v2/pokemon/pikachu)")
respuesta2 = requests.get("https://pokeapi.co/api/v2/pokemon/pikachu")
json2 = respuesta2.json()
print("JSON completo:")
print(json2)
print("\nPares clave:valor (nivel superior):")
mostrar_claves_valores(json2)

# 3. API de información sobre criptomonedas (CoinDesk Bitcoin Price Index)
print("\n🔹 API 3: CoinDesk BTC (https://api.coindesk.com/v1/bpi/currentprice.json)")
respuesta3 = requests.get("https://api.coindesk.com/v1/bpi/currentprice.json")
json3 = respuesta3.json()
print("JSON completo:")
print(json3)
print("\nPares clave:valor (nivel superior):")
mostrar_claves_valores(json3)

```
