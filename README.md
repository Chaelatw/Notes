# Notes

# Plural Sight

# Chapter 7 - Working with Strings
# String Class
    Stores a sequence of Unicode characters
        -Literals are stored in double quotes
    
    ex: 
        String name = "Jim"
        String greeting = "Hello " + name; // Hello Jim
        System.out.println(greeting); 
        greeting += " good to see you! ";
        Sytem.out.println(greeting); // Hello Jim good to see you!

    Strings Are Immutable
    
    String variables do not directly hold the string value
        -Hold a reference to the instance of string
        -Changes in the value create a new instance of the string
    ex:
        String message = "I";
        message += " Love ";
        message += " Java";

   # String Equality
     
     Comparing strings with the equality operator (==)
        -Checks to see if both string variables reference the same string instance
     Comparing strings with the equal methos
        -Performs a character-by-character comparison

     ex:   
        String s1 = "I love";
        s1 += " Java ";
        s2 += " love Java";
        if(s1 == s2) // false
                // do something 
        if(s1.equals(s2))
                // do something 
 
     Interning a string: 
        -provides a canonicalized value
             (When you inern a string, a string of any given value will always 
             return back a reference to the same string instance.)
        -enables reliable == operator comparison
        -Improves performance of frequently compared strings

    ex:
        String s1 = "I love";
        s1 += " Java ";
        s2 += " love Java";
        if(s1 == s2) // false
                // do something
        String s3 = s1.intern();
        String s4 = s2.intern();
        if(s3 == s4) // true
                // do something

   # String Methods and String Conversions

   Classes provides Methods
        
        Operation                       Methods
        ___________________________________________________________

        - Length                        -length
        - Create new string(s)          -concat, replace, toLowerCase,
            from existing               trim, split
        - Extract substring             -charAt, substring
        - Test substring                -contains, endsWith, startsWith,
                                        indexOf, lastIndexOf
        - Comparison                    -equals, equalsIgnoreCase, isEmpty,
                                        compareTo, compareToIgnoreCase
        - Formatting                    -format
        - String for non-string         -valueOf


    Converting Non-string Types to String

        Virtually all data types can be converted into a String
            -Can use String.valueOf
            - Conversion often happens implicitly

        ex: 
            int iVal = 100;
            String sVal = String.valueOf(iVal); // "100"

            int i = 2, j = 3;
            int result = i * j;
            String output = i + " * " + j + " = " + result; // "2 * 3 = 6"

   # String Builders

    String builder class: 
        Provides mutable string buffer
            - Efficiently constructs string values
            - Add new content to end with append
            - Add new content within with insert
         Extract content to a string
            - Use toString method

        ex:
            String location = "Florida"
            int flightNumber = 175;
            StringBuilder sb = new StringBuilder(40);
            sb.append("I flew to ");
            sb.append(" on Flight #");
            sb.append(flightNumber);
            String message = sb.toString(); // "I flew to Florida on Flight #175"

            String time = "9.00";
            int pos = sb.indexOf(" on");
            sb.insert(pos, " at ");
            sb.insert(pos + 4, time);
            message = sb.toString(); "I flew to Florida at 9.00 on Flight #175"



# Chapter 8 - Understanding Classes and Objects
# Declaring Classes
    Java is an Object-oriented Language
        -Objects encapsulate data, operations and usage semantics
        -Allows storage and manipulation details to be hidden
        -Separates what is to be done from how it is done
    A class is a template for creating objects
        -Declared with class keyword followed by the class name
            (always capitalize the name)
        -Body of the class is contained within brackets
        -Java source file name normally has same name as class


     ex:
        File name: Flight.java

        class Flight {
        // class members
    }

    Classes
    A class is made up of both state and executable code
        -fields: store object state
        -methods: executable code that manipulates state and performs operations
        -constructors: executable code used during object creation to set intitial s                       state

     ex:
        int passengers;
        int seats;          //fields
        
        Flight(){           //constructors
            seats = 150;
            passengers = 0;
        }
        


        void add1Passenger() {          // method
            if(passengers < seats)
               passengers += 1; 
            }
        }

