# Perl-for-DevOps-Engineers

![Perl](https://img.shields.io/badge/perl-%2339457E.svg?style=for-the-badge&logo=perl&logoColor=white)

![](Perl.png)

## Perl Self Assessment

<details>
<summary><b><i>1.What is Perl?</i></b></summary>

$\color{green}{\text{Answer}}$

It's a general purpose programming language developed for manipulating texts mainly. It has been used to perform system administration tasks, networking, building websites and more.

</details>

<details>
<summary><b><i>2.What data types Perl has? And how can we define it?</i></b></summary>

$\color{green}{\text{Answer}}$

- Scalar: This is a simple variable that stores single data items. It can be a string, number or reference.

```Perl
my $number = 5;
```

- Arrays: This is a list of scalars.

```Perl
my @numbers = (1, 2, 3, 4, 5);
# or using the `qw` keyword (quote word):
my @numbers = qw/1 2 3 4 5/; 
# '/' can be another symbol, e.g qw@1 2 3 4 5@
```

- Hashes (or associative arrays): This is an unordered collection of key-value pairs. We can access to a hash using the keys.

```Perl
my %numbers = (
  First => '1',
  Second => '2',
  Third => '3'
);
```

</details>

<details>
<summary><b><i>3.How can you access to a hash value, add and delete a key/value pair and modify a hash?</i></b></summary>

$\color{green}{\text{Answer}}$

```Perl
my %numbers = (
  'First' => '1',
  'Second' => '2',
  'Third' => '3'
);
```

- Access:

```Perl
print($numbers{'First'});
```

- Add:

```Perl
$numbers{'Fourth'} = 4;
```

- Delete:

```Perl
delete $numbers{'Third'};
```

- Modify:

```Perl
$numbers{'Fifth'} = 6;
$numbers{'Fifth'} = 5;
```

</details>

<details>
<summary><b><i>4.How can you iterate an array? And a hash?</i></b></summary>

$\color{green}{\text{Answer}}$

- Array:

```Perl
my @numbers = qw/1 2 3 4 5/;

# Using `$_` that represents the current iteration in a loop. It starts from index array 0 until the last index.
foreach (@numbers) {
    print($_);
}
# Output: 12345


# "$#" returns the max index of an array. That's the reason because we can iterate accessing to the array from the index 0 to the max index.
for my $i (0..$#numbers) {
    print($numbers[$i]);
}
# Output: 12345


# Using the `map` keyword:
print map {$_} @numbers;
# Output: 12345

# Using `while`. We should take care with this option. When we use `shift` we're deleting the first element of the array and assigning it to the `element` variable. 
# After this `loop` the `numbers` array will not have elements.
while (my $element = shift(@numbers)) {
    print($element);
}
# Output: 12345
```

- Hashes:

```Perl
my %capital_cities = (
 'Madrid' => 'Spain',
 'Rome' => 'Italy',
 'Berlin' => 'Germany'
);

# Iterate and get the `keys`:
foreach my $city (keys %capital_cities) {
   print($city . "\n");
}
# Iterate and get the `values`:
foreach my $country (values %capital_cities) {
   print($country . "\n");
}

# Iterate and get the values and keys (first option):
foreach my $city (keys %capital_cities) {
   print("City: $city - Country: $capital_cities{$city}" . "\n");
}

# Iterate and get the values and keys (first option):
while(my ($city, $country) = each %capital_cities) {
   print("City: $city - Country: $capital_cities{$city}" . "\n");
}
```

</details>

<details>
<summary><b><i>5.What is a Perl subroutine? How to define it?</i></b></summary>

$\color{green}{\text{Answer}}$

It's the perl model for user defined functions (this is also called function like other programming languages). We can define a subroutine with the keyword `sub`.

```Perl
sub hello {
  print "hello";
}
```

</details>

<details>
<summary><b><i>6.Describe the different ways to receive parameters in a subroutine</i></b></summary>

$\color{green}{\text{Answer}}$

- List assignment: Using the `@_` array. It's a list with the elements that are being passed as parameters.

```Perl  
sub power {
    my ($b, $e) = @_;
    return $b ** $e; 
}

&power(2, 3);
```

- Individual assignment: We should access to every element of the `@_` array. It starts from zero.

```Perl
sub power {
    my $b = $_[0];
    my $e = $_[1];
    return $b ** $e; 
}

&power(2, 3);
```

- Using `shift` keyword: It's used to remove the first value of an array and it's returned.

```Perl
sub power {
    my $b = shift;
    my $3 = shift;
    return $b ** $e; 
}

&power(2, 3);
```

</details>

<details>
<summary><b><i>7.What is lexical and dynamic scoping?</i></b></summary>

$\color{green}{\text{Answer}}$

- Lexical scoping (also known as static scoping) is the default for variables declared with `my`. These variables are visible only within the specific block of code, file, or subroutine where they are defined, regardless of which functions are called from within that block. This provides a predictable environment where the variable's "neighborhood" is determined entirely by the physical layout of the source code.

- Dynamic scoping is achieved using the `local` keyword, which temporarily shadows a global variable's value for the duration of the current block and any subroutines called from it. Unlike lexical scoping, the value of a `local` variable depends on the call stack (the order in which functions are executed) rather than the physical location of the code. Once the block finishes, the original value of the global variable is automatically restored.

</details>

<details>
<summary><b><i>8.How to apply referencing and dereferencing?</i></b></summary>

$\color{green}{\text{Answer}}$

- Referencing: Creating the Link

  To create a reference, you use the backslash operator (`\`) on an existing variable. This creates a scalar that "points" to the memory location of that variable. You can also create anonymous references directly using square brackets for arrays or curly braces for hashes.

   - From variables:
   
   ```Perl
   $scalar_ref = \$name;
   ```

   ```Perl
   @array_ref = \@list;
   ```
   
   - Anonymous:
   ```Perl
   $array_ref = [1, 2, 3];
   ```

   ```Perl
   $hash_ref = { key => 'value' };
   ```

- Dereferencing: Accessing the Data

  Dereferencing tells Perl to "follow the pointer" to get to the underlying value. There are two primary ways to do this:

  - Sigil Prefixing: Use the appropriate sigil (`$`, `@`, `%`) in front of the reference variable.

     ```Perl
     $value = $$scalar_ref; (Access a scalar)
     ```

     ```Perl
     @values = @$array_ref; (Access a whole array)
     ```

  - The Arrow Operator (`->`): This is the most common and readable method for accessing specific elements.

     ```Perl
     $item = $array_ref->[0]; (Access array element)
     ```

     ```Perl
     $val = $hash_ref->{'key'}; (Access hash value)
     ```

</details>

<details>
<summary><b><i>9.Does Perl have conventions?</i></b></summary>

$\color{green}{\text{Answer}}$

Yes, Perl is famous for its flexibility, but it follows several core conventions to keep code readable and maintainable.

1. The Golden Rule
    - TIMTOWTDI: "There Is More Than One Way To Do It." This is the Perl motto, emphasizing flexibility over a single "correct" style.

2. Standard Naming & Formatting
    - Snake Case: Use lowercase with underscores for variables and subroutines (e.g., `$user_name`).

    - Indentation: Most Perl developers use 4 spaces per level.

    - Braces: The "K&R" style is standard (opening brace on the same line as the keyword).

3. Best Practices (Modern Perl)
    - The "Preamble": Always start scripts with `use strict;` and `use warnings;`. This forces you to declare variables and catches common mistakes.

    - Lexical Scoping: Prefer `my` for all variable declarations.

    - Internal Documentation: Use POD (Plain Old Documentation) within your code to explain how it works.

4. File Extensions
    - `.pl` for scripts.

    - `.pm` for modules.

    - `.t` for test files.

</details>

<details>
<summary><b><i>10.What is Perl POD? Can you code an example?</i></b></summary>

$\color{green}{\text{Answer}}$

Perl POD is a simple-to-use markup language used for writing documentation for Perl, Perl programs, and Perl modules.

```Perl
=item
    This function returns the factorial of a number.
    Input: $n (number you wanna calculate).
    Output: number factorial.
=cut
sub factorial {
    my ($i, $result, $n) = (1, 1, shift);
    $result = $result *= $i && $i++ while $i <= $n;
    return $result;
}
```

</details>
