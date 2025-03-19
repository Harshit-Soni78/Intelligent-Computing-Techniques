# **Unit 3: Knowledge Representation & Reasoning**

## **1. Introduction to Knowledge Representation (KR)**

Knowledge Representation (KR) is a key aspect of AI that involves storing and organizing knowledge to enable reasoning and decision-making.

### **Types of Knowledge Representation:**

1. **Propositional Logic** - Uses statements that are either true or false.
2. **Predicate Logic** - Uses predicates and quantifiers for more complex relationships.
3. **Semantic Networks** - Graph-based representation of knowledge.
4. **Frames and Scripts** - Structured way of storing concepts and their relationships.
5. **Ontologies** - Formal representation of knowledge in a domain.

---

## **2. Hands-on: Implementing Propositional & Predicate Logic**

### **Propositional Logic using Python**

```python
from sympy import symbols, And, Or, Not, Implies

# Define propositions
P = symbols('P')  # Example: "It is raining"
Q = symbols('Q')  # Example: "I will carry an umbrella"

# Logical Statements
statement1 = Implies(P, Q)  # If it is raining, then I will carry an umbrella
statement2 = And(P, Not(Q)) # It is raining, but I am not carrying an umbrella

print("Statement 1 (Implication):", statement1)
print("Statement 2 (Contradiction Example):", statement2)
```

**Explanation:** This demonstrates how to represent propositional logic using Python.

---

### **Predicate Logic in Python using Prolog-style Representation**

```python
from kanren import Relation, facts, run, var

parent = Relation()
facts(parent, ('John', 'Alice'), ('Alice', 'Bob'), ('Bob', 'Charlie'))

x = var()
print(run(1, x, parent(x, 'Bob')))  # Who is Bob’s parent?
print(run(1, x, parent('Alice', x)))  # Who is Alice's child?
```

**Explanation:** This uses logic programming to find relationships between entities.

---

## **3. Forward & Backward Reasoning**

### **Forward Chaining (Data-driven Reasoning)**

- Starts with known facts and applies rules to infer new facts until the goal is reached.
- Example: If we know "Socrates is a man" and "All men are mortal," we can infer "Socrates is mortal."

```python
knowledge_base = {
    "Socrates is a man": True,
    "All men are mortal": True,
}

def forward_chaining(kb):
    if kb["Socrates is a man"] and kb["All men are mortal"]:
        return "Socrates is mortal"
    return "Cannot conclude"

print(forward_chaining(knowledge_base))
```

**Explanation:** Checks facts iteratively to infer new knowledge.

---

### **Backward Chaining (Goal-driven Reasoning)**

- Starts with the goal and works backward to see if known facts support it.
- Example: If we want to prove "Socrates is mortal," we check if there is evidence for it.

```python
def backward_chaining(goal, kb):
    if goal == "Socrates is mortal":
        return kb.get("Socrates is a man", False) and kb.get("All men are mortal", False)
    return False

print("Is Socrates mortal?", backward_chaining("Socrates is mortal", knowledge_base))
```

**Explanation:** The system works backward from the goal to verify its validity.

---

## **4. Slot & Filler Structures**

Slot and filler structures help represent knowledge using predefined templates.

### **Example: Representing a Car Using Slots**

```python
car = {
    "Make": "Toyota",
    "Model": "Camry",
    "Year": 2022,
    "Features": ["Airbags", "Sunroof", "GPS"]
}
print("Car Information:", car)
```

**Explanation:** This structure allows easy retrieval and updating of information.

---

## **5. Natural Language Processing (NLP) Basics**

NLP involves processing human language for AI applications such as chatbots and sentiment analysis.

### **Tokenization, Stopwords, and Stemming in NLP**

```python
import nltk
from nltk.tokenize import word_tokenize
from nltk.corpus import stopwords
from nltk.stem import PorterStemmer

nltk.download('punkt')
nltk.download('stopwords')

text = "AI is transforming the world through automation and data analysis."
tokens = word_tokenize(text)
stemmer = PorterStemmer()
filtered_words = [stemmer.stem(word) for word in tokens if word.lower() not in stopwords.words('english')]

print("Original Tokens:", tokens)
print("Processed Tokens:", filtered_words)
```

**Explanation:** Demonstrates how to preprocess text data for AI models.

---

## **6. Discussion Questions**

1. How do forward and backward chaining differ in real-world applications?
2. Why is predicate logic more powerful than propositional logic?
3. How does knowledge representation impact AI-driven decision-making?
