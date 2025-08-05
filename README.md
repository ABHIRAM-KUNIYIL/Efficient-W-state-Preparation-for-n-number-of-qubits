Quantum Circuit for Generating a W-like State
This repository contains a Jupyter Notebook that demonstrates the construction of a quantum circuit to generate a specific superposition of states, often referred to as a W-like state, where the basis states have consecutive ones (e.g., |0...01⟩, |0...10⟩, |0...100⟩, etc.).

Overview
The notebook uses the Qiskit library to build a quantum circuit that takes an n-qubit system from the initial |0⟩<sup>⊗n</sup> state to an equal superposition of states with a single '1' bit. This is a common pattern in quantum algorithms and is useful for understanding state preparation techniques.

How It Works
The circuit is constructed using a specific sequence of gates:

Initial Rotation: An RY gate is applied to the most significant qubit. The angle of rotation is calculated as θ = 2 * arccos(sqrt(1/n)), where n is the number of qubits.

Controlled Rotations: A series of controlled-RY gates are applied in a cascading manner. For each step k from n-1 down to 2, a controlled-RY gate is applied with the angle θ_k = 2 * arccos(sqrt(1/k)).

CNOT Cascade: A cascade of CNOT (or CX) gates is used to create the desired entanglement pattern across the qubits.

Final X Gate: An X gate (or NOT gate) is applied to the most significant qubit to finalize the state preparation.

Code
The core of the implementation is the create_consecutive_ones_circuit function, which programmatically builds the circuit for a given number of qubits n.

from qiskit import QuantumCircuit, transpile
from qiskit_aer import Aer
from qiskit import assemble
from qiskit.circuit.library import RYGate, HGate
import numpy as np
%matplotlib inline
import matplotlib.pyplot as plt
from numpy import arccos,sqrt,log2,ceil,floor
from qiskit.quantum_info import Statevector
from qiskit.visualization import plot_histogram, circuit_drawer

def create_consecutive_ones_circuit(n):
    qc = QuantumCircuit(n)

    # Calculate angles for rotations: theta_k = 2 * arccos(sqrt(1/k)) for k = n down to 2
    angles = [2 * np.arccos(np.sqrt(1/k)) for k in range(n, 1, -1)]

    # Apply initial rotation to the most significant qubit (index n-1)
    if n > 0:
        qc.ry(angles[0], n-1)

    # Apply controlled rotations (cry gates)
    for j in range(0, n-2):
        control_qubit = n-1 - j
        target_qubit = control_qubit - 1
        qc.cry(angles[j+1], control_qubit, target_qubit)

    # Apply cascade of CNOT gates
    for control in range(1, n):
        qc.cx(control, control-1)

    # Apply X gate to the most significant qubit
    qc.x(n-1)

    return qc

Simulation and Results
The notebook then simulates the generated circuit for n=12 qubits using the qiskit_aer simulator.

Statevector Simulation: It calculates the final statevector of the circuit to confirm that it is indeed the expected equal superposition of states.

Measurement Simulation: It runs the circuit on a simulated quantum computer (qasm_simulator) for 50,000 shots and plots a histogram of the measurement outcomes. The histogram shows that each of the basis states with a single '1' is measured with approximately equal probability, as expected.

How to Run
To run the notebook yourself, you will need to have Python and the following libraries installed:

qiskit

qiskit_aer

numpy

matplotlib

You can install them using pip:

pip install qiskit qiskit_aer numpy matplotlib

Then, you can open and run the general case for w (2).ipynb file in a Jupyter environment.
