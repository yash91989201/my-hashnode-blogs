---
title: "⚙️ Operations on python data structures for DevOps engineers (Part - 2)"
seoTitle: "Operations on python data structures for DevOps engineers (Part - 2)"
seoDescription: "Master Python tuple/dictionary operations for DevOps. Boost skills in immutable data structures, indexing, updating. Series Part 2"
datePublished: Sat Jul 29 2023 14:14:12 GMT+0000 (Coordinated Universal Time)
cuid: clko3fp4g00010amfee6d8p72
slug: operations-on-python-data-structures-for-devops-engineers-part-2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690638558219/0e59ea3a-be0c-4502-b5c9-908787523377.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1690638772744/1a47bac8-131f-447a-8eef-dc12544cb2a0.png
tags: python, devops, 90daysofdevops, trainwithshubham, tws

---

## **📍** Introduction:

Let's proceed with exploring operations on data structures. In this blog, we will dive into various operations that can be executed on tuple and dictionary data structures in Python. If you haven't read the first part, feel free to check it out here: [https://yashraj-jaiswal.hashnode.dev/operations-on-python-data-structures-for-devops-engineers-part-1](https://yashraj-jaiswal.hashnode.dev/operations-on-python-data-structures-for-devops-engineers-part-1)

## ✔ Python tuple operations:

A tuple is similar to a list, meaning we can create a tuple with the same or mixed elements but with one key difference: the elements of a tuple are immutable, meaning they cannot be updated or removed, and we cannot even add new values to a tuple after it has been created.

### 🔸 Creating a tuple:

A tuple is created by placing all the items (elements) inside parentheses (), separated by commas. Although parentheses are optional, it is good practice to use them.

1. **Tuple with similar data type:**
    
    ```python
    # tuple with similar data type elements
    tuple1=(1,2,3,4)
    tuple2=('Hello','this is ','yash')
    print(tuple1)
    print(tuple2)
    
    output:
    (1,2,3,4)
    ('Hello','this is ','yash')
    ```
    
2. **Tuple with mixed data type:**
    
    ```python
    # tuple with mixed data type elements
    mixed_tuple=("Hello",-1.25,20,'Y',False,[5,6,7])
    print(mixed_tuple)
    
    output:
    ('Hello', -1.25, 20, 'Y', False, [5, 6, 7])
    ```
    
3. **Tuple with and without ():**
    
    ```python
    # tuple with ()
    tuple1=(1,2,3,4)
    # tuple without using (), this is also valid,
    # but it is advised to use () for better readiblity
    tuple2=2,4,6,8
    print(tuple1)
    print(tuple2)
    
    output:
    (1,2,3,4)
    (2,4,6,8)
    ```
    
4. **List within a tuple:** a tuple is immutable, but if there is a list within a tuple it remains mutable.
    
    ```python
    mixed_tuple=(1,2,3,['Hello','Readers!!'])
    print(mixed_tuple)
    print(mixed_tuple[-1])
    mixed_tuple[-1].extend(['python is','awesome'])
    print(mixed_tuple)
    
    output:
    (1,2,3,['Hello','Readers!!'])
    ['Hello','Readers!!','python is','awesome']
    ```
    

### 🔸 Accessing tuple elements:

Since a tuple works like lists, we can access tuple elements just like we can do with lists.

1. **Indexing:** just like in the list we can use indexing in tuples.
    
    ```python
    mixed_tuple=(1,2,3,['Hello','Readers!!'])
    print(mixed_tuple[2])
    # print the second item in the list 
    print(mixed_tuple[3][1])
    
    output:
    2
    'Readers!!'
    ```
    
2. **Negative Indexing:** negative indexing is also possible in tuples.
    
    ```python
    tuple1=(1,2,3,4)
    # print the last second element in tuple
    print(tuple1[-2])
    ```
    
3. **Slicing:** The concept of slicing can be applied to tuples just as it is used with lists.
    
    ```python
    tuple1=(1,2,3,4,5,6,7)
    # print 2nd till 5th element
    print(tuple1[1:5])
    
    output:
    (2, 3, 4, 5)
    ```
    
4. **Iterating through a tuple:** use a for loop to iterate through a tuple.
    
    ```python
    tuple1=(1,2,3,4)
    for i in tuple1:
        print(i)
    
    output:
    1
    2
    3
    4
    ```
    
5. **in keyword:** with the help of in keyword we can check if a specific element exists in a tuple.
    
    ```python
    tuple=('python','is awesome')
    print('python' in tuple)
    
    output:
    True
    ```
    
6. **Unpacking a tuple:** all the values of a tuple are kept within a pair of parenthesis and can be said that they are packed, but we can also access these values individually by unpacking them.
    
    ```python
    packed_tuple=('hello','dosto!!')
    a,b=packed_tuple
    print(a)
    print(b)
    
    output:
    hello
    dosto!!
    ```
    

## ✔ Python dictionary operations:

In Python, a dictionary is a mutable data structure that allows us to store data in a key-value format (i.e., for every key, there is a specified value) within curly brackets. In a dictionary, only an immutable data structure can be used as a key, such as tuples, strings, or integers.

### 🔸 Creating a dictionary:

```python
# creating a dictionary with string keys
country_capitals = {
  "United States": "Washington D.C.", 
  "Italy": "Rome", 
  "England": "London"
}

# printing the dictionary
print(country_capitals)

output:
{'United States': 'Washington D.C.', 'Italy': 'Rome', 'England': 'London'} 
```

```python
# Valid dictionary
my_dict = {
  1: "Hello", 
  (1, 2): "Hello Hi", 
  3: [1, 2, 3]
}
print(my_dict)

# Invalid dictionary
# Error: using a list as a key is not allowed
my_dict = {
  1: "Hello", 
  [1, 2]: "Hello Hi", 
}
print(my_dict)

output:
{1: 'Hello', (1, 2): 'Hello Hi', 3: [1, 2, 3]}
Traceback (most recent call last):
  File "c:\Users\LENOVO\Desktop\DevOps\python\tuple.py", line 13, in <module>
    my_dict = {
TypeError: unhashable type: 'list'
```

### 🔸 Accessing items of a dictionary:

1. **Accessing dictionary values using:** we can access values of a specific key in a dictionary using the \[\] or get() method.
    
    ```python
    # using [] to access specific value
    country_capitals = {
      "United States": "Washington D.C.", 
      "Italy": "Rome", 
      "England": "London"
    }
    
    print(country_capitals["United States"])  # Washington D.C.
    # using get() method to access specific value
    print(country_capitals.get("England")) # London
    
    output:
    Washington D.C.
    London
    ```
    
2. **Accessing dictionary keys:** to get all the keys within a dictionary we can use the keys() method.
    
    ```python
    country_capitals = {
      "United States": "Washington D.C.", 
      "Italy": "Rome", 
      "England": "London"
    }
    
    print(country_capitals.keys())
    
    output:
    dict_keys(['United States', 'Italy', 'England'])
    ```
    
3. **Accessing dictionary values:** We can use the values() method to access all the values of a dictionary.
    
    ```python
    country_capitals = {
        "United States": "Washington D.C.",
        "Italy": "Rome",
        "England": "London"
    }
    
    print(country_capitals.values())
    
    output:
    dict_values(['Washington D.C.', 'Rome', 'London'])
    ```
    
4. Accessing elements using a loop: when accessing a dictionary using a for loop we get both the key and value.
    
    ```python
    country_capitals = {
        "United States": "New York",
        "Italy": "Naples"
    }
    
    # print dictionary keys one by one
    for country in country_capitals:
        print(country)
    
    output:
    United States
    Italy
    ```
    

### 🔸 Updating a dictionary:

1. **Change dictionary items:** since dictionaries are mutable we can change specific values using the key.
    
    ```python
    country_capitals = {
      "United States": "New York", 
      "Italy": "Naples", 
      "England": "London"
    }
    
    # change the value of "Italy" key to "Rome"
    country_capitals["Italy"] = "Rome"
    
    print(country_capitals)
    
    output:
    {'United States': 'Washington D.C.', 'Italy': 'Rome', 'England': 'London'}
    ```
    
2. **Add items to a dictionary:** We can add an item to the dictionary by assigning a value to a new key (that does not exist in the dictionary). For example,
    
    ```python
    country_capitals = {
      "United States": "New York", 
      "Italy": "Naples" 
    }
    
    # add an item with "Germany" as key and "Berlin" as its value
    country_capitals["Germany"] = "Berlin"
    
    print(country_capitals)
    
    output:
    {'United States': 'Washington D.C.', 'Italy': 'Rome', 'Germany': 'Berlin'}
    ```
    
3. **Removing items from a dictionary:** to remove a specific item from a dictionary we can use the del keyword and the key of that item.
    
    ```python
    country_capitals = {
      "United States": "New York", 
      "Italy": "Naples" 
    }
    
    # delete item having "United States" key
    del country_capitals["United States"]
    print(country_capitals)
    
    output:
    {'Italy': 'Naples'}
    ```
    

### 🔸 Dictionary membership test:

To check if a key exists in a dictionary we can use the `in` and `not in` operator.

```python
my_list = {1: "Hello", "Hi": 25, "Howdy": 100}

print(1 in my_list) # True

# the not in operator checks whether key doesn't exist
print("Howdy" not in my_list) # False

print("Hello" in my_list) # False
```

## ✔ Advantages of tuple over a list:

* Tuples are stored in a single block of memory. Since tuples are immutable, they do not require additional space to store new objects.
    
* Lists are allocated in two blocks: a fixed one containing all the Python object information and a variable-sized block for the data.
    
* It is the reason creating a tuple is faster than List.
    
* It also explains the slight difference in indexing speed is faster than lists, because in tuples for indexing it follows fewer pointers.
    

## **📍** Conclusion:

We've been discussing some operations on basic Python data structures, but there's so much more to explore! Python has a bunch of other cool data structures like stacks, linked lists, graphs, trees, and many more. Don't worry, we'll dive deeper into these fascinating data structures as we move forward. Stay tuned and keep learning.