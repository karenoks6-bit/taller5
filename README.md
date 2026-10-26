"""Gestor de inventario con listas paralelas.

productos[i] y cantidades[i] describen siempre el mismo producto.
No se usan diccionarios, clases, archivos ni librerías externas.
"""

productos = []
cantidades = []


# ---------- Funciones auxiliares ----------

def leer_entero_no_negativo(mensaje):
    """Pide un entero >= 0 hasta que el usuario lo escriba bien."""
    while True:
        texto = input(mensaje).strip()
        if texto.isdigit():
            return int(texto)
        print("Entrada no valida. Escriba un numero entero mayor o igual a 0.")


def buscar_indice(nombre):
    """Devuelve el indice del producto (sin distinguir mayusculas) o -1."""
    for i in range(len(productos)):
        if productos[i].lower() == nombre.lower():
            return i
    return -1


# ---------- Funciones del menu ----------

def registrar_producto():

    nombre = input("Nombre del producto: ").strip()
    if nombre == "":
        print("El nombre no puede estar vacio.")
        return
    # Decision: no se permiten duplicados. Si el producto ya existe,
    # se informa y el usuario puede usar la opcion 4 para cambiar su cantidad.
    if buscar_indice(nombre) != -1:
        print("El producto '" + nombre + "' ya esta registrado. "
              "Use la opcion 4 para modificar su cantidad.")
        return
    cantidad = leer_entero_no_negativo("Cantidad disponible: ")
    productos.append(nombre)
    cantidades.append(cantidad)
    print("Producto registrado correctamente.")


def mostrar_inventario():
    if len(productos) == 0:
        print("El inventario esta vacio.")
        return
    print("\n--- INVENTARIO ---")
    for i in range(len(productos)):
        print(i + 1, "-", productos[i], "-", cantidades[i], "unidades")


def buscar_producto():
    nombre = input("Nombre del producto a buscar: ").strip()
    i = buscar_indice(nombre)
    if i == -1:
        print("El producto '" + nombre + "' no existe en el inventario.")
    else:
        print("Encontrado:", productos[i], "-", cantidades[i],

              "unidades (posicion", i + 1, ")")


def modificar_cantidad():
    if len(productos) == 0:
        print("El inventario esta vacio.")
        return
    nombre = input("Producto cuya cantidad desea modificar: ").strip()
    i = buscar_indice(nombre)
    if i == -1:
        print("El producto '" + nombre + "' no existe en el inventario.")
        return
    nueva = leer_entero_no_negativo("Nueva cantidad: ")
    anterior = cantidades[i]
    cantidades[i] = nueva
    print(productos[i] + ": cantidad cambiada de", anterior, "a", nueva)


def eliminar_producto():
    if len(productos) == 0:
        print("El inventario esta vacio.")
        return
    nombre = input("Producto que desea eliminar: ").strip()
    i = buscar_indice(nombre)
    if i == -1:
        print("El producto '" + nombre + "' no existe en el inventario.")
        return
    # Se elimina el MISMO indice en ambas listas para mantenerlas sincronizadas.
    eliminado = productos.pop(i)
    cantidades.pop(i)
    print("Producto eliminado:", eliminado)



def contar_productos():
    print("Productos diferentes registrados:", len(productos))


def producto_mayor_cantidad():
    if len(productos) == 0:
        print("El inventario esta vacio.")
        return
    mayor = max(cantidades)
    print("Mayor cantidad disponible (" + str(mayor) + " unidades):")
    for i in range(len(productos)):
        if cantidades[i] == mayor:  # muestra todos si hay empate
            print(" -", productos[i])


def mostrar_menu():
    print("\n===== GESTOR DE INVENTARIO =====")
    print("1. Registrar producto")
    print("2. Mostrar inventario")
    print("3. Buscar producto")
    print("4. Modificar cantidad")
    print("5. Eliminar producto")
    print("6. Cantidad de productos diferentes")
    print("7. Producto con mayor cantidad")
    print("8. Salir")


def main():
    opcion = ""
    while opcion != "8":
        mostrar_menu()

        opcion = input("Elija una opcion: ").strip()
        if opcion == "1":
            registrar_producto()
        elif opcion == "2":
            mostrar_inventario()
        elif opcion == "3":
            buscar_producto()
        elif opcion == "4":
            modificar_cantidad()
        elif opcion == "5":
            eliminar_producto()
        elif opcion == "6":
            contar_productos()
        elif opcion == "7":
            producto_mayor_cantidad()
        elif opcion == "8":
            print("Hasta luego.")
        else:
            print("Opcion no valida. Elija un numero del 1 al 8.")


if __name__ == "__main__":
    main()
