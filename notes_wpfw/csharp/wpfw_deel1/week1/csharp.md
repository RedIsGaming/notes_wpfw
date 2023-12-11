# Intro

Hier vind je de onderdelen van lesweek1. Alles wat je moet weten van deze week wat ook in het #toetsmatrijs staat beschreven. Als er een stukje staat met dat er nog later uitleg komt, dan vul ik dat later in. Er is geen garantie dat #code  perfect is. Daar gaat het niet om. Als je de #code  shit vindt, dan snap je niet het punt, want het gaat puur om het concept. 

Als je de concepten begrijpt, dan ben je al een stap vooruit. Voor vragen of opmerkingen kun je me altijden dmen op #Discord: redisgaming of #Whatsapp. Deze intro zal ook in de andere documenten als intro staan, dus al je dit hebt gelezen, kun je de intro H1 skippen. Voor de rest ben ik meer gefocust op voorbeelden dan op het uitleggen. Houdt daar rekening mee. Good luck :)

> Note: De uitleg is in het Nederlands. De code en H2/H3 in het Engels.

## Method Hiding

```C#
//namespace ConsoleApp1;  
  
public struct Bar(string type, ushort weight, ushort protein)  
{  
  public string Type { get; set; } = type;  
  public ushort Weight { get; } = weight;  
  public ushort Protein { get; } = protein;  
}  
  
public class MethodNotHiding  
{  
  public virtual void Print(Bar bar)   
  {  
    var print = $"The Proteine Bar is called: {bar.Type}.\n" +  
    $"Which weights: {bar.Weight}.\n" +  
    $"And contains: {bar.Protein}.\n";  
      
    Console.WriteLine($"\n{print}");  
  }   
}  
  
public class MethodHiding : MethodNotHiding  
{  
  public sealed override void Print(Bar bar)  
  {  
    var print = $"The Proteine Bar is called: {bar.Type = "Grenade"}.\n" +  
    $"Which weights: {bar.Weight}.\n" +  
    $"And contains: {bar.Protein}.\n";  
      
    Console.WriteLine($"\n{print}");  
  }  
}

//Add this struct/classes in a seperate file or place it somewhere you like.

```

We hebben hierboven een #public #struct Bar die dient als een proteine reep. We hebben 3 arguments in de #Primary-Constructor . Die geven we mee aan de #Properties. Type is aanpasbaar, de rest is #readonly. Vervolgens maken me twee nieuwe #class aan. MethodNotHiding en de andere MethodHiding die inherited van MethodNotHiding.

We maken 1 method aan genaamd: Print. Hierin geven we 1 argument van type Bar. Ze hebben allebij precies dezelfde implementatie, maar bij de MethodHiding #class wordt de Bar Type aangepast. Vervolgens printen we dat op het scherm in Main. We maken hieronder een nieuw #object aan van Bar met de waardes. Ook roepen we de methods aan en geven we Bar mee.

```C#
namespace ConsoleApp1;

public class Program 
{
  private static void Hide()  
  {  
    var bar = new Bar("Bom123", 80, 25);  
  
    var methodNotHiding = new MethodNotHiding();  
    methodNotHiding.Print(bar);  
    
    MethodNotHiding methodHiding = new MethodHiding();  
    methodHiding.Print(bar);  
  }

  public static void Main() {} //Call method here between {}.
}

//Call this method in public static void Main() {} for it to work.

```

### Scheme Result Method Hiding

| MethodNotHiding(A) | MethodHiding(B) | Resultaat(C) |
| --- | --- | --- |
| <span style=color:00FF00>x</span> | <span style=color:00FF00>x</span> | "Bom123" |
| sealed override | <span style=color:00FF00>x</span> | <span style=color:#FF0000>error</span>, There is no suitable method for override. |
| virtual | <span style=color:00FF00>x</span> | "Bom123" && <span style=color:#FFFF00>warning</span>, Virtual method 'Print' is never overridden. |
| <span style=color:00FF00>x</span> | new | "Bom123" |
| sealed override | new | <span style=color:#FF0000>error</span>, There is no suitable method for override. |
| virtual | new | "Bom123" |
| <span style=color:00FF00>x</span> | override | <span style=color:#FF0000>error</span>, There is no suitable method for override. |
| sealed override | override | <span style=color:#FF0000>error</span>, There is no suitable method for override. |
| virtual | override | "Grenade" |
| <span style=color:00FF00>x</span> | sealed override | <span style=color:#FF0000>error</span>, There is no suitable method for override. |
| sealed override | sealed override | <span style=color:#FF0000>error</span>, There is no suitable method for override. |
| virtual | sealed override | "Grenade" |

