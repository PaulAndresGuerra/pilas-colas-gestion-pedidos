# Pilas y Colas — Gestión de Pedidos en Hora Pico

Unidad 2, Tema 2 de Estructuras de Datos. Sistema interno de asignación de pedidos de una aplicación de entrega de comida, donde dos estructuras conviven sobre el mismo tipo de nodo.

## El escenario

Durante el día los pedidos entran en una **cola FIFO**: el primero que pide es el primero al que se le cocina. En hora pico empiezan a llegar reclamos ("mi pedido llegó frío", "falta la bebida") que no pueden esperar al final de la fila, así que se apilan en una **pila LIFO** de atención prioritaria: el último reclamo en entrar es el primero que el supervisor resuelve.

Cuando la aplicación se satura, el gerente activa el modo de contingencia masiva: la cola se congela y todos sus pedidos pendientes se transfieren a la pila. Al trasladar los nodos uno a uno, el orden se invierte de forma natural y el sistema pasa a atender primero los pedidos ordinarios más recientes, que son los que todavía se pueden salvar.

## Implementación

Ambas estructuras se construyen sobre la misma clase `NodoPedido`, usando solo punteros:

| Método | Comportamiento |
| --- | --- |
| `registrar_pedido` | Un pedido `ESTANDAR` entra al final de la cola; uno de tipo `RECLAMO` entra al tope de la pila |
| `despachar_siguiente` | Siempre atiende primero la pila de reclamos; si está vacía, hace dequeue de la cola; si no hay nada, devuelve `None` |
| `activar_contingencia_masiva` | Desconecta todos los nodos de la cola y los apila uno a uno, invirtiendo el orden y dejando la cola vacía |

El notebook incluye además la reflexión sobre el caso del puntero fantasma: qué ocurre cuando se desencola sin actualizar correctamente el puntero de fin.

## Ejecución

Abrir `Guerra_Paul_Unidad2_Tema2.ipynb` y ejecutar las celdas en orden.

---

**Paúl Andrés Guerra Vicuña** · Estructuras de Datos · Ingeniería en Ciencias de Datos e Inteligencia Artificial · Universidad Nacional de Chimborazo (UNACH)
