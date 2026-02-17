Here is your project written in a clean, professional **GitHub README.md format** 👇
(You can directly copy-paste this into your `README.md` file.)

---

# 🧪 Three-Tank Dynamic Mixing System Simulation

**Author:** Krishil Choksi
**Roll No:** 23BME055
**Course:** Computational Engineering / Engineering Mathematics
**Tool Used:** MATLAB

---

## 📌 Project Overview

This project models and simulates a **three-tank interconnected mixing system** using first-order differential equations.

The objective is to:

* Formulate mass balance equations
* Analyze three operating conditions
* Simulate system dynamics using MATLAB
* Demonstrate convergence to a common equilibrium
* Study system stability

The system is solved numerically using MATLAB’s `ode45` solver.

---

## ⚙️ System Description

The system consists of:

* 3 perfectly mixed tanks
* Constant flow rate
* No chemical reaction
* Tank 1 receives external input concentration
* Tanks exchange material with each other

### Governing Principle

> **Accumulation = Inflow − Outflow**

---

## 🧮 Mathematical Model

Let:

* `C1(t)` = Concentration in Tank 1
* `C2(t)` = Concentration in Tank 2
* `C3(t)` = Concentration in Tank 3
* `Cin = 15 kg/m³`

### Differential Equations

[
\frac{dC_1}{dt} = 15 + C_2 + C_3 - 3C_1
]

[
\frac{dC_2}{dt} = C_1 + C_3 - 2C_2
]

[
\frac{dC_3}{dt} = C_1 + C_2 - 2C_3
]

This is a **coupled linear first-order ODE system**.
<img width="235" height="141" alt="image" src="https://github.com/user-attachments/assets/e8b4a5b6-6fe3-4d73-9785-193933b47ba8" />
<img width="474" height="414" alt="image" src="https://github.com/user-attachments/assets/d03e8404-b8df-4a07-b6c7-65e8d1d38824" />

---

## 🔄 Three Operating Conditions

### 🔵 Condition 1 – Low Initial State

```
C1(0) = 5
C2(0) = 2.5
C3(0) = 2.5
```

* Concentrations increase over time
* System moves upward toward equilibrium

---

### 🔴 Condition 2 – High Initial State

```
C1(0) = 10
C2(0) = 5
C3(0) = 5
```

* Concentrations decrease over time
* System moves downward toward equilibrium

---

### 🟢 Condition 3 – Steady-State (Equilibrium)

At equilibrium:

```
dC1/dt = dC2/dt = dC3/dt = 0
```

Solving algebraically:

```
C1 = 7.5 kg/m³
C2 = 3.75 kg/m³
C3 = 3.75 kg/m³
```

Final Equilibrium Vector:

```
Ceq = [7.5; 3.75; 3.75]
```

---

## 💻 MATLAB Implementation

```matlab
clc
clear
close all

tspan = [0 20];
Cin = 15;

initial_low  = [5 2.5 2.5];
initial_high = [10 5 5];

f = @(t,C)[ Cin + C(2) + C(3) - 3*C(1);
             C(1) + C(3) - 2*C(2);
             C(1) + C(2) - 2*C(3) ];

[t1,C_low]  = ode45(f,tspan,initial_low);
[t2,C_high] = ode45(f,tspan,initial_high);

Ceq = [7.5 3.75 3.75];

fprintf('Final Equilibrium Concentrations (Cin = 15)\n')
fprintf('C1 = %.4f kg/m^3\n', Ceq(1))
fprintf('C2 = %.4f kg/m^3\n', Ceq(2))
fprintf('C3 = %.4f kg/m^3\n', Ceq(3))

figure

plot(t1,C_low(:,1),'LineWidth',2)
hold on
plot(t2,C_high(:,1),'LineWidth',2)

yline(Ceq(1),'LineWidth',2)

xlabel('Time (s)')
ylabel('Concentration in Tank 1 (kg/m^3)')
title('Convergence to Common Equilibrium (Cin = 15)')
legend('Start from Low State','Start from High State','Equilibrium Value')
grid on
```

---

## 📊 Results

| Condition    | Behavior   | Final Value     |
| ------------ | ---------- | --------------- |
| Low Initial  | Increasing | 7.5, 3.75, 3.75 |
| High Initial | Decreasing | 7.5, 3.75, 3.75 |
| Equilibrium  | Constant   | 7.5, 3.75, 3.75 |
![Uploading image.png…]()
![Uploading image.png…]()

Both initial conditions converge to the **same equilibrium**, proving system stability.

---

## 📈 Stability Analysis

The system can be written in matrix form:

```
dC/dt = AC + B
```

Since eigenvalues of matrix `A` are negative:

* Equilibrium is unique
* System is asymptotically stable
* Convergence occurs for any initial condition





## ✅ Conclusion

This project demonstrates how a three-tank interconnected system can be modeled using first-order differential equations and solved numerically in MATLAB.

The study confirms that **regardless of initial conditions**, the system converges to a unique and stable equilibrium concentration.

