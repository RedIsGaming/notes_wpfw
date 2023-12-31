> Note: Explicit, Eager en Lazy Loading wordt ook in dit hoofdstuk beschreven.

# Intro

Hier vind je de onderdelen van lesweek4. Alles wat je moet weten van deze week wat ook in het #toetsmatrijs staat beschreven. Als er een stukje staat met dat er nog later uitleg komt, dan vul ik dat later in. Er is geen garantie dat #code  perfect is. Daar gaat het niet om. Als je de #code  shit vindt, dan snap je niet het punt, want het gaat puur om het concept. 

Als je de concepten begrijpt, dan ben je al een stap vooruit. Voor vragen of opmerkingen kun je me altijden dmen op #Discord: redisgaming of #Whatsapp. Deze intro zal ook in de andere documenten als intro staan, dus al je dit hebt gelezen, kun je de intro H1 skippen. Voor de rest ben ik meer gefocust op voorbeelden dan op het uitleggen. Houdt daar rekening mee. Good luck :)

> Note: De uitleg is in het Nederlands. De code en H2/H3 in het Engels.

## #linq

Wat is #linq? #linq staat voor Language Integrated Query en is bedoeld om iets met de #state te doen op een #collection. Een #collection , zoals een #array, #Dictionary / #Hashmap of #List kun je gebruiken om bepaalde data in op te slaan. #Hashmap bestaat niet in C#, dat is iets voor Java, daarvoor heb je #Dictionary .

Op de #collection kun je elementen toevoegen, verwijderen, een bepaald element ophalen, converten, sorteren, omkeren, iets opzoeken, kijken of het van een bepaald type is, checken of de waarde wel de waarde is die het bevat, naar andere #collection omzetten en nog veel meer. Omdat dit buiten de scope zit van het onderwerp, gaan we snel verder met de lijst van #linq .

#linq kent twee soorten syntaxxen. #method-syntax en #query-syntax. Omdat we alleen #method-syntax hoeven te weten, zullen we #query-syntax niet behandelen hier. Hieronder is een lijst van alle (66) methods die op de #collection zitten. Schrik niet. Na deze lijst is er een korte versie, van de methods die je moet weten op de toets voor #wpfw deel1. Het type is aangegeven.

## #linq #method-syntax All

```C#
Aggregate //TSource
All //bool
Any //bool
Append //IEnumerable<TSource>
Average //double
Cast<> //IEnumerable<TResult>
Chunk //IEnumerable<TSource[]>
Concat //IEnumerable<TSource>
Count //int
Distinct //IEnumerable<TSource>
Except //IEnumerable<TSource>
First //Tsource
Intersect //IEnumerable<TSource>
Join //IEnumerable<TResult>
Last //TSource
Max //int
Min //int
Order //IOrderedEnumerable<T>
Prepend //IEnumerable<TSource>
Select //IEnumerable<TResult>
Single //TSource
Skip //IEnumerable<TSource>
Sum //int
Take //IEnumerable<TSource>
Union //IEnumerable<TSource>
Where //IEnumerable<TSource>
Zip //IEnumerable<(TFirst First, TSecond, Second)>
AsEnumerable //IEnumerable<TSource>
AsParellel //ParallelQuery
AsQueryable //IQueryable
DistinctBy //IEnumerable<TSource>
ElementAt //TSource
ExceptBy //IEnumerable<TSource>
GroupBy //IEnumerable<IGrouping<TKey,TSource>>
GroupJoin //IEnumerable<TResult>
IntersectBy //IEnumerable<TSource>
LongCount //long
MaxBy //TSource?
MinBy //TSource?
OfType<> //IEnumerable<TResult>
OrderBy //IOrderedEnumerable<TSource>
OrderDescending //IOrderedEnumerable<T>
SelectMany //IEnumerable<TResult>
SequenceEqual //bool
SkipLast //IEnumerable<TSource>
SkipWhile //IEnumerable<TSource>
TakeLast //IEnumerable<TSource>
TakeWhile //IEnumerable<TSource>
ToDictionary //Dictionary<TKey,Tsource>
ToLookup //ILookup<TKey,TSource>
UnionBy //IEnumerable<TSource>
DefaultIfEmpty //IEnumerable<TSource?>
FirstOrDefault //TSource?
LastOrDefault //TSource?
OrderByDescending //IEnumerable<TSource>
SingleOrDefault //TSource?
ToHashSet //HashSet<TSource>
ElementAtOrDefault //TSource?
TryGetNonEnumeratedCount //bool
ToFrozenDictionary //FrozenDictionary<TKey,TSource>
ToFrozenSet //FrozenSet<T>
ToImmutableArray //ImmutableArray<TSource>
ToImmutableDictionary //ImmutableDictionary<TKey,TSource>
ToImmutableList //ImmutableList<TSource>
ToImmutableHashSet //ImmutableHashSet<TSource>
ToImmutableSortedDictionary //ImmutableSortedDictionary<TKey,TSource>
ToImmutableSortedSet //ImmutableSortedSet<TSource>
```

