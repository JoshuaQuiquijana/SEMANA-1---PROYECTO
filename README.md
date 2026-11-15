# SIMTELE-RISK

**Sistema de simulación y análisis de riesgos · Proyecto integrador de Métodos Numéricos**

Aplicación web educativa que estudia cuatro casos hipotéticos inspirados en un sistema de transporte por cable (tipo Mi Teleférico, La Paz, Bolivia), aplicando métodos numéricos con teoría de errores transversal.

> ⚠️ **Aviso:** los escenarios, datos y parámetros son **sintéticos e hipotéticos**, con fines estrictamente educativos. No describen fallas verificadas de Mi Teleférico ni se conectan a equipos de control reales.

## Estado del proyecto

| Semana | Alcance | Estado |
|---|---|---|
| 1 | Modelos de los 4 casos, prototipo web, teoría de errores y sistemas lineales, DER inicial | ✅ Entregable |
| 2 | Interpolación, raíces, integración, EDO, escenarios en los 4 módulos, base de datos | ⬜ Pendiente |
| 3 | Validación, conclusiones, video y defensa | ⬜ Pendiente |

### Implementado hasta ahora

- Navegación entre los cuatro módulos y el historial.
- Cada módulo muestra su modelo, fórmulas, métodos previstos y los tres escenarios.
- **Laboratorio de sistemas lineales** (módulo Deterioro mecánico), con cálculo real:
  - Métodos: Jacobi, Gauss-Seidel, LU con pivoteo parcial, gradiente conjugado y solución directa de referencia por Cholesky.
  - Se fija la solución exacta x\* = (1, 2, …, n) y se calcula b = A x\*, de modo que el error real es medible.
  - Tolerancia (residuo relativo) e iteraciones máximas editables, con validación.
  - Salidas: tabla de iteraciones, convergencia, residuo ‖r‖₂, error absoluto, error relativo y error porcentual.
  - Número de condición κ∞(A) y sensibilidad ante una perturbación relativa del 0,1 % en b.
  - Gráfico del residuo por iteración en escala logarítmica.
  - Conclusión numérica y conclusión del problema, separadas.
- **Historial** de experimentos: guardar, abrir, relanzar y eliminar. Se almacena en `localStorage` del navegador.

### Pendiente

- Cálculo en los módulos Detención, Oscilaciones y Sensores.
- Interpolación, raíces, integración y EDO.
- Base de datos real (DER, modelo relacional y script SQL) y prueba de recuperación tras reiniciar.
- Panel general de comparación y gráficos de error por módulo.

## Módulos (casos de estudio)

| Módulo | Pregunta | Modelo de referencia |
|---|---|---|
| Detención de emergencia | ¿Cómo varían tiempo y distancia de detención con velocidad, reacción y frenado? | v(t) = v₀ − at; x(t) = x₀ + v₀t − (a/2)t²; t_det = v₀/a; d = v₀²/(2a) |
| Deterioro mecánico | ¿Cuándo alcanza el deterioro un umbral de inspección? | D(t) = D₀ + αt + βt²; D(t) − D_umbral = 0 |
| Oscilaciones por viento | ¿Cómo cambia la oscilación con fuerza externa y amortiguamiento? | x′ = v; v′ = [F(t) − cv − kx]/m |
| Reconstrucción de sensores | ¿Cómo reconstruir datos faltantes y medir el efecto del ruido? | y(t) = sin(t), y(t) = e⁻ᵗ |

## Escenarios del laboratorio de sistemas lineales

| Escenario | Matriz | Propósito |
|---|---|---|
| Normal | Tridiagonal 4×4 (diagonal 4, vecinos −1), SPD y diagonalmente dominante | Caso base con convergencia rápida |
| Estrés | Tridiagonal 10×10 (diagonal 2,2), con perturbación del 0,1 % en b | Más datos y convergencia lenta |
| Mal condicionado | Matriz de Hilbert 5×5 (SPD, κ alto) | Mostrar que un residuo pequeño no garantiza un error pequeño, y distinguir mal condicionamiento de falta de convergencia |

## Métodos numéricos del sistema completo

- **Errores (transversal):** absoluto, relativo, porcentual, residual y sensibilidad.
- **Sistemas lineales:** Jacobi, Gauss-Seidel, LU, gradiente conjugado y referencia directa.
- **Interpolación:** Lagrange, Newton (diferencias divididas) y splines cúbicos.
- **Raíces:** bisección, Newton-Raphson y secante.
- **Integración:** trapecio compuesto, Simpson 1/3 compuesto y Romberg.
- **EDO:** Runge-Kutta de 2.º y 4.º orden.

## Estructura del repositorio

```
SIMTELE-RISK/
├── simtele-risk.html   # Aplicación web (HTML, CSS y JavaScript en un solo archivo)
├── README.md
└── docs/
    ├── Desafio_Integrador.pdf
    ├── Entrega_Semana_1.docx
    └── DER/            # Diagrama entidad-relación
```

> Ajusta esta estructura a los archivos que realmente tengas en el repositorio.

## Cómo ejecutar

No requiere instalación ni dependencias.

1. Clona el repositorio:
   ```bash
   git clone https://github.com/<usuario>/SIMTELE-RISK.git
   cd SIMTELE-RISK
   ```
2. Abre `simtele-risk.html` en el navegador, o sírvelo localmente:
   ```bash
   python -m http.server 8000
   ```
   y entra a `http://localhost:8000/simtele-risk.html`.

### Prueba rápida

1. Entra al módulo **Deterioro**.
2. Elige un escenario (Normal, Estrés o Mal condicionado) y pulsa **Ejecutar**.
3. Revisa la tabla de errores, el gráfico de convergencia y las dos conclusiones.
4. Pulsa **Guardar experimento**, recarga la página y recupéralo desde **Historial** con **Relanzar**.

## Modelo de datos (resumen)

Entidades mínimas: `caso_estudio`, `escenario`, `simulacion`, `ejecucion_metodo`, `iteracion_resultado`, `resultado_resumen`. El DER, el modelo relacional y el script SQL se agregarán en `docs/DER/` y `db/`.

## Limitaciones actuales

- El historial usa `localStorage` y es local a cada navegador; no sustituye la base de datos exigida.
- Solo el módulo Deterioro tiene cálculo activo.

## Equipo

| Integrante | Mención | Aporte |
|---|---|---|
| _Nombre_ | _Mención_ | _Descripción_ |

## Referencias

- Consigna oficial: *Desafío Integrador SIMTELE-RISK, Métodos Numéricos* (3 semanas, 25 puntos).

## Licencia

Uso académico y educativo.
