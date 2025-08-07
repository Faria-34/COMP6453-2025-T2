# COMP6453 Project – BBS+ and Threshold BBS+ Signatures

This repository presents a practical implementation and comprehensive evaluation of the BBS+ signature scheme and its threshold variant (Threshold BBS+). The project was completed for **COMP6453: Advanced Topics in Cyber Security** at UNSW, T2 2025. The work includes both benchmarking and real-world test cases to assess the performance, correctness, and practical applicability of both schemes.

---

## Project Overview

The aim of this project is to implement, benchmark, and validate two cryptographic signature schemes:

- **BBS+ Signature**: Standard BBS+ multi-message signature over the BLS12-381 curve.
- **Threshold BBS+ Signature**: A threshold variant using Shamir secret sharing, allowing any subset of `t` out of `n` participants to jointly produce a valid signature.

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

## Folder Structure

```
COMP6453_BBSplus/
├── basic_bbsplus.ipynb        # Main notebook: BBS+ & Threshold BBS+ implementation, benchmarks, and test cases
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
```

**Step 4: Open the notebook and run**
Open `basic_bbsplus.ipynb` with Jupyter Notebook and run the cells.

---




## References

- [BBS+ Signature Scheme](https://eprint.iacr.org/2016/663.pdf)
- Threshold cryptography and Shamir secret sharing
- [py_ecc library](https://github.com/ethereum/py_ecc)

---

## License

This code is intended for educational and research use at UNSW for COMP6453 Term 2, 2025.