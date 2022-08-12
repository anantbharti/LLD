<h1 align="center">
    Object Oriented Design
 </h1>

 <p align="center">
   Author: Anant Bharti
 </p>
 
 <h4 > Principles of object oriented design</h4>
 
 <h3>
1. Program to an interface not an implementation
</h3>

```java

 interface Shape {

    void draw();
}

class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println(" drawing circle ....");
    }
}

class Rectangle implements Shape {
    @Override
    public void draw() {
        System.out.println(" drawing rectangle ....");
    }
}

class Square implements Shape {
    @Override
    public void draw() {
        System.out.println(" drawing square ....");
    }
}

 public class Test {


    public static void main(String[] args) {
        Shape shape = new Circle();
        print(shape);
	shape = new Square();
	print(shape);
	shape = new Rectangle();
	print(shape);
    }

    private static void print(Shape shape) {
        shape.draw();
    }
}
```
Output

```
drawing circle ....
drawing square ....
drawing rectangle ....
```

```java

// 1. Always use interface type as a reference type.

 // Better
List<String> list = new ArrayList<>(); 

// Avoid
ArrayList<String> list = new ArrayList<>();

// By declaring a collection using an interface type, the code would be more flexible 
// as you can change the concrete implementation easily when needed, 
// for example:
List<String> list = new LinkedList<>();

// Better
Set<String> set = new HashSet<>();

//Avoid
HashSet<String> employees = new HashSet<>();

// Better
Map<String,String> map = new HashMap<>();

//Avoid
HashMap<String,String> map = new HashMap<>();


// 2. Always use interface type as a return type

public Collection listEmployees() {

    List<Employee> employees = new ArrayList<>();
    // add Employees to the list
    return employees;
}

// 3. Always use Interface Types as a method argument

public void foo(Set<Integer> numbers) {
   // do something
}

```
 
<h3>
2. Favor object composition over inheritance
</h3>

<p>
<ol>
	
	i.   Java does not support multiple inheritances
	ii.  Composition offers better test-ability of a class than Inheritance
	iii. Inheritance’s disadvantages is that it breaks encapsulation
	iv.  Flexible enough to replace the better and updated version of the Composed class implementation

</ol>
</p>


```java

// Inheritance

class Person {
 String title;
 String name;
 int age;
}

class Employee extends Person {
 int salary;
 String title;
}

```

```java

// composition

class Person {
 String title;
 String name;
 int age;

 public Person(String title, String name, String age) {
    this.title = title;
    this.name = name;
    this.age = age;
 }

}

class Employee {
 int salary;
 private Person person;

 public Employee(Person p, int salary) {
     this.person = p;
     this.salary = salary;
 }
}

Person p = new Person ("Mr.", "Kapil", 25);
Employee kapil = new Employee (p, 100000);

```
 
 <h3 align="center">
    Design Patterns
 </h3>
 
 | Patterns  | Description |
| --- | --------- |
| **Creational** | These design patterns provide a way to create objects while hiding the creation logic, rather than instantiating objects directly using new operator. This gives program more flexibility in deciding which objects need to be created for a given use case. Ex: Factory, Abstract Factory, Singleton, Builder |
| **Structural** | These design patterns concern class and object composition. Concept of inheritance is used to compose interfaces and define ways to compose objects to obtain new functionalities. Ex: Decorator, Adapter |
| **Behavioral** | These design patterns are specifically concerned with communication between objects. Ex: Behavior |

 
 ### Contents  
 
