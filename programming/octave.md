
# Octave

## Using the prompt

Elementary math & logical operations:

```octave
> 1+2
3

> 2^3
8

> 1 == 2
ans = 0

> 1 && 2
ans = 0

> xor(1,0)
```

Change the prompt:

```octave
PS1('>> ')
```

Variables:

```octave
> a = 3
> a
3

> b = 'hi'
> b
'hi'

> a = pi
> a
3.1416

> disp(sprintf('6 decimals: %0.6f', pi))
6 decimals: 3.141593

% get list of variables defined
> whos

% remove a variable
> clear a

% remove all variables
> clear
```

Vectors and matrices:

```octave
% 3x3 matrix
> A = [1 2; 3 4; 5 6]
> size(A)
ans =

   3   3

% Vector
> v = [1; 2; 3]
> length(v)
ans = 3

% 1x3 random matrix
> w = rand(1,3)
> w
ans =

   0.152253   0.329972   0.921088
   0.062060   0.911577   0.560723
   0.756555   0.743394   0.426702
```

Indexing operations:

```octave
> A = [1 2; 3 4; 5 6]
A =
   1  2
   3  4
   5  6

> A(2,:)
ans =
    3   4

> A(:,2)
ans =
    2
    4
    6

> A([1 3], :)
ans =
  1   2
  5   6

% replace the second column
> A(:,2) = [10; 11; 12]
A =
    1   10
    3   11
    5   12

% Add a new vector to the matrix
> A = [A, [100; 101; 102]]

% put all elements of A into single vector
> A(:)

% concat two matrices
> B = [11 12; 13 14; 15 16]
> C = [A B]

% Or put them on top of eachother
> C = [A; B]
```

Histogram:

```octave
> hist(w)
```

Identity matrices:

```octave
> eye(3)
ans =

Diagonal Matrix

   1   0   0
   0   1   0
   0   0   1
```

## Moving Data Around

Navigating in the filesystem:

```octave
> pwd
/home/azer

> ls
machine-learning dotfiles .config

> cd machine-learning
> load('features.dat')
```

Saving changes:

```octave
> save('hello.mat')

% save in human readable format;
> save('hello.txt') -ascii
```
