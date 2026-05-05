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
