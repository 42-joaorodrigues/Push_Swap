# Push_swap

![42 Badge](https://img.shields.io/badge/42-Push__swap-brightgreen)
![C Badge](https://img.shields.io/badge/Language-C-blue)
![Status Badge](https://img.shields.io/badge/Status-Completed-success)
![Score Badge](https://img.shields.io/badge/Score-118%2F100-gold)

## Project Details

For full project requirements, see the [Subject File](./subject.md).

## What I Learned

Through this challenging algorithm optimization project at 42 School, I developed advanced programming skills and algorithmic thinking:

- **Algorithm complexity analysis** - Deep understanding of Big O notation and performance optimization trade-offs
- **Advanced data structures** - Implemented dual-stack architecture with sophisticated chunk-based management
- **Divide and conquer algorithms** - Mastered 3-way quicksort implementation with recursive partitioning
- **Memory-efficient programming** - Optimized stack operations to minimize memory allocations and copies
- **Algorithm selection strategies** - Learned when to use different sorting approaches based on input size
- **Performance benchmarking** - Analyzed and optimized operation counts to meet strict performance requirements
- **Recursive algorithm design** - Implemented elegant recursive solutions with proper base cases
- **Edge case handling** - Robust error management for invalid inputs and boundary conditions
- **Code modularity** - Created clean, reusable function interfaces for complex operations
- **Mathematical optimization** - Applied pivot selection techniques for optimal partitioning

This project significantly enhanced my problem-solving methodology, algorithmic intuition, and ability to optimize code for specific performance constraints.

## About the Project

Push_swap is an advanced sorting algorithm project that challenges students to sort integer arrays using only stack operations. The goal is to find the **minimum number of operations** needed to sort any given input, requiring deep understanding of:

- Sorting algorithm complexity
- Stack-based data manipulation
- Algorithm optimization techniques
- Performance analysis and benchmarking

## Performance Results

My implementation achieves exceptional performance benchmarks:

### 📊 Benchmark Results
- **100 numbers**: Average **634 operations** (Target: <700)
- **500 numbers**: Average **4,233 operations** (Target: <5,500)
- **Efficiency**: Consistently **10-25% better** than benchmark requirements

### 🏆 Score Achievement
- **Mandatory Part**: 100/100 (Perfect)
- **Bonus Part**: 18/25 
- **Final Score**: **118/100**

## Algorithm Strategy

### Dual-Stack Architecture

My implementation uses an innovative **dual-stack system** where each logical stack (A and B) is split into two physical stacks:

```c
typedef struct s_pushswap
{
    t_stack a_top;    // Top portion of stack A
    t_stack a_bot;    // Bottom portion of stack A  
    t_stack b_top;    // Top portion of stack B
    t_stack b_bot;    // Bottom portion of stack B
    t_list  *ops;     // Operation history
} t_ps;
```

This design enables:
- **Efficient chunk management** during partitioning
- **Reduced rotation costs** by accessing both ends
- **Optimal memory usage** with minimal data movement

### Algorithm Selection Strategy

#### Small Stacks (≤5 elements)
**Hardcoded optimal algorithms** for maximum efficiency:

- **Size 2**: Single swap operation
- **Size 3**: Hardcoded 6-case analysis (max 2 operations)
- **Size 4-5**: Two-minimum extraction + three-sort (max 12 operations)

#### Large Stacks (>5 elements)
**3-Way Quicksort** with intelligent optimizations:

```c
typedef struct s_chunk
{
    t_loc loc;    // Location: A_TOP, A_BOT, B_TOP, B_BOT
    int   size;   // Number of elements in chunk
} t_chunk;

typedef struct s_split
{
    t_chunk min;  // Elements < pivot1
    t_chunk med;  // Elements between pivots
    t_chunk max;  // Elements > pivot2
} t_split;
```

## Implementation Highlights

### Smart Pivot Selection
```c
void ft_get_pivots(int *pivots, const t_ps *pushswap, 
                   const t_chunk *chunk_data);
```
- Uses **33rd and 66th percentiles** for optimal 3-way partitioning
- Minimizes worst-case scenarios with balanced splits
- Adapts to data distribution patterns

### Efficient Chunk Manipulation
```c
void ft_chunk_split(t_ps *pushswap, t_chunk *src, t_split *dest);
```
- **O(n) partitioning** with minimal stack operations
- Intelligent use of both stack ends to reduce rotations
- Memory-efficient chunk tracking without data copying

### Operation Optimization
```c
void ft_clean_ops(t_list **ops);
```
- **Post-processing optimization** removes redundant operations
- Combines consecutive operations (e.g., `ra` + `ra` → `rr`)
- Eliminates cancel-out sequences (`ra` followed by `rra`)

## Technical Architecture

### Core Components

#### Stack Operations Engine
- **11 atomic operations**: `sa`, `sb`, `ss`, `pa`, `pb`, `ra`, `rb`, `rr`, `rra`, `rrb`, `rrr`
- **Operation tracking**: Complete history for optimization and verification
- **Error-free execution**: Robust handling of edge cases and invalid states

#### Quicksort Engine
- **Recursive partitioning**: Elegant divide-and-conquer implementation
- **Base case optimization**: Seamless transition to hardcoded small-stack algorithms
- **Adaptive chunk management**: Dynamic stack allocation based on partition sizes

#### Input Processing
- **Robust parsing**: Handles multiple argument formats and edge cases
- **Duplicate detection**: O(n²) validation with early termination
- **Integer overflow protection**: Safe conversion with range checking

### Memory Management
- **Zero memory leaks**: Comprehensive cleanup in all execution paths
- **Efficient allocation**: Minimal dynamic memory usage
- **Stack-based operations**: Most computations use stack memory for speed

## Bonus: Checker Program

The bonus `checker` program validates push_swap output:

```bash
# Usage example
./push_swap 4 67 3 87 23 | ./checker 4 67 3 87 23
OK

# Invalid operation sequence
echo -e "sa\ninvalid_op\nra" | ./checker 3 2 1
Error
```

### Features:
- **Standard input parsing**: Reads operations from stdin
- **Complete validation**: Verifies both operation validity and final sort state
- **Error handling**: Comprehensive error detection and reporting

## Usage

```bash
# Compile the project
make

# Compile with bonus (checker)
make bonus

# Basic usage
./push_swap 3 2 1 0
./push_swap "4 67 3 87 23"

# Verify with checker
./push_swap 5 2 4 1 3 | ./checker 5 2 4 1 3

# Performance testing
ARG=$(shuf -i 1-1000 -n 100 | tr '\n' ' '); ./push_swap $ARG | wc -l

# Clean builds
make clean    # Remove object files
make fclean   # Remove all generated files
make re       # Rebuild everything
```

## Algorithm Reference

This implementation was inspired by the comprehensive guide:
**["Push_swap in less than 4200 operations"](https://medium.com/@ulysse.gks/push-swap-in-less-than-4200-operations-c292f034f6c0)**

### Key Optimizations Applied:
- **Dual-ended stack access** for reduced rotation costs
- **Intelligent pivot selection** using tertile-based partitioning
- **Recursive depth optimization** with early base-case transitions
- **Operation sequence post-processing** for redundancy elimination

## Testing & Validation

### Comprehensive Test Suite
```bash
# Random testing for various sizes
for i in {3..100}; do
    ARG=$(shuf -i 1-1000 -n $i | tr '\n' ' ')
    OPS=$(./push_swap $ARG | wc -l)
    RESULT=$(./push_swap $ARG | ./checker $ARG)
    echo "Size $i: $OPS operations - $RESULT"
done
```

### Edge Cases Tested
- **Empty input**: No arguments provided
- **Single element**: Already sorted
- **Duplicate numbers**: Error handling
- **Invalid integers**: Non-numeric input, overflow
- **Already sorted**: Zero operations output
- **Reverse sorted**: Worst-case scenario

## Performance Analysis

### Complexity
- **Time**: O(n log n) average case, O(n²) worst case
- **Space**: O(log n) recursion depth, O(n) operation storage
- **Operations**: Empirically ~6-7n for random inputs

### Optimization Techniques
1. **Adaptive algorithm selection** based on input size
2. **Greedy optimization** for small fixed-size cases
3. **Balanced partitioning** to maintain logarithmic depth
4. **Operation consolidation** to minimize instruction count

---

*This project demonstrates mastery of advanced algorithms, performance optimization, and systems programming in C. The implementation consistently outperforms benchmark requirements while maintaining clean, maintainable code architecture.*

---

## License

This project is licensed under the [MIT License](./LICENSE).