> Je hoeft niet alles van deze lijst te weten.

## #linq #method-syntax Required

- #Aggregate is een #accumulator die een aantal elementen samenvoegt tot 1 resultaat. Je kan dit bijvoorbeeld gebruiken in combinatie met een #lambda expression. Als voorbeeld kun je twee getallen met elkaar optellen of aftrekken, wat samengevoegd wordt tot 1 resultaat.

- #All checkt of alle waarde uit de #collection voldoen aan een bepaalde voorwaarde.
- #Any checkt of tenminste 1 waarde uit de #collection voldoen aan een bepaalde voorwaarde.
- #Average pakt het gemiddelde van alle elementen samen uit de #collection . Dit werkt alleen op arithmatic datatypes en dus niet op string bijvoorbeeld.

- #Count telt het aantal elementen in de #collection . Werkt alleen op arithmatic datatypes. #Count eindigt niet op ( ) wanneer je deze aanroept in de IDE. Dit kun je handmatig doen. Anders wordt het een #Property.

### Example with #Count

```C#
namespace ConsoleApp4;  
  
public class Program  
{  
  public static void Main()  
  {  
    var list = new List<int> { 1, 2, 3, 4, 5, 6 };  
    Console.WriteLine($"{list.Count}"); //6
  }  
}

```

- #Distinct filtert op unieke waardes. Alle dubbele waardes worden verwijderd of meer als het niet minstens 1 is.

- #First pakt het eerste element die aan de voorwaarde voldoet, daarna stopt het programma. Als er geen element is gevonden, krijg je een error: Unhandled exception. System.InvalidOperationException: Sequence contains no matching element.

- #Max pakt het hoogste element uit de #collection .
- #Min pakt het laagste element uit de #collection .
- #Select selecteert de velden die je eraan geeft, net zoals je gewend bent in #sql.
- #Single pakt precies 1 element die aan de voorwaarde voldoet, daarna stopt het programma. Als er geen element is gevonden, krijg je een error: Unhandled exception. System.InvalidOperationException: Sequence contains no matching element. Ook moet de waarde uniek zijn. Krijg je meer dan 1 resultaat? Dan krijg je hierop ook een error: Unhandled exception. System.InvalidOperationException: Sequence contains more than one matching element. #First is in dit geval veel beter om te gebruiken, maar #FirstOrDefault nog beter.

- #Skip pakt het aantal elementen van de startwaarde. Als je als voorbeeld 2 invoert, worden de eerste 2 genegeerd.

- #Sum telt alle elementen uit de #collection bij elkaar op.
- #Take pakt het aantal elementen van de startwaarde. Als je als voorbeeld 2 invoert, krijg je de eerste 2 terug.

- #Where als bool die checkt op een bepaalde conditie. Net zoals je gewend bent in #sql.
- #GroupBy is wat lastiger, omdat je met #key-value werkt. Het groepeert elementen bij elkaar.

### Example with #GroupBy on a #key-value 

