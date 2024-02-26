# Algorithms

This section documents algorithms and calculations for attacks, movement, and more.

Conquer Online's client and server both utilize Microsoft's `rand` function for random number generation. This can be seen when generating a seed for RC5 in later patches of the client. Algorithms documented by this section that reference `rand` are assumed to use the Microsoft C implementation.

## Subsections

* [Calculations](calculations/README.md): Algorithms used in calculating distance, damage, etc.
* [Rates](rates/README.md): Descriptions of random rates for various systems.
