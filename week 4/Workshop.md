# Week 4: Workshop opdracht
## Step by step

In deze opdracht ga je stap voor stap een applicatie bouwen waarbij we steeds meer validatie regels gaan toevoegen. 

Wil je een uitdagende opdracht? Kijk dan meteen naar de huiswerk opdracht!

---

## Setup

1. Maak een nieuw project - ASP.NET Core Web App (model-view-controller)

2. Maak in dit project een klasse FormulierVM met in het begin 1 property 'Naam'

#### **`FormulierVM.cs`**
```c#
public class FormulierVM 
{
    public string Naam {get; set;}
}
```

3. Maak of met de hand (of scaffold) een vieuw voor de *Index* action van de *HomeController*. Deze view is een formulier die de action **Verstuur** gaat aanroepen. 

#### **`HomeController.cs > Index`**
```c#
public IActionResult Index()
{
    FormulierVM formulier = new FormulierVM();
    return View(formulier);
}
```

#### **`index.cshtml`**
```html
@model RoosterApp.Controllers.FormulierVM

<h4>Het formulier</h4>

<div class="row">
    <div class="col-md-4">
        <form asp-action="Verstuur">
            <div asp-validation-summary="ModelOnly" class="text-danger"></div>
            <div class="form-group">
                <label asp-for="Naam" class="control-label"></label>
                <input asp-for="Naam" class="form-control" />
            </div>
            <div class="form-group">
                <input type="submit" value="Create" class="btn btn-primary" />
            </div>
        </form>
    </div>
</div>
```

4. Bijna klaar om te testen! Maak nu nog een action **Verstuur** met de HTTP-methode POST. Voor deze action mag je ook een view maken maar een hele simpele is voldoende.

#### **`HomeController.cs > Verstuur`**
```c#
[HttpPost]
public IActionResult Verstuur(FormulierVM formulier)
{
    return View();
}
```

#### **`Verstuur.cshtml`**
```html
<h1>Formulier is verstuurd!</h1>
```

Als het goed is kun je nu het formulier versturen maar gebeurd er nog niks. Controleer via de debugger of de waardes van het formulier goed aankomen in de parameter van de action Verstuur. 

---

## Validation Recap!

1. Voeg het juiste attribuut toe om:
    1.1 Naam verplicht te maken
    1.2 Naam een minimale lengte van 2 te geven

<details>
<summary>Bekijk uitwerking</summary>

#### **`FormulierVM.cs`**

```c#
[Required]
[MinLength(2)]
public string Naam { get; set; }
```

</details>


<br>

2. Voeg Server side validatie toe

#### **`HomeController.cs > Index`**
```c#
if(!ModelState.IsValid)
{
    return View("Index", formulier);
}
```


**Note:** Als je dit nu uitprobeert zal je merken dat de client validatie wel al werkt. Dit zie je terug in de html (inspect element).  
{: .note}

testen