```C#
namespace ConsoleApp4;  
  
public class Program  
{  
  public static void Main()  
  {  
    var list = new List<int> { 1, 2, 2, 3, 4, 4, 4, 5, 5, 6, 7, 7, 8, 9, 0 };  
    Console.Clear();  
  
    foreach (var collection in list.GroupBy(x => x % 3))  
    {  
      Console.WriteLine($"Key: {collection.Key} ");  
      Console.WriteLine($"Value: {String.Join(", ", collection)}");  
    }  
  }  
}

//Result
Key: 1
Value: 1, 4, 4, 4, 7, 7
Key: 2
Value: 2, 2, 5, 5, 8
Key: 0
Value: 3, 6, 9, 0

```

- #OrderBy sorteert de elementen op volgorde, duplicates zijn mogelijk.
- #FirstOrDefault pakt het eerste element die aan de voorwaarde voldoet, daarna stopt het programma. Als er geen element is gevonden, dan wordt de default waarde #null of de absolute 0 bij arithmatic datatypes.

- #SingleOrDefault pakt precies 1 element die aan de voorwaarde voldoet, daarna stopt het programma. Als er geen element is gevonden, dan wordt de default waarde #null of de absolute 0 bij arithmatic datatypes. Ook moet de waarde uniek zijn. Krijg je meer dan 1 resultaat? Dan krijg je hierop een error: Unhandled exception. System.InvalidOperationException: Sequence contains more than one matching element. #FirstOrDefault is in dit geval veel beter om te gebruiken.

> Dit is de lijst die je zeker moet weten. Het zijn er 19/66. Dit staat ook in de slides. Er staat meer in de lesstof zelf, maar aangezien het heel algemeen is omgeschreven, kan het geen kwaad om alles goed door te nemen. Je hoeft niet alles uit je hoofd te weten, als je maar begrijpt hoe het werkt. Alles wat hier staat is volgens het #toetsmatrijs. De overige behandel ik hier niet.

```C#
Aggregate //TSource
All //bool
Any //bool
Average //double
Count //int
Distinct //IEnumerable<TSource>
First //Tsource
Max //int
Min //int
Select //IEnumerable<TResult>
Single //TSource
Skip //IEnumerable<TSource>
Sum //int
Take //IEnumerable<TSource>
Where //IEnumerable<TSource>
GroupBy //IEnumerable<IGrouping<TKey,TSource>>
OrderBy //IOrderedEnumerable<TSource>
FirstOrDefault //TSource?
SingleOrDefault //TSource?
```

> Note: Niet alle methods kunnen direct worden aangeroepen. Als je geen rare syntax wilt en je een method wilt laten werken, dan kun je daarop het beste een loop gebruiken, zoals een #foreach. Daarop geldt ook dat niet alles in een loop hoeft als dat niet nodig is. Zie voorbeeld:

## #linq Example With #foreach

```C#
namespace ConsoleApp4;  
  
public class Program  
{  
  public static void Main()  
  {  
    var list = new List<int> { 1, 2, 3, 4, 5 };  
  
    foreach (var collection in list.Take(4).Skip(1))  
    {  
      Console.Write($"{collection} "); //2 3 4  
    }  
  }  
}

```

> Het ligt aan de #usecase welke #linq methods je precies nodig zal hebben. Je zult niet alles hoeven te gebruiken in een real world scenario.

## #linq Example Without #foreach

```C#
namespace ConsoleApp4;  
  
public class Program  
{  
  public static void Main()  
  {  
    var list = new List<int> { 1, 2, 3, 4, 5 };  
	Console.WriteLine($"{list.Max()} "); //5  
  }  
}

```

## Practice

> Vergeet niet de oefenopdracht van #linq te doen. Die is bij lesweek4 te vinden in Brightspace. Het is wel een handige oefening, om mee aan de gang te gaan. Hieronder is een mogelijk uitwerking. Het blijft altijd goed om zelf nog ermee te oefenen.

