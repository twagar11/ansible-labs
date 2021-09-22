Learning the YAML syntax
------------------------

In this section, you will learn how to write a YAML file with the correct syntax and best practices and tips for running a playbook on multiple remote machines. Ansible uses YAML because it is easier
for humans to read and write than other common data formats, such as XML or JSON. There are no commas, curly braces, or tags to worry about, and the enforced indentation in the code ensures that it is
tidy and easy on the eye. In addition, there are libraries available in most programming languages for working with YAML.

Before you starting, inspect the original `JSON` file that we are going to convert to `YAML`

- Inspect [Employee.json](employees.json)

Let's explore the YAML language :

### Dictionaries

Dictionaries are another important concept in YAML---they are represented by a [key: value] format, as we have already extensively seen, but all the items in the dictionary are indented by one more
level. This is easiest explained by an example, so consider the following code:

```
    Family:
      son: John
      daughter: Jane
```

### Lists

Lists are an important construct in the YAML language---in fact, although it might not be obvious, A list in YAML lists all of its items at the same indentation level, with each line starting with [-]
. For example:

```
  - name: John
    children:
      name: Jane
      state: single
```

However, we could have specified a list of child names:

```
  - name: John
    apt:
      name:
        - Jane
        - Sarah
      state: single
```

Now, rather than passing a single value to the [name:] key, we pass a YAML-formatted list containing the names of two packages to be updated.

----

Already, we have observed in these two examples that you can produce quite complicated data structures by mixing lists and dictionaries.

As you become more advanced at playbook design (we will see examples of this later on in this course), you may very well start to produce quite complicated variable structures that you will put into
their own separate files to keep your playbook code readable.

The following is an example of a file that provides the details of two employees of a company:

- Inspect [Employee.yaml](employees.yml)

In this example, you can see that we have a dictionary containing the details of each employee. The employees themselves are list items (you can spot this because the lines start with [-]) and
equally, the employee skills are denoted as list items. You will notice the
[fullname], [role], [level], and [skills] keys are at the same indentation level as [name] but do not feature
[-] before them. This tells you that they are in the dictionary with the list item itself, and so they represent the details of the employee.

### Literal block

YAML is very literal when it comes to parsing the language and a new line always represents a new line of code. What if you actually need to add a block of text (for example, to a variable)? In this
case, you can use a literal block scalar, [\|], to write multiple lines and YAML will faithfully preserve the new lines, carriage returns, and all the whitespace that follows each line (note, however,
that the indentation at the beginning of each line is part of the YAML syntax):

```
Specialty: |
  Agile methodology
  Cloud-native app development practices
  Advanced enterprise DevOps practices
```

So, if we were to get Ansible to print the preceding contents to the screen, it would display as follows:

```
Agile methodology
Cloud-native app development practices
Advanced enterprise DevOps practices
```

### Folded block

Similar to the preceding is the folded block scalar, [\>], which does the same as the literal block scalar but does not preserve line endings. This is useful for very long strings that you want to
print on a single line, but also want to wrap across multiple lines in your code for the purpose of readability. Take the following variation on our example:

```
Specialty: >
  Agile methodology
  Cloud-native app development practices
  Advanced enterprise DevOps practices
```

Now, if we were to print this, we would see the following:

```
Agile methodologyCloud-native app development practicesAdvanced enterprise DevOps practices
```

We could add trailing spaces to the preceding example to stop the words from running into each other, but I have not done this here as I wanted to provide you with an easy-to-interpret example.

One additional example is provided in the following code block of a [variables] file for you to consider, which shows the various examples we have covered all in one place:

- Inspect [Employee With Blocks](employee.json)

## Practices

- Duration: 40 minutes

Convert the following `JSON` strings to a `YAML` file and verify it by (yamllint.com)[http://www.yamllint.com/]

- [First Practice](practice-1.json)
-
- [Second Practice](practice-2.json)

**NOTE:** Solution to the practice will be provided after instructor solves the problem.


- [First Practice - Solution](practice-1.yaml)
-
- [Second Practice - Solution](practice-2.yaml)