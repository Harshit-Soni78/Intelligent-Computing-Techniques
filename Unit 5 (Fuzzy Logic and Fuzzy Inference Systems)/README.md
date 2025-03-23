# **Unit 5: Fuzzy Logic and Fuzzy Inference Systems**

- **Run Fuzzy Logic and Fuzzy Inference Systems(Hands-on).ipynb Notebook in Google Colab:** <a href="https://colab.research.google.com/github/Harshit-Soni78/Intelligent-Computing-Techniques/blob/main/Unit%205%20(Fuzzy%20Logic%20and%20Fuzzy%20Inference%20Systems)/Fuzzy%20Logic%20and%20Fuzzy%20Inference%20Systems(Hands-on).ipynb" target="_blank">Click Here 🔗</a>

---

## **1. Introduction to Fuzzy Logic**

Fuzzy logic is a form of many-valued logic that deals with reasoning that is approximate rather than fixed and exact. Unlike classical binary logic (true/false), fuzzy logic allows for intermediate values (partially true/false).

### **Key Concepts of Fuzzy Logic:**

1. **Fuzzy Sets:** A set where an element's membership is expressed in degrees (0 to 1).
2. **Membership Functions:** Define the degree to which an element belongs to a fuzzy set.
3. **Fuzzy Rules:** If-Then rules used in decision-making.
4. **Fuzzy Inference System (FIS):** Processes input data using fuzzy rules to generate an output.

---

## **2. Formation of Fuzzy Rules**

Fuzzy rules are conditional statements used to describe relationships between input and output variables.

### **Example Rule:**

- IF temperature is high THEN fan speed is fast.
- IF temperature is moderate THEN fan speed is medium.
- IF temperature is low THEN fan speed is slow.

---

## **3. Hands-on: Implementing a Fuzzy System in Python**

### **Defining Fuzzy Sets and Rules**

```python
import numpy as np
import skfuzzy as fuzz
import skfuzzy.control as ctrl

# Define fuzzy variables
temperature = ctrl.Antecedent(np.arange(0, 41, 1), 'temperature')
speed = ctrl.Consequent(np.arange(0, 101, 1), 'speed')

# Define membership functions
temperature['low'] = fuzz.trimf(temperature.universe, [0, 0, 20])
temperature['moderate'] = fuzz.trimf(temperature.universe, [10, 20, 30])
temperature['high'] = fuzz.trimf(temperature.universe, [20, 40, 40])

speed['slow'] = fuzz.trimf(speed.universe, [0, 0, 50])
speed['medium'] = fuzz.trimf(speed.universe, [30, 50, 70])
speed['fast'] = fuzz.trimf(speed.universe, [50, 100, 100])

# Define fuzzy rules
rule1 = ctrl.Rule(temperature['low'], speed['slow'])
rule2 = ctrl.Rule(temperature['moderate'], speed['medium'])
rule3 = ctrl.Rule(temperature['high'], speed['fast'])

# Control system
speed_ctrl = ctrl.ControlSystem([rule1, rule2, rule3])
speed_sim = ctrl.ControlSystemSimulation(speed_ctrl)

# Test input
test_temp = 25
speed_sim.input['temperature'] = test_temp
speed_sim.compute()

print(f"For temperature {test_temp}°C, the fan speed is {speed_sim.output['speed']:.2f}%")
```

**Explanation:**

- Defines fuzzy sets for temperature and speed.
- Implements fuzzy rules to determine fan speed.
- Uses a fuzzy inference system to compute the output based on the input temperature.

---

## **4. Fuzzy Reasoning and Inference Systems**

A **Fuzzy Inference System (FIS)** processes input variables through fuzzy rules to produce an output.

### **Types of FIS:**

1. **Mamdani FIS:** Uses fuzzy sets for both input and output.
2. **Sugeno FIS:** Uses crisp values as outputs.

---

## **5. Fuzzy Decision Making**

Fuzzy logic is widely used in decision-making applications where uncertainty exists.

### **Examples of Fuzzy Decision Making:**

- Automatic climate control systems.
- Stock market prediction models.
- Medical diagnosis systems.

---

## **6. Applications of Fuzzy Logic**

- **Consumer Electronics:** Washing machines, air conditioners.
- **Automotive Systems:** ABS braking, cruise control.
- **Medical Diagnosis:** Patient risk assessment.
- **Industrial Automation:** Control of robotic arms.

---

## **7. Discussion Questions**

1. How does fuzzy logic differ from traditional Boolean logic?
2. What are the advantages of fuzzy inference systems in real-world applications?
3. Why is fuzzy logic useful in situations with uncertainty and imprecision?

## Author

**Harshit Soni**  
GitHub: [Harshit-Soni78](https://github.com/Harshit-Soni78)

---
Made with ❤️ by Harshit Soni
