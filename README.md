# 3Evaluacion-Leonardo-gonzalez_PGY1121_SECCION_JORNADA-VESPERTINA
machine





import datetime


num_pisos = 10
departamentos_por_piso = 4
departamentos_disponibles = [['A' + str(p) for p in range(1, departamentos_por_piso + 1)] for _ in range(num_pisos)]
departamentos_vendidos = [['' for _ in range(departamentos_por_piso)] for _ in range(num_pisos)]
precios = {'A': 3800, 'B': 3000, 'C': 2800, 'D': 3500}
compradores = {}

def mostrar_menu():
    print("1. Comprar departamento")
    print("2. Mostrar departamentos disponibles")
    print("3. Ver listado de compradores")
    print("4. Mostrar ganancias totales")
    print("5. Salir")

def comprar_departamento():
    mostrar_departamentos()
    try:
        piso = int(input("Ingrese el número del piso: "))
        tipo = input("Ingrese el tipo de departamento (A, B, C o D): ").upper()
        run = input("Ingrese el RUN del comprador (sin guiones ni puntos): ")

        if piso < 1 or piso > num_pisos or tipo not in precios:
            print("Opción inválida. Intente nuevamente.")
            return

        if departamentos_vendidos[piso - 1][ord(tipo) - ord('A')] == 'X':
            print("Departamento no disponible. Seleccione otro.")
        else:
            compradores[run] = (tipo, piso)
            departamentos_vendidos[piso - 1][ord(tipo) - ord('A')] = 'X'
            print("Operación realizada correctamente.")
    except ValueError:
        print("Error: Ingrese un valor numérico para el piso.")

def mostrar_departamentos():
    for i in range(num_pisos):
        print(f"Piso {i + 1}:", end=' ')
        for j in range(departamentos_por_piso):
            if departamentos_vendidos[i][j] == 'X':
                print(f"{departamentos_disponibles[i][j]} (Vendido)  ", end=' ')
            else:
                print(f"{departamentos_disponibles[i][j]} (Disponible)", end=' ')
        print()

def ver_listado_compradores():
    for run, (tipo, piso) in sorted(compradores.items()):
        print(f"RUN: {run}, Tipo: {tipo}, Piso: {piso}")

def mostrar_ganancias_totales():
    total_por_tipo = {tipo: 0 for tipo in precios}
    total_general = 0

    for run, (tipo, _) in compradores.items():
        total_por_tipo[tipo] += precios[tipo]
        total_general += precios[tipo]

    print("Tipo de Departamento  Precio Unitario  Cantidad  Total")
    for tipo in precios:
        cantidad = total_por_tipo[tipo] // precios[tipo]
        total_tipo = cantidad * precios[tipo]
        print(f"{tipo} {precios[tipo]} UF {cantidad} {total_tipo} UF")

    print(f"TOTAL {len(compradores)} {total_general} UF")


while True:
    mostrar_menu()
    opcion = input("Ingrese la opción deseada (1-5): ")

    if opcion == '1':
        comprar_departamento()
    elif opcion == '2':
        mostrar_departamentos()
    elif opcion == '3':
        ver_listado_compradores()
    elif opcion == '4':
        mostrar_ganancias_totales()
    elif opcion == '5':
        print("Saliendo del sistema. Gracias.")
        print("Nombre: [Tu Nombre]")
        print("Apellido: [Tu Apellido]")
        print("Fecha: " + datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S"))
        break
    else:
        print("Opción inválida. Intente nuevamente.")
