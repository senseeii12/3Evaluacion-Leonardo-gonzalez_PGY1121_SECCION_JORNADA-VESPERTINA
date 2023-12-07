# 3Evaluacion-Leonardo-gonzalez_PGY1121_SECCION_JORNADA-VESPERTINA
machine


import datetime


    class CasaFeliz:
    
    def __init__(self):
        self.departamentos_disponibles = [['A'] * 4, ['B'] * 4, ['C'] * 4, ['D'] * 4]
        self.departamentos_vendidos = [[''] * 4 for _ in range(4)]
        self.compradores = {}
        self.precios = {'A': 3800, 'B': 3000, 'C': 2800, 'D': 3500}
        self.menu_principal()

    def menu_principal(self):
        while True:
            print("""\nMenú Principal
            1. comprar departamento
            2. Mostrar departamentos disponibles
            3. Ver listado de compradores
            4. Mostrar ganancias totales
            5. Salir""")
            opcion = input("Ingrese el número de la opción deseada: ")

            if opcion == '1':
                self.comprar_departamento()
            elif opcion == '2':
                self.mostrar_departamentos_disponibles()
            elif opcion == '3':
                self.ver_listado_compradores()
            elif opcion == '4':
                self.mostrar_ganancias_totales()
            elif opcion == '5':
                self.salir()
                break
            else:
                print("Opción no válida. Intente de nuevo.")

    def comprar_departamento(self):
        piso = int(input("Ingrese el número del piso (1-10): "))
        tipo = input("Ingrese el tipo de departamento (A, B, C, D): ").upper()

        if piso < 1 or piso > 10 or tipo not in ['A', 'B', 'C', 'D']:
            print("Datos ingresados no válidos. Intente de nuevo.")
            return

        if (self).departamentos_vendidos[piso - 1][ord(tipo) - ord('A')] == 'X':
            print("Departamento no disponible. Seleccione otro.")
            return

        run_comprador = input("Ingrese el RUN del comprador (sin guiones ni puntos): ")
        if not run_comprador.isdigit():
            print("RUN no válido. Intente de nuevo.")
            return

        self.departamentos_vendidos[piso - 1][ord(tipo) - ord('A')] = 'X'
        self.compradores[(piso, tipo)] = run_comprador

        print("Operación realizada correctamente.")

    def mostrar_departamentos_disponibles(self):
        print("\nEstado actual de la venta de departamentos:")
        for i, piso in enumerate(self.departamentos_disponibles, start=1):
            print(f"Piso {i}:", end=" ")
            for j, tipo in enumerate(piso, start=65):  # ASCII de 'A'
                if self.departamentos_vendidos[i - 1][j - 65] == 'X':
                    print(f"{chr(j)}X", end=" ")
                else:
                    print(chr(j), end=" ")
            print()

    def ver_listado_compradores(self):
        print("\nListado de compradores:")
        for key in sorted(self.compradores.keys(), key=lambda x: (x[0], x[1])):
            print(f"Piso {key[0]}, Tipo {key[1]}: {self.compradores[key]}")

    def mostrar_ganancias_totales(self):
        print("\nVentas totales:")
        total_ventas = 0
        for tipo in self.precios:
            cantidad_vendidos = sum(row.count('X') for row in self.departamentos_vendidos)
            total_tipo = cantidad_vendidos * self.precios[tipo]
            total_ventas += total_tipo
            print(f"Tipo {tipo} {self.precios[tipo]} UF {cantidad_vendidos} {total_tipo} UF")
        print(f"TOTAL {sum(map(lambda x: x.count('X'), self.departamentos_vendidos))} {total_ventas} UF")

    def salir(self):
        fecha_actual = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        print(f"\nSaliendo del sistema. Nombre: [Tu Nombre], Apellido: [Tu Apellido], Fecha: {fecha_actual}")

CasaFeliz()
