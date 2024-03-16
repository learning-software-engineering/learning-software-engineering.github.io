# Code Smells

## Table of Contents
1. [What is code smell?](#what-is-code-smell)
2. [Duplicate Code](#duplicate-code)
3. [Improper Names](#improper-names)
4. [Dead Code](#dead-code)
5. [Middle Man](#middle-man)
6. [Feature Envy](#feature-envy)
7. [Long Functions](#long-functions)
8. [Data Clumps](#data-clumps)
9. [Additional Resources](#additional-resources)

### What is a code smell?

Code smells are indicators of potential issues or weaknesses in software code. They are not bugs or errors, but rather patterns or 

practices that may lead to problems in the future. 

# Common Types of Code Smells and How They Can Harm your Code

There are a vast number of code smells and they differ from project to project and developer to developer, and business to business. 

So, it is crucial to thoroughly understand the organization’s design and development standards before handling any code smell. 

Here are the most common code smells that developers usually encounter with:

## Duplicate Code

In simple terms, duplicate code happens when two code fragments look almost identical. Consider this piece of code:

```
def calculate_rectangle_area(length, width):
    return length * width

# Duplicate code
def calculate_square_area(side):
    return side * side
```

In this example, the `calculate_square_area` function duplicates the functionality of the `calculate_rectangle_area` function but only for squares. This coding habit makes it harder to debug a program because any changes or bug fixes need to be applied to multiple places. Also, duplicated code makes the codebase harder to read and understand. Developers might need to analyze multiple sections of code that are essentially doing the same thing.

## Improper Names

If your variables, classes, and functions lack proper names, this can be an indicator that your code isn’t clean. For example, 

```
def func(a, b):
    return a + b
```
This function is simple enough to understand despite its naming issue. However, imagine that we have a big function to perform some backend tasks for our program,
then it would be more problematic for other developers.  Without additional context or comments, it's not immediately clear what the function is supposed to do. 
This can lead to confusion for others who encounter this code later or who need to work with it.

## Dead Code 

Dead code is code that’s in the application but not in use. Here is an example,

```
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }

    // This method is never called, making it dead code
    public int subtract(int a, int b) {
        return a - b;
    }
}

```

The `subtract` method is never called from any part of the application. It remains in the codebase, occupying space and potentially causing confusion for developers who might assume it serves a purpose.

## Middle Man

This code smell refers to a situation where an object or method serves mainly as a pass-through or intermediary, delegating most of its functionality to another object or method without adding significant value or functionality of its own. This can introduce unnecessary complexity and reduce the clarity and efficiency of the codebase.

```
class DataManager:
    def __init__(self, data):
        self.data = data

    def process_data(self):
        data_processor = DataProcessor()
        return data_processor.process(self.data)

class DataProcessor:
    def process(self, data):
        # Some complex data processing logic here
        processed_data = data * 2
        return processed_data
```

In this example, the `DataManager` class serves as a middle man that merely delegates the data processing to the `DataProcessor` class. It doesn't add any additional functionality or logic of its own and exists primarily to pass data to another class.

## Feature Envy

This happens when a method accesses the data of another object more than its own data. Consider this piece of code:

```
class ShoppingCart:
    def __init__(self):
        self.items = []

    def add_item(self, item):
        self.items.append(item)

    def total_price(self, tax_rate):
        total = 0
        for item in self.items:
            total += item.price
        total *= (1 + tax_rate)
        return total

class Item:
    def __init__(self, name, price):
        self.name = name
        self.price = price

class User:
    def __init__(self):
        self.shopping_cart = ShoppingCart()

    def calculate_total_price(self, tax_rate):
        return self.shopping_cart.total_price(tax_rate)
```

The `User` class has a method calculate_total_price that calculates the total price of items in the user's shopping cart. However, instead of directly accessing the user's shopping cart and performing the calculation there, it invokes the `total_price` method of the `ShoppingCart` class. This leads to poor encapsulation and violate the principle of encapsulation, where each class should encapsulate its own behavior and data.

## Long Functions

Long functions is a code smell that occurs when a function or method is excessively long, containing a large number of lines of code. Long functions can be difficult to understand, maintain, and test. They often violate the Single Responsibility Principle, which states that a function should only have one reason to change.

```
def process_order(order):
    # Step 1: Validate order data
    if not order:
        return None
    # Step 2: Fetch product information
    product_info = fetch_product_info(order.product_id)
    # Step 3: Calculate total price
    total_price = order.quantity * product_info.price
    # Step 4: Apply discounts
    if order.discount_code == 'DISCOUNT10':
        total_price *= 0.9
    # Step 5: Apply taxes
    total_price *= 1.15  # Assuming 15% tax rate
    # Step 6: Generate invoice
    invoice = generate_invoice(order, product_info, total_price)
    # Step 7: Send confirmation email
    send_confirmation_email(order.email, invoice)
```

In this example, the `process_order` function performs multiple steps, including validation, fetching product information, calculating total price, applying discounts and taxes, generating an invoice, and sending a confirmation email. The function is long and complex, which makes it difficult to understand and maintain.

## Data Clumps

Data clumps occur when multiple pieces of data go together. One easy way to spot a data clump is when one component doesn’t make sense in isolation but makes sense as a group. Here's an example to illustrate the data clumps:

```
def create_user(name, email, phone):
    # Function to create a user using name, email, and phone
    pass

def update_user_email(user_id, new_email):
    # Function to update user's email
    pass

def send_notification(email, message):
    # Function to send email notification
    pass
```

In this example, the `name`, `email`, and `phone` parameters are frequently passed together in various functions. This suggests that these pieces of data are closely related and should be put together in the same class.


# Additional Resources
1. [Refactoring Guru](https://refactoring.guru/refactoring/smells)
2. [What is a code smell?](https://linearb.io/blog/what-is-a-code-smell)
