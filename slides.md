---
# You can also start simply with 'default'
theme: seriph

background: https://cover.sli.dev

title: Währungsumrechner

class: text-center
# https://sli.dev/features/drawing

transition: slide-left

mdc: true
---

# Währungsumrechner



<div @click="$slidev.nav.next" class="mt-12 py-1" hover:bg="white op-10">
 Nächste Seite <carbon:arrow-right />
</div>

<div class="abs-br m-6 text-xl">
  <button @click="$slidev.nav.openInEditor" title="Open in Editor" class="slidev-icon-btn">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>



---
transition: fade-out
---

# Converter.cs

```cs
namespace Waehrungsumrechner;

public class Converter : DollarCurrency, YenCurrency
{
    private DollarCurrency Dcurrency;

    public string UnitD => this.Dcurrency.Unit;
    public Converter(DollarCurrency currency)
    {
       this.Dcurrency = currency;
    }
    public double ConvertD(double money) => money * Dcurrency.Rate;

    private YenCurrency Ycurrency;

    public string UnitY => this.Ycurrency.Unit;
    public Converter(YenCurrency currency)
    {
        this.Ycurrency = currency;
    }
    public double ConvertY(double money) => money * Ycurrency.Rate;
}

```
<br>



---
transition: slide-up
level: 2
---

# DollarCurrency.cs

```cs
namespace Waehrungsumrechner;

public interface DollarCurrency
{
    public double Rate => 0.95;
    public string Unit => "USD";
}

```


---
layout: two-cols
layoutClass: gap-16
---

# YenCurrency.cs

```cs
namespace Waehrungsumrechner;

public interface YenCurrency
{
    public double Rate => 159.95;
    public string Unit => "JPY";
}

```

---
layout: 

---

# Program.cs
## Teil 1

```cs
using System;
using Waehrungsumrechner;

Console.WriteLine("Währungsumrechner");
Console.WriteLine("Betrag in EUR:");
double money = Convert.ToDouble(Console.ReadLine());
Console.WriteLine("Gewünschte Währung: ");
```

---
level: 2
---

# Program.cs
## Teil 2

```cs
string unit = Console.ReadLine();


    if (unit == "Dollar")
    {
        Converter convD = new Converter(new DollarCurrency());
        double result = convD.ConvertD(money);
        Console.WriteLine("Ergebnis in {0}: {1}", convD.UnitD, result);

    }
    else if (unit == "Yen")
    {
        Converter convY = new Converter(new YenCurrency());
        double result = convY.ConvertY(money);
        Console.WriteLine("Ergebnis in {0}: {1}", convY.UnitY, result);
    }
    else
    {
        Console.WriteLine("Keine gültige Währung");
        
    }
```


