---
title: "👉 Introductory Python Guide for DevOps Engineers."
seoTitle: "Python Intro Guide: DevOps Engineers"
seoDescription: "Master DevOps Python with this guide on data types, type conversion, and non-primitive structures for effective scripting and automation"
datePublished: Thu Jul 27 2023 18:12:36 GMT+0000 (Coordinated Universal Time)
cuid: clklh2l0900080amf3hve8kfw
slug: introductory-python-guide-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690481517806/80b7f124-0956-45a1-b2cf-9a764ab9f354.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1690481502975/0d95d758-e74c-4473-9846-56c93003d076.png
tags: python, devops, 90daysofdevops, trainwithshubham, tws

---

## **📍** Introduction:

Hey there, readers! After covering various concepts that lay a solid foundation for a DevOps engineer, we will now delve into Python. This programming language is incredibly useful for DevOps engineers, as they often need to write scripts to automate tasks.

Python is a popular programming language. It was created by Guido van Rossum, and released in 1991. It is mainly used for server-side scripting, software development and system scripting.

## ✔ Data types in Python:

Data types are an important concept in programming, as they define the type of data that a variable can store. Python is a dynamically typed language, which means that the data types of variables are checked at runtime i.e when the program is being executed.

When categorizing data types in python there are two types:

When categorizing data types in Python, there are two types:

1. **Primitive data type:** A primitive data type is predefined by the programming language. The size and type of variable values are specified.
    
2. **Non-primitive data type:** The non-primitive data types instead of storing just a single value, store a collection of values in various formats.
    

## ✔ Primitive Data types in Python:

There are 4 primitive data types in Python:

1. **integer:** This is used to store whole numbers i.e. all the negative and positive values but without decimal points. for example -1, 2, 10 1345, -234 etc.
    
2. **float:** This is used to store negative or positive decimal numbers. for example, -2.45, 5.62, 250.0 etc
    
3. **string:** any character typed between a set of single, double or triple quotes is a string. for example: 'A', "hello", ''' this is a string.''
    
4. **boolean:** a boolean variable only contains two values ie True or False, keep in mind that the case matters here.
    

In Python, we can also use the **type()** method to check the data type of a variable.

Here's an example demonstrating the primitive data types in Python:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690472980106/1ecc37ba-f461-4b26-9489-7987b9dd55f3.png align="center")

### 🔸 Type conversion in Python:

In programming, type conversion refers to the process of converting data from one type to another. For instance, converting integer data to a string.

There are two types of type conversion in Python:

1. **Implicit type conversion:** when the data type conversion takes place during compilation or the runtime, it’s called an implicit data type conversion. Python handles the implicit data type conversion, so we don’t have to explicitly convert the data type into another data type.
    
    ```python
    a = 5
    b = 5.5
    sum = a + b
    print (sum)
    print (type (sum)) #type() is used to display the datatype of a variable
    
    Output:
    10.5
    <class ‘float’>
    ```
    
    In this example, the sum variable is converted to float instead of integer to avoid data loss. Python automatically converts smaller data types to larger ones to prevent data loss.
    
2. **Explicit type conversion:** Explicit type conversion is also known as typecasting. Explicit type conversion takes place when the programmer clearly and explicitly defines the same in the program. For explicit type conversion, there are some in-built Python functions. The following table contains some of the in-built functions for type conversion, along with their descriptions.
    
    ```python
    english, science, maths, sst, it = 95, 92, 97, 90, 98
    
    total = english + science + maths + sst + it
    message1 = "Total marks: " + str(total)
    print (message1)
    
    percentage = total / 5
    message2 = "Percentage: " + str(percentage)
    print (message2)
    
    output:
    Total marks: 472
    Percentage: 94.4
    ```
    

## ✔ Non-Primitive data types in Python:

There are mainly 4 non-primitive data types in python:

1. **lists:** A list is an ordered collection of items and is one of the most fundamental data structures to implement in any Python project. Since these are "ordered collections," each item in the list has a unique order that identifies it. You can assign addresses to each element of the list, which are known as indexes. The index value starts at zero and continues through to the last element (the positive index).
    
    ```python
    # Creating a List of numbers
    list1 = [10, 20, 14]
    print("\nList of numbers: ")
    print(list)
      
    # Creating a List of strings 
    list = ["python", "for", "devops"]
    print("\nList Items: ")
    print(list[0])
    print(list[2])
    
    output:
    List of numbers: 
    [10, 20, 14]
    
    List Items: 
    python
    devops
    ```
    
2. **sets:** Sets are an unordered collection of unique elements. Similar to lists, sets are mutable, which means you can modify, replace, or add elements after creating them. Also, like lists, you need to enclose sets within curly brackets for them to appear in the final output. You can only have unique values in a set.
    
    ```python
    # typecasting list to set
    myset = set(["a", "b", "c"])
    print(myset)
     
    # Adding element to the set
    myset.add("d")
    print(myset)
    
    output:
    {'b', 'a', 'c'}
    {'b', 'd', 'a', 'c'}    
    ```
    
3. **tuple:** Tuples contain ordered items that are immutable and can have duplicate values. Each item in a tuple is indexed, with the first item having an index of \[0\], the second item an index of \[1\], and so on.
    
    ```python
    mytuple = (1, 2, 3, 4, 5)
     
    # tuples are indexed
    print(mytuple[1])
    print(mytuple[4])
     
    # tuples contain duplicate elements
    mytuple = (1, 2, 3, 4, 2, 3)
    print(mytuple)
    
    output:
    2
    5
    (1, 2, 3, 4, 2, 3)
    ```
    
4. **dictionary:** Dictionary items are ordered, and mutable, and do not allow duplicates. Dictionary items are represented as key-value pairs and can be accessed by using the key name.
    
    ```python
    # Creating a Dictionary
    # with Integer Keys
    dict1= {1: 'Geeks', 2: 'For', 3: 'Geeks'}
    print("\nDictionary with the use of Integer Keys: ")
    print(dict1)
      
    # Creating a Dictionary
    # with Mixed keys
    mixed_dict= {'Name': 'Geeks', 1: [1, 2, 3, 4]}
    print("\nDictionary with the use of Mixed Keys: ")
    print(mixed_dict)
    
    output:
    Dictionary with the use of Integer Keys: 
    {1: 'Geeks', 2: 'For', 3: 'Geeks'}
    
    Dictionary with the use of Mixed Keys: 
    {'Name': 'Geeks', 1: [1, 2, 3, 4]}
    ```
    

## **📍** Conclusion:

In conclusion, getting the hang of various data types and data structures in Python is super handy! It'll help us create super efficient scripts, making our lives easier, especially in DevOps situations where we automate our daily tasks. 😊