> Bij override zien we dat het result anders wordt. In andere gevallen wordt deze method gehided.

## Properties

```C#
//namespace ConsoleApp1;  
  
public struct Property(string level)  
{  
  public required string Easy { get; init; } = level;  
  public string Normal { get; } = level;  
    
  public required string Hard {   
    get   
    {  
      return level;  
    }
  
    init  
    {  
      level = value;  
    }  
  }  
}

//Add this struct in a seperate file or place it somewhere you like.

```

Hierboven hebben we een #Property #struct met een #Primary-Constructor met 1 argument van #string level. Daarbij hebben we 3 #Properties aangemaakt. De eerste is een #auto-implemented #Property . Deze heeft een ingebouwde getter en een setter. #init betekent, dat je na het aanmaken van de #Property je deze niet meer mag aanpassen.

De #state wordt #immutable. De tweede is een #readonly . Deze kan alleen via de #constructor worden meegegeven en kan dus niet worden ingevuld apart als #object initializer. #required is dat het #object deze moet gebruiken. De laatste is een #Property waarin je bepaalde waardes kan aangeven. Om dit simpel te houden gebruiken we een getter en een setter.

```C#
namespace ConsoleApp1;

public class Program 
{
  private static void DumbProperty()  
  {  
    var property = new Property("Just fucking easy!!!")  
    {  
      Easy = "Easy",  
      Hard = "Hard"  
    };  
  
    Console.WriteLine(  
      $"The current levels have the following difficulties: {property.Easy}.\n" +  
      $"{property.Normal} and {property.Hard}.\n"  
    );
    
	/*The current levels have the following difficulties: Easy. 
	Just fucking easy!!! and Hard.*/
  }

  public static void Main() {} //Call method here between {}.
}

//Call this method in public static void Main() {} for it to work.

```

> Hier zie je wat de #code doet. Wanneer je dit runt, zul je het volgende resultaat krijgen:
> 
> The current levels have the following difficulties: Easy. 
> Just fucking easy!!! and Hard.

## #Contravariance and #Covariance

### #Contravariance and #Covariance Example 1

```C#
//namespace ConsoleApp1  
  
interface IProducer<out T> //Covariance, out, high to low, get.  
{  
  public T Produce();  
}  
  
interface IConsumer<in T> //Contravariance, in, low to high, args.  
{  
  public void Consume(T obj);  
}  
  
class Producer<T> : IProducer<T> //Covariance, return, no args.  
{  
  public T Produce() => default;  
}  
  
class Consumer<T> : IConsumer<T> //Contravariance, no return, args.  
{  
  public void Consume(T obj)  
  {  
    Console.WriteLine($"This contravariance returns: {obj}.\n");  
  }  
}  

//Add this classes/interfaces in a seperate file or place it somewhere you like.

```

Hierboven is de layout voor #contravariantie en #covariantie. Schrik niet. Ik zal precies uitleggen wat het nou eigenlijk is. We maken 2 #interface en #class aan. In IProducer passen we #covariantie toe. Dit geven we expliciet met het keyword #out. Je kunt het zien als argument is uit de method en als return type. #T heeft een return type met waarde #T.

Daarna laten we #class Producer inheriten van IProducer. Beide hebben de #generics waarde van #T. Voor #T returnen we #default. Dit zet alle waardes op #null of de absolute 0 waarde wanneer dit van toepassing is. Dan hebben we een #interface IConsumer. Hier passen we #contravariantie toe. Met het keyword #in maak je #T expliciet #contravariant.

Je ziet dat we geen return type hebben. Wel hebben we een obj argument van type #T. #in is als argument in de method. Dit is van laag naar hoog, #contravariantie is van hoog naar laag. Vervolgens hebben we een #class Consumer met type #T als #generics type. Daarna implementeren we de method met argument obj van type #T. We zetten hier onze #code.

> We zetten daar het volgende in: #Console.WriteLine($"This contravariance returns: {obj}.\n");

### #Contravariance and #Covariance Result

