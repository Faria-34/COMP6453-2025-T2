# COMP6453 Project – BBS+ and Threshold BBS+ Signatures

This repository presents a practical implementation and comprehensive evaluation of the BBS+ signature scheme and its threshold variant (Threshold BBS+). The project was completed for **COMP6453: Applied Cryptography** at UNSW, T2 2025. The work includes both benchmarking and real-world test cases to assess the performance, correctness, and practical applicability of all schemes, including the distributed threshold variant using MPC and a optimization method of BBS+.

---

## Project Overview

The aim of this project is to implement, benchmark, and validate two cryptographic signature schemes:

- **BBS+ Signature**: Standard BBS+ multi-message signature over the BLS12-381 curve.
- **Threshold BBS+ Signature**: A threshold variant using Shamir secret sharing, allowing any subset of `t` out of `n` participants to jointly produce a valid signature.
- **Threshold BBS+ with MPC (ThresholdBBSMPC)**: An advanced distributed threshold scheme using secure multi-party computation (MPyC), where the signing key is never reconstructed in the clear and all signing operations are performed collaboratively.
- **BBS+ Signature Optimization**: Using MSM and Multi-Pairing to optimize BBS+

The project features:

- **Performance Benchmarking**: 
  - Measuring signing and verification speed, signature size, and correctness for various parameter settings (number of messages, threshold, number of participants).
  - Direct comparison between BBS+ and Threshold BBS+.
- **Real Data Test Cases**: 
  - Signing and verifying actual message data (e.g., names, student IDs, emails) to demonstrate practical usability.

---

## Experimental Setup

- **Library Requirements**:
  - Python 3.7+
  - [py_ecc](https://github.com/ethereum/py_ecc) for BLS12-381 curve operations.

- **Benchmark Parameters**:
  - Number of messages (`ell`): tested with 1, 3, 10, 30.
  - Threshold group settings (`n`, `t`): tested with (3,2), (5,3), (10,5).
  - All experiments run in Jupyter Notebook cells.

- **Real Data Cases**:
  - Messages encoded from strings (e.g., `"Alice"`, `"2025123456"`, `"alice@example.com"`) to integers for cryptographic operations.

- **Metrics**:
  - Signing time, verification time, signature size, and correctness (validity of verification).

---


## Performance Optimizations: Multi-Scalar Multiplication (MSM) & Multi-Pairing

### MSM (Multi-Scalar Multiplication)
We often need sums like:
B = g1 + s·H0 + Σ_{i=1}^ℓ m_i·H_i  = Σ_j α_j P_j
Instead of doing each scalar multiplication separately, a windowed MSM (e.g., Pippenger) groups work:

1. Choose window size w.
2. Decompose each scalar α = Σ_j d_j 2^{w·j}, with digits d_j in [0, 2^w − 1].
3. For each window: bucket points by digit, sum buckets (high → low) to reuse partial sums.
4. Between windows: apply w doublings to the accumulator and add the window contribution.

Benefits: Fewer additions and better cache locality; readily parallelizable.

### Multi-Pairing
To check e(A, X + e·g2) = e(B, g2), compute:
e(A, X + e·g2) · e(B, g2)^{-1} ?= 1
Rather than two full pairings + two final exponentiations:
- Accumulate both terms in one multi-pairing (Miller loop).
- Use point negation (−B) instead of an explicit inverse.
- Perform a single final exponentiation.

Benefits: Speed up by avoiding the second final exponentiation.

---

## Folder Structure

```
├── BBSplus.ipynb              # Main notebook: BBS+ & Threshold BBS+ implementation, Threshold BBS+ MPC implementation, benchmarks, and test cases
├── Optimization.ipynb         # Optimized method
├── README.md                  # Project documentation
```

---

## How to Run


**Step 1: Clone the repository to your local machine**
```bash
git clone https://github.com/Faria-34/COMP6453-2025-T2.git
```

**Step 2: Enter the repository directory**
```bash
cd COMP6453-2025-T2
```

**Step 3: (Optional) Install dependencies**
```bash
pip install py-ecc
pip install mpyc
```

**Step 4: Open the notebook and run**
Open `basic_bbsplus.ipynb` with Jupyter Notebook and run the cells.

---




## References

- [Threshold BBS+ Signatures for Distributed Anonymous Credential Issuance](https://eprint.iacr.org/2023/602)
- [py_ecc library](https://github.com/ethereum/py_ecc)

---

## License

This code is intended for educational and research use at UNSW for COMP6453 Term 2, 2025.