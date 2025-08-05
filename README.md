# Quantum Circuit for Generating a W-state

This project contains a Python script within a Jupyter Notebook that uses Qiskit to construct and simulate a quantum circuit designed to prepare a W-state for a given number of qubits.

## Description

The core of the project is the `create_consecutive_ones_circuit(n)` function, which programmatically builds a quantum circuit for an n-qubit system. The W-state is a specific type of multi-qubit entangled state where only one qubit is in the |1⟩ state and all others are in the |0⟩ state, in a superposition of all such possibilities.

### Circuit Construction

1. **Initialization**: A quantum circuit with `n` qubits is created.
2. **Rotations**: A series of `RY` and controlled-`RY` gates are applied. Specific rotation angles are calculated to create the desired superposition.
3. **Entanglement**: A cascade of `CNOT` gates is used to entangle the qubits.
4. **Final Operation**: An `X` gate is applied to the most significant qubit to complete the state preparation.

The circuit is then simulated using:
- `statevector_simulator` to obtain the ideal resulting statevector.
- `qasm_simulator` to observe the measurement outcome probabilities as a histogram.

## Getting Started

### Prerequisites

- Python 3.x
- Qiskit
- Matplotlib
- NumPy

You can install the required packages using:

```bash
pip install qiskit matplotlib numpy qiskit-aer
```

## Running the Code

1. Open the Jupyter Notebook: `general case for w (2).ipynb`
2. Launch it in a Jupyter environment (e.g., Jupyter Notebook or JupyterLab).
3. Set the desired number of qubits by modifying the value of `n`. Default is `n = 12`.
4. Run all cells in sequence to:
   - Generate and visualize the circuit.
   - Display the final statevector.
   - Simulate and plot the measurement results.

## Example Output

For `n = 12` qubits, the script will:

- Display the quantum circuit diagram.
- Print the circuit's depth.
- Show the final statevector in LaTeX format, representing an equal superposition of states with a single `1` (e.g., `|100...⟩`, `|010...⟩`, etc.).
- Plot a histogram of the measurement outcomes, showing approximately equal probabilities for each basis state that forms the W-state.

## License

This project is open-source and available under the MIT License.
