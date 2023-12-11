# Intro

Hier vind je de onderdelen van lesweek2. Alles wat je moet weten van deze week wat ook in het #toetsmatrijs staat beschreven. Als er een stukje staat met dat er nog later uitleg komt, dan vul ik dat later in. Er is geen garantie dat #code  perfect is. Daar gaat het niet om. Als je de #code  shit vindt, dan snap je niet het punt, want het gaat puur om het concept. 

Als je de concepten begrijpt, dan ben je al een stap vooruit. Voor vragen of opmerkingen kun je me altijden dmen op #Discord: redisgaming of #Whatsapp. Deze intro zal ook in de andere documenten als intro staan, dus al je dit hebt gelezen, kun je de intro H1 skippen. Voor de rest ben ik meer gefocust op voorbeelden dan op het uitleggen. Houdt daar rekening mee. Good luck :)

> Note: De uitleg is in het Nederlands. De code en H2/H3 in het Engels.

## Create Mock

Wat is een Mock in #unit-testing? Een Mock is ervoor zorgen dat je niet afhankelijk bent van andere classen en objecten. Je test niet productie #code en dus niet de implementatie. Wat je test is de nabootsing van de methods om bepaald gedrag terug te krijgen. Hieronder zie je een Mock in actie. Je moeten weten hoe je een Mock moet schrijven. Dus niet het Framework: Moq.

```C#
using System.Numerics;  
namespace TestProject1;  
  
public interface ICalculator<T>  
{  
  public T Add(T a, T b);  
  public T Substract(T a, T b);  
}  
  
struct MockCalculator<T> : ICalculator<T>  
where T : INumber<T>  
{  
  public T Add(T a, T b)  
  {  
    dynamic c = a;  
    return c + b;  
  }  
    
  public T Substract(T a, T b)  
  {  
    dynamic c = a;  
    return c - b;  
  }  
}  
  
public struct Calculator<T>(ICalculator<T> iCalculator)  
where T : INumber<T>  
{  
  private ICalculator<T> Icalculator { get; } = iCalculator;  
  public T Add(T a, T b) => Icalculator.Add(a, b);  
  public T Substract(T a, T b) => Icalculator.Substract(a, b);  
}

```

We maken een #interface ICalculator met een #generics met type #T. Daaraan geven we twee methods: Add en Substract. Die hebben beide 2 arguments met #T a en #T b. Vervolgens maken we een MockCalculator die de #interface implementeert. We geven een #dynamic c die we vullen met waarde a. Vervolgens returnen we die c en b. Hierboven zie je hoe dat gebeurd.

Nadat we de Mock hebben, maken we een #class / #struct met de daadwerkelijke implementatie. We maken een Calculator en in de #Primary-Constructor geven we de #interface mee met iCalculator argument. Dit is #Dependency-Injection . Je implementeert niet de #interface, maar geeft dit als waarde mee.

> Hier is hoe #Primary-Constructor werkt met #Dependency-Injection :

![[primaryconstructor_dependency.png]]

> url: https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/tutorials/primary-constructors

De MockCalculator die de #interface implementeert is #Dependency-Inversion. Terug naar Calculator. De argument die meegegeven is een #interface-Injection en de #Property een #setter-Injection. Die is #readonly en #private. We willen niet de Mock implementatie aanroepen. Je ziet ook een #generics constraint met where #T : #INumber #T.

Nu is het alleen mogelijk om arithmatic getallen eraan mee te geven. Als laatste hebben we de twee methods die we in de test gaan gebruiken. De implementatie lijkt bijna hetzelfde als de #interface , maar we kunnen de namen van die method voor de => aanpassen. Voor het gemak laten we het zoals het is. #generics types zijn optioneel. Het is geen requirement voor een Mock.

## Test Mock

```C#
namespace TestProject1;  
  
public class TestCalculator  
{  
  [Fact]  
  public void TestAdd()  
  {  
    //Arrange  
    var mock = new MockCalculator<uint>();  
    var calculator = new Calculator<uint>(mock);  
      
    //Act  
    var add = calculator.Add(66, 600);  
  
    //Assert  
    Assert.Equal(666, Convert.ToInt32(add));  
  }  
    
  [Fact]  
  public void TestSubstract()  
  {  
    //Arrange  
    var mock = new MockCalculator<uint>();  
    var calculator = new Calculator<uint>(mock);  
      
    //Act  
    var substract = calculator.Substract(732, 66);  
  
    //Assert  
    Assert.Equal(666, Convert.ToInt32(substract));  
  }  
}

```

Laten we nu naar de tests gaan. De best practice voor een test is maximaal 1 #assert per method. Hoe je je methods en #class noemt is aan jou, maar houdt het simpel. We hebben een TestCalculator #class en twee methods. Beide zijn het van het type #void en ze heten: TestAdd en TestSubstract. Je kunt met data annotaties #Fact of #Theory je test maken.

We maken een nieuw object van MockCalculator met het type #u32 / #uint. Daarna maken we ook een nieuw object aan van Calculator met hetzelfde type. Daar gooien we de mock in. Hierbij wordt #Dependency-Injection toegepast. Het is slim om de test op te delen met de 3 AAA's. Arrange, Act en Assert. In Arrange maak je nieuwe objecten aan. In de Act set je de waardes.

In de Assert test je hetgeen dat je wilt testen. Er zijn verschillende methods die je kan gebruiken om te testen, maar we zullen dat niet behandelen hier. Speel daar zelf mee. Equal en True zul je het meest gebruiken. We roepen in de Act de method aan die we willen gebruiken. Add of Substract. Hier geven we de waardes mee. Vervolgens testen we die. De test slaagt, congrats!

![[mock_result.png]]
