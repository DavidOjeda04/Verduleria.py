inventario = []

def agregar_producto():
    """ALTA: crea un diccionario con el producto y lo guarda en la lista"""
    nombre = input("Nombre de la fruta o verdura: ").strip()
    
    # Validamos que el precio sea un número positivo usando un bucle y try/except
    while True:
        try:
            precio = float(input("Precio por kilo: "))
            if precio > 0:
                break
            print("Error: El precio debe ser mayor a 0.")
        except ValueError:
            print("Error: Ingrese un número válido.")
            
    while True:
        try:
            stock = float(input("Kilos disponibles: "))
            if stock >= 0:
                break
            print("Error: El stock no puede ser negativo.")
        except ValueError:
            print("Error: Ingrese un número válido.")

    producto = {
        "nombre": nombre,
        "precio": precio,
        "stock": stock
    }
    
    inventario.append(producto)
    print("¡Registro agregado con éxito!")
def mostrar_inventario():
    """Muestra todos los productos registrados en la verdulería"""
    if len(inventario) == 0:
        print("\nEl inventario está vacío. ¡Todavía no cargaste ningún producto!")
    else:
        print("\n--- LISTA DE PRODUCTOS EN EL INVENTARIO ---")
        for i, producto in enumerate(inventario, 1):
            print(f"{i}. {producto['nombre'].capitalize()} - Precio: ${producto['precio']} | Stock: {producto['stock']} kg")
    
agregar_producto()
mostrar_inventario()
def buscar_producto():
    """Busca un producto por su nombre en el inventario"""
    nombre_buscar = input("\nIngrese el nombre de la fruta o verdura que busca: ").strip().lower()
    encontrado = False
    
    for producto in inventario:
        if producto["nombre"].lower() == nombre_buscar:
            print("\n¡Producto encontrado!")
            print(f"- Nombre: {producto['nombre'].capitalize()}")
            print(f"- Precio: ${producto['precio']}")
            print(f"- Stock: {producto['stock']} kg")
            encontrado = True
            break
            
    if not encontrado:
        print("\nNo se encontró ningún producto con ese nombre en el inventario.")
def modificar_producto():
    """Modifica el precio o el stock de un producto existente"""
    if len(inventario) == 0:
        print("\nEl inventario está vacío. No hay productos para modificar.")
        return
        
    nombre_modificar = input("\nIngrese el nombre del producto que desea modificar: ").strip().lower()
    encontrado = False
    
    for producto in inventario:
        if producto["nombre"].lower() == nombre_modificar:
            encontrado = True
            print(f"\nProducto encontrado: {producto['nombre'].capitalize()}")
            print(f"Precio actual: ${producto['precio']} | Stock actual: {producto['stock']} kg")
            
            print("\n¿Qué desea modificar?")
            print("1. Precio")
            print("2. Stock")
            print("3. Ambos")
            opcion = input("Elija una opción (1-3): ").strip()
            
            if opcion == '1' or opcion == '3':
                try:
                    nuevo_precio = float(input("Ingrese el nuevo precio: "))
                    producto['precio'] = nuevo_precio
                except ValueError:
                    print("⚠️ Error: Debe ingresar un número válido.")
            
            if opcion == '2' or opcion == '3':
                try:
                    nuevo_stock = float(input("Ingrese el nuevo stock (kg): "))
                    producto['stock'] = nuevo_stock
                except ValueError:
                    print("⚠️ Error: Debe ingresar un número válido.")
                    
            print("\n¡Producto modificado con éxito!")
            break
            
    if not encontrado:
        print("\nNo se encontró ningún producto con ese nombre.")

def eliminar_producto():
    """Elimina un producto del inventario"""
    if len(inventario) == 0:
        print("\nEl inventario está vacío. No hay productos para eliminar.")
        return
        
    nombre_eliminar = input("\nIngrese el nombre del producto que desea eliminar: ").strip().lower()
    encontrado = False
    
    for i, producto in enumerate(inventario):
        if producto["nombre"].lower() == nombre_eliminar:
            encontrado = True
            confirmacion = input(f"¿Está seguro que desea eliminar '{producto['nombre'].capitalize()}'? (s/n): ").strip().lower()
            if confirmacion == 's':
                inventario.pop(i)
                print("\n¡Producto eliminado con éxito!")
            else:
                print("\nOperación cancelada.")
            break
            
    if not encontrado:
        print("\nNo se encontró ningún producto con ese nombre.")
def menu():
        """Menú principal interactivo de la verdulería"""
        while True:
            print("\n--- 🍎 MENÚ INVENTARIO VERDULERÍA 🥬 ---")
            print("1. Agregar producto")
            print("2. Mostrar inventario")
            print("3. Buscar producto")
            print("4. Modificar producto")
            print("5. Eliminar producto")
            print("6. Salir")
        
            opcion = input("\nElige una opción (1-6): ").strip()
        
            if opcion == '1':
                agregar_producto()
            elif opcion == '2':
                mostrar_inventario()
            elif opcion == '3':
                buscar_producto()
            elif opcion == '4':
             modificar_producto()
            elif opcion == '5':
             eliminar_producto()
            elif opcion == '6':
                print("\n¡Gracias por usar el sistema de la verdulería! ¡Hasta luego!")
                break
            else:
                print("\n⚠️ Opción no válida. Por favor, elegí un número entre 1 y 6.") 
menu()
