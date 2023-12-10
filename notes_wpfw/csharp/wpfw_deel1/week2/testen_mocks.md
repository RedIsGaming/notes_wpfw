# Intro

Hier vind je de onderdelen van lesweek2. Alles wat je moet weten van deze week wat ook in het #toetsmatrijs staat beschreven. Als er een stukje staat met dat er nog later uitleg komt, dan vul ik dat later in. Er is geen garantie dat #code  perfect is. Daar gaat het niet om. Als je de #code  shit vindt, dan snap je niet het punt, want het gaat puur om het concept. 

Als je de concepten begrijpt, dan ben je al een stap vooruit. Voor vragen of opmerkingen kun je me altijden dmen op #Discord: redisgaming of #Whatsapp. Deze intro zal ook in de andere documenten als intro staan, dus al je dit hebt gelezen, kun je de intro H1 skippen. Voor de rest ben ik meer gefocust op voorbeelden dan op het uitleggen. Houdt daar rekening mee. Good luck :)

> Note: De uitleg is in het Nederlands. De code en H2/H3 in het Engels.

## Create Mock

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

Hier komt nog uitleg.

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

Hier komt ook wat uitleg later.
