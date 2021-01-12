# quantum dice
![Open Source? Yes!](https://badgen.net/badge/Open%20Source%20%3F/Yes%21/blue?icon=github)


Repositery that hold a simple quantum program made with IBM Q and qiskit.

## Quantum_Dice
In the notebook that hold the code that simulate a quantum dice with an finite number of side.
You can not change the number of side the dice has. You can only roll the dice.

Here a short version of the code but you can find the entire notebook [here]().

```python
from functools import reduce

# the backend that is going to simulate our quantum program
backend_sim = Aer.get_backend("qasm_simulator")

# create the quantum circuit
dice_circuit = QuantumCircuit(3, 3)
dice_circuit.h(0)
dice_circuit.h(1)
dice_circuit.h(2)

# map a qubit to a classical bit
dice_circuit.measure(range(3), range(3))

# execute the quantum circuit on the quantum simulator
dice_job  = execute(dice_circuit, backend_sim, shots = 1)
dice_result = dice_job.result()

# the result will be an string of number that is either 1 or 0.
dice_counts = dice_result.get_counts(dice_circuit)
dice_counts_val = "".join(dice_counts.keys())

dice_val = [int(val) for val in dice_counts_val]

# take the string of 1 and 0 and transform it into a decimal number and give the decimal number.
dice_nb = reduce(lambda x, y: (2*x) + y, dice_val, 0)
print("Your quantum dice give the result:", dice_nb )
```

## Quantum_dice2
This programm is the same as __quantum_Dice__. The only difference is that it allow you to chose the size of the dice.
You only need to add some few code to allow you to change the size of the dice.
You can see the notebook of the code [here]()

###### Add this at the top of the code.
```python
try:
 dice_size = int(input("type the size of the dice (i.e the number of face your dice has.): "))
except ValueError:
    print("You need to enter a number")
```

###### Change those piece of code in quantum_Dice.
```python
# create the quantum circuit
dice_circuit = QuantumCircuit(3, 3)
dice_circuit.h(0)
dice_circuit.h(1)
dice_circuit.h(2)

# map a qubit to a classical bit
dice_circuit.measure(range(3), range(3))
```

###### With those line of code.
```python
dice_circuit = QuantumCircuit(dice_size, dice_size)
dice_circuit.h(range(dice_size))
dice_circuit.measure(range(dice_size), range(dice_size))
dice_circuit.draw()

```

#### Ressource and Inspiration.
[Qiskit documentation made by IBM](https://qiskit.org/textbook/preface.html)
[Medium article that insprire me to make this repositery](https://medium.com/rigetti/how-to-write-a-quantum-program-in-10-lines-of-code-for-beginners-540224ac6b45)
