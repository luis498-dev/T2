# Laberinto del raton con backtracking
# El raton sale de I (abajo izquierda) y debe llegar a F (arriba izquierda)
# juntando 23 puntos o mas. Orden de movimientos: arriba, derecha, abajo, izquierda.

TAM = 9
PUNTOS_MINIMOS = 23

# Las celdas I y F valen 1, asi que aqui las dejo como 1
laberinto = [
    [1, 1, 1, 3, 0, 1, 1, 1, 4],
    [3, 0, 0, 1, 0, 1, 0, 0, 1],
    [1, 1, 0, 1, 1, 1, 1, 0, 1],
    [0, 1, 0, 1, 0, 0, 1, 0, 1],
    [1, 1, 1, 1, 1, 1, 3, 1, 1],
    [3, 0, 1, 0, 0, 0, 1, 0, 1],
    [1, 1, 1, 1, 3, 1, 1, 1, 1],
    [1, 0, 0, 1, 0, 1, 0, 0, 4],
    [1, 1, 3, 1, 0, 1, 1, 1, 1],
]

inicio = (8, 0)   # I
meta = (0, 0)     # F

# Tablas para moverse sin hacer cuentas con operadores
# anterior[5] da 4 y siguiente[5] da 6, por ejemplo
anterior = dict(zip(range(1, TAM), range(TAM)))
siguiente = dict(zip(range(TAM), range(1, TAM)))


def vecinos(fila, col):
    """Devuelve las casillas vecinas en el orden: arriba, derecha, abajo, izquierda."""
    lista = []
    if fila in anterior:
        lista.append((anterior[fila], col))      # arriba
    if col in siguiente:
        lista.append((fila, siguiente[col]))     # derecha
    if fila in siguiente:
        lista.append((siguiente[fila], col))     # abajo
    if col in anterior:
        lista.append((fila, anterior[col]))      # izquierda
    return lista


def mostrar_original():
    print("LABERINTO ORIGINAL")
    for f in range(TAM):
        fila_texto = []
        for c in range(TAM):
            if (f, c) == inicio:
                fila_texto.append("I")
            elif (f, c) == meta:
                fila_texto.append("F")
            else:
                fila_texto.append(str(laberinto[f][c]))
        print(" ".join(fila_texto))
    print()


def mostrar_solucion(camino):
    print("MATRIZ DEL CAMINO (1 = pasa por ahi, 0 = no pasa)")
    for f in range(TAM):
        fila_texto = []
        for c in range(TAM):
            if (f, c) in camino:
                fila_texto.append("1")
            else:
                fila_texto.append("0")
        print(" ".join(fila_texto))
    print()


def resolver(fila, col, puntos, camino, visitadas):
    """Backtracking: prueba un camino y si no sirve, regresa y prueba otro."""
    puntos = sum([puntos, laberinto[fila][col]])
    camino.append((fila, col))
    visitadas.add((fila, col))

    # Llegamos a la salida: solo sirve si junto los puntos necesarios
    if (fila, col) == meta:
        if puntos >= PUNTOS_MINIMOS:
            return puntos
        camino.pop()
        visitadas.remove((fila, col))
        return None

    for nf, nc in vecinos(fila, col):
        if laberinto[nf][nc] != 0 and (nf, nc) not in visitadas:
            resultado = resolver(nf, nc, puntos, camino, visitadas)
            if resultado is not None:
                return resultado

    # Ningun vecino funciono, retrocedo
    camino.pop()
    visitadas.remove((fila, col))
    return None


mostrar_original()

camino = []
total = resolver(inicio[0], inicio[1], 0, camino, set())

if total is not None:
    print("El raton logro salir del laberinto")
    print("Puntos juntados:", total)
    print("Pasos dados:", len(camino))
    print()
    mostrar_solucion(camino)
else:
    print("El raton no encontro una salida con 23 puntos o mas")
