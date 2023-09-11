# Perl

## Variables

Creating a new public variable:

```perl
$var = "value";
```

Creating a new private variable:

```perl
my $var = "value";
```

Creating a new constant:

```perl
use constant PI => 3.14;
```

## Arrays

Creating a new array:

```perl
@arr = (1, 2, 3);
```

Adding an element to the end of the array:

```perl
push(@arr, 4);
```

Removing the last element from the array:

```perl
pop(@arr);
```

Remove an a element by index

```perl
splice(@arr, 1, 1);
```

Adding an element to the beginning of the array:

```perl
unshift(@arr, 0);
```

Removing the first element from the array:

```perl
shift(@arr);
```

Getting the length of the array:

```perl
$len = @arr;
```

Get elements by index

```perl
@arr[0, 1, 2];
```