```C#
namespace ConsoleApp1;

public class Program 
{
  private static void Variant()  
  {  
    IProducer<char> producer = new Producer<char>(); //Covariance  
    IConsumer<char> consumer = new Consumer<char>(); //Contravariance  
  
    producer.Produce();  
    consumer.Consume('h');  
  }

  public static void Main() {} //Call method here between {}.
}

//Call this method in public static void Main() {} for it to work.

```

We roepen het programma aan met de #interface en maken twee objecten aan. Hierboven zie je #Covariance en #Contravariance in actie. Het is duidelijk wat het resultaat is van deze code.

> Het volgende resultaat is: This #contravariance returns: h.

### #Contravariance and #Covariance Example 2

We maken een super simpel programma. 2 #class met eentje genaamd: Base en de andere genaamd: Derived. Deze inherited van Base. Beide #class hebben hun eigen method, die iets uitprinten in de #Console . In Program hebben we ook 2 methods die we gebruiken voor de #Action. In de uitleg in de #code kun je precies zien hoe dit nou eigenlijk te werk gaat.

```C#
namespace ConsoleApp1; 

public class Base 
{ 
  public void PrintBase() 
  { 
    Console.WriteLine("Base"); 
  } 
} 

public class Derived : Base 
{ 
  public void PrintDerived() 
  { 
    Console.WriteLine("Derived"); 
  } 
} 

public class Program 
{ 
  private static void PrintActionBase(Base b) 
  { 
    Console.WriteLine("Action Base"); 
  } 
  
  private static void PrintActionDerived(Derived d) 
  { 
    Console.WriteLine("Action Derive"); 
  } 
  
  public static void Main() 
  { 
    var base1 = new Base(); //Invariant met implicit typing 
    Derived derived1 = new(); //Invariant met new() object
    
    object Base base2 = new Derived(); //Covariant, hoog naar laag 
    Derived derived2 = new Base(); //Contravariant, laag naar hoog
      
    List<Base> base3 = new List<Derived>(); //Covariant, hoog naar laag 
    List<Derived> derived3 = new List<Base>(); //Contravariant, laag naar hoog
      
	IEnumerable<Base> base4 = new List<Derived>(); //Covariant, werkt met een type dat hoger is. //In dit geval de IEnumerable. Interfaces kunnen alleen voor de eerste komen te staan. 
	IEnumerable<Derived> derived4 = new List<Base>(); //Contravariant, werkt niet met een type dat lager is, je krijgt //hierop een error. Type 'Base' doesn't match expected type 'Derived'. 
	  
	Action<Base> base5 = new Action<Derived>(PrintActionDerived); //Covariant, werkt niet met een type dat hoger is. Je krijgt hierop een error.
	Action<Derived> derived5 = new Action<Base>(PrintActionBase); //Contravariant, werkt met eem type dat lager is. In dit geval de Action. Interfaces kunnen alleen voor de eerste komen te staan.
  } 
}

```

> Hierboven staat in het Nederlands uitgelegd, wat #covariantie en #contravariantie nou doen.

### #Contravariance and #Covariance Example 3

Hier zullen we de boven genoemde voorbeelden nog verder verduidelijken. We maken 2 #interface en #class aan en doen daar iets mee. IGalaxy en Planet zijn #covariant. IPlanet en Orbit zijn #contravariant. We zullen met #object en #string werken. Let goed op de keywords: #out en #in. In de #code staat in het Nederlands beschreven hoe dit allemaal te werk gaat.

```C#
namespace ConsoleApp1;  
  
public interface IGalaxy<out T> //Covariance, keyword => out, want type T is uit de argument list.  
{  
  public T? Covariance(); //Return type T  
}  
  
public class Planet : IGalaxy<string> //Verander dit van string naar object en het return type ook, wat merk je op?  
{  
  public string Covariance() => "Planet"; //Return type  
}  
  
public interface IPlanet<in T> //Contravariance, keyword => in, want type T is in de argument list.  
{  
  public void Contravariance(T obj); //Argument type T  
}  
  
public class Orbit : IPlanet<object> //Verander dit van object naar string en het argument type ook, wat merk je op?  
{  
  public void Contravariance(object obj) => Console.WriteLine(obj); //Argument type  
}  
  
public class Program  
{  
  public static void Main()  
  {  
    //Allemaal high to low, maar:
     
    IGalaxy<object> galaxy = new Planet(); //Het is covariant, kijk naar de type tussen <>. Ik kan object erin stoppen en  
    //vervangen met string. Dit werkt, want object is een collectie die de string in zich heeft. Dit werkt.    
    IGalaxy<string> extraGalaxy = new Planet(); //Invariant type werkt ook.  
    //IGalaxy<string> g = new Planet(); //Contravariant werkt niet hierop. string kan niet naar object. Zie regel 8/10.    
    
    IPlanet<string> planet = new Orbit(); //Het is Contravariant, kijk naar de type tussen <>. Ik kan string erin stoppen  
    //en vervangen met object. Dit werkt, want string behoort tot een collectie die vanuit object komt. Dit werkt.    
    IPlanet<object> extraplanet = new Orbit(); //Invariant type werkt ook.  
    //IPlanet<object> p = new Orbit(); //Covariant werkt niet hierop. object kan niet naar string. Zie regel 18/20.  
  }
}

```

