import random  # Importamos el módulo random para generar números aleatorios

# Definimos los números de la ruleta y sus colores en un diccionario
ruleta = {
    0: 'verde', 32: 'rojo', 15: 'rojo', 19: 'rojo', 4: 'rojo', 21: 'rojo', 2: 'rojo', 25: 'rojo',
    17: 'rojo', 34: 'rojo', 6: 'rojo', 27: 'rojo', 13: 'rojo', 36: 'rojo', 11: 'rojo',
    30: 'rojo', 8: 'rojo', 23: 'rojo', 10: 'rojo', 5: 'rojo', 24: 'rojo', 16: 'rojo',
    33: 'rojo', 1: 'negro', 20: 'negro', 14: 'negro', 31: 'negro', 9: 'negro', 22: 'negro',
    18: 'negro', 29: 'negro', 7: 'negro', 28: 'negro', 12: 'negro', 35: 'negro', 3: 'negro'
}

# Inicializamos variables para el juego
saldo = 100  # El jugador comienza con 100 coins
total_apostado = 0  # Total de coins apostados
total_ganado = 0  # Total de coins ganados
ganadas = 0  # Contador de apuestas ganadas
perdidas = 0  # Contador de apuestas perdidas

def girar_ruleta():
    """Simula el giro de la ruleta y devuelve el número y color resultante."""
    numero_ganador = random.choice(list(ruleta.keys()))  # Selecciona un número aleatorio de la ruleta
    color_ganador = ruleta[numero_ganador]  # Obtiene el color correspondiente al número ganador
    return numero_ganador, color_ganador  # Devuelve el número y el color ganador

def mostrar_saldo():
    """Muestra el saldo actual del jugador."""
    print(f"Saldo actual: {saldo} coins")  # Imprime el saldo actual

def realizar_apuesta():
    """Permite al jugador realizar una apuesta en la ruleta."""
    global saldo, total_apostado, total_ganado, ganadas, perdidas  # Usamos variables globales para el saldo y estadísticas

    mostrar_saldo()  # Muestra el saldo actual del jugador

    # Solicitar al jugador que seleccione un número para apostar
    apuesta_numero = int(input("Seleccione un número (0-36): "))
    while apuesta_numero < 0 or apuesta_numero > 36:  # Validar que el número esté en el rango correcto
        apuesta_numero = int(input("Entrada inválida. Por favor, elige un número entre 0 y 36: "))

    # Solicitar la cantidad de coins que el jugador desea apostar
    cantidad = int(input("¿Cuántos coins quiere apostar?: "))
    while cantidad <= 0 or cantidad > saldo:  # Validar que la cantidad sea positiva y no exceda el saldo
        cantidad = int(input("Entrada inválida. Por favor, ingresa una cantidad válida: "))

    # Solicitar al jugador que elija un color para apostar
    color = input("¿A qué color quiere apostar? (N/R): ").upper()  # N para negro, R para rojo
    while color not in ['N', 'R']:  # Validar que la entrada sea correcta
        color = input("Entrada inválida. Por favor, elige un color válido (N/R): ").upper()

    # Actualizar el saldo y el total apostado
    saldo -= cantidad  # Restar la cantidad apostada del saldo
    total_apostado += cantidad  # Sumar la cantidad apostada al total apostado

    # Girar la ruleta y obtener el número y color ganadores
    numero_ganador, color_ganador = girar_ruleta()
    print(f"La ruleta ha girado y el número ganador es {numero_ganador} (Color: {color_ganador}).")

    # Comprobar si el jugador ha ganado
    if apuesta_numero == numero_ganador:  # Si el número apostado coincide con el número ganador
        ganancia = cantidad * 20  # Calcular la ganancia por acertar el número
        saldo += ganancia  # Sumar la ganancia al saldo
        total_ganado += ganancia  # Sumar la ganancia al total ganado
        ganadas += 1  # Incrementar el contador de apuestas ganadas
        print(f"¡Felicidades! Has ganado {ganancia} coins por acertar el número.")
    elif (color == 'R' and color_ganador == 'rojo') or (color == 'N' and color_ganador == 'negro'):
        ganancia = cantidad * 2  # Calcular la ganancia por acertar el color
        saldo += ganancia  # Sumar la ganancia al saldo
        total_ganado += ganancia  # Sumar la ganancia al total ganado
        ganadas += 1  # Incrementar el contador de apuestas ganadas
        print(f"¡Felicidades! Has ganado {ganancia} coins por acertar el color.")
    else:
        perdidas += 1  # Incrementar el contador de apuestas perdidas
        print("Lo siento, has perdido tu apuesta.")  # Mensaje de pérdida

def mostrar_estadisticas():
    """Muestra las estadísticas del jugador."""
    if ganadas + perdidas > 0:  # Comprobar si hay apuestas ganadas o perdidas
        promedio_exito = ganadas / (ganadas + perdidas) * 100  # Calcular el porcentaje de éxito
    else:
        promedio_exito = 0  # Si no hay apuestas, el promedio de éxito es 0
    # Imprimir estadísticas del jugador
    print(f"Total apostado: {total_apostado} coins")
    print(f"Total ganado: {total_ganado} coins")
    print(f"Promedio de éxito: {promedio_exito:.2f}%")  # Mostrar el promedio de éxito con dos decimales

def main():
    """Función principal que controla el flujo del juego."""
    while True:  # Bucle infinito para permitir múltiples rondas de juego
        realizar_apuesta()  # Llamar a la función para realizar una apuesta
        mostrar_estadisticas()  # Mostrar estadísticas después de cada ronda
        continuar = input("¿Quieres jugar de nuevo? (s/n): ").strip().lower()  # Preguntar al jugador si quiere continuar
        if continuar != 's':  # Si la respuesta no es 's', salir del bucle
            break

if __name__ == "__main__":
    main()  # Ejecutar la función principal al iniciar el programa
