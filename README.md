class Nodo:
    def __init__(self, dato):
        self.dato = dato
        self.siguiente = None
        self.anterior = None

class ListaDoble:
    def __init__(self):
        self.cabeza = None
        self.cola = None

    # 1. Insertar al inicio
    def insertar_inicio(self, dato):
        nuevo = Nodo(dato)
        if self.cabeza is None:
            self.cabeza = self.cola = nuevo
        else:
            nuevo.siguiente = self.cabeza
            self.cabeza.anterior = nuevo
            self.cabeza = nuevo

    # 2. Eliminar nodo por valor
    def eliminar(self, valor):
        actual = self.cabeza
        while actual:
            if actual.dato == valor:
                if actual == self.cabeza:
                    self.cabeza = actual.siguiente
                    if self.cabeza:
                        self.cabeza.anterior = None
                elif actual == self.cola:
                    self.cola = actual.anterior
                    if self.cola:
                        self.cola.siguiente = None
                else:
                    actual.anterior.siguiente = actual.siguiente
                    actual.siguiente.anterior = actual.anterior
                return
            actual = actual.siguiente

    # 3. Mostrar inverso
    def mostrar_inverso(self):
        actual = self.cola
        while actual:
            print(actual.dato, end=" ")
            actual = actual.anterior
        print()

    # 4. Insertar en una posición
    def insertar_posicion(self, dato, pos):
        if pos == 0:
            self.insertar_inicio(dato)
            return
        nuevo = Nodo(dato)
        actual = self.cabeza
        i = 0
        while actual and i < pos:
            actual = actual.siguiente
            i += 1
        if actual:
            nuevo.siguiente = actual
            nuevo.anterior = actual.anterior
            if actual.anterior:
                actual.anterior.siguiente = nuevo
            actual.anterior = nuevo

    # 5. Modificar posición
    def modificar_posicion(self, pos, nuevo_dato):
        actual = self.cabeza
        i = 0
        while actual and i < pos:
            actual = actual.siguiente
            i += 1
        if actual:
            actual.dato = nuevo_dato

    # 6. Ordenar de mayor a menor
    def ordenar_descendente(self):
        actual = self.cabeza
        while actual:
            siguiente = actual.siguiente
            while siguiente:
                if actual.dato < siguiente.dato:
                    actual.dato, siguiente.dato = siguiente.dato, actual.dato
                siguiente = siguiente.siguiente
            actual = actual.siguiente

    # 7. Ordenar de menor a mayor
    def ordenar_ascendente(self):
        actual = self.cabeza
        while actual:
            siguiente = actual.siguiente
            while siguiente:
                if actual.dato > siguiente.dato:
                    actual.dato, siguiente.dato = siguiente.dato, actual.dato
                siguiente = siguiente.siguiente
            actual = actual.siguiente

    # 8. Suma de todos los nodos
    def suma_nodos(self):
        suma = 0
        actual = self.cabeza
        while actual:
            suma += actual.dato
            actual = actual.siguiente
        return suma

    # 9. Insertar al final
    def insertar_final(self, dato):
        nuevo = Nodo(dato)
        if self.cola is None:
            self.cabeza = self.cola = nuevo
        else:
            self.cola.siguiente = nuevo
            nuevo.anterior = self.cola
            self.cola = nuevo

    # 10. Mostrar normal
    def mostrar_normal(self):
        actual = self.cabeza
        while actual:
            print(actual.dato, end=" ")
            actual = actual.siguiente
        print()

    # 11. Insertar después de un elemento buscado
    def insertar_despues_de(self, valor_buscado, dato):
        actual = self.cabeza
        while actual:
            if actual.dato == valor_buscado:
                nuevo = Nodo(dato)
                nuevo.siguiente = actual.siguiente
                nuevo.anterior = actual
                if actual.siguiente:
                    actual.siguiente.anterior = nuevo
                actual.siguiente = nuevo
                if actual == self.cola:
                    self.cola = nuevo
                return
            actual = actual.siguiente


# ------------------ BLOQUE DE PRUEBAS ------------------

lista = ListaDoble()

# Insertar al final
lista.insertar_final(10)
lista.insertar_final(20)
lista.insertar_final(30)
print("Lista normal:")
lista.mostrar_normal()

# Insertar al inicio
lista.insertar_inicio(5)
print("Después de insertar al inicio:")
lista.mostrar_normal()

# Insertar en posición
lista.insertar_posicion(15, 2)
print("Después de insertar en posición 2:")
lista.mostrar_normal()

# Modificar posición
lista.modificar_posicion(1, 99)
print("Después de modificar posición 1:")
lista.mostrar_normal()

# Mostrar inverso
print("Lista inversa:")
lista.mostrar_inverso()

# Ordenar ascendente
lista.ordenar_ascendente()
print("Orden ascendente:")
lista.mostrar_normal()

# Ordenar descendente
lista.ordenar_descendente()
print("Orden descendente:")
lista.mostrar_normal()

# Suma de nodos
print("Suma de nodos:", lista.suma_nodos())

# Insertar después de un elemento
lista.insertar_despues_de(20, 77)
print("Después de insertar después de 20:")
lista.mostrar_normal()

# Eliminar nodo
lista.eliminar(99)
print("Después de eliminar 99:")
lista.mostrar_normal()