```C#
using System.Numerics;  
namespace ConsoleApp4;  
  
public class Movie  
{  
    public string Title { get; init; }  
  
    public int Year { get; init; }  
  
    public string? Director { get; init; }  
  
    public string? Genre { get; init; }  
}  
  
public class Program  
{  
    private static IList<Movie> Movies = new List<Movie>  
        {  
            new() {Title = "2001 A Space Odessy", Year = 1968, Director = "Stanley Kubrick", Genre = "Sci-Fi"},  
            new() {Title = "The Shining", Year = 1980, Director = "Stanley Kubrick", Genre = "Horror"},  
            new() {Title = "Dead Poets Society", Year = 1989, Director = "Peter Weir", Genre = "Drama"},  
            new() {Title = "The Truman Show", Year = 1998, Director = "Peter Weir", Genre = "Sci-Fi"},  
            new() {Title = "Blade Runner", Year = 1982, Director = "Ridley Scott", Genre = "Sci-Fi"},  
            new() {Title = "Easy Rider", Year = 1969, Director = "Dennis Hopper", Genre = "Adventure"},  
            new() {Title = "Once Upon a Time in the West", Year = 1968, Director = "Sergio Leone", Genre = "Western"},  
            new() {Title = "12 Angry Men", Year = 1957, Director = "Sidney Lumet", Genre = "Drama"},  
            new() {Title = "A Clockwork Orange", Year = 1971, Director = "Stanley Kubrick", Genre = "Drama"},  
            new() {Title = "One Flew Over the Cuckoo's Nest", Year = 1975, Director = "Milos Forman", Genre = "Drama"},  
            new() {Title = "Brazil", Year = 1985, Director = "Terry Gilliam", Genre = "Sci-Fi"},  
            new() {Title = "Rain Man", Year = 1988, Director = "Barry Levinson", Genre = "Drama"},  
            new() {Title = "The Good, the Bad and the Ugly", Year = 1968, Director = "Sergio Leone", Genre = "Western"},  
            new() {Title = "The Perks of Being a Wallflower", Year = 2012, Director = "Stephen Chosky", Genre = "Drama"},  
            new() {Title = "Wag The Dog", Year = 1997, Director = "Barry Levinson", Genre = "Drama"},  
            new() {Title = "For A Few Dollars More", Year = 1965, Director = "Sergio Leone", Genre = "Western"},  
            new() {Title = "Thelma & Louise", Year = 1991, Director = "Ridley Scott", Genre = "Drama"},  
            new() {Title = "Ali G IndaHouse", Year = 2002, Director = "Mark Mylod", Genre = "Comedy"}  
        };  
  
    static IEnumerable<BigInteger> Fibonacci()  
    {  
        BigInteger number1 = 1;  
        BigInteger number2 = 1;  
        yield return number1;  
        while (true)  
        {  
            yield return number2;  
            BigInteger temp = number1 + number2;  
            number1 = number2;  
            number2 = temp;  
        }  
    }  
  
    static void Main()  
    {  
        Opdracht1();  
        Opdracht2();  
        Opdracht3();  
        Opdracht4();  
        Opdracht5();  
        Opdracht6();  
        Opdracht7();  
    }  
  
    static void Opdracht1() // Toon van alle films de titel en het jaartal, gesorteerd op jaartal.  
    {  
        foreach (Movie movie in Movies.OrderBy(m => m.Year))  
        {  
            Console.WriteLine("1. {0} - {1}", movie.Title, movie.Year);  
        }  
    }  
  
    static void Opdracht2() // In welk jaar bracht 'Sergio Leone' zijn eerste film uit?  
    {  
        Console.WriteLine($"2. {Movies.OrderBy(m => m.Year).First(m => m.Director == "Sergio Leone").Year}");  
    }  
  
    static void Opdracht3() // Hoeveel films zijn er van 'Peter Weir' van het genre 'Sci-Fi'?.  
    {  
        Console.WriteLine($"3. {Movies.Count(m => m.Director == "Peter Weir" & m.Genre == "Sci-Fi")}");  
    }  
  
    static void Opdracht4() // Toon de 6e t/m 10e film uit de lijst.  
    {  
        foreach (Movie movie in Movies.Skip(5).Take(5))  
        {  
            Console.WriteLine($"4. {movie.Title}");  
        }  
    }  
  
    static void Opdracht5() // Is er een film uit 1997 (True/False)?  
    {  
        Console.WriteLine($"5. {Movies.Any(m => m.Year == 1997)}");  
    }  
  
    static void Opdracht6() // Van welke regisseur is de film 'One Flew over the Cuckoo's Nest'?  
    {  
        Console.WriteLine(  
            $"6. {Movies.Single(m => m.Title.Equals("One Flew Over the Cuckoo's Nest")).Director}"  
        );  
    }  
  
    static void Opdracht7() // Wat is het 1000e Fibonacci getal?  
    {  
        /*Verwijder een method om deze functie te laten werken. Als je dit niet aanpast, zal de IDE memory uit je heap  
        allocaten wat betekent dat je RAM usage naar 100% kan gaan. BigInteger is een 128 bit datatype. Let daar op!!!*/        Console.WriteLine($"7. {Fibonacci().ElementAt(1000 - 1)}");  
    }  
}

```

