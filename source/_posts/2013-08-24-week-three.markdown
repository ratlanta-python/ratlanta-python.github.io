---
layout: post
title: "Week Three"
date: 2013-08-19 19:00
comments: true
categories: strings dictionaries lists formatting
---
In this week's class, we covered:

* Lists, re-visited
* Dictionaries
* String formatting

Lists
-----

To review, lists in Python are ordered collections of objects (such as strings or numbers). Declaring a list is easy:

```python
geeks = ['Jim', 'Chad', 'Cody', 'Nic', 'Rader']
```


To add an element to the end of a list:

```python
geeks.append('Josh')
print geeks
```
	['Jim', 'Chad', 'Cody', 'Nic', 'Rader', 'Josh']


To insert an element at the beginning of a list:
	
```python
geeks.insert(0, 'Tony')
print geeks
```
	['Tony', 'Jim', 'Chad', 'Cody', 'Nic', 'Rader', 'Josh']

Copy a list:

```python
all_geeks = list(geeks)
print all_geeks
```
	['Tony', 'Jim', 'Chad', 'Cody', 'Nic', 'Rader', 'Josh']


To remove an element from a list:

```python
geeks.remove('Jim')
print geeks
```
	['Tony', 'Chad', 'Cody', 'Nic', 'Rader', 'Josh']

You may also remove an element from a list using the `del` function and specifying a position in the list. For example, to remove the first element:

```python
del(geeks[0])
print geeks
```
	['Chad', 'Cody', 'Nic', 'Rader', 'Josh']

Python, like many languages, starts counting at zero. So the first element in a list has index `0`, the second index `1`, and so one. `-1` represents the last element in a list; `-2` the second-to-last, etc.

```python
print geeks[0], geeks[1], geeks[-1], geeks[-2]
del(geeks[1])
print geeks
```
	Chad Cody Josh Rader
	['Chad', 'Nic', 'Rader', 'Josh']

We have gotten rid of a bunch of our geeks. Fortunately, we made a copy of our list of geeks earlier, so let's make a copy of that copy, assign all the geeks' names to `geeks` once again:

```python
geeks = list(all_geeks)
```

We discussed a few ways to put two lists together. One common way is using the `+` (plus) operator:

```python
freaks = ['Frankenstein', 'Waffleman', 'Swampthing']
freaks_and_geeks = geeks + freaks
print 'geeks: %s' % geeks
print 'freaks: %s' % freaks
print 'freaks and geeks: %s' % freaks_and_geeks
```
	geeks: ['Chad', 'Nic', 'Rader', 'Josh']
	freaks: ['Frankenstein', 'Waffleman', 'Swampthing']
	freaks and geeks: ['Chad', 'Nic', 'Rader', 'Josh', 'Frankenstein', 'Waffleman', 'Swampthing']

Using `+` is useful when we want to assign the combined list to a new variable. But we can also `extend` a list, adding another list to it and changing the original list:

```python
nerds = ['Urkel', 'Alfred E. Neuman']
geeks.extend(nerds)
print geeks
```
	['Tony', 'Jim', 'Chad', 'Cody', 'Nic', 'Rader', 'Josh', 'Urkel', 'Alfred E. Neuman']

Wait, what are those last two guys doing in there? They don't belong. Let's get rid of them. You can delete multiple elements at a time:

```python
del(geeks[-2:])
print geeks
```
	['Tony', 'Jim', 'Chad', 'Cody', 'Nic', 'Rader', 'Josh']

Recall that `[-2]` refers to the second-to-last element in a list. So `del(geeks[-2:])` means, delete elements in `geeks`, starting from the second-to-last element and going to the end of the list. If we omitted the colon (i.e., `del(geeks[-2])`), that would mean delete the second-to-last element and stop there; don't delete to the end of the list. Urkel would have been yanked, but Alfred E. Neuman would have remanded.

### List Comprehensions

List comprehensions are a powerful construct in Python that let you concisely create a new list from an existing list. 

To create a list, `upper_geeks`, with the values of `geeks` converted to upper case, you could loop over them like this:

```python
# There's a better way!
upper_geeks = []  # create an empty list
for geek in geeks:
	upper_geeks.append(geek.upper())
```

The list comprehension version is shorter and more "Pythonic":
```python
upper_geeks = [geek.upper() for geek in geeks]
```

