# Project Overview

## Purpose
This project provides a lightweight implementation of core Ethereum-related data encoding and parsing utilities, focusing on RLP (Recursive Length Prefix) encoding and transaction-related operations.

## Key Features
- RLP Encoding and Decoding: A custom implementation of the Recursive Length Prefix (RLP) encoding standard used in Ethereum
  - Supports encoding and decoding of integers, strings, and lists
  - Handles various data type conversions and binary representations
- Transaction Parsing: Basic transaction data parsing capabilities
- Binary Conversion Utilities: Tools for converting between different numeric representations

## Benefits
- Lightweight and focused implementation of core Ethereum encoding mechanisms
- Provides low-level utilities for blockchain and Ethereum-related data processing
- Offers precise control over binary and numeric data transformations

## Technical Highlights
- Supports encoding of integers up to 2^256
- Handles different length encodings for various data types
- Provides both encoding and decoding functionality for complex data structures

## Installation

### Prerequisites
- Python 3.7 or higher
- pip (Python package manager)

### Installing the Library

You can install this library directly from the repository using pip:

```bash
pip install git+https://github.com/ethereum/pyethereum.git
```

### Local Development Setup

1. Clone the repository:
```bash
git clone https://github.com/ethereum/pyethereum.git
cd pyethereum
```

2. Create a virtual environment (recommended):
```bash
python3 -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
```

3. Install dependencies:
```bash
pip install -r requirements.txt  # Note: Create a requirements.txt if not present
```

### Verification
To verify the installation, you can run:
```bash
python -c "import pyethereum; print(pyethereum.__version__)"
```

### Note
This installation method assumes the project is intended to be installed as a package. Always refer to the project's official documentation for the most up-to-date installation instructions.

## API Reference

### Classes

#### `Block` Class
A class representing an Ethereum block with methods for block manipulation and state management.

**Constructor**:
```python
def __init__(self, data=None)
```
- `data` (optional): Block data, can be hex-encoded or RLP-encoded
  - If None, creates an empty block
  - If hex-encoded or RLP-encoded, parses the block data

**Methods**:
1. `pay_fee(address, fee, tominer=True)`
   - Deducts a fee from the sender's account and optionally pays it to the miner
   - **Parameters**:
     - `address`: Sender's address
     - `fee`: Amount of fee to deduct
     - `tominer`: Whether to pay the fee to the miner (default: True)
   - **Returns**: `Boolean` indicating success of fee payment

2. `get_nonce(address)`
   - Retrieves the nonce (transaction count) for a given address
   - **Parameters**: 
     - `address`: Account address
   - **Returns**: Account nonce or `False` if not found

3. `get_balance(address)`
   - Retrieves the balance for a given address
   - **Parameters**: 
     - `address`: Account address
   - **Returns**: Account balance (integer)

4. `set_balance(address, balance)`
   - Sets the balance for a given address
   - **Parameters**:
     - `address`: Account address
     - `balance`: New balance to set

5. `get_contract(address)`
   - Retrieves the contract state for a given address
   - **Parameters**:
     - `address`: Contract address
   - **Returns**: `Trie` object representing contract state or `False`

6. `update_contract(address, contract)`
   - Updates the contract state for a given address
   - **Parameters**:
     - `address`: Contract address
     - `contract`: Updated contract `Trie`
   - **Returns**: `Boolean` indicating success

7. `serialize()`
   - Serializes the block into RLP-encoded format
   - **Returns**: RLP-encoded block data

8. `hash()`
   - Generates the block's hash
   - **Returns**: Block hash (SHA256)

#### `Transaction` Class
A class representing an Ethereum transaction with methods for parsing, signing, and serialization.

**Constructors**:
```python
def __init__(self, nonce, to, value, fee, data)
def __init__(self, data)
```
- First constructor: Creates a transaction with explicit parameters
- Second constructor: Parses transaction from encoded data

