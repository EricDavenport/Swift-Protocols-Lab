
## Protocols Lab

## Instructions for lab submission

1. Fork the assignment repo
1. Clone your Fork to your machine
1. Complete the lab
1. Push your changes to your Fork
1. Submit a Pull Request back to the assignment repo
1. Paste a link of the pull request on Canvas and submit


<br>

> Questions adapted from [Swift student lessons: 4 - Tables and Persistence -> 1 - Protocols](https://developer.apple.com/go/?id=app-dev-swift-student)

## Question 1

a. Create a `Human` class with two properties:
- `name` of type String
- `age` of type Int.

Then create an initializer for the class and create two `Human` instances.
```
Answer: 
class Human {
    var name: String
    var age: Int
    
    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
}

var eric = Human(name: "Eric", age: 28)
var emily = Human(name: "Emily", age: 2)

```

b. Make the `Human` class adopt the CustomStringConvertible protocol. Then print both of your previously initialized
`Human` objects.
```
Answer:
class Human: CustomStringConvertible {
    var name: String
    var age: Int
    
    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
    
    var description: String {
        return "My name is \(name) sand I sam \(age) years old."
    }
}

var eric = Human(name: "Eric", age: 28)
var emily = Human(name: "Emily", age: 2)

print(eric)
print(emily)

```

c. Make the `Human` class adopt the Equatable protocol. Two instances of `Human` should be considered equal
if their names and ages are identical to one another. Print the result of a boolean expression
evaluating whether or not your two previously initialized `Human` objects are equal to eachother
(using ==). Then print the result of a boolean expression evaluating whether or not your two
previously initialized `Human` objects are not equal to eachother (using !=).
```
Answer:class Human: CustomStringConvertible, Equatable {
    
    var name: String
    var age: Int
    
        static func == (lhs: Human, rhs: Human) -> Bool {
        return lhs.age == rhs.age && lhs.name == rhs.name
    }
    static func != (lhs: Human, rhs: Human) -> Bool {
        return lhs.age != rhs.age && lhs.name != rhs.name
    }

    
    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
    
    var description: String {
        return "My name is \(name) sand I sam \(age) years old."
    }
}
if eric == emily {
    print("Humans equal one another")
} else if eric != emily {
    print("These are two different Humans")
}
```

d. Make the `Human` class adopt the `Comparable` protocol. One `Human` is greater than another `Human` if its age is bigger. Create another
three instances of a `Human`, then create an array called people of type [`Human`] with all of the
`Human` objects that you have initialized.

Create a new array called sortedPeople of type [`Human`] that is the people array sorted by age.

</br> </br>

```
Answer:
class Human: CustomStringConvertible, Equatable, Comparable {
    
    var name: String
    var age: Int
    
    static func == (lhs: Human, rhs: Human) -> Bool {
        return lhs.age == rhs.age && lhs.name == rhs.name
    }
    static func != (lhs: Human, rhs: Human) -> Bool {
        return lhs.age != rhs.age && lhs.name != rhs.name
    }
    
    static func > (lhs: Human, rhs: Human) -> Bool {
        return lhs.age > rhs.age
    }
    static func < (lhs: Human, rhs: Human) -> Bool {
        return lhs.age < rhs.age
    }
   
    
    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
    
    var description: String {
        return "My name is \(name) sand I sam \(age) years old."
    }
}

var eric = Human(name: "Eric", age: 28)
var emily = Human(name: "Emily", age: 2)
var erika = Human(name: "Erika", age: 31)
var bigEric = Human(name: "Eric", age: 60)
var mom = Human(name: "Mommy", age: 58)

var humanArray: [Human] = [eric, emily, erika, bigEric, mom]
var sortedPeople = humanArray.sorted()

if eric == emily {
    print("Humans equal one another")
} else if eric != emily {
    print("These are two different Humans")
}

if eric < emily {
    print("Emily is older than Eric")
} else {
    print("Emily is younger than Eric")
}
if eric > emily {
    print("Eric is older than Emily")
} else {
    print("Eric is younger than Emily")
}

print(sortedPeople)
```


## Question 2

a. Create a protocol called `Vehicle` with two requirements:
- a nonsettable `numberOfWheels` property of type Int,
- a function called drive().
```
Answer:
protocol Vehicle {
    var numberOfWheels: Int { get }
    
    func drive()
    
}

```

b. Define a `Car` struct that implements the `Vehicle` protocol. `numberOfWheels` should return a value of 4,
and drive() should print "Vroom, vroom!" Create an instance of `Car`, print its number of wheels,
then call drive().
```
Answer:
protocol Vehicle {
    var numberOfWheels: Int { get }
    
    func drive()
    
}

struct Car: Vehicle {
    var numberOfWheels: Int = 4
    func drive() {
        print("VROOM VROOM")
    }
}

var myCar = Car()
print(myCar.numberOfWheels)
myCar.drive()
```

c. Define a Bike struct that implements the `Vehicle` protocol. `numberOfWheels` should return a value of 2,
and drive() should print "Begin pedaling!". Create an instance of Bike, print its number of wheels,
then call drive().

</br> </br>

```
Answer:

protocol Vehicle {
    var numberOfWheels: Int { get }
    
    func drive()
    
}

struct Car: Vehicle {
    var numberOfWheels: Int = 4
    func drive() {
        print("VROOM VROOM")
    }
}

struct Bike: Vehicle {
    var numberOfWheels: Int = 2
    func drive() {
        print("Begin Pedaling")
    }
}
var myBike = Bike()
print(myBike.numberOfWheels)
myBike.drive()
```


## Question 3
// Given the below two protocols, create a struct for penguin(a flightless bird) and an eagle.

Give your structs some properties and have them conform to the appropriate protocols.

```swift
protocol Bird {
 var name: String { get }
 var canFly: Bool { get }
}

protocol Flyable {
 var airspeedVelocity: Double { get }
}
```
```
Answer:
protocol Bird {
 var name: String { get }
 var canFly: Bool { get }
}

protocol Flyable {
 var airspeedVelocity: Double { get }
}

struct Penguin: Bird {
    var name: String = "Penguin"
    var canFly: Bool = false
    
}
struct Eagle: Bird, Flyable {
    var name: String = "Eagle"
    var canFly: Bool = true
    var airspeedVelocity: Double = 20
}
```
</br> </br>

## Question 4

a. Create a protocol called `Transformation`.  The protocol should specify a mutating method called transform
```
Answer:

```

b. Make an enum called `SuperHero` that conforms to `Transformation` with cases `notHulk` and `hulk`
```
Answer:

```

c. Create an instance of it named `bruceBanner`. Make it so that when the transform function is called that bruceBanner turns from
`.notHulk` to `.hulk.``

```swift
enum SuperHero: Transformation {
    // write code here.
}

// Example Output:
var bruceBanner = SuperHero.notHulk

bruceBanner.transform() . // hulk

bruceBanner.transform()  // notHulk
```

</br> </br>
```
Answer:

```


## Question 5

a. Create a protocol called `Communication`

b. Give it a property called `message`, of type String, and assign it an explicit getter.

c. Create three Classes. `Cow`, `Dog`, `Cat`.

d. Have your three classes conform to `Communication`

e. `message` should return a unique message for each animal when talk is called.

f. Put an instance of each of your classes in an array.

g. Iterate over the array and have them print their `message` property


## Question 6

The HeartRateReceiver class below represents a very simplified example of a class dedicated to receiving information from fitness tracking hardware with monitoring heart rate. The function startHeartRateMonitoringExample will generate random heart rates and assign them to currentHR, simulating how an instance of HeartRateReceiver may pick up on new heart rate readings at specific intervals.

HeartRateViewController below is a view controller that will present the heart rate information to the user. Throughout the exercises below you'll use the delegate pattern to pass information from an instance of HeartRateReceiver to the view controller so that anytime new information is obtained it is presented to the user.

```swift
class HeartRateReceiver {
    var currentHR: Int? {
        didSet {
            if let currentHR = currentHR {
                print("The most recent heart rate reading is \(currentHR).")
            } else {
                print("Looks like we can't pick up a heart rate.")
            }
        }
    }

    func startHeartRateMonitoringExample() {
        for _ in 1...10 {
            let randomHR = 60 + Int.random(in: 0...15)
            currentHR = randomHR
            Thread.sleep(forTimeInterval: 2)
        }
    }
}

class HeartRateViewController: UIViewController {
    var heartRateLabel: UILabel = UILabel()
}
```

First, create an instance of HeartRateReceiver and call startHeartRateMonitoringExample. Notice that every two seconds currentHR get set and prints the new heart rate reading to the console.

In a real app, printing to the console does not show information to the user. You need a way of passing information from the HeartRateReceiver to the HeartRateViewController. To do this, create a protocol called HeartRateReceiverDelegate that requires a method heartRateUpdated(to bpm:) where bpm is of type Int and represents the new rate as beats per minute. Since playgrounds read from top to bottom and the two previously declared classes will need to use this protocol, you'll need to declare this protocol above the declaration of HeartRateReceiver.

Now make HeartRateViewController adopt the protocol you've just created. Inside the body of the required method you should set the text of heartRateLabel and print "The user has been shown a heart rate of <INSERT HEART RATE HERE>."

Now add a property called delegate to HeartRateReceiver that is of type HeartRateReceiverDelegate?. In the didSet of currentHR where currentHR is successfully unwrapped, call heartRateUpdated(to bpm:) on the delegate property.

Finally, return to the line of code just after you initialized an instance of HeartRateReceiver. Initialize an instance of HeartRateViewController. Then, set the delegate property of your instance of HeartRateReceiver to be the instance of HeartRateViewController that you just created. Wait for your code to compile and observe what is printed to the console. Every time that currentHR gets set, you should see both a printout of the most recent heart rate, and the print statement stating that the heart rate was shown to the user.
