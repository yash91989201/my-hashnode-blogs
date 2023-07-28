---
title: "Operations on python data structures for DevOps engineers (Part - 1)"
seoTitle: "Python Data Structures for DevOps: Part 1"
seoDescription: "Master Python data structures in DevOps: learn list, set, comprehension, conditionals. Enhance skills, optimize code, boost efficiency"
datePublished: Fri Jul 28 2023 18:27:00 GMT+0000 (Coordinated Universal Time)
cuid: clkmx0yft000809lh0qkj0ibe
slug: operations-on-python-data-structures-for-devops-engineers-part-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690568740358/c5adb964-a40e-466d-b37e-6aaa8c1461d8.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1690568792840/14b4b99c-5e34-45d4-ae1e-a9e85d34b5ca.png
tags: python, devops, 90daysofdevops, trainwithshubham, tws

---

## **📍** Introduction:

Hey there, friends! Following our fun introduction to Python and its data types, we've got another exciting ✨🎉 blog for you. This time, we'll explore the various operations you can perform on Python's different data structures. If you're looking for a quick refresher on Python basics, feel free to check out my previous blog post right here [https://yashraj-jaiswal.hashnode.dev/introductory-python-guide-for-devops-engineers](https://yashraj-jaiswal.hashnode.dev/introductory-python-guide-for-devops-engineers). Enjoy!

## ✔ Python list operations:

A list is a data structure in Python that is a mutable, or changeable, ordered sequence of elements. Each element or value that is inside a list is called an item. Let's see what all operations can be performed on a list:

```python
# creating a list 
list_of_fruits=["apple","banana","kiwi","orange","mango","guava"]
# index is the numbering of elements in a list starting 
# from the left most element and index starts from 0 
```

1. **Accessing list elements:** when accessing specific elements from a list we can use its index number.
    
    ```python
    # access item at index 3
    print(list_of_fruits[3])
    #access item at last index
    print(list_of_fruits[len(list_of_fruits)-1])
    
    output:
    orange
    guava
    ```
    
2. **Negative indexing:** In Python, we also have a concept of negative indexes which means the last element is -1, the last second element is -2 and so on.
    
    ```python
    #accessing the last item
    print(list_of_fruits[-1])
    print(list_of_fruits[-2])
    
    output:
    guava
    mango
    ```
    
3. **List slicing:** In Python, we can access specific items from a list by using the slice operator `:`
    
    ```python
    # items from index 2 to 5
    print(list_of_fruits[2:5])
    # items from index 3 to the end
    print(list_of_fruits[3:])
    
    output:
    ['kiwi', 'orange', 'mango']
    ['orange', 'mango', 'guava']
    ```
    
4. **Adding elements:** Lists are mutable (ie they can be changed when required). Different list methods allow adding or removing elements from a list.
    
    ```python
    # append method
    list_of_fruits.append("litchi")
    new_list_of_fruits=["musk melon","dragon fruit","grapes"]
    #extend method
    list_of_fruits.extends(new_list_of_fruits)
    print(list_of_fruits)
    #insert method - insert element at index 1 i.e second position
    list_of_fruits.insert(1,"pear")
    
    output:
    ['apple', 'banana', 'kiwi', 'orange', 'mango', 'guava', 'litchi', 'musk melon', 'dragon fruit', 'grapes']
    ['apple', 'pear', 'banana', 'kiwi', 'orange', 'mango', 'guava', 'litchi', 'musk melon', 'dragon fruit','grapes']
    ```
    
5. **Changing list elements:** If we want to assign a new value to an element at a specific index we can use the assignment operator.
    
    ```python
    # change the last element to watermelon
    list_of_fruits[-1] = "watermelon"
    print(list_of_fruits)
    
    output:
    ['apple', 'pear', 'banana', 'kiwi', 'orange', 'mango', 'guava', 'litchi', 'musk melon', 'dragon fruit', 'watermelon']
    ```
    
6. **Removing elements:** To remove elements from the list in Python there are many ways.
    
    ```python
    # delete element at a specific index
    del list_of_fruits[2]
    # delete the last item
    del list_of_fruits[-1]
    # delete all elements after index 5
    del list_of_fruits[5:]
    
    output:
    ['apple', 'pear', 'kiwi', 'orange', 'mango']
    ```
    
7. **Iterating through a list:** To act with every element of a list we can use loops.
    
    ```python
    # iterate through a list using for loop 
    for fruit in list_of_fruits:
        print(fruit)
    
    output:
    apple
    pear
    kiwi
    orange
    mango
    ```
    
8. **in** keyword**:** returns True or False base on if the specified element is present in the list or not.
    
    ```python
    # the in keyword can be used to check 
    #the existence of a specific element in a list
    print('kiwi' in list_of_fruits)
    print('guava' in list_of_fruits)
    
    output:
    True
    False
    ```
    

### 🔸 List comprehension:

* It is an elegant way to define and create lists based on existing lists.
    
* It is generally more compact and faster than normal functions and loops for creating lists.
    
* However, we should avoid writing very long list comprehensions in one line to ensure that the code is user-friendly.
    
* Remember, every list comprehension can be rewritten in for loop, but every for loop can’t be rewritten in the form of list comprehension.
    

```python
# without using list comprehension
limit=int(input("Enter a limit. "))
even_list=[]
for i in range(2,limit+1,2):
    even_list.append(i)
print(even_list)

output: 
[2, 4, 6, 8, 10, 12, 14, 16, 18, 20] 

# using list comprehension
limit=int(input("Enter a limit. "))
even_list=[i for i in range(2,limit+1,2)]
print(even_list)

output:
[2, 4, 6, 8, 10, 12, 14, 16, 18, 20] 
```

In the code above, you can see how we made a list of even numbers in two different ways - once without using list comprehension, and then with list comprehension. Both methods give us the same result, but list comprehension makes it a bit more concise and neat. 😊

### Conditional in list comprehension:

We can even include the if condition in a list comprehension, how cool is that. Let's see an example where we again take a limit from the user but create a list where numbers are divisible by 5.

```python
limit = int(input("Enter a limit. "))
num_list = [i for i in range(limit) if i % 5 == 0]
print(num_list)
```

## ✔ Python set operations:

A set is a collection of unique data, meaning that the elements within a set cannot be duplicated. For example, consider the following scenario:

If we want to store information about employee IDs and, since employee IDs must be unique, we can utilize a set to accomplish this task.

In Python, we create sets by placing all the elements inside curly braces {}, separated by a comma.

A set can have any number of items and they may be of different types (integer, float, tuple, string etc.). But a set cannot have mutable elements like lists, sets or dictionaries as its elements.

```python
# creating an integer type set
employee_id = {112, 113, 114, 115}
print('Employee ID:', employee_id)

student_id = {110,111,112,113}

# create a set of string type
vowels = {'a', 'e', 'i', 'o', 'u'}
print('Vowel Letters:', vowels)

# create a set of mixed data types
mixed_set = {'Hello', 101, -2, 'Bye',1.01}
print('Set of mixed data types:', mixed_set)

#trying to create a set with duplicate elements
duplicate_set={11,1,2,11,3,4,22}
print("Duplicate set:", duplicate_set)

output:
Employee ID: {112, 114, 115, 116, 118}
Vowel Letters: {'u', 'a', 'e', 'i', 'o'}
Set of mixed data types: {'Hello', 'Bye', 101, -50,1.01}
Duplicate set: {1, 2, 3, 4, 22, 11}
```

Sets are mutable. However, because they are unordered, indexing has no meaning. We cannot access or change an element of a set using indexing or slicing. The set data type does not support it.

1. **Adding items to a set:** we can use the add() method to add an item to a set.
    
    ```python
    employee_id.add(116)
    print(employee_id)
    
    output:
    {112, 113, 114, 115, 116}
    ```
    
2. **Updating a set:** The update() method is used to update the set with items of other collection types (lists, tuples, sets, etc).
    
    ```python
    new_employee_list=[116,117]
    employee_id.update(new_employee_list)
    print(employee_id)
    
    output:
    {112, 113, 114, 115, 116, 117}
    ```
    
3. **Remove element from a set:** To remove a specified element from a set we use the discard() method.
    
    ```python
    employee_id.discard(113)
    print(employee_id)
    
    output:
    {112, 114, 115, 116, 117}
    ```
    
4. **Iterate over a set:** we can use the for loop to iterate over set elements.
    
    ```python
    for id in employee_id:
        print(id)
    
    output:
    112
    114
    115
    116
    117
    ```
    
5. **Find the number of set elements:** we can use the len() method to find the number of elements in a set.
    
    ```python
    print(len(employee_id))
    
    output:
    5
    ```
    
6. **Union of two sets: the** union of two sets means creating a new set with the elements of both sets. We can use the `|` operator or the `union()` method to perform the union of two sets.
    
    ```python
    # | operator
    print('Union using |:', A | B)
    # union() method
    print('Union using union():', A.union(B)) 
    
    output:
    Union using |: {110, 111, 112, 113, 114, 115, 116, 117}      
    Union using union(): {110, 111, 112, 113, 114, 115, 116, 117}
    ```
    
7. **Intersection of two sets:** the intersection of two sets means creating a new set with the common elements from two given sets. We can use the `&` operator or the `intersection()` method to perform the intersection of two sets.
    
    ```python
    # & operator
    print('Intersection using &:', employee_id & student_id)
    # intersection() method
    print('Intersection using intersection():', employee_id.intersection(student_id))
    
    output:
    Intersection using &: {112}
    Intersection using intersection(): {112}
    ```
    
8. **Difference between two sets:** the difference between two sets means creating a new set with elements only from one of the two sets. We use the `-` operator or the `difference()` method to perform the difference between two sets.
    
    ```python
    # - operator
    print('Difference using &:', employee_id - student_id)
    # difference() method
    print('Difference using difference():', employee_id.difference(student_id))
    
    output:
    Difference using &: {114, 115, 116, 117}
    Difference using difference(): {114, 115, 116, 117} 
    ```
    
9. **Set symmetric difference:** The symmetric difference between two sets refers to creating a new set containing only the elements unique to each of the given sets, excluding any common elements between them. In Python, we use the ^ operator or the symmetric\_difference() method to perform symmetric differences between two sets.
    
    ```python
    # ^ operator
    print('Symmetric Difference using &:', employee_id ^ student_id)
    # symmetric_difference() method
    print('Symmetric Difference using symmetric_difference():',
          employee_id.symmetric_difference(student_id))
    
    Symmetric Difference using &: {110, 111, 113, 114, 115, 116, 117}
    Symmetric Difference using symmetric_difference(): {110, 111, 113, 114, 115, 116, 117}
    ```
    
10. **Check if two sets are equal:** We can use the `==` operator to check if two sets are equal or not.
    
    ```python
    print(employee_id == student_id)
    print({1,2} == {1,2})
    output:
    False
    True
    ```
    

## **📍** Conclusion:

In conclusion, it's super important to know how to work with different data structures in Python and how to manipulate them. But don't worry, we're not done yet! We still have to explore operations on tuples and dictionaries, which I'll be sharing with you tomorrow. So, keep practicing and have fun learning!