## #ORM

#ORM staat voor Object Relational Mapping en zorgt ervoor dat je data kan aansturen van en naar Databases. Het maakt de vertaalslag naar queries, zodat je niet dit zelf hoeft te schrijven. Terwijl je focust op de datastructuren, doet het #ORM de rest voor je. Hieronder staat een goeie uitleg van #ChatGPT die in het Engels is geschreven. 

> Het gaat over wat een #ORM precies oplost en tegen welke problemen je kan aanlopen.

**ChatGPT**
**Object-Relational Mapping (ORM)** is a programming technique that allows data to be seamlessly transferred between an object-oriented system and a relational database system. The main problems that #ORM aims to solve are related to the impedance mismatch between the object-oriented programming paradigm and the relational database model.

### Problems #ORM Solves:

1. **Impedance Mismatch:**
    
    - **Problem:** Object-oriented languages (like Java or C#) represent data using objects, while relational databases store data in tables. The differences between these models create an impedance mismatch.
    - **Solution:** #ORM provides a way to map objects to database tables and vice versa, helping to bridge the gap between the object-oriented and relational worlds.
2. **Boilerplate Code:**
    
    - **Problem:** Manually writing SQL queries and mapping database results to objects can be tedious and error-prone, leading to a lot of boilerplate code.
    - **Solution:** #ORM tools automate the process of #CRUD (Create, Read, Update, Delete) operations, reducing the amount of boilerplate #code and improving developer productivity.
3. **Database Abstraction:**
    
    - **Problem:** Without #ORM, developers need to write code specific to the database they are using. Switching databases can be challenging.
    - **Solution:** #ORM abstracts away the underlying database details, making it easier to switch between different database systems without major code changes.
4. **Maintainability:**
    
    - **Problem:** When the data model changes, manual updates to SQL queries and #object mappings are required, making maintenance challenging.
    - **Solution:** #ORM tools often provide automated schema generation and migration tools, making it easier to adapt to changes in the data model.

### Problems Encountered with #ORM:

1. **Performance Overhead:**
    
    - **Issue:** #ORM tools may introduce performance overhead compared to hand-tuned SQL queries, especially for complex or performance-critical applications.
    - **Mitigation:** #ORM tools often provide ways to optimize queries, and developers can choose to use native SQL queries when necessary.
2. **Learning Curve:**
    
    - **Issue:** There can be a learning curve associated with understanding and effectively using an #ORM, especially for developers new to the tool.
    - **Mitigation:** Training, documentation, and experience can help developers become proficient with the #ORM tool.
3. **Customization Limitations:**
    
    - **Issue:** Some #ORMs might limit the flexibility to perform highly customized or optimized database operations.
    - **Mitigation:** Some #ORM tools provide ways to write custom queries or use native SQL when needed, but it depends on the specific #ORM.
4. **Mapping Complex Relationships:**
    
    - **Issue:** Mapping complex relationships between objects and database tables can be challenging and may require additional configuration.
    - **Mitigation:** #ORMs often provide features and annotations to handle complex relationships, but developers need to be aware of and properly configure these.

While #ORM tools can greatly simplify database interaction in many scenarios, it's important to be aware of their limitations and potential issues. The choice to use an #ORM should be based on the specific requirements and constraints of the project.

## Explicit, Eager and Lazy #Loading

#Loading is een proces dat geldt voor de Entity Framework (EF) en de omliggende data in het #ORM. Welke #Loading je moet gebruiken en welke sneller is aan de #usecase en wat je ermee wilt bereiken. Hieronder zullen alle verschillende #Loading worden beschreven. Omdat dit een best uitgebreid stuk kan zijn, zullen we de #code uit de docs gebruiken en niet zelf aanmaken.

> Url behorend tot de #code voorbeelden: https://blog.jetbrains.com/dotnet/2023/09/21/eager-lazy-and-explicit-loading-with-entity-framework-core/ en https://dzone.com/articles/working-with-lazy-loading-and-eager-loading-in-ent

### Explicit #Loading

Explicit #Loading is het proces waar de gegevens worden geladen wanneer je dit specifiek doet. De data wordt alleen opgehaald wanneer dit nodig is. Doe je dit niet? Dan krijg je een lege #collection . Het wordt duidelijk waar de #code voor de query wordt aangeroepen, maar je hebt nog steeds het resultaat + 1 probleem. Hieronder is een voorbeeld van Explicit #Loading .

```C#
var invoices = db.Invoices
  .ToList();

// All invoices are already loaded...
foreach (var invoice in invoices)
{
  // ...but you'll have to explicitly load invoice lines when they are needed
  db.Entry(invoice).Collection(p => p.InvoiceLines).Load();

  foreach (var invoiceLine in invoice.InvoiceLines)
  {
    // ...
  }
}

```

> Om Explicit #Loading toe te passen, gebruik je het keyword #Load. Zie het voorbeeld hier.

## Eager #Loading 

Eager #Loading is het proces waarop je op een query iets aanroept en daarboven op de gerelateerde gegevens ermee laad. Dit kun je doen met de #Include keyword. Eager #Loading is het niet het tegenovergestelde van Lazy #Loading ,  je laad wel meteen alle gegevens in. Dit kan voor een overhead zorgen. Hieronder is een voorbeeld hoe je #Loading kunt toepassen.

```C#
var invoices = db.Invoices
  .Include(invoice => invoice.InvoiceLines)
  .ToList();

// All invoices are already loaded...
foreach (var invoice in invoices)
{
  // ...including all their Invoice lines
  foreach (var invoiceLine in invoice.InvoiceLines)
  {
    // ...
  }
}

```

> Voor meerdere calls kun je na de #Include erop #ThenInclude gebruiken.

```C#
using (var context = new AdventureWorksContext())
{
  var data = context.Employee
    .Include(j => j.JobCandidate)
    .ThenInclude(b => b.BusinessEntity)
    .ToList();
}

```

## Lazy #Loading 

Lazy #Loading is het proces waarbij de query automatisch worden geladen wanneer dit nodig is. Alleen de nodige gegevens die je verwacht worden geladen. In tegenstelling tot Eager #Loading is Lazy #Loading niet perse veel sneller. Je krijgt het volledige resultaat + 1. In het meeste gevallen is het niet aan te raden om dit te gebruiken. Kijk naar de benaming: Lazy.

```C#
var invoices = db.Invoices
  .ToList();

// All invoices are already loaded...
foreach (var invoice in invoices)
{
  // ...invoice lines are queried when accessed...
  foreach (var invoiceLine in invoice.InvoiceLines)
  {
    // ...the related product is also queried when accessed
    var product = invoiceLine.Product;
    
    // ...
  }
}

```

Maar het kan ook je #performance naar beneden halen, wanneer je met bepaalde stukken data werkt. Dit is voornamelijk waar voor het serializeren van bepaalde gegevens. Het is mogelijk om Lazy #Loading uit te schakelen. Hieronder is een voorbeeld hoe het werkt en hoe je dit kunt uitzetten.

### Turning off Lazy #Loading

```C#
public sealed class NorthwindModelOptimized: NorthwindModel
{
  public NorthwindModelOptimized()
  {
    ChangeTracker.QueryTrackingBehavior = QueryTrackingBehavior.NoTracking;
  	this.ChangeTracker.LazyLoadingEnabled = false; //Turn off Lazy Loading
  }

  protected override void OnModelCreating(ModelBuilder modelBuilder)
  {
   	// Write your implementation here
  }
}

```

### Explicit, Eager and Lazy #Loading Video

> Hier een video: https://www.youtube.com/watch?v=T9fTFynqvCw
