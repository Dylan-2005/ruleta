import random  # Importamos el módulo random para generar números aleatorios

# Definimos los números de la ruleta y sus colores en un diccionario
ruleta = {
    0: 'verde',  # El número 0 es de color verde
    32: 'rojo', 15: 'rojo', 19: 'rojo', 4: 'rojo', 21: 'rojo', 2: 'rojo', 25: 'rojo',
    17: 'rojo', 34: 'rojo', 6: 'rojo', 27: 'rojo', 13: 'rojo', 36: 'rojo', 11: 'rojo',
    30: 'rojo', 8: 'rojo', 23: 'rojo', 10: 'rojo', 5: 'rojo', 24: 'rojo', 16: 'rojo',
    33: 'rojo', 1: 'negro', 20: 'negro', 14: 'negro', 31: 'negro', 9: 'negro', 22: 'negro',
    18: 'negro', 29: 'negro', 7: 'negro', 28: 'negro', 12: 'negro', 35: 'negro', 3: 'negro'
}

def girar_ruleta():
    """Simula el giro de la ruleta y devuelve el número y color resultante."""
    # Elegimos un número aleatorio de la ruleta
    numero_ganador = random.choice(list(ruleta.keys()))
    # Obtenemos el color correspondiente al número ganador
    color_ganador = ruleta[numero_ganador]
    return numero_ganador, color_ganador  # Devolvemos el número y el color ganador

def realizar_apuesta():
    """Permite al usuario realizar una apuesta."""
    print("Bienvenido a la ruleta!")  # Mensaje de bienvenida

    # Preguntamos al usuario si desea realizar una apuesta
    continuar = input("¿Deseas realizar una apuesta? (si/no): ").strip().lower()
    if continuar != 'si':  # Si la respuesta no es 'si'
        print("Gracias por jugar. ¡Hasta luego!")  # Mensaje de despedida
        return None, None  # Retornamos None para indicar que no se desea continuar

    # Pedimos al usuario que elija un número para apostar
    apuesta = input("¿En qué número (0-36) deseas apostar? ")

    # Validamos que la entrada sea un número válido
    while not apuesta.isdigit() or int(apuesta) not in ruleta:
        apuesta = input("Entrada inválida. Por favor, elige un número entre 0 y 36: ")

    apuesta = int(apuesta)  # Convertimos la apuesta a un entero
    cantidad = input("¿Cuánto deseas apostar? ")  # Pedimos la cantidad a apostar

    # Validamos que la cantidad apostada sea un número positivo
    while not cantidad.isdigit() or int(cantidad) <= 0:
        cantidad = input("Entrada inválida. Por favor, ingresa una cantidad válida: ")

    cantidad = int(cantidad)  # Convertimos la cantidad a un entero
    return apuesta, cantidad  # Devolvemos la apuesta y la cantidad

def main():
    while True:  # Bucle principal del juego
        apuesta, cantidad = realizar_apuesta()  # Llamamos a la función para realizar una apuesta
        if apuesta is None and cantidad is None:  # Si el usuario no desea continuar
            break  # Salimos del bucle

        numero_ganador, color_ganador = girar_ruleta()  # Giramos la ruleta

        # Mostramos el resultado del giro
        print(f"La ruleta ha girado y el número ganador es {numero_ganador} ({color_ganador}).")

        # Comprobamos si el usuario ha ganado
        if apuesta == numero_ganador:
            print(f"¡Felicidades! Has ganado {cantidad * 35} unidades.")  # Mensaje de victoria
        else:
            print("Lo siento, has perdido tu apuesta.")  # Mensaje de derrota

        # Preguntamos al usuario si quiere jugar de nuevo
        continuar = input("¿Quieres jugar de nuevo? (s/n): ")
        if continuar.lower() != 's':  # Si la respuesta no es 's'
            break  # Salimos del bucle

if __name__ == "__main__":
    main()  # Iniciamos el juego llamando a la función principal
