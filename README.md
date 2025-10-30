# juego_facil
Juan David Rayo Tejada - 20231020023
Jonnatan Camargo Camacho - 20231020204
🎮 Space Invaders – Patrones de Diseño (Command & Chain of Responsibility)
📘 Descripción General

Este proyecto es una versión simplificada del clásico Space Invaders, desarrollada en Python con Pygame, que implementa dos patrones de diseño fundamentales:

🧩 Command Pattern – para manejar las acciones del jugador.

🔗 Chain of Responsibility Pattern – para gestionar los eventos de colisiones, puntuaciones y power-ups.

El objetivo principal es demostrar cómo aplicar patrones de diseño en un entorno de videojuego orientado a objetos.

🧠 Patrones de Diseño Implementados
🧩 1. Patrón Command

Propósito:
Encapsular cada acción del jugador (moverse, disparar) como un objeto comando independiente.

Ventajas:

Desacopla la lógica de entrada (teclado) de la ejecución real.

Facilita agregar o modificar acciones sin alterar el código del jugador.

Permite futuras extensiones como macros o deshacer acciones.

Ejemplo en el código:

self.commands = {
    pygame.K_LEFT: MoveLeftCommand(),
    pygame.K_RIGHT: MoveRightCommand(),
    pygame.K_SPACE: ShootCommand()
}


Cada tecla ejecuta un comando que contiene la acción correspondiente.

🔗 2. Patrón Chain of Responsibility

Propósito:
Permitir que múltiples objetos manejen un evento (en este caso, las colisiones) sin acoplar el emisor con un único receptor.

Ventajas:

Cada clase se encarga de una sola responsabilidad (colisión, puntuación, power-ups).

Permite extender fácilmente la cadena con nuevos comportamientos.

Mejora la organización y legibilidad del código.

Estructura de la cadena:

CollisionHandler → ScoreHandler → PowerUpHandler


Cada handler procesa una parte del evento y pasa el control al siguiente.

⚙️ Estructura del Código
SpaceInvaders/
│
├── main.py              # Archivo principal del juego
│
├── Command Pattern
│   ├── Command           # Clase abstracta base
│   ├── MoveLeftCommand   # Mueve el jugador a la izquierda
│   ├── MoveRightCommand  # Mueve el jugador a la derecha
│   └── ShootCommand      # Dispara una bala
│
├── Chain of Responsibility
│   ├── Handler           # Interfaz abstracta para la cadena
│   ├── CollisionHandler  # Detecta colisiones
│   ├── ScoreHandler      # Calcula puntuación
│   └── PowerUpHandler    # Gestiona power-ups
│
└── Entidades del juego
    ├── Player            # Controla al jugador
    ├── Enemy             # Controla enemigos
    ├── Bullet            # Controla las balas
    └── Game              # Clase principal que integra todo

🎮 Controles del Juego
Acción	Tecla
Mover izquierda	← (flecha izquierda)
Mover derecha	→ (flecha derecha)
Disparar	Espacio (SPACE)
Salir del juego	Cerrar ventana
🧾 Requisitos

Python 3.8+

Pygame (instalar con pip install pygame)

🚀 Cómo Ejecutarlo

Clona o descarga el proyecto:

git clone https://github.com/usuario/space-invaders-patterns.git
cd space-invaders-patterns


Instala dependencias:

pip install pygame


Ejecuta el juego:

python main.py

🧩 Lógica Principal del Juego

Inicialización:
Se crean el jugador, los enemigos y los grupos de sprites.

Bucle principal (run):

Se manejan los eventos de teclado mediante el patrón Command.

Se actualizan los sprites (jugador, enemigos, balas).

Se detectan colisiones entre balas y enemigos.

Se pasa la información de colisiones a la cadena de Handlers:

CollisionHandler → registra impactos.

ScoreHandler → aumenta la puntuación.

PowerUpHandler → activa mejoras si se cumplen condiciones.

Condiciones de victoria y derrota:

Si todos los enemigos son destruidos → “¡Ganaste!”

Si un enemigo llega al fondo → “Game Over”.

🧱 Ejemplo de Salida en Consola
=== SPACE INVADERS INICIADO ===
Patrones implementados:
1. COMMAND: Movimiento y disparos encapsulados en objetos
2. CHAIN OF RESPONSIBILITY: Manejo de colisiones en cadena
===============================

Comando ejecutado: Disparar
--- Inicio de procesamiento en cadena ---
CollisionHandler: Detectadas 2 colisiones
ScoreHandler: +20 puntos! Total: 50
PowerUpHandler: ¡Power-up desbloqueado! Disparo rápido activado
--- Fin de procesamiento en cadena ---

🧩 Posibles Extensiones

Agregar más comandos (pausar, cambiar arma, etc.).

Nuevos handlers (vidas extra, enemigos especiales, combos).

Implementar el patrón Observer para actualizar interfaz.

Incluir sonidos y efectos visuales.
