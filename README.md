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

## Perl Regex

<details>
<summary><b><i>11.Check if the word `electroencefalografista` exists in a string.</i></b></summary>

$\color{green}{\text{Answer}}$

```Perl
my $string = "The longest accepted word by RAE is: electroencefalografista";
if ($string =~ /electroencefalografista/) {                                                         
    print "Match!";
}
```

</details>

<details>
<summary><b><i>12.Check if the word `electroencefalografista` does not exists in a string.</i></b></summary>

$\color{green}{\text{Answer}}$

```Perl
my $string = "The longest not accepted word by RAE is: Ciclopentanoperhidrofenantreno";
if ($string !~ /electroencefalografista/) {
    print "Does not match!";
}
```

</details>

<details>
<summary><b><i>13.Replace the word amazing.</i>,</b></summary>

$\color{green}{\text{Answer}}$

```Perl
my $string = "Perl is amazing!";
$string =~ s/amazing/incredible/;
print $string;
# Perl is incredible!
```

</details>

<details>
<summary><b><i>14.Extract `hh:mm:ss` with capturing group `()` in the following datetime</i></b></summary>

$\color{green}{\text{Answer}}$

```Perl
my $date = "Fri Nov 19 20:09:37 CET 2021";
my @matches = $date =~ /(.*)(\d{2}:\d{2}:\d{2})(.*)/;
print $matches[1];
# Output: 20:09:37
```

</details>

<details>
<summary><b><i>15.Extract all the elements that are numbers in an array.</i></b></summary>

$\color{green}{\text{Answer}}$

```Perl
my @array = ('a', 1, 'b', 2, 'c', 3);
my @numbers = grep (/\d/, @array);    # Note: \d involves more digits than 0-9
map {print $_ . "\n" } @numbers;
```

</details>

<details>
<summary><b><i>16.Print all the linux system users that starts with d or D.</i></b></summary>

$\color{green}{\text{Answer}}$

- With a Perl one liner:

    ```Perl
    open(my $fh, '<', '/etc/passwd');
    my @user_info = <$fh>;
    map { print $& . "\n" if $_ =~ /^d([^:]*)/  } @user_info;
    close $fh;
    ```

- Avoiding one-liners:

    ```Perl
    foreach my $user_line (@user_info) {
        if ($user_line =~ /^d([^:]*)/) {
            print $& . "\n";
        }
    }
    ```

</details>

## Perl Files Handle

<details>
<summary><b><i>17.Mention the different modes in File Handling.</i></b></summary>

$\color{green}{\text{Answer}}$

- Read only: `<`
- Write mode. It creates the file if doesn't exist: `>`
- Append mode. It creates the file if doesn't exist: `>>`
- Read and write mode: `+<`
- Read, clear and write mode. It creates the file if doesn't exist: `+>`
- Read and append. It creates the file if doesn't exist: `+>>`

</details>

<details>
<summary><b><i>18.How to write into a file?</i></b></summary>

$\color{green}{\text{Answer}}$

```Perl
# We can use:
# '>' Write (it clears a previous content if exists).
# '>>' Append.
open(my $fh, '>>', 'file_name.ext') or die "Error: file can't be opened";
print $fh "writing text...\n";
close($fh);
```

</details>

<details>
<summary><b><i>19.How can you read a file and print every line?</i></b></summary>

$\color{green}{\text{Answer}}$

```Perl
open(my $fh, '<', 'file_to_read.ext') or die "Error: file can't be opened";
my @file = <$fh>;
foreach my $line (@file) {
    print $line;
}
```

We can use the file handle without assigning it to an array:

```Perl
open(my $fh, '<', 'file_to_read.ext') or die "Error: file can't be opened";

foreach my $line (<$fh>) {
    print $line;
}
```

</details>

## Perl OOP

<details>
<summary><b><i>20.Does Perl have support for OOP?</i></b></summary>

$\color{green}{\text{Answer}}$

"By default, Perl's built-in OO system is very minimal, leaving you to do most of the work."

</details>

<details>
<summary><b><i>21.What is the purpose of the bless function?</i></b></summary>

$\color{green}{\text{Answer}}$

The function os the bless function is used to turning a plain data structure into an object.

</details>

<details>
<summary><b><i>22.How to create a Perl class? How can you call a method?</i></b></summary>

$\color{green}{\text{Answer}}$

- Let's create the package: `Example.pm`

  ```Perl
  package Example;

  sub new {
    my $class = shift;
    my $self = {};
    bless $self, $class;
    return $self;
  }

  sub is_working {
    print "Working!";
  }

  1;

- Now we can instance the Example class and call is_working method:

  ```Perl
  my $e = new Example();
  $e->is_working();
  # Output: Working!
  ```

</details>

<details>
<summary><b><i>23.Does Perl have inheritance? What is the `SUPER` keyword?</i></b></summary>

$\color{green}{\text{Answer}}$

Yes, Perl supports inheritance. `SUPER` keyword is used to call a method from the parent class. It gives an example about how we can apply inheritance.

</details>

<details>
<summary><b><i>24.Does Perl have polymorphism? What is method overriding?</i></b></summary>

$\color{green}{\text{Answer}}$

Yes, it has polymorphism. In fact method overriding is a way to apply it in Perl.

Method overriding in simple words appears when we have a class with a method that already exist in a parent class.

```Perl
package A;