> Hierboven staat in het Nederlands uitgelegd, wat #covariantie en #contravariantie nou doen.

## Generics and Generic Type Constraints

Wat zijn #generics? #Generics zijn waardes die je kan toekennen om #type-safety te garanderen. Elke letter geeft aan van welke type het moet zijn en die kun je met Generic Type Constraints beheren. De hoofdletters tussen <> zijn de generics. In dit voorbeeld kan #T voor elk mogelijk datatype gebruikt worden mits die aan de voorwaarden voldoet die je eraan geeft. 

```C#
using System.Numerics;  
//namespace ConsoleApp1;  
  
public struct Generic<T, R>  
where T : INumber<T>  
where R : IConvertible  
{  
  public T Count(T a, R b) => a + (T) Convert.ChangeType(b, typeof(T));  
}

//Add this struct in a seperate file or place it somewhere you like.

```

Hierbij is #T #ushort / #u16 en #R #float / #f32. Deze heeft de Generic Type Constraint van #INumber. Dit is een #interface constraint die alleen om numerieke waardes werkt. Vervolgens kennen we die #T daaraan toe. Zolang het een numerieke waarde is, maakt de soort ervan niet uit. #R is een #IConverible. Een andere #interface waarbij je een type kan converten.

Maar dat even terzijde. We hebben een method met het return type #T. De argumenten hebben a als #T en b als #R. Om dit te kunnen returnen, moeten de types wel gelijk zijn aan elkaar alvorens ze kunnen worden gereturnd. Om a en b te kunnen optellen en te kunnen returnen, veranderen we b die #R heeft met type van #T. In de #code block zie je dit in werking.

```C#
namespace ConsoleApp1;

public class Program 
{
  private static void TypeConstraint()  
  {  
    var x = new Generic<ushort, float>().Count(5, 4);  
    Console.WriteLine($"Result is: {x}.\n"); //Result is: 9.
  }
  
  public static void Main() {} //Call method here between {}.
}

//Call this method in public static void Main() {} for it to work.

```

We maken hier een variabele x, waarin we een nieuw #object aanmaken. Daarin kunnen we meteen de method aanroepen. De types die je tussen <> geeft, moeten gelijk zijn aan het type dat je als argument in de argument lijst zet. Dit om #type-safety te garanderen. Wat gebeurd er als je een #string toevoegt in plaats van een #float / #f32 ? Wat gebeurd er dan? Kijk goed.

> Het resultaat is het volgende: Result is: 9.

## Object and List Initializers

Hier gebruiken we weer #generics voor #type-safety. Aan dit stukje valt niet veel uit te leggen. We geven een #T mee en die geven we ook mee als argument in latitude en longtitude. Daarna maken we een #Property aan waarin we deze #fields aan kunnen toevoegen. Hier kunnen we elke type aan geven, want we printen letterlijk uit, nadat we een waarde hebben toegekend.

```C#
//namespace ConsoleApp1;  
  
public struct Initializer<T>(T latitude, T longtitude)  
{  
  public T Latitude { get; init; } = latitude;  
  public T Longtitude { get; init; } = longtitude;  
}

//Add this struct in a seperate file or place it somewhere you like.

```

In de method maken we een nieuwe #object aan en die geven we het type #float / #f32. We kunnen deze toevoegen als fields in de #Primary-Constructor. Dit zijn de arguments die je aan het begin neerzet, zodat je niet een vieze #constructor hoeft te maken, wat weer extra regels aan code oplevert. Het is eigenlijk #syntactic-suger. De waardes tussen { } zijn de initializers.

Een #object initializer zijn de waardes tussen { } die aan een object is gekoppeld. Deze overriden de waardes van de #Primary-Constructor. Vervolgens maken we een nieuwe variabele data aan en maken we daarvan een #List. Die geven we een initializer #struct mee met het type #float / #f32. 

