# pezetrialtest.py

# 1

Explain with your own words what is an object in Object Oriented Programming

# Answer 

An object in object-oriented programming is a representation of a class that includes data and activity. A class acts as a blueprint for an object, outlining its properties and operations. In software, real-world entities or concepts are represented by objects. A automobile object,
Example; Includes characteristics like make, model, and color, as well as operations like start, decelerate, and stop.



# 2

Explain with your own words what is a getter and a setter! Why is it better to use these instead of public fields?

# Answer 

The private fields of an object can be accessed and changed using getters and setters. While setters change the value of a private field, getters retrieve its value. Getters and setters offer encapsulation, which implies that the implementation specifics of the class are concealed from outside code, making them preferable to public fields. Because of this, a class's implementation can be modified without having an impact on the code that utilizes it. 
Example: All the codes that makes use of the public field would need to be altered if the implementation changed to save the birthday rather than the person's age in a public field. The implementation can be updated without affecting the code that uses the class by using a private field, getters, and setters.


# 3

In the following code we have code duplication: we are defining the same fields in both Cat and Dog classes as well. How could we refactor this solution to avoid this code duplication? Write actual code as a solution (not just describe it)!

Below the class definitions you can find example instantiations. Don’t touch these lines, your solution should be able to work with this usage.

class Dog:
   def __init__(self, name, age, color):
       self.type = 'dog'
       self.name = name
       self.age = age
       self.color = color

class Cat:
   def __init__(self, name, age, color):
       self.type = 'cat'
       self.name = name
       self.age = age
       self.color = color


dog = Dog('Furkesz', 5, 'white')
cat = Cat('Grumpy', 6, 'grey')



# Answer 

We can create a parent class called Animal with the common fields and then make Dog and Cat inherit from this the parent Animal class we have created. 


class Animal:
   def __init_ _(self, name, age, color):
       self.name = name
       self.age = age
       self.color = color

class Dog(Animal):
   def __init__(self, name, age, color):
       super().__init__(name, age, color)
       self.type = 'dog'

class Cat(Animal):
   def __init__(self, name, age, color):
       super().__init__(name, age, color)
       self.type = 'cat'

dog = Dog('Furkesz', 5, 'white')
cat = Cat('Grumpy', 6, 'grey')

Now that Dog and Cat are descended from Animal, the common fields are only defined once in the Animal class. The common fields are defined in the Animal class, but the type field is unique to either the Dog or Cat.




# 4 

 What is the output of the following code? Explain your answer!

class Book:
   print_number = 1
   def __init__(self, author, title, price):
       self.author = author
       self.title = title
       self.price = price
       if Book.print_number <= 1:
           self.price *= 2
       Book.print_number += 1
   def sell(self, money):
       print(money - self.price if money >= self.price else money)

class HardCover(Book):
   def __init__(self, author, title, price, cover_price = 100):
       super().__init__(author, title, price + cover_price)
       self.coverPrice = cover_price

class PaperCover(Book):
   def __init__(self, author, title, price):
       super().__init__(author, title, price)
   def sell(self, money):
       print(max(money - self.price, 0))


lotr = HardCover('J.R.R. Tolkien', 'The Lord of the Rings: The Fellowship of the Ring', 1000)
hp = HardCover('J.K. Rowling', "Harry Potter and the Philosopher's Stone", 1000, 200)
lp = PaperCover('Antoine de Saint-Exupéry', "The Little Prince", 1000)
lotr.sell(1200)
hp.sell(1200)
lp.sell(1200)


# Answer 


The output of the code is:

800
1100
200

HardCover and PaperCover, two subclasses of the Book class, use the super() method to invoke the __init__ method of their parent class, Book. 

A print_number variable is set to 1 and increased by 1 for each new Book instance in the Book __init__ method. The price is twice if the print number is less than or equal to 1. This requirement is satisfied in the case of the HardCover and PaperCover instances since they are the first and second Books ever made.

The cover_price is added to the price for HardCover instances before being supplied to the Book __init__ method. The cover_price value is then assigned to the coverPrice attribute.

Only the author, title, and price inputs are given to the Book __init__ method for PaperCover objects.

For the PaperCover class, the sale function has been overwritten. In this implementation, the difference between the money and the price is printed if the money is greater than or equal to the price. If not, 0 is displayed.

