# Unix Philosophy

- Make each program do one thing well. To do a new job build afresh rather than complicate

- Expect the output of every program to become the input to another as yet unknown program . Dont clutter with extraneous information. Avoid strictly columnar or binary input formats. Dont insist on interactive input.

# Uniform interace

- If we expect output of program to become the input to another program this means those programs must use same data format, (i.e.) a compatible interface.

- If we want to connect any programs output to any programs input that means all programs must have same input/output.

- In unix that interface is a file (or more precisely a ``file descriptor``) 

- A file is just an ordered sequence of bytes, Because it is a simple interface many things can be represented using the same interface. An actual file on the system, a communication channel or another process.

- Unix socket , stdin , stdout  device driver a socket representing a TCP connection etc.

## Seperation of Logic and wiring

- Another characterstic is their use of standard input(stdin) and standard output(stdout)

- If we run a program and dont message any input , the default stdin comes from keyboard and default stdout goes to the screen.

- However we can take input from a file and redirect output to a file. Pipe lets us attach the stdout of one process to stdin of another process.

- It is upto us to wire which file descriptor acts as stdin and which acts as stdout.