```C#
namespace ConsoleApp1;

public class Program 
{
  private static void Initialize()  
  {  
    var initialize = new Initializer<float>(4.653861f, 3.293164f)  
    {  
      Latitude = 6.490459f,  
      Longtitude = 2.640913f  
    };  
  
    var data = new List<Initializer<float>> { initialize }; // For illustration purposes. You can do with the List whatever your want. 
	var print = $"The following latitude/longtitude are: {initialize.Latitude} and {initialize.Longtitude}.\n";
	Console.WriteLine(print); 
	//The following latitude/longtitude are: 6.490459 and 2.640913.
  }
  
  public static void Main() {} //Call method here between {}.
}

//Call this method in public static void Main() {} for it to work.

```

> Resultaat: The following latitude/longtitude are: 6.490459 and 2.640913.

Omdat de eerste variabele het juiste type heeft, kunnen we hiervan een #List initializer van maken. Ook dit gaat tussen de { }. Vervolgens printen we dit op het scherm en krijg je nieuwste waarde terug. Als je de #generics datatype hier aanpast, moeten beide variabelen compatibel zijn, anders moet je een extra #generics type in de #struct zetten: #R. Mag ook anders heten.

## Operator Overloading

Het is niet mogelijk om in C# met twee dezelfde klassen, records of structs een Arimathic operatie uit te voeren. Dit kan wel worden gedaan met een Operator Overloading met het keyword #operator. Om dit succesvol uit te voeren moet de overload aan de juiste voorwaarden voldoen. De operator moet #public zijn en #static. 

Daarnaast moet het return type overeen komen met het type die je in de #class, #record of #struct aangeeft. In dit voorbeeld is dat #Overloading. Voor de method met de parameters of direct aan de #operator  zelf geef je een #operator type mee. In dit voorbeeld is dat +. Dit is niet het enige type wat je aan een #operator kan meegeven, maar we houden het simpel.

```C#
//namespace ConsoleApp1;

public struct Overloading(uint result)  
{  
  public uint Result { get; } = result;
  public static Overloading operator +(Overloading a, Overloading b) => new(a.Result - b.Result);  
}

//Add this struct in a seperate file or place it somewhere you like.

```

Zoals je ziet hoef je geen method naam toe te voegen. Dat is niet nodig en levert bovendien een error op als je dit wel neerzet. De argument bevat het type die uit de #class , #record  of #struct vandaan komt, dus #Overloading . We hebben hier een #Property  van type #uint of #u32 van #Result . 

Daarin geven we een #field mee die we aan de #Property meegeven. Vervolgens returnen we het resultaat van a en b #Result die we van elkaar aftrekken. De operatie in de return type is leidend en zal dus het effect overriden. Bovendien moet de #operator  type als in de call van de variabele overeenkomen, anders krijg je een error.

```C#
namespace ConsoleApp1;

public class Program 
{
  private static void Operator()  
  {  
    var a = new Overloading(6);  
    var b = new Overloading(2);  
    var c = a + b;  
    Console.WriteLine($"Result after operator overloading is: {c.Result}.\n");
    //Result after operator overloading is: 4. 
  }

  public static void Main() {} //Call method here between {}.
}

//Call this method in public static void Main() {} for it to work.

```

> Resultaat: Result after operator overloading is: 4.

Hier maken we een method, waarin we de #operator gaan implementeren. We maken twee impliciete variabelen aan met onze struct #Overloading . Die krijgen het type die we aan hebben gegeven in de #struct , namelijk #uint / #u32. Daarna tellen we die op en tonen we dit in de #Console. Het resultaat is niet 6 + 2 = 8, maar 6 - 2 = 4. Het return type is leidend.

Je kunt deze twee stukken #code uitvoeren en kijken wat het precies doet. Deed het wat je had verwacht? Roep de Operator method aan in Main en zie wat er gebeurd. Probeer eens een keer of een min in variabele c aan te passen. Krijg je een foutmelding of gaat dit goed? Wat gebeurd er wanneer je het return arithmatic operatoie aanpast? Test dit uit en zie wat er tevoorschijn komt.

## Implicit Types

In dit voorbeeld zal er niet een uitgebreide #code voorbeeld gegeven worden. Gezien de vele types die er in C# zijn. Hoe je dit implementeert is aan jou.