# Using Classes
        
        Use the new keyword to create a class instance (a.k.a an object)
            -Allocates the memory described by the class, and runs the constructor
            -Returns a reference to the allocated memory

        ex: 
            Flight nycToLv;
            nycToLv = new Flight();
            Flight slcToSf = new Flight();

        Understanding Classes as Reference Types

        ex:
            Flight flight1 = new Flight();
            Flight flight2 = new Flight();
            flight2.add1Passenger();
            System.out.println(flight2.passengers); // 1

            flight2 = flight1;
            System.out.println(flight2.passengers); // 0

            flight1.add1Passenger();
            flight1.add1Passenger();
            System.out.println(flight2.passengers); // 2

# Encapsulation and Access Modifiers
    
    Encapsulation:
    -The implementation details of a class are generally hidden
    Access Modifiers:
    -To achieve encapsulation. Allows us to control the visibilty of classes and 
    their members

     Basic Access Modifiers
     Modifier           Visibility          Usable on Classes      Usable on Members
     _______________________________________________________________________________
    
     -No access        -Only within its own         Y                       Y
      modifier          package(aka package
                        private)
    
     -public           -Everywhere                  Y                       Y

     -private          -Only within the             N*                      Y
                        declaring class 
     
     *As private applies to top level classes; private is available to nested class
     


Main.java                                   Flight.java
___________                                 _______________



Flight flight1 = new Flight();              public class Flight {
System.out.println(                             
    flight1.passengers); // ERROR               private int passengers;
   flight1.passenger();                         private int seats;

                                                public Flight(){...}
                                                public void add1Passenger(){...}
                                            }            



    public class Flight {
        // other members elided for clarity
        public void add1Passenger() {
            if(passengers < seats)
               passengers += 1; 
        }
        private void handleTooMany(){
           System.out.println("Too many");
        }
    }





Main.java                                   Flight.java
___________                                 _______________