1200 is more than the price in the lotr.sell(1200) function (which is made up of 1000 + 100), therefore 1200 - 1200 = 800 is shown. Since 1200 in the hp.sell(1200) function is more than the price, which is made up of 1000 and 200, 1200 - 1100 = 1100 is printed. Since 1200 is less than the price, which is 1000, in the lp.sell(1200) function, max(1200 - 1000, 0) = 200 is reported.



# 5 Write a zoo management program.

We want to register new zoos in the system. Every zoo has a name and the size of its territory. The territory of a zoo is by default 100.

We want to place animals in zoos. Every animal has a name and a territory requirement (the amount of territory the animal needs to live). The territory requirement of an animal is by default 20.

When a zoo has enough free territory for the animal which we want to place there, then the zoo places the animal.

We also want to sell animals from a zoo to free up some territory to other animals. A zoo always sells the animal which requires the most territory. When a zoo sells an animal, it returns the sold animal and frees up its territory to be able to place new animals.

Using your solution, the following code should run without errors and print the expected results.

budapest_zoo = Zoo('Budapest Zoo') # Created with 100 territory
berlin_zoo = Zoo('Berlin Zoo', 200) # Created with 200 territory
elephant = Animal('elephant', 50) # Created with 50 territory
giraffe = Animal('giraffe', 40) # Created with 40 territory
zebra = Animal('zebra') # Created with 20 territory

budapest_zoo.sell() # Should print: no animals to sell
budapest_zoo.place_animal(elephant) # Should print: elephant is placed in Budapest Zoo
budapest_zoo.place_animal(giraffe) # Should print: giraffe is placed in Budapest Zoo
budapest_zoo.place_animal(zebra) # Should print: no territory for zebra in Budapest Zoo
berlin_zoo.place_animal(budapest_zoo.sell()) # Should print: elephant is placed in Berlin Zoo
budapest_zoo.place_animal(zebra) # Should print: zebra is placed in Budapest Zoo




# Answer

class Zoo:
    def __init__(self, name, territory=100):
        self.name = name
        self.territory = territory
        self.animals = []

    def place_animal(self, animal):
        if self.territory >= animal.territory:
            self.animals.append(animal)
            self.territory -= animal.territory
            print(f"{animal.name} is placed in {self.name}")
        else:
            print(f"no territory for {animal.name} in {self.name}")

    def sell(self):
        if not self.animals:
            print("no animals to sell")
            return None
        else:
            animal_to_sell = max(self.animals, key=lambda animal: animal.territory)
            self.animals.remove(animal_to_sell)
            self.territory += animal_to_sell.territory
            print(f"{animal_to_sell.name} is sold from {self.name}")
            return animal_to_sell


class Animal:
    def __init__(self, name, territory=20):
        self.name = name
        self.territory = territory


budapest_zoo = Zoo('Budapest Zoo') # Created with 100 territory
berlin_zoo = Zoo('Berlin Zoo', 200) # Created with 200 territory
elephant = Animal('elephant', 50) # Created with 50 territory
giraffe = Animal('giraffe', 40) # Created with 40 territory
zebra = Animal('zebra') # Created with 20 territory

budapest_zoo.sell() # Should print: no animals to sell
budapest_zoo.place_animal(elephant) # Should print: elephant is placed in Budapest Zoo
budapest_zoo.place_animal(giraffe) # Should print: giraffe is placed in Budapest Zoo
budapest_zoo.place_animal(zebra) # Should print: no territory for zebra in Budapest Zoo
berlin_zoo.place_animal(budapest_zoo.sell()) # Should print: elephant is placed in Berlin Zoo
budapest_zoo.place_animal(zebra) # Should print: zebra is placed in Budapest Zoo


A Zoo class and an Animal class are created using this code. Zoo keeps track of the zoo's name, the extent of its grounds, and a list of the animals that are presently housed there. The name of the animal and how much space it needs to survive are kept at animal stores.

The Zoo class's place_animal function determines whether the zoo has adequate open space for the given animal. If so, it subtracts the animal's necessary territory from the zoo's remaining area and adds the animal to the list of creatures that live there. If not, a notice stating that the animal has no open area is printed.

If there are any animals present in the zoo, it is determined by the sell function of the Zoo class. If not, it produces a message informing the user that no animals are available for purchase and returns None. If so, it locates the animal that needs the most space to survive, crosses it off the list of zoo animals, adds its necessary space to the remaining zoo space, and then brings the animal back.

We establish two Zoo objects with predefined territories, three Animal objects with predefined territorial specifications, and test the place_animal and sale methods of the Zoo class in accordance with the instructions in the main code block displayed here.
