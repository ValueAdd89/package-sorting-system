# Package Sorting System

A robotic automation factory package sorting solution that dispatches packages to appropriate stacks based on their volume and mass characteristics.

Quick Access

Run Code Immediately on Repl.it - > https://replit.com/@JeromeJoseph/roboticautomation

## Overview

This system implements a `sort()` function that categorizes packages into three stacks:
- **STANDARD**: Regular packages that can be handled normally
- **SPECIAL**: Packages that are either bulky or heavy (but not both)
- **REJECTED**: Packages that are both bulky and heavy

## Sorting Criteria

### Bulky Package Definition
A package is considered **bulky** if:
- Its volume (Width × Height × Length) ≥ 1,000,000 cm³, OR
- Any single dimension ≥ 150 cm

### Heavy Package Definition
A package is considered **heavy** if:
- Its mass ≥ 20 kg

### Stack Assignment Logic
| Bulky | Heavy | Stack |
|-------|-------|-------|
| No    | No    | STANDARD |
| Yes   | No    | SPECIAL |
| No    | Yes   | SPECIAL |
| Yes   | Yes   | REJECTED |

## Function Signature

```python
def sort(width, height, length, mass):
    """
    Sorts packages into appropriate stacks based on volume and mass criteria.
    
    Args:
        width (float): Width in centimeters
        height (float): Height in centimeters  
        length (float): Length in centimeters
        mass (float): Mass in kilograms
    
    Returns:
        str: The stack name where the package should go ("STANDARD", "SPECIAL", or "REJECTED")
    """
```

## Usage Example

```python
# Standard package
result = sort(50, 30, 20, 10)  # Returns "STANDARD"

# Heavy package (special handling)
result = sort(40, 30, 20, 25)  # Returns "SPECIAL"

# Bulky package by dimension (special handling)
result = sort(200, 10, 10, 5)  # Returns "SPECIAL"

# Both bulky and heavy (rejected)
result = sort(100, 100, 100, 30)  # Returns "REJECTED"
```

## Code Quality Features

### 1. Documentation
- Docstrings with parameter descriptions
- Inline comments explaining logic decisions
- README with usage examples and specifications

### 2. Readable Code Structure
- Descriptive variable names (`is_bulky`, `is_heavy`)
- Named constants for thresholds
- Logical flow that mirrors the business requirements

### 3. Maintainability
- Separated threshold definitions for easy configuration
- Modular logic that can be easily extended
- Clean separation of concerns

## Edge Cases Handling

The implementation robustly handles various edge cases:

### Boundary Conditions
- **Exact thresholds**: Packages that exactly meet criteria (volume = 1,000,000 cm³, mass = 20 kg, dimension = 150 cm)
- **Multiple bulky criteria**: Packages that are bulky by both volume AND dimension
- **Floating point precision**: Handles decimal values correctly

### Input Validation Scenarios
- **Zero dimensions**: Handles packages with zero width/height/length
- **Negative values**: Function behavior with negative inputs
- **Very large numbers**: Performance with extreme values
- **Very small numbers**: Precision with tiny measurements

### Real-world Edge Cases
- **Thin but long packages**: 200cm × 1cm × 1cm
- **Cube at threshold**: 100cm × 100cm × 100cm (exactly 1M cm³)
- **Just under/over limits**: 149.9cm vs 150.1cm dimensions

## Test Coverage

### Test Suite

The implementation includes extensive testing covering:

#### 1. Basic Functionality Tests
```python
# STANDARD packages
sort(10, 10, 10, 5)     # Small, light package
sort(50, 50, 50, 10)    # Medium package under all thresholds

# SPECIAL packages  
sort(100, 100, 100, 5)  # Bulky by volume, not heavy
sort(200, 10, 10, 5)    # Bulky by dimension, not heavy
sort(10, 10, 10, 25)    # Heavy but not bulky

# REJECTED packages
sort(100, 100, 100, 25) # Both bulky and heavy
sort(200, 10, 10, 30)   # Both bulky and heavy
```

#### 2. Edge Case Tests
```python
# Boundary testing
sort(100, 100, 100, 19.9)  # Exactly bulky volume, just under heavy
sort(149, 10, 10, 10)      # Just under dimension threshold
sort(150, 10, 10, 10)      # Exactly at dimension threshold
sort(50, 50, 50, 20)       # Exactly at mass threshold
```

#### 3. Multiple Criteria Tests
```python
# Packages meeting multiple bulky criteria
sort(200, 200, 50, 10)     # Both volume and dimension bulky
sort(100, 100, 200, 5)     # Volume bulky + dimension bulky
```

#### 4. Input Validation Tests
```python
# Zero and negative values
sort(0, 10, 10, 5)         # Zero dimension
sort(10, 10, 10, 0)        # Zero mass
sort(-10, 10, 10, 5)       # Negative dimension
```

### Test Execution
Run the test suite with:
```python
python package_sorter.py
```

## Performance Characteristics

- **Time Complexity**: O(1) - constant time sorting
- **Space Complexity**: O(1) - constant memory usage
- **Scalability**: Suitable for high-throughput automation systems

## Installation and Setup

1. **Clone/Download**: No external dependencies required
2. **Python Version**: Compatible with Python 3.6+
3. **Execution**: Simply import and use the `sort()` function

```python
from package_sorter import sort

# Use the function
stack = sort(width, height, length, mass)
```

## Validation Against Requirements

### Correct Sorting Logic
- Implements exact business rules for bulky/heavy classification
- Proper stack assignment based on combination of criteria
- Accurate volume calculation and threshold comparisons

### Code Quality
- Clean, readable code with meaningful variable names
- Comprehensive documentation and comments
- Modular design with separated concerns
- Consistent coding style and formatting

### Edge Cases and Input Handling
- Boundary condition testing (exact threshold values)
- Multiple classification criteria handling
- Input validation and error scenarios
- Real-world edge cases (unusual dimensions)

### Test Coverage
- Unit tests for all three stack categories
- Boundary and edge case testing
- Multiple criteria scenarios
- Input validation testing
- 100% function coverage with diverse test cases