|   | [Standard Design Patterns](#design-patterns) |
| --- | --------- |
|1   | [Factory](#factory-pattern) |
|2   | [Abstract Factory](#abstract-factory-pattern)|
|3   | [Singleton](#singleton-pattern)|
|4   | [Builder](#builder-pattern) |
|5   | [Decorator](#decorator-pattern) |
|6   | [Adapter](#adapter-pattern) |
|7   | [Strategy](#strategy-pattern) |


##  Factory Pattern

```java

public interface Shape {
   void draw();
}

public class Rectangle implements Shape {

   @Override
   public void draw() {
      System.out.println("Inside Rectangle::draw() method.");
   }
}

public class Square implements Shape {

   @Override
   public void draw() {
      System.out.println("Inside Square::draw() method.");
   }
}

public class Circle implements Shape {

   @Override
   public void draw() {
      System.out.println("Inside Circle::draw() method.");
   }
}

public class ShapeFactory {
	
   //use getShape method to get object of type shape 
   public Shape getShape(String shapeType){
      if(shapeType == null){
         return null;
      }		
      if(shapeType.equalsIgnoreCase("CIRCLE")){
         return new Circle();
         
      } else if(shapeType.equalsIgnoreCase("RECTANGLE")){
         return new Rectangle();
         
      } else if(shapeType.equalsIgnoreCase("SQUARE")){
         return new Square();
      }
      
      return null;
   }
}

public class FactoryPatternDemo {

   public static void main(String[] args) {
      ShapeFactory shapeFactory = new ShapeFactory();

      //get an object of Circle and call its draw method.
      Shape shape1 = shapeFactory.getShape("CIRCLE");

      //call draw method of Circle
      shape1.draw();

      //get an object of Rectangle and call its draw method.
      Shape shape2 = shapeFactory.getShape("RECTANGLE");

      //call draw method of Rectangle
      shape2.draw();

      //get an object of Square and call its draw method.
      Shape shape3 = shapeFactory.getShape("SQUARE");

      //call draw method of square
      shape3.draw();
   }
}
```
Output
```
Inside Circle::draw() method.
Inside Rectangle::draw() method.
Inside Square::draw() method.
```

**[⬆ Back to Top](#----design-patterns-)** 

##  Abstract Factory Pattern

```java

public interface Shape {
   void draw();
}

public class RoundedRectangle implements Shape {
   @Override
   public void draw() {
      System.out.println("Inside RoundedRectangle::draw() method.");
   }
}

public class RoundedSquare implements Shape {
   @Override
   public void draw() {
      System.out.println("Inside RoundedSquare::draw() method.");
   }
}

public class Rectangle implements Shape {
   @Override
   public void draw() {
      System.out.println("Inside Rectangle::draw() method.");
   }
}

public class Square implements Shape {
   @Override
   public void draw() {
      System.out.println("Inside Square::draw() method.");
   }
}

public abstract class AbstractFactory {
   abstract Shape getShape(String shapeType) ;
}

public class ShapeFactory extends AbstractFactory {
   @Override
   public Shape getShape(String shapeType){    
      if(shapeType.equalsIgnoreCase("RECTANGLE")){
         return new Rectangle();         
      }else if(shapeType.equalsIgnoreCase("SQUARE")){
         return new Square();
      }	 
      return null;
   }
}

public class RoundedShapeFactory extends AbstractFactory {
   @Override
   public Shape getShape(String shapeType){    
      if(shapeType.equalsIgnoreCase("RECTANGLE")){
         return new RoundedRectangle();         
      }else if(shapeType.equalsIgnoreCase("SQUARE")){
         return new RoundedSquare();
      }	 
      return null;
   }
}

public class FactoryProducer {
   public static AbstractFactory getFactory(boolean rounded){   
      if(rounded){
         return new RoundedShapeFactory();         
      }else{
         return new ShapeFactory();
      }
   }
}

public class AbstractFactoryPatternDemo {
   public static void main(String[] args) {
      //get shape factory
      AbstractFactory shapeFactory = FactoryProducer.getFactory(false);
      //get an object of Shape Rectangle
      Shape shape1 = shapeFactory.getShape("RECTANGLE");
      //call draw method of Shape Rectangle
      shape1.draw();
      //get an object of Shape Square 
      Shape shape2 = shapeFactory.getShape("SQUARE");
      //call draw method of Shape Square
      shape2.draw();
      //get shape factory
      AbstractFactory shapeFactory1 = FactoryProducer.getFactory(true);
      //get an object of Shape Rectangle
      Shape shape3 = shapeFactory1.getShape("RECTANGLE");
      //call draw method of Shape Rectangle
      shape3.draw();
      //get an object of Shape Square 
      Shape shape4 = shapeFactory1.getShape("SQUARE");
      //call draw method of Shape Square
      shape4.draw();
      
   }
}
```
Output
```
Inside Rectangle::draw() method.
Inside Square::draw() method.
Inside RoundedRectangle::draw() method.
Inside RoundedSquare::draw() method.
```

**[⬆ Back to Top](#----design-patterns-)** 

##  Singleton Pattern

```java

public class SingleObject {

   //create an object of SingleObject
   private static SingleObject instance = new SingleObject();

   //make the constructor private so that this class cannot be
   //instantiated
   private SingleObject(){}

   //Get the only object available
   public static SingleObject getInstance(){
      return instance;
   }

   public void showMessage(){
      System.out.println("Hello World!");
   }
}

public class SingletonPatternDemo {
   public static void main(String[] args) {

      //illegal construct
      //Compile Time Error: The constructor SingleObject() is not visible
      //SingleObject object = new SingleObject();

      //Get the only object available
      SingleObject object = SingleObject.getInstance();

      //show the message
      object.showMessage();
   }
}
```
Output
```
Hello World!
```

**[⬆ Back to Top](#----design-patterns-)** 

##   Builder Pattern

```java

public interface Item {
   public String name();
   public Packing packing();
   public float price();	
}

 public interface Packing {
   public String pack();
}

 public class Wrapper implements Packing {
   @Override
   public String pack() {
      return "Wrapper";
   }
}

 public abstract class Burger implements Item {

   @Override
   public Packing packing() {
      return new Wrapper();
   }

   @Override
   public abstract float price();
}

 public abstract class ColdDrink implements Item {

	@Override
	public Packing packing() {
       return new Bottle();
	}

	@Override
	public abstract float price();
}

 public class VegBurger extends Burger {

   @Override
   public float price() {
      return 25.0f;
   }

   @Override
   public String name() {
      return "Veg Burger";
   }
}

 public class ChickenBurger extends Burger {

   @Override
   public float price() {
      return 50.5f;
   }

   @Override
   public String name() {
      return "Chicken Burger";
   }
}

 public class Coke extends ColdDrink {

   @Override
   public float price() {
      return 30.0f;
   }

   @Override
   public String name() {
      return "Coke";
   }
}

 public class Pepsi extends ColdDrink {

   @Override
   public float price() {
      return 35.0f;
   }

   @Override
   public String name() {
      return "Pepsi";
   }
}

public class Meal {
   private List<Item> items = new ArrayList<Item>();	

   public void addItem(Item item){
      items.add(item);
   }

   public float getCost(){
      float cost = 0.0f;
      
      for (Item item : items) {
         cost += item.price();
      }		
      return cost;
   }

   public void showItems(){
   
      for (Item item : items) {
         System.out.print("Item : " + item.name());
         System.out.print(", Packing : " + item.packing().pack());
         System.out.println(", Price : " + item.price());
      }		
   }	
}

 public class MealBuilder {

   public Meal prepareVegMeal (){
      Meal meal = new Meal();
      meal.addItem(new VegBurger());
      meal.addItem(new Coke());
      return meal;
   }   

   public Meal prepareNonVegMeal (){
      Meal meal = new Meal();
      meal.addItem(new ChickenBurger());
      meal.addItem(new Pepsi());
      return meal;
   }
}

 public class BuilderPatternDemo {

   public static void main(String[] args) {
   
      MealBuilder mealBuilder = new MealBuilder();

      Meal vegMeal = mealBuilder.prepareVegMeal();
      System.out.println("Veg Meal");
      vegMeal.showItems();
      System.out.println("Total Cost: " + vegMeal.getCost());

      Meal nonVegMeal = mealBuilder.prepareNonVegMeal();
      System.out.println("\n\nNon-Veg Meal");
      nonVegMeal.showItems();
      System.out.println("Total Cost: " + nonVegMeal.getCost());
   }
}
```
Output
```
 Veg Meal
 Item : Veg Burger, Packing : Wrapper, Price : 25.0
 Item : Coke, Packing : Bottle, Price : 30.0
 Total Cost: 55.0

 Non-Veg Meal
 Item : Chicken Burger, Packing : Wrapper, Price : 50.5
 Item : Pepsi, Packing : Bottle, Price : 35.0
 Total Cost: 85.5
```

**[⬆ Back to Top](#----design-patterns-)** 

##  Decorator Pattern

```java

public interface Shape {
   void draw();
}

public class Rectangle implements Shape {

   @Override
   public void draw() {
      System.out.println("Shape: Rectangle");
   }
}

public class Circle implements Shape {

   @Override
   public void draw() {
      System.out.println("Shape: Circle");
   }
}

public abstract class ShapeDecorator implements Shape {

   protected Shape decoratedShape;

   public ShapeDecorator(Shape decoratedShape){
      this.decoratedShape = decoratedShape;
   }

   public void draw(){
      decoratedShape.draw();
   }	
}

public class RedShapeDecorator extends ShapeDecorator {

   public RedShapeDecorator(Shape decoratedShape) {
      super(decoratedShape);		
   }

   @Override
   public void draw() {
      decoratedShape.draw();	       
      setRedBorder(decoratedShape);
   }

   private void setRedBorder(Shape decoratedShape){
      System.out.println("Border Color: Red");
   }
}

public class DecoratorPatternDemo {

   public static void main(String[] args) {

      Shape circle = new Circle();

      Shape redCircle = new RedShapeDecorator(new Circle());

      Shape redRectangle = new RedShapeDecorator(new Rectangle());
      System.out.println("Circle with normal border");
      circle.draw();

      System.out.println("\nCircle of red border");
      redCircle.draw();

      System.out.println("\nRectangle of red border");
      redRectangle.draw();
   }
}
```
Output
```
 Circle with normal border

 Shape: Circle

 Circle of red border
 Shape: Circle
 Border Color: Red

 Rectangle of red border
 Shape: Rectangle
 Border Color: Red
```

**[⬆ Back to Top](#----design-patterns-)** 

##  Adapter Pattern

```java

 public interface MediaPlayer {

   public void play(String audioType, String fileName);
}

 public interface AdvancedMediaPlayer {	

   public void playVlc(String fileName);
   public void playMp4(String fileName);
}

 public class VlcPlayer implements AdvancedMediaPlayer{

   @Override
   public void playVlc(String fileName) {
      System.out.println("Playing vlc file. Name: "+ fileName);		
   }

   @Override
   public void playMp4(String fileName) {
      //do nothing
   }
}

 public class Mp4Player implements AdvancedMediaPlayer{

   @Override
   public void playVlc(String fileName) {
      //do nothing
   }

   @Override
   public void playMp4(String fileName) {
      System.out.println("Playing mp4 file. Name: "+ fileName);		
   }
}

 public class MediaAdapter implements MediaPlayer {

   AdvancedMediaPlayer advancedMusicPlayer;

   public MediaAdapter(String audioType){
   
      if(audioType.equalsIgnoreCase("vlc") ){
         advancedMusicPlayer = new VlcPlayer();			
         
      }else if (audioType.equalsIgnoreCase("mp4")){
         advancedMusicPlayer = new Mp4Player();
      }	
   }

   @Override
   public void play(String audioType, String fileName) {
   
      if(audioType.equalsIgnoreCase("vlc")){
         advancedMusicPlayer.playVlc(fileName);
      }
      else if(audioType.equalsIgnoreCase("mp4")){
         advancedMusicPlayer.playMp4(fileName);
      }
   }
}

 public class AudioPlayer implements MediaPlayer {

   MediaAdapter mediaAdapter; 

   @Override
   public void play(String audioType, String fileName) {		

      //inbuilt support to play mp3 music files
      if(audioType.equalsIgnoreCase("mp3")){
         System.out.println("Playing mp3 file. Name: " + fileName);			
      } 
      
      //mediaAdapter is providing support to play other file formats
      else if(audioType.equalsIgnoreCase("vlc") || audioType.equalsIgnoreCase("mp4")){
         mediaAdapter = new MediaAdapter(audioType);
         mediaAdapter.play(audioType, fileName);
      }
      
      else{
         System.out.println("Invalid media. " + audioType + " format not supported");
      }
   }   
}

 public class AdapterPatternDemo {

   public static void main(String[] args) {
      AudioPlayer audioPlayer = new AudioPlayer();

      audioPlayer.play("mp3", "beyond the horizon.mp3");
      audioPlayer.play("mp4", "alone.mp4");
      audioPlayer.play("vlc", "far far away.vlc");
      audioPlayer.play("avi", "mind me.avi");
   }
}
```
Output
```
Playing mp3 file. Name: beyond the horizon.mp3
Playing mp4 file. Name: alone.mp4
Playing vlc file. Name: far far away.vlc
Invalid media. avi format not supported
```

**[⬆ Back to Top](#----design-patterns-)** 

##  Strategy Pattern

```java

 public interface Strategy {

   public int doOperation(int num1, int num2);
}

public class OperationAdd implements Strategy{

   @Override
   public int doOperation(int num1, int num2) {
      return num1 + num2;
   }
}

public class OperationSubstract implements Strategy{

   @Override
   public int doOperation(int num1, int num2) {
      return num1 - num2;
   }
}

public class OperationMultiply implements Strategy{

   @Override
   public int doOperation(int num1, int num2) {
      return num1 * num2;
   }
}

public class Context {

   private Strategy strategy;

   public Context(Strategy strategy){
      this.strategy = strategy;
   }

   public int executeStrategy(int num1, int num2){
      return strategy.doOperation(num1, num2);
   }
}

public class StrategyPatternDemo {

   public static void main(String[] args) {
      Context context = new Context(new OperationAdd());		
      System.out.println("10 + 5 = " + context.executeStrategy(10, 5));

      context = new Context(new OperationSubstract());		
      System.out.println("10 - 5 = " + context.executeStrategy(10, 5));

      context = new Context(new OperationMultiply());		
      System.out.println("10 * 5 = " + context.executeStrategy(10, 5));
   }
}
```
Output
```
10 + 5 = 15
10 - 5 = 5
10 * 5 = 50
```

**[⬆ Back to Top](#----design-patterns-)** 