Here's a list comprehension for the squares of the numbers zero through nine:
```python
squares = [x ** 2 for x in range(10)]
print squares
```
	[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

Dictionaries
------------

Dictionaries in Python are a data collection to maps one object (the key) to another object (the value). (In other languages, these are called associative arrays, hashes, maps, etc.) You could use this to map the states' two letter abbreviates to their names, or geeks to their ages:

```python
geek_ages = {'Jim': 37, 'Chad' : 37, 'Cody': 26, 'Rader': 28, 'Nic': 21, 'Josh': 25, 'Tony': 26}
```

Curly brackets (`{}`) are used to declare dictionaries. A key comes before a colon (`:`), and the value after the colon. A comman (`,`) is used to separate key:value pairs. 

In the example above, the keys are strings, so we put them in quotes, and the values are numbers (integers, specifically), so we did not use quotes for the values.

To retrieve a value for a key, use square brackets (`[]`), like you do to access an element from a list. Instead of the index (0, 1, 2, etc.), put the key in the brackets:

```python
codys_age = geek_ages['Cody']  # gets value 26
```
 
You can change the value of an item in a dictionary (for example, if someone has a birthday):

```python
geek_ages['Rader'] = 29
```

A short-hand way to add one to an existing value is the `+=` operator:

```
geek_ages['Nic'] += 1  # Nic's age goes from 21 to 22
```

A element can be added to a dictionary by assigning a value to a key that doesn't yet exist:

```python
geek_ages['Ethan'] = 9
```

Ethan isn't yet old enough to have a beer. We better get him out of here:

```python
del(geek_ages['Ethan'])
```

Looping over the keys in a dictionary is easy:

```python
for name in geek_ages:
	print name
```

If you want to loop over the values instead:

```python
for age in geek_ages.values():
	print age
```

What if you want to the key and values? You could do the following, but there's a better way:

```python
# Not the easiest way to do this
for name in geek_ages:
	age = geek_ages[name]
	print '{0} is {1} years old'.format(name, age)
```

The better, simpler, and more "Pythonic" way uses the `items()` method of the `Dictionary` class:

```python
for name, age in geek_ages.items():
	print '{0} is {1} years old'.format(name, age)
```

You can use list comprehensions with a dictionary. What's will be the result, a list or a dictionary? Let's try:

```python
geek_names_and_ages = ['{} is {} years old'.format(name,age)
						for name, age in geek_ages.items()]
print geek_names_and_ages
```
	['Rader is 28 years old', 'Chad is 37 years old', 'Nic is 21 years old', 'Jim is 37 years old', 'Josh is 25 years old', 'Tony is 26 years old', 'Cody is 26 years old']

It's a list; note the square brackets instead of curly brackets. This makes sense: A list comprehension always makes a list.

Is there such a thing a dictionary comprehesion? Starting with Python 2.7, there is:

```python
geek_ages_next_decade = {name: 10 + age for name, age in geek_ages.items()}
print geek_ages_next_decade
```
	{'Rader': 38, 'Chad': 47, 'Nic': 31, 'Jim': 47, 'Josh': 35, 'Tony': 36, 'Cody': 36}

We're getting old, my friends!


String Formatting
-----------------

If you've been paying close attention, you've already seen two ways to format strings in examples above: Using the percent (`%`) character, and using the `String.format()` method. While the latter is the prefered way, the former has been around in Python for longer, so you'll still see it used frequently. Thus, it's useful understanding so you can read others' code.

The example below shows both the `%` and `format()` ways of formatting strings:

```python
name = 'Jim'
age = 37
print '%s is %d years old.' % (name, age)
print '{} has been alive for {} years.'.format(name, age)
print 'About {1} years ago, {0} was born.'.format(name, age)
```
	Jim is 37 years old
	Jim has been alive for 37 years
	About 37 years ago, Jim was born

Notice in the first two `print` statements, the arguments are given in the same order as they appear in the string: first `name` and then `age`. On line 5, however, the order of the arguments is different than the order they appear in the printed string. This is because the placeholders (`{1}` and `{0`}) refer to, respectively, the second and first arguments to `format()` (arguments, like elements in a list, are numbered starting at zero).

The `format()` method allows the same argument to appear multiple places in a string. See the example below:

```python
name = 'Jim'
beverage = 'beer'
print "{0}'s favorite beverage is {1}. Here's your {1}, {0}!".format(name, beverage)
```
	Jim's favorite beverage is beer. Here's your beer, Jim!

To do the same thing with `%s`, you'd have to list the arguments twice each:

```python
print "%s's favorite beverage is %s. Here's your %s, %s!" % (name, beverage, beverage, name)
```
	Jim's favorite beverage is beer. Here's your beer, Jim!

The `format()` method allows you to do other things that you can't do as easily, or at all,  with `%`. For example, if you want to display a list of items on a check and their prices, with two decimal places each, neatly aligned, here's how to do so with `format()`:

```python
check = {'water': 0, 'beer': 4.95, 'hamburger': 6.50, 'steak': 18.95, 'glen garioch whiskey': 2600 }
for item, price in check.items():
	print '{0:22} {1:8,.2f}'.format(item.title(), price)

print '-' * 31
total = sum(check.values())
print '{0:22} {1:8,.2f}'.format("Total", total)
```
	Water                      0.00
	Glen Garioch Whiskey   2,600.00
	Beer                       4.95
	Steak                     18.95
	Hamburger                  6.50
	-------------------------------
	Total                  2,630.40

The first placeholder, `{0:22}`, tells Python to print the item name in a field 22 characters wide. The second place holder, `{1:8,.2f}`, tells Python to print the price in a field 8 characters wide, to include commas to separate thousands, to include two decimal points, and to format the number as a floating-point (`f`).

For more information on how to format strings using the `format()` method, see the [Python language documentation](http://docs.python.org/2/library/string.html#format-specification-mini-language).

Also demonstrated in that example is the `sum()` function which, you guessed it, gives the sum of a list of numeric values.