Flight flight2 = new Flight();              public class Flight {

flight2.handleTooMany(); // ERROR            private int passengers;
flight2.add1Passenger();                        private int seats;
                                                public Flight(){...}
                                                public void add1Passenger(){...}
                                                
                                                private void handleTooMany(){...}


# Special References
    this: implicit reference to current object
        -usefule for reducing ambiguity
        -allows an object to pass itself as a parameter
    null: represents an uncreated object
        -can be assigned to any reference variable

    this ex:
        public class Flight {
            private int passengers;
            private int seats;
            // other members elided for charity
            public boolean hasRoom(Flight f2) {
                int total =  this.passengers + f2.passengers;
                return total <= seats;

            }
       } 

     null ex:
        
            Flight lax1 = new Flight();
            Flight lax2 = new Flight();

            // add passengers to both flights

            Flight lax3 = null;
            if(lax1.hasRoom(lax2))
                lax3 = lax1.createNewWith Both(lax2);

            // do some other work

            if(lax3 != null)
                System.out.println("Flights combined");

# Field Acessors and Mutators
    Field Encapsulation
        -The specific fields a class uses to manage data values is generally 
        considered to be an implementation detail
        -In most cases these details should not be directly accessible outside the 
        class
        -Use methods to control field access

     Accessors and Mutators
     Use the accessor/mutator pattern to control field access
        -Accessor: retrieves field value (getter)
            -Method name: getFieldName
        -Mutator: modifies field value (setter)
            -Method name: setFieldName

       ex:
            class Flight {
                private int seats;
            // other members elided for clarity
            
            public in getSeats() {
                returns seats;
            }

            public void setSeats(int seats) {
                this.seats = seats;
             }
           }

        
        Main.java
        ___________



        Flight slcToNyc = new Flight();
        slcToNyc.setSeats(200);
        System.out.println(slcToNyc.getSeats()); // 200


# Chapter 9 - Implementing Class Constructors and Initializers
# Class Initial State

    When an object is created, it is expected to be in a useful state
    Defualt initial state set by Java often not enough
    May need specific action 
    Set field values
    Execute code
    Each field is set to 0 by default

    bye/short/              float/              char            boolean
    int/long                double
 _______________________________________________________________________________
        0                    0.0              '\u0000'           false


reference types = null

Establishing Initial State
    3 ways to initialize state:
        -field initializers
        -constructors
        -initialization blocks

Field Initializers
    Specify field's intial value as part of the field's declaration
        -Can be an equation
        -Can include other fields
        -Can include method calls
    ex:
        public class Earth {
            long circumferenceInMiles = 24901;
            long circumferenceInKms = (long)(circumferenceInMiles * 1.6d);
        } 
Constructors
    Code that runs during object creation
        -Named same as the class
        -No return type

    ex:
        class Flight {
            private int passengers;
            private int seats = 150;
            Flight() {

            }
Number of Constructors
    Must have at least one
    When no explicit constructor, Java provides one
    
    Can have multiple
    Each must have a unique parameter list (signatures)
    Different number of parameters 
    Different parameter types

    Main.java                                   Passenger.java
  ________________                          ___________________________

                                            public class Passenger{
  Passenger bob = new Passenger();              private int checkedBags:    
  bob.setCheckedBags(3);                        private int freeBags;
                                                // getters and setters elided
                                                private double perBagFee;
                                                public Passenger() { }
                                              } 



    Main.java                                   Passenger.java
  ________________                          ___________________________

                                            public class Passenger{
  Passenger bob = new Passenger();          
  bob.setCheckedBags(3);                        
                                                // other members elided
                                                public Passenger() // default constructor doesn't accept                                                                        any arguments
                                                public Passenger(int freeBags) {
  Passenger nia = new Passenger(2)              this.freeBags = freeBags;
                                                }
                                              }


# Chaining Constructors

    One constructor can call another
        -Chaining the constructors together
        -Must be the first line of the constructor
        -Use the "this" keyword followed by the parameter list


    ex:
        public class Passenger {
        
        public Passenger(int freeBags) {
        this(freeBags > 1 ? 25.0d : 50.0d); 
        this.freeBags = freeBags;
       }
       public Passenger(int freeBags, int checkedBags) {
            this(freeBags);
            this.checkedBags = checkedBags;
        }
        public Passenger(double perBagFee) {
            this.perBagFee = perBagFee;
    }

# Constructor Visiblity
    Making a constructor private, only code in that class can access it.
    Can still chain to other constructors

# Initializing Blocks
    Share code across all constructors
        -Cannot recieve parameters
        -Place code within brackets outside of any method or constructor

      A class can have multiple
        -All always execute
        -Execute in order starting at the top of the source file

      ex:  
        public class Flight {
            private int passengers, int seats = 150;
            private int flightNumber;
            private char flightClass;
            private boolean[] is SeatAvailable = new boolean[seats];

            {

                for(int i = 0; i < seats; i++)
                    isSeatAvailable[i] = true;
             } 

             public Flight(int flightNumber) {
                this.flightNumber = flightNumber;
               }

              public Flight(char flightClass) {
                 this.flightClass = flightClass;
                 }
                public Flight(char flightClass) {} 
        }
    Inizialization and Constructor Order:
        1. Field initializers
        2. Initialization blocks
        3. Constructors


# Chapter 10 - Using Static Members
# Static Members
    Static members
    :are shared class-wide
        -Not associated with individual instance
    :Declared using the static keyword
        -Accessible using the class name

    Static field
        -A value not associated with a specific instance
        -All instances access the same value
    Static method
        -Performs an action not tied to a specific instance
        -Has access to static members only

    ex:
        public class Flight {
            private int passengers, int seats = 150; //instance field
            private static int allPassengers;
            public void ass1Passengers() {
                if(passengers < seats) {
                    passengers += 1;
                    allPassengers += 1;
             }       
        
            }


        public class Flight {
            private int passengers, int seats = 150; //instance field
            private static int allPassengers;
            private static int getAllPassengers(){
                return allPassengers;
             }

            public static void resetAllPassengers() {
                allPassengers = 0;
             }

# Static Import Statement
    Import Statement
        -Allows a type name to be used without being package-qualified

        Static import statement
            -Used with static methods
            -Allows method name to be used without being class-qualified


    ex:
        import static com.pluralsight.flight.app.Flight.resetAllPassengers;
        import static com.pluralsight.flight.app.Flight.getAllPassengers;

        or

        import static com.pluralsight.flight.app.Flight.*; // star imports all static members 


        
        resetAllPassengers();

        Flight laxToSlc = new Flight();
        laxToSlc.add1Passenger();
        laxToSlc.add1Passenger();

        Flight dfwToNyc = new Flight();
        dfwToNyc.add1Passenger();

        System.out.println(Flight.getAllPassengers());
 
# Static Initializers
    Static Initialization Blocks
        Perform one-time type initialization
            -execute before type's first use
            -has access to static members only

        Statements enclosed in brackets
            -preceded by static keyword
            -outside of any method or constructor


    ex:
        public class Flight {

            private int passengers, seats = 150;
            private static int allPassengers, maxPassengersPerFlight;

            static {
                AdminServie admin = new AdminService() ?
                    admin.getMaxFlightPassengers() : Integer.MAX_VALUE;
            admin.close();

           } 

           public void add1Passenger() {
                if(passengers < seats && passengers < maxPassengersPerFlight) {
                passengers += 1;
                allPassengers += 1;
                }
               } 
            











# Head First Java Chapter 9
        Instance variables and Local Variables
        
        Instance variables 
            -are declared inside a class but not inside a method
        Local variables (stack variables)
            -are declared inside a method, including method parameters

        When you call a method, the method lands on the top of a call stack.
        The new thing pushed onto the stack is the stack frame. It holds the state of the method.

        The method on top of the stack is always currently executing the method.
                

            ex:
                public void doStuff () {
                    boolean b = true;
                    go(4);
                }

            public void go(int x) {
                int z = x + 24;
                crazy();

               } 
            public void crazy(){
            char c= 'a'
            }


        The values of an objext's instance variables live inside the object.
        If the instance variables are all primitives, Java makes space for the instance variables based on the primitive type.


        3 steps of Object deckaration:

        1. Declare a reference variable
            ex: Duck myDuck

        2. Create an object
            ex:             new Duck();

        3. Link the object and the reference
            ex: Duck myDuck = new Duck();

         Duck() = constructor 
         A constructor is the code that runs when you instatiate an object
         public Duck() {
         }

         It runs before the object can be assigned to a reference

         Instance variable do have a default value. 0 or 0.0 for numeric primitives, false for booleans, and null for references.

         setSize method sets the size

         public class Duck {
            int size;

                public Duck(int duckSize)
                    System.out.println("Quack");

                    size = duckSize;

                    Systen.out.println("size is " + size);
                  }
                }
             ___________________________________________________

                public calss UseADuck 
                    
                    public static void main (String[] args) {
                        Duck d = new Duck(42);
                       }
                     }

                If you write a constructor that takes arguments, and you still want a no-arg constructor, you'll have to build the 
                no-arg constructor yourself.
                If you have more than one constructor in a class, the constructors MUST have different argument lists.
                Overloaded constructors
                        -you have more than 1 constructor in your class
                        -you must have different argument lists

                Every objext holds not just its declared variables but also everything from its superclass.
                    -every class extends to that class

                All constructrs in an object's inheritance tree must run when you make a new object.
                When a constructor runs, it immediately calls its superclass constructor, all the way up the chain until you get to                 the class "Object" constructor.

                The only way to call a super constructor is by calling super().
                The superclass parts of an object have to be fully-formed before the subclass parts can be constructed.
                The call to super() must be the first statement in each constructor.


                    ex:

                        public Boop(){
                            super();
                        }

                        public Boop(int i) {
                            super();
                            size = i:

                           }
                  
                  Every constructor can have a call to super() or this() but never both

                  A local variable lives only within the method that declared the variable.
                  An instance variable lives as long as the object does. If the object is still alive so
                  are the instance variables.


                  Life 
                    A local variable is alove as long as its Stack frame is on the Stack.
                    (until the method completes)
                  Scope
                    A local variable is in the scope only within the method in which the variable was declared.
                    When its oen method calls another, the variable is alive, but not in the scope until its
                    method resumes. (You can use a variable only when it is in scope)


                    3 ways to get rid of an object's reference:
                        1. The reference goes out of scope, permanently
                                void go () {
                                    Life z = new Life();
                                   }
                        2. The reference is assigned another objext
                                Life z = new Life();
                                z = new Life();
                        
                        3. The reference is explicitly set to null
                                Life z = new Life();
                                z = null;

                                
                        