**Methods**:
1. `parse(data)`
   - Parses transaction data from hex or RLP-encoded input
   - **Parameters**:
     - `data`: Transaction data to parse
   - **Returns**: Parsed transaction object

2. `sign(key)`
   - Signs the transaction with a private key
   - **Parameters**:
     - `key`: Private key for signing
   - **Returns**: Signed transaction object

3. `serialize()`
   - Serializes the transaction into RLP-encoded format
   - **Returns**: RLP-encoded transaction data

4. `hex_serialize()`
   - Serializes the transaction into hex-encoded format
   - **Returns**: Hex-encoded transaction data

5. `hash()`
   - Generates the transaction's hash
   - **Returns**: Transaction hash (SHA256)

### Example Usage

```python
# Creating and signing a transaction
tx = Transaction(
    nonce=0,  # Transaction nonce
    to='recipient_address',  # Recipient address
    value=100,  # Transaction value
    fee=1,  # Transaction fee
    data=None  # Optional transaction data
)
tx.sign(private_key)

# Working with a block
block = Block(block_data)
balance = block.get_balance(address)
block.pay_fee(address, fee)
```

**Note**: This implementation is a simplified blockchain block and transaction representation, likely for educational or experimental purposes.

## Repository Structure

The repository contains the following key files and their purposes:

- `blocks.py`: Defines the Block class, which represents blockchain blocks and manages block-related operations.
- `manager.py`: Handles core blockchain management functions, including address generation, transaction pool management, and block processing.
- `parser.py`: Provides parsing functionality for blockchain-related data structures.
- `processblock.py`: Contains logic for evaluating and processing blockchain blocks.
- `rlp.py`: Implements RLP (Recursive Length Prefix) encoding and decoding, a serialization method used in Ethereum-like blockchain systems.
- `transactions.py`: Defines the Transaction class for handling blockchain transactions.
- `trie.py`: Likely implements a Merkle Patricia Trie data structure used for state storage.
- `trietest.py`: Contains tests for the trie implementation.

The project appears to be a lightweight blockchain implementation with core functionalities for managing blocks, transactions, and state.

# Contributing

We welcome contributions to this project! Here are some guidelines to help you get started:

## How to Contribute

1. **Fork the Repository**: Create a fork of the project on GitHub.

2. **Create a Branch**: 
   ```
   git checkout -b feature/your-feature-name
   ```

3. **Make Your Changes**: 
   - Ensure your code follows the project's coding style
   - Add or update tests as appropriate
   - Write clear, concise commit messages

4. **Run Tests**:
   Before submitting a pull request, run the existing tests:
   ```
   python trietest.py
   ```
   This will execute the test suite and verify the functionality of the Trie implementation.

5. **Submit a Pull Request**:
   - Push your changes to your fork
   - Open a pull request with a clear description of your changes
   - Provide context about the problem you're solving

## Testing

The project includes a test file `trietest.py` which:
- Generates random keys and values
- Updates a Trie data structure
- Verifies data consistency
- Raises an exception if any inconsistencies are found

To run tests:
```
python trietest.py
```

## Code of Conduct

- Be respectful and considerate of others
- Provide constructive feedback
- Focus on collaboration and improving the project

## Reporting Issues

If you find a bug or have a suggestion:
- Check existing issues to avoid duplicates
- Provide a clear description of the problem
- Include steps to reproduce the issue
- If possible, suggest a potential solution

Thank you for contributing!

## License

This project is currently unlicensed. 

**Important Notice**: Without an explicit license, the default copyright laws apply. This means:
- The original authors retain all rights to the code
- No one else has permission to reproduce, distribute, or create derivative works
- Commercial use, modification, and distribution are prohibited without explicit permission

We strongly recommend the project maintainers add an open-source license to clarify usage rights and encourage collaboration. For guidance, visit [Choose an Open Source License](https://choosealicense.com/).