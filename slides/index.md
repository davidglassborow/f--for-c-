- title : Introduction to F#
- description : Introduction to F#
- author : Dave Glassborow
- theme : night
- transition : default

***

## Intro to fsharp

- Who I am
- Quick intro and some code
- Slides and source code on Github
- __Please__ ask questions

---

## Who I am

- Developing for ~25 years
- Mostly C# / Web / SQL
- Some F#

![](images/me.svg)

---

## Why I learnt F#

- Fun learning something new
- Usable in my day to day job
- Makes my C# coding better

***

## Code

Code here

---

### Send an email C#

```csharp
using System.Net;
using System.Net.Mail;

public static class Emailer
{
  public static void SendTestEmail(string toEmail, string body)
  {
    var user = "dave.glassborow@myemail.co.uk";
    using (var msg = new MailMessage(user, toEmail))
    {
      msg.Subject = "Test";
      msg.Body = body;
      using(var client = new SmtpClient("smtp.office365.com",587))
      {
        client.EnableSsl = true;
        client.Credentials = new NetworkCredential(user, "****");
        client.Send(msg);
      }
    }
  }
}

Emailer.SendTestEmail( "dave@conceptfirst" "From Office365")
```
---

### Send an email F#

    open System.Net
    open System.Net.Mail

    /// Send email via office 365
    let sendTestEmail toEmail body =
        let user = "dave.glassborow@myemail.co.uk"
        use msg = new MailMessage(user,toEmail)
        msg.Subject <- "Test"
        msg.Body <- body 
        use client = new SmtpClient("smtp.office365.com",587)
        client.EnableSsl <- true  
        client.Credentials <- NetworkCredential(user,"****")
        client.Send(msg)

    //sendTestEmail "dave@conceptfirst" "From Office365"

---

![](images/new_project.png)

---

![](images/define.png)

---

![](images/vscode.png)


***

## F#

- ML (1974) / OCaml
- Open source since 2005
- Functional First but very pragmatic
- Full interop with C#
- Runs everywhere C# does + a few more
- Test bed for C#

---

### Who uses it

- Kaggle
- Jet.com (3.3 billion)
- The City (top 3 paid)
- Microsoft internally

---

### Union types

    type PaymentType =
    | Cash
    | Cheque
    | CreditCard of Number:string * CCV:string
    | Bitcoin of key:string

    type CustomerID = CustomerID of int

---

### Record types

    type Person = { Name: string }

    { Name = "David" } = { Name = "David" }

---

### F# features

    open System
    let simpleValue = 5
    let upper (s:string) = s.ToUpper()
    let fact      x      = List.reduce (fun total v -> v * total ) [1..x]
    let factorial x      = List.reduce (*) [1..x]
    let factorialPipe x  = [1..x] |> List.reduce (*)
    type Person = {
        Name: string
        Dob: DateTime option
    }

[F# cheatsheet](http://dungpa.github.io/fsharp-cheatsheet/)

---

## Different Defaults

- Null vs no nulls
- Mutable vs Immutable
- Change properties vs Pipelines (e.g. Linq)
- Reference vs Structual Equality

---

## Extras beyond C#

- Agents
- Type Providers
- Monads e.g. async/await
- Units of Measure


    [<Measure>] type m
    [<Measure>] type sec
    [<Measure>] type kg

    let distance = 1.0<m>
    let time = 2.0<sec>
    let speed = 2.0<m/sec>
    let acceleration = 2.0<m/sec^2>
    let force = 5.0<kg m/sec^2>
    let travel = time * speed

***

## Functional programming

- _I have to think less, the compiler does more for me_
- Seperate Data and Logic e.g. _SQL Select_

---

_Controlling complexity is the essence of computer programming._

![](images/fp.svg)

---

## Core values

- Seperate data and processes
- Transform into new data
- Sane defaults
- _Reason_ about code
- Composiblity: Lego
- Declarative
- Functions: first class, making them, changing them

---

_There are two ways of constructing a software design: One way is to make it so simple that there are obviously no deficiencies and the other way is to make it so complicated that there are no obvious deficiencies._

---

## Object Orientation

- _Object oriented programming makes code understandable by encapsulating moving parts. Functional programming makes code understandable by minimizing moving parts._

---

## Object Orientation

_The problem with object-oriented languages is they’ve got all this implicit environment that they carry around with them. You wanted a banana but what you got was a gorilla holding the banana and the entire jungle._

- Packets of hidden state, hard to reason about
- Things can change behind your back, especially in multi-threading
- Model with Subclassing, but not always worth the hassle ?

---

## FP Advantages

- Manage complexity
- Less stressful to code
- More powerful, program at a higher level
- Think differently, apply it to other langauges
- Pit of success
- REPL

--- 

## FP Disadvantages

- More abstract
- Mathematical naming
- Different way of thinking
- More thinking, less typing, which is harder
- Rabbit hole: Haskell, Dependant types, Category Theory

---

## F# Disadvantages

- Available developers
- Size of community is smaller
- VS tooling (but not VSCode)

***

## Where to use F#

- REPL
  - utilities
  - machine learning
  - exploring
- Complex
  - complex logic and domains
  - async code 
- Functional
  - pipelines
  - parsers

---

## Where NOT to use F#

- Basic mvc
- Xamarin (except Fabulous)

***

## F# -> C#

- C# with static functions and dtos

```csharp
public class Person
{
    public string Email { get; set; }
    public string Name { get; set; }
}

public static class Emailer
{
    public static void SendEmail(Person who)
    {
        // emailing code ...
    }
}
```

*** 

## Find out more

- http://fsharpforfunandprofit.com
- http://connelhooley.uk/blog/2017/04/10/f-sharp-guide
- http://connelhooley.uk/blog/2017/04/30/f-sharp-to-c-sharp
- https://channel9.msdn.com/events/Build/2017/T6064
- [F# koans](https://github.com/ChrisMarinos/FSharpKoans/)
- [Video: F# for C# developers](https://vimeo.com/131640714)

---

## Thought for the day

_Always code as if the guy who ends up maintaining your code will be a violent psychopath who knows where you live._
