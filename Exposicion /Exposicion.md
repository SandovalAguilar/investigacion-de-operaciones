---
marp: true
theme: default
class: invert
paginate: true
---

# Programación No Lineal y Dinámica

![bg right:40% 80%](fcfm.png)

### 031 E2024 Investigación de Operaciones

Dr. Luis Ángel Gutiérrez Rodríguez

Ismael Sandoval Aguilar

25 de Febrero de 2024

---

## Programación No Lineal: Situación Problema

Para ayudar a los propietarios de restaurantes a reabrir sus negocios durante la pandemia de COVID-19, el gobierno creó un índice de riesgo de capacidad generalizado (CRI), para ayudar a comprender cuán riesgoso es abrir sus áreas de asientos interiores y exteriores.

$$CRI = 4x^2_1 - 4x^4_1 + 4x^{6/3}_1 + x_1 x_2 - 4x^2_2 + 4x^4_2$$

---

## Programación No Lineal: Situación Problema

Mary, una propietaria de restaurante local, quiere reabrir su restaurante con el menor riesgo posible. Sin embargo, comprende que para ofrecer a su personal horas de trabajo valiosas, tendrá que abrir al menos el 10% de su capacidad de asientos interiores y el 25% de su capacidad de asientos exteriores.

¿Cuál es la forma más segura (según el CRI) para que Mary reabra su negocio?

---

### Modelación del Problema

Función objetivo:

$$\text{Min} \hspace{2mm} Z = 4x^2_1 - 4x^4_1 + 4x^{6/3}_1 + x_1 x_2 - 4x^2_2 + 4x^4_2$$

Sujeto a las restricciones:

- $x_1 \geq 0.1$
- $x_2 = 0.25$
- $x_1, x_2 \leq 1$

---

### Modelación Computacional

---

## Descripción del Problema

Se busca minimizar la cantidad total de monedas de denominaciones dadas para alcanzar una suma de dinero específica. Este problema es un clásico de la programación entera que tiene aplicaciones en sistemas de pago, cajeros automáticos, y optimización financiera.

---

## Datos del Problema

- Denominaciones de monedas disponibles: 1, 2, 5
- Suma objetivo: 11

---

## Modelación del Problema

```python
from pyomo.environ import ConcreteModel, Var, Objective, Constraint, SolverFactory, NonNegativeIntegers, minimize

# Crear un modelo de Pyomo
model = ConcreteModel()

# Variables de decisión: cantidad de cada moneda
model.num_coins = Var([1, 2, 5], within=NonNegativeIntegers)

# Función objetivo: Minimizar el total de monedas usadas
model.total_coins = Objective(expr=sum(model.num_coins[c] for c in [1, 2, 5]), sense=minimize)

# Restricción: El valor total debe igualar la suma objetivo
model.amount_constraint = Constraint(expr=sum(c * model.num_coins[c] for c in [1, 2, 5]) == 11)