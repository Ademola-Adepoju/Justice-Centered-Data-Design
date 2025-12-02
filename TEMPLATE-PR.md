# CHAPTER X.x - Firstname Lastname

## Triumphs

Reflect on 2-3 triumphs in the list format below.

1. **Template Typo**: The starter code used personAage instead of person3Age. I copied it, so my else if (person3Age === 30) was checking a variable that didn’t exist. Renaming to person3Age fixed it immediately—the Console showed “Person is exactly 30 years old.”
2. **Redeclarations across js blocks**: I had declared the same names (e.g., person1Age, childrenTotal) in multiple executable blocks. In Observable, all js blocks share the same module scope, so top-level names can only be declared once. I moved all person/children declarations into a single starter block and only used them later.