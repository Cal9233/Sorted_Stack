# Sorted Stack Program

A Java console application demonstrating efficient sorted data structure implementation using Stack (LIFO) operations. This is a **maintenance update** from the original LinkedList implementation, showcasing how different data structures can be seamlessly integrated using solid architectural principles.

## Table of Contents

- [What's New in Version 2.0](#whats-new-in-version-20)
- [Features](#features)
- [Demo](#demo)
- [Architecture](#architecture)
- [Installation](#installation)
- [Usage](#usage)
- [Documentation](#documentation)
- [Project Structure](#project-structure)
- [Stack Implementation Details](#stack-implementation-details)
- [Migration from LinkedList](#migration-from-linkedlist)
- [Code Reuse Philosophy](#code-reuse-philosophy)
- [License](#license)
- [Author](#author)

## What's New in Version 2.0

🎉 **Major Update**: Transitioned from LinkedList to Stack-based implementation while maintaining architectural integrity!

### ✨ New Features
- **Stack-Based Storage**: Uses `Stack<Integer>` with LIFO (Last In, First Out) operations
- **Advanced Sorting Algorithm**: Custom stack-based insertion maintaining sorted order
- **Temporary Stack Operations**: Intelligent use of auxiliary stack for sorting
- **Enhanced Display**: Shows total count and Stack-specific messaging
- **Improved Performance**: Leverages Stack's natural LIFO behavior for efficient operations

### 🔄 Maintained Compatibility
- **Same Interfaces**: All existing interfaces unchanged for seamless integration
- **Consistent API**: External behavior remains identical despite internal Stack implementation
- **Backward Compatible**: Architecture supports both LinkedList and Stack implementations

### 📈 Performance Improvements
- **Optimized Insertion**: Stack-based sorting with O(n) complexity for each insertion
- **Memory Efficiency**: Stack operations with minimal temporary storage
- **LIFO Optimization**: Natural stack behavior for certain use cases

## Features

- **Real-time Stack Sorting**: Numbers maintain sorted order using intelligent stack operations
- **LIFO Operations**: Leverages Last-In-First-Out stack behavior for efficient processing
- **Temporary Stack Algorithm**: Uses auxiliary stack for maintaining sort order during insertion
- **Input Validation**: Graceful handling of invalid input with user-friendly error messages
- **Clean Architecture**: SOLID principles implementation with interface-based design
- **Extensive Code Reuse**: Leverages Java Collections Framework and Stack operations
- **Professional Documentation**: Comprehensive Javadoc with Stack-specific reuse analysis
- **Seamless Migration**: Demonstrates architectural flexibility with data structure changes

## Demo

```
=== Sorted Stack Program ===
Enter integer numbers (one per line).
Press Enter on an empty line to finish input.
Numbers will be stored in a Stack and displayed sorted from smallest to largest.

Enter number: 25
Added 25
Enter number (or press Enter to finish): 10
Added 10
Enter number (or press Enter to finish): 30
Added 30
Enter number (or press Enter to finish): 15
Added 15
Enter number (or press Enter to finish): 

=== Final Results ===
Stack contents sorted (smallest to largest): [10, 15, 25, 30]
Total numbers in Stack: 4
```

## Architecture

The application maintains the same SOLID principles with enhanced Stack implementation:

- **Single Responsibility**: Each class maintains one clear purpose
- **Open/Closed**: **New**: Easy to switch between LinkedList and Stack implementations
- **Liskov Substitution**: Interface implementations remain interchangeable
- **Interface Segregation**: Focused interfaces enable seamless data structure changes
- **Dependency Inversion**: Depends on abstractions, allowing Stack substitution

### Stack Integration Architecture

```
┌─────────────────┐
│   SortedStack   │ ← Main Coordinator (Updated)
│   (v2.0.0)      │
└─────────────────┘
         │
         ├─────────────────────────────────┐
         │                                 │
         ▼                                 ▼
┌─────────────────┐                ┌─────────────────┐
│  InputHandler   │                │ DisplayManager  │
│   (unchanged)   │                │    (enhanced)   │
└─────────────────┘                └─────────────────┘
         │                                 │
         ▼                                 ▼
┌─────────────────┐                ┌─────────────────┐
│ConsoleInput     │                │ConsoleDisplay   │
│Handler          │                │Manager          │
│   (unchanged)   │                │   (enhanced)    │
└─────────────────┘                └─────────────────┘
         │
         ▼
┌─────────────────┐
│SortedCollection │
│   (unchanged)   │
└─────────────────┘
         │
         ▼
┌─────────────────┐
│SortedInteger    │ ← NEW: Stack Implementation
│Stack (v2.0.0)   │
└─────────────────┘
```

## Installation

### Prerequisites

- Java Development Kit (JDK) 8 or higher
- Command line terminal
- Git (for cloning the repository)

### Quick Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/Calvin-1996/Sorted_Stack.git
   cd Sorted_Stack
   ```

2. **Navigate to the source directory**
   ```bash
   cd src
   ```

3. **Compile the program**
   ```bash
   javac *.java
   ```

4. **Run the program**
   ```bash
   java SortedStack
   ```


## Usage

### Basic Usage

1. Start the program:
   ```bash
   cd src
   java SortedStack
   ```
2. Enter integer numbers one per line when prompted
3. Press Enter on an empty line to finish input
4. View your numbers displayed in sorted order with total count

### Advanced Usage - Stack vs LinkedList

Choose your implementation at runtime:

```java
// Stack implementation (new in v2.0)
SortedCollection stackCollection = new SortedIntegerStack();
InputHandler inputHandler = new ConsoleInputHandler(stackCollection);
DisplayManager displayManager = new ConsoleDisplayManager();

SortedStack program = new SortedStack(stackCollection, inputHandler, displayManager);
program.run();

// Original LinkedList implementation (still supported)
SortedCollection listCollection = new SortedIntegerCollection();
// ... same pattern
```

## Documentation

### Generate Javadoc

Navigate to the source directory and generate documentation:

```bash
cd src
javadoc -d javadoc -author -version -use -windowtitle "Sorted Stack Program v2.0" -doctitle "CSC6301 Module 5 - Sorted Stack Implementation" *.java
```

### View Documentation

After generating Javadoc, open the documentation:

- **File Explorer/Finder**: Navigate to `src/javadoc/` and double-click `index.html`
- **Command Line**:
  - **macOS**: `open src/javadoc/index.html`
  - **Windows**: `start src/javadoc/index.html`
  - **Linux**: `xdg-open src/javadoc/index.html`

## Project Structure

```
sorted-stack-program/
├── README.md                           # Main project documentation (updated)
├── LICENSE                             # MIT License
├── .gitignore                          # Git ignore rules
│
├── src/                                # Source code
       ├── SortedStack.java             # Main coordinator (updated from SortedList)
       ├── SortedIntegerStack.java      # NEW: Stack implementation
       ├── ConsoleInputHandler.java     # Console input (unchanged)
       ├── ConsoleDisplayManager.java   # Console display (enhanced)
       ├── SortedCollection.java        # Collection interface (unchanged)
       ├── InputHandler.java            # Input interface (unchanged)
       └── DisplayManager.java          # Display interface (unchanged)
```

## Stack Implementation Details

### Key Algorithm: Sorted Stack Insertion

The core innovation of v2.0 is the **stack-based sorting algorithm**:

```java
public void add(Integer number) {
    // Pop elements smaller than new number to temporary stack
    while (!numbers.isEmpty() && numbers.peek() < number) {
        tempStack.push(numbers.pop());
    }
    
    // Push the new number
    numbers.push(number);
    
    // Push back all elements from temporary stack
    while (!tempStack.isEmpty()) {
        numbers.push(tempStack.pop());
    }
}
```

### Stack Organization

- **Main Stack**: Stores numbers with largest on top, smallest on bottom
- **Temporary Stack**: Used during insertion for maintaining sort order
- **Display Conversion**: Reverses stack contents for user-friendly smallest-to-largest display

### Performance Characteristics

| Operation | LinkedList v1.0 | Stack v2.0 | Notes |
|-----------|-----------------|------------|-------|
| Insert | O(n) | O(n) | Stack uses temporary stack operations |
| Display | O(n) | O(n) | Stack requires reversal for display |
| Memory | ~24 bytes/node | ~16 bytes/element + stack overhead | Stack more memory efficient |
| Access Pattern | Random access | LIFO only | Different use case optimization |

## Migration from LinkedList

### What Changed

✅ **Enhanced Components**:
- `SortedList.java` → `SortedStack.java` (renamed + updated)
- `SortedIntegerCollection.java` → `SortedIntegerStack.java` (completely rewritten)
- `ConsoleDisplayManager.java` (enhanced with Stack messaging)

✅ **Unchanged Components** (demonstrating architectural stability):
- `SortedCollection.java` interface
- `InputHandler.java` interface  
- `DisplayManager.java` interface
- `ConsoleInputHandler.java` implementation

### Migration Benefits

1. **Interface Stability**: No changes to client code using interfaces
2. **Drop-in Replacement**: Stack implementation substitutes seamlessly
3. **Enhanced Features**: Added Stack-specific functionality without breaking existing code
4. **Performance Options**: Choose LinkedList or Stack based on use case

## Code Reuse Philosophy

### Stack-Specific Reuse Enhancements

This v2.0 implementation extends our reuse philosophy with Stack-specific components:

#### 1. **Stack Operations Reuse**
**New Reused**: `Stack.push()`, `Stack.pop()`, `Stack.peek()`, `Stack.isEmpty()`
**Avoided**: Custom LIFO implementation with array management
**Benefits**: 
- Proven LIFO operations with capacity management
- Automatic bounds checking and exception handling
- Optimized performance for stack-specific operations

#### 2. **Collections Framework Integration**
**Enhanced Reuse**: Maintains use of Collections utilities while adding Stack support
**New Components**: Stack iteration, ArrayList conversion for display
**Benefits**: Seamless integration between Stack and List interfaces

#### 3. **Temporary Stack Pattern**
**Reuse Strategy**: Uses additional Stack for sorting instead of custom algorithms
**Components**: Multiple Stack instances with coordinated operations
**Benefits**: Leverages proven Stack behavior for complex sorting logic

### Original Reuse Components (Maintained)

- **Scanner**: Input processing (unchanged from v1.0)
- **Integer.parseInt()**: Type conversion (unchanged from v1.0)
- **StringBuilder**: String operations (unchanged from v1.0)
- **Interface Patterns**: SOLID principles (maintained in v2.0)

See the [generated Javadoc](src/javadoc/index.html) for detailed Stack-specific code reuse documentation.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Author

**Calvin Malagon**
- Course: CSC6301 - Module 5 (Stack Maintenance Update from Module 4)
- Version: 2.0.0.0 (Stack Implementation)
- Email: [malagonc@merrimack.edu](mailto:malagonc@merrimack.edu)
- GitHub: [@Calvin-1996](https://github.com/Calvin-1996)

---

## Version History

- **v1.0.0** (Module 4): Original LinkedList implementation
- **v2.0.0** (Module 5): **Current** - Stack implementation with maintained interface compatibility