# Unix Philosophy

- Make each program do one thing well. To do a new job build afresh rather than complicate

- Expect the output of every program to become the input to another as yet unknown program . Dont clutter with extraneous information. Avoid strictly columnar or binary input formats. Dont insist on interactive input.

# Uniform interace

- If we expect output of program to become the input to another program this means those programs must use same data format, (i.e.) a compatible interface.

- If we want to connect any programs output to any programs input that means all programs must have same input/output.

- In unix that interface is a file (or more precisely a file descriptor) 