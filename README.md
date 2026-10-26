notas = []

# 1. Leer cuatro notas
for i in range(4):
    nota = float(input("Ingrese una nota entre 0 y 5: "))
    notas.append(nota)

# 2. Mostrar las notas
print("\n--- NOTAS REGISTRADAS ---")
for i in range(len(notas)):
    print("Nota", i + 1, ":", notas[i])

# 3. Estadisticas
promedio = sum(notas) / len(notas)
print("Promedio:", round(promedio, 2))
print("Nota mayor:", max(notas))
print("Nota menor:", min(notas))

# 4. Modificar una nota
posicion = int(input("Posicion de la nota que desea modificar (1-4): "))
if posicion >= 1 and posicion <= len(notas):
    nueva_nota = float(input("Nueva nota: "))
    notas[posicion - 1] = nueva_nota
    print("Notas despues de modificar:", notas)
else:
    print("Posicion no valida.")

# 5. Eliminar una nota
if len(notas) > 0:
    posicion = int(input("Posicion que desea eliminar (1-" + str(len(notas)) + "): "))
    if posicion >= 1 and posicion <= len(notas):
        eliminada = notas.pop(posicion - 1)
        print("Se elimino:", eliminada)
        print("Notas finales:", notas)
    else:
        print("Posicion no valida.")