```C#
var number = 0; //byte, sbyte, ushort, short, uint, int, ulong, long, BigInteger
var floatPoint = 0.0f; //float
var decimalPoint = 0.0; //double of decimal
var boolean = true; //bool
var character = 'P' //char
var str = "Skill issue"; //string
var enum = Enum.TYPE; //enum, after calling the Enum, you put the value after this with the TYPE you defined in your custom enum.
var structure = new Struct(); //struct, a struct that you defined somewhere.
var class = new Class() //class, a class that you defined somewhere.
var list = new List<int>(); //List<T>, A empty list which you can assign any type too.
var record = new Record(); //record, a record that you defined somewhere.
var recordStruct = new RecordStruct(); //record struct, a record struct that you defined somewhere.
var obj = new Object(); //Object
//There are more types available, but I won't display them all!
```

Je maakt een implicit type met het keyword #var . Tijdens #compile-time wordt het type aangegeven die je eraan wilt geven. Hierboven is een voorbeeld met de mogelijke waardes.

## Extension Methods

```C#
//namespace ConsoleApp1;
  
public static class Method  
{  
  public static double Extension(this double x, double y) => x + y;  
}

//Add this class in a seperate file or place it somewhere you like.

```

Een extension method stelt je in staat om een method te callen zonder deze #class te hoeven aanroepen. Om een extension method succesvol te implementeren, moet de #class en de extension method #static zijn. Daarbij moet de eerste argument #this zijn. In dit voorbeeld hebben we twee variabelen van type #double / #f64. De #this moet hetzelfde type hebben.

#this en de return type moeten hetzelfde zijn, want anders krijg je een error. In dit geval zullen we deze variabelen met elkaar optellen. We maken in de Program #class een method aan die op 2 manieren doorgegeven wordt. De extend variabele is een extension method waarin deze voor de arguments worden ingevuld. Daarna printen we dit op het scherm. De datatypes komen overeen.

```C#
namespace ConsoleApp1;

public class Program 
{
  private static void ExtensionMethod()  
  {  
    const double DEVIL = 333.0;  
    var extend = DEVIL.Extension(DEVIL); //Extension Method call
    var overextend = Method.Extension(DEVIL, DEVIL); 
    Console.WriteLine($"Local variable extends with value: {extend} and overextends with value: {overextend}."); 
    //Local variable extends with value: 666 and overextends with value: 666.
  }

  public static void Main() {} //Call method here between {}.
}

//Call this method in public static void Main() {} for it to work.

```

> Resultaat: Local variable extends with value: 666 and overextends with value: 666.

## Value and Reference Types, Structs

### #value-types

```C#
sbyte //i8
byte //u8
short //i16
ushort //u16
int //i32
uint //u32
long //i64
ulong //u64
BigInteger //i128
double //f64
float //f32
decimal //decimal
struct
enum
record struct
char //2 bytes or 16 bits
```

Hier zie je de types voor #value-types en #reference-types. #value-types worden op de #stack geplaatst. Een kopie van een waarde. #reference-types worden op de #heap opgeslagen. Dit is #pointer van de #stack die op de #heap leeft. Het is een #memory-address die geheugen uit #ram allocate. De Garbage Collector (GC) managed een groot gedeelte al voor je.

### #reference-types

```C#
string
array //[]
List<T>
dynamic
delegate
class
interface
record
IEnumerable<T>
Object
```

> Er zijn nog meer types, maar om het simpel te houden laten we het hierbij.

### #struct

```C#
//namespace ConsoleApp1;
  
struct Point(int x, int y)  
{  
  public int X { get; set; } = x;  
  public int Y { get; set; } = y;  
}

//Add this struct in a seperate file or place it somewhere you like.

```

Hier komt later nog wat uitleg.

```C#
namespace ConsoleApp1;

public class Program 
{  
  public static void Main()  
  {
    var point = new Point(4, 6);  
    Console.WriteLine($"Point x is: {point.X}.\nPoint y is: {point.Y}.");  
    Console.WriteLine($"Point x is now: {point.X = 6}.\nPoint y is now: {point.Y = 4}.");
    /*Point x is: 4.
    Point y is 6.
	Point x is now: 6.
	Point y is now: 4.*/
  }  
}

//No seperate method made here. You can directly call this to see the result.

```

> Resultaat: Point x is: 4.
> Point y is 6.
> Point x is now: 6.
> Point y is now: 4.
