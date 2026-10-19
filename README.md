# Métodos Numéricos: Jacobi y Gauss-Seidel en Java ^v^

Práctica de Métodos Numéricos (Instituto Tecnológico Superior de Xalapa) que resuelve un sistema de ecuaciones lineales con los métodos iterativos de **Jacobi** y **Gauss-Seidel**, usando una arquitectura modular de tres componentes y comparando cuántas iteraciones necesita cada método.

## ¿Qué son estos métodos?

Son **métodos iterativos** para resolver sistemas de ecuaciones lineales de la forma `Ax = b`. En lugar de despejar todo de una sola vez, parten de una aproximación inicial y la van mejorando en cada vuelta (iteración) hasta que el cambio entre una iteración y la siguiente es menor que una tolerancia establecida.

**Método de Jacobi.** En cada iteración calcula todas las incógnitas usando únicamente los valores de la iteración anterior. Los resultados nuevos se guardan en un vector auxiliar y solo se usan hasta que termina la vuelta completa.

```
x_i(k+1) = ( b_i - suma(a_ij * x_j(k)) ) / a_ii        con j distinto de i
```

**Método de Gauss-Seidel.** Funciona parecido, pero cada valor recién calculado se usa de inmediato en las ecuaciones siguientes de la misma iteración. Por eso suele converger en menos iteraciones.

```
x_i(k+1) = ( b_i - suma(a_ij * x_j(k+1)) - suma(a_ij * x_j(k)) ) / a_ii
            (primera suma: j < i, segunda suma: j > i)
```

Ambos métodos tienen garantizada la convergencia cuando la matriz es estrictamente diagonal dominante, como la de este sistema.

## Sistema que se resuelve

```
5x +  y +  z = 7
 x + 4y +  z = 6
 x + 2y + 5z = 8
```

- Aproximación inicial: X(0) = [0, 0, 0]
- Tolerancia: ε = 0.0001
- Criterio de paro: mayor diferencia absoluta entre dos iteraciones consecutivas menor que ε

## Estructura del proyecto

```
Unidad03y04/
└── MetodosIterativos/
    ├── DefMatriz.java          (Módulo 1: definición del sistema)
    ├── MetodosIterativos.java  (Módulo 2: métodos iterativos)
    └── Main.java               (Módulo 3: ejecución)
```

| Módulo | Clase | Qué hace |
|---|---|---|
| 1 | `DefMatriz` | Guarda la matriz A, el vector b, la aproximación inicial y la tolerancia |
| 2 | `MetodosIterativos` | Contiene Jacobi (con vector auxiliar) y Gauss-Seidel (con actualización inmediata) |
| 3 | `Main` | Ejecuta ambos métodos y compara el número de iteraciones |

## Qué se utiliza

- **Lenguaje:** Java (probado con JDK 21 y JDK 26).
- **Arquitectura:** modular, con las responsabilidades separadas en tres clases (datos, cálculo y ejecución).
- **Herramientas:** JDK de Java para compilar y ejecutar; IntelliJ IDEA (opcional) como editor; Git y GitHub para el control de versiones.
- **Sin librerías externas:** solo se usa la biblioteca estándar de Java.

## Cómo compilar y ejecutar

1. Verifica que tengas el JDK instalado:

```
javac -version
java -version
```

2. Clona el repositorio y entra a la carpeta:

```
git clone https://github.com/Lalis-707/Metodos-Numericos-Iterativos.git
cd Metodos-Numericos-Iterativos
```

3. Compila y ejecuta desde la raíz del repositorio:

```
javac -d out Unidad03y04/MetodosIterativos/*.java
java -cp out Ecuaciones_Lineales.Unidad03y04.MetodosIterativos.Main
```

También se puede abrir el proyecto en IntelliJ IDEA y correr la clase `Main`.

## Resultados

| Método | Iteraciones | Solución aproximada |
|---|---|---|
| Jacobi | 16 | x ≈ 0.999987, y ≈ 0.999985, z ≈ 0.999983 |
| Gauss-Seidel | 6 | x ≈ 0.999994, y ≈ 1.000000, z ≈ 1.000001 |

Con la misma tolerancia, Gauss-Seidel converge en menos de la mitad de iteraciones que Jacobi.
