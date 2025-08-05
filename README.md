Quantum Circuit for Generating a W-state
This project contains a Python script within a Jupyter Notebook that uses Qiskit to construct and simulate a quantum circuit designed to prepare a W-state for a given number of qubits.
Description
The core of the project is the create_consecutive_ones_circuit(n) function, which programmatically builds a quantum circuit for an n-qubit system. The W-state is a specific type of multi-qubit entangled state where only one qubit is in the |1⟩ state, and all others are |0⟩, in a superposition of all such possibilities.
The circuit construction involves:
Initialization: A quantum circuit with n qubits is created.
Rotations: A series of Ry and controlled-Ry gates are applied to the qubits. The specific rotation angles are calculated to create the desired superposition.
Entanglement: A cascade of CNOT gates is used to entangle the qubits.
Final Operation: An X-gate is applied to the most significant qubit to finalize the state preparation.
The script then simulates the circuit using both the statevector_simulator to display the ideal resulting state vector and the qasm_simulator to show the measurement outcome probabilities in a histogram after a number of shots.
Getting Started
Prerequisites
Python 3.x
Qiskit
Matplotlib
NumPy
You can install the necessary libraries using pip:
pip install qiskit matplotlib numpy qiskit-aer


Running the Code
The main script is provided in the Jupyter Notebook (general case for w (2).ipynb).
Open the notebook in a Jupyter environment (like Jupyter Lab or Jupyter Notebook).
You can modify the number of qubits n in the code cell. The example is set to:
n = 12


Run the cells sequentially to generate the circuit, display its structure, show the output statevector, and plot the simulation results.
Example Output
For n = 12 qubits, the script will:
Display the quantum circuit diagram.
Print the circuit's depth.
Show the final statevector in LaTeX format, which will be an equal superposition of states with a single '1' (e.g., |100...⟩, |010...⟩, etc.).
Plot a histogram of the measurement outcomes from the simulation, showing roughly equal probabilities for each of the basis states that constitute the W-state.