sub new { return bless {}, shift; };
sub printMethod { print "A\n"; };

package B;

use parent -norequire, 'A';

sub new { return bless {}, shift; };
sub printMethod { print "B\n"; };

my $a = A->new();
my $b = B->new();

A->new()->printMethod();
B->new()->printMethod();

# Output:
# A
# B
```

</details>

<details>
<summary><b><i>24.How can you call a method of an inherited class?</i></b></summary>

$\color{green}{\text{Answer}}$

```Perl
# Class `A` with `printA` method.
package A;

sub new { return bless {}, shift; };
sub printA { print "A"; };

# Class `B` that extends or use the parent class `A`.
package B;

use parent -norequire, 'A';

sub new { return bless {}, shift; };

# Instance class `B` allows call the inherited method
my $b = B->new();
$b->printA();
```

</details>

## Perl Exception Handling

<details>
<summary><b><i>25.How can we evaluate and capture an exception in Perl?</i></b></summary>

$\color{green}{\text{Answer}}$

`eval` in all its forms is used to execute a little Perl program, trapping any errors encountered so they don't crash the calling program.

Eg:
```Perl
eval {
    die;
};
if ($@) {
    print "Error. Details: $@";
}
```

If we execute this we get the next output:

```Perl
Error. Details: Died at eval.pl line 2.
```

The `eval` (`try` in another programming languages) is trying to execute a code. This code fails (it's a die), and then the code continues into the `if` condition that evaluates `$@` error variable have something stored. This is like a `catch` in another programming languages. At this way we can handle errors.

## Perl OS

<details>
<summary><b><i>26.What is Perl Open3?</i></b></summary>

$\color{green}{\text{Answer}}$

"IPC::Open3 - open a process for reading, writing, and error handling using open3()".

With `open3` we can have the full control of the STDIN, STDOUT, STDERR. It's usually used to execute commands.

</details>

<details>
<summary><b><i>27.Using Open3: Create a file with the size of 15MB and check it's created successfully.</i></b></summary>

$\color{green}{\text{Answer}}$

- Code:

```Perl
use IPC::Open3;
use Data::Dumper;

sub execute_command {
    my @command_to_execute = @_;
    my ($stdin, $stdout, $stderr);
    eval {
        open3($stdin, $stdout, $stderr, @command_to_execute);
    };
    if ($@) {
        print "Error. Details: $@";
    }
    close($stdin);
    return $stdout;
}

my $file_name = 'perl_open3_test';
&execute_command('truncate', '-s', '15M', $file_name);
my $result = &execute_command('stat', '-c', '%s', $file_name);
print Dumper(<$result>);
```

- Result:

```Perl
$ -> perl command.pl 
$VAR1 = '15728640
';
```

</details>

## Perl Packages & Modules

<details>
<summary><b><i>28.What is a Perl package? And a module?</i></b></summary>

$\color{green}{\text{Answer}}$

With a Perl package we are defining a namespace. A Perl module in one simple word can be defined as a `class`. When we create a `class` in Perl we use the `package` keyword. A module can be used with the use keyword.

</details>

<details>
<summary><b><i>29.What is the difference between .pl and .pm extensions?</i></b></summary>

$\color{green}{\text{Answer}}$

There's no a real difference between a .pm and .pl extensions. Perl use .pm extensions just to difference it as a perl module (a class). .pl extensions are usually named for perl scripts without OOP classes.

</details>

<details>
<summary><b><i>30.Why a Perl class (or module) should return something at the end of the file? Check the example.</i></b></summary>

$\color{green}{\text{Answer}}$

If we want to `use` a Perl module (`import` a class), this module should end in a value different than 0. This is necessary because if we try to import the class and it has a false value, we will not be able to use it.

```Perl
package A;

sub new { return bless {}, shift; };
sub printMethod { print "A\n"; };

1;
```

<details>
<summary><b><i>31.What is cpan? And cpanm?</i></b></summary>

$\color{green}{\text{Answer}}$

- CPAN (Comprehensive Perl Archive Network) is a massive, centralized repository containing over 200,000 modules of open-source Perl code written by thousands of contributors. It serves as the primary ecosystem for Perl developers to find, share, and reuse libraries for everything from database integration and web development to advanced mathematics and system administration.

- cpanm (App::cpanminus) is a popular, lightweight command-line client used to install modules from CPAN. Unlike the traditional CPAN shell, it is designed to be "zero-config," extremely fast, and memory-efficient. It automates the process of downloading, unpacking, building, and installing modules and their dependencies with minimal output, making it the preferred tool for modern Perl development and automated deployment environments.

</details>

<details>
<summary><b><i>32.How can you install cpanm and a Perl module?</i></b></summary>

There are some different alternatives to install Perl modules. We will use `cpanm.`

- Install `cpanm`:

```Perl
$ cpan App::cpanminus
```

- Install the `Test` module with `cpanm`:

```Perl
cpanm Test
```

- Now we can test the `Test` installed module:

```Perl
$ perl -M'Test::Simple tests => 1' -e 'ok( 1 + 1 == 2 );'
1..1
ok 1
```

```Perl
$ perl -M'Test::Simple tests => 1' -e 'ok( 1 + 1 == 3 );'
1..1
not ok 1
#   Failed test at -e line 1.
# Looks like you failed 1 test of 1.
```
