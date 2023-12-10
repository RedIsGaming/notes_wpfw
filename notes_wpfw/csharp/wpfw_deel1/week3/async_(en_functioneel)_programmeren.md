# Intro

Hier vind je de onderdelen van lesweek3. Alles wat je moet weten van deze week wat ook in het #toetsmatrijs staat beschreven. Als er een stukje staat met dat er nog later uitleg komt, dan vul ik dat later in. Er is geen garantie dat #code  perfect is. Daar gaat het niet om. Als je de #code  shit vindt, dan snap je niet het punt, want het gaat puur om het concept. 

Als je de concepten begrijpt, dan ben je al een stap vooruit. Voor vragen of opmerkingen kun je me altijden dmen op #Discord: redisgaming of #Whatsapp. Deze intro zal ook in de andere documenten als intro staan, dus al je dit hebt gelezen, kun je de intro H1 skippen. Voor de rest ben ik meer gefocust op voorbeelden dan op het uitleggen. Houdt daar rekening mee. Good luck :)

> Note: De uitleg is in het Nederlands. De code en H2/H3 in het Engels.

## Async programming with Await and Task

```C#
namespace ConsoleApp3;  
  
public class DownloadSource  
{  
  private const int TOTAL = 50;  
    
  public async Task DownloadAsync()  
  {  
    Console.WriteLine("Awaiting downloads...");  
    await Task.Delay(3000);  
    var source = new List<string> { "Downloading from Source" };  
    var download = Enumerable.Range(0, TOTAL);  
  
    foreach (var downloads in download)  
    {  
      var result = await Task.Run(() => source  
        .Select((value, number) => new { Value = value, Number = number })
        .OrderBy(d => d.Value)  
        .ToList());  
        
      result.ForEach(d =>  
      {  
        Console.WriteLine($"Task: {source[d.Number]} {downloads + 1}...");  
        Task.Delay(150).Wait();  
      });  
    }  
  
    await Task.CompletedTask;  
  }  
  
  public async Task SourceAsync()  
  {  
    await Task.Delay(1500);  
    var process = new List<string> { "Processing data from Source" };  
    var download = Enumerable.Range(0, TOTAL);  
  
    foreach (var processes in download)  
    {  
      var result = await Task.Run(() => process  
        .Select((value, number) => new { Value = value, Number = number})  
        .OrderBy(p => p.Value)  
        .ToList());  
        
      result.ForEach(p =>  
      {  
        var random = new Random().Next(1, TOTAL);  
        Console.WriteLine($"Process: {process[p.Number]} {processes + 1} {random}MB / {random}MB...");  
        Task.Delay(75).Wait();  
      });  
    }  
      
    Console.WriteLine("All downloads and processes completed!!!");  
    await Task.CompletedTask;  
  }
}

```

Hier zal later wat uitgelegd worden. Alhoewel beide methodes bijna precies op elkaar lijken, gaat het hier niet om of de code perfect is en aan alle principes van OOP voldoet, het gaat om de concepten. En deze keer is dat voor week3 async/await/Task.

```C#
namespace ConsoleApp3;  
  
public class Program  
{  
  public static async Task Main()  
  {  
    var async = new DownloadSource();  
    await async.DownloadAsync();  
    Console.WriteLine("Awaiting processes...");  
    await async.SourceAsync();  
  }  
}

```
