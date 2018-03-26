﻿# Module 5: Developing Views

# Lesson 1: Creating Views with Razor Syntax

### Demonstration: How to Use the Razor Syntax

#### Preparation Steps 

1. Ensure that you have cloned the 20486D directory from GitHub. It contains the code segments for this course's labs and demos. https://github.com/MicrosoftLearning/20486D-DevelopingASPNETMVCWebApplications/tree/master/Allfiles.

2. Go to **Allfiles\Mod05\Democode\01_RazorSyntaxExample_begin\RazorSyntaxExample**, and then double-click **RazorSyntaxExample.sln**.

#### Demonstration Steps

1. In the Solution Explorer pane of the **RazorSyntaxExample - Microsoft Visual Studio** window, expand **RazorSyntaxExample** project file, right-click **Controllers**, and then click **ProductController**.

2. In the **ProductController.cs** code window, locate and select the following code. 
```cs
    return View();
```

3. Replace the code you selected with the following code
```cs
    ViewBag.ProductPrices = new Dictionary<string,int>();
    ViewBag.ProductPrices.Add("Bread", 5);
    ViewBag.ProductPrices.Add("Rice", 3);
    return View();
```

4. In the **ProductController.cs** code window, locate the following code:
```cs
    public IActionResult Index()
```

5. Right click on the **Index** method name, and click **Add View...**.

6. In the **Add MVC View** dialog window leave all the default values as they are, and press **OK**.
>**Note** : See that the Views and the Products folders were created. Inside them there is new file named Index.cshtml.

7. Inside the **body** element, type the following code.
```cs
    @foreach (KeyValuePair<string, int> ProductPrices in ViewBag.ProductPrices)
    {  

    }
```

8. Inside the **@foreach** code block, type the following code
```cs
    <p>
       
    </p>
```

9. In the **p** element, type the following code.
```cs
    <div>
        Product Name: @ProductPrices.Key
    </div>
```

10. In the **p** element, below the **div** element, type the following code.
```cs
    <div>
        Product Price + Tax: @(ProductPrices.Value * 1.2)
    </div>
```

11. On the **DEBUG** menu of the **RazorSyntaxExample –  Microsoft Visual Studio** window, click **Start Debugging**.
    >**Note** : Displayed results:
    > Product Name: Bread
    > Product Price + Tax: 6
    > Product Name: Rice
    > Product Price + Tax: 3.6
    
12. In the **Microsoft Edge** window, click **Close**.

13. On the **Debug** Menu, click **Stop Debugging**.


# Lesson 2: Using HTML Helpers and Tag Helpers

### Demonstration: How to Use HTML Helpers

#### Preparation Steps 

1. Ensure that you have cloned the 20486D directory from GitHub. It contains the code segments for this course's labs and demos. https://github.com/MicrosoftLearning/20486D-DevelopingASPNETMVCWebApplications/tree/master/Allfiles.

2. Go to **Allfiles\Mod05\Democode\02_HTMLHelpersExample_begin\RazorSyntaxExample**, and then double-click **HTMLHelpersExample.sln**.


#### Demonstration Steps

1. On the **Solution Explorer** pane, of the **HTMLHelpersExample - Microsoft Visual Studio** window, expand the **Views** folder, then expand the the **Home** folder, and click **Index.cshtml**.

2. In the **Index.cshtml** code window, locate the following code.
```cs
    <h2>Index Action, Home Controller</h2>
```

3. Place the mouse cursor at the end of the code, press Enter, and then type the following code:
```cs
    <p>@Html.ActionLink("Path: " + Url.Action("Normal", "Main"), "Normal", "Main")</p>
```

4. On the **Solution Explorer** pane, of the **HTMLHelpersExample - Microsoft Visual Studio** window, expand the **Views** folder, then expand the the **Main** folder, and click **Normal.cshtml**.

5. In the **Normal.cshtml** code window, locate the following code.
```cs
    <h2>Normal Action, Main Controller</h2>
```

6. Place the mouse cursor at the end of the code, press Enter, and then type the following code:
```cs
    <p>@Html.ActionLink("Path: " + Url.Action("Index"), "Index")</p>
```    

7. On the **Solution Explorer** pane, of the **HTMLHelpersExample - Microsoft Visual Studio** window, under the **Views** folder and the **Main** subfolder, click **Index.cshtml**.

8. In the **Index.cs** code window, locate the following code.
```cs
    <h2>Index Action, MainController</h2>
```

9. Place the mouse cursor at the end of the code, press Enter, and then type the following code:
```cs
<p>
    @Html.ActionLink("Path: " + Url.Action("RegularWithParameter"), "RegularWithParameter", "Main",
        new
        {
            parameter1 = "Passing a value to the first parameter",
            parameter2 = "Passing a value to the second parameter"
        })
</p>
```   

10. On the **Solution Explorer** pane, of the **HTMLHelpersExample - Microsoft Visual Studio** window, under the **Controllers** folder, click **MainController.cs**.

11. In the **MainController.cs** code window, locate and select the following code. 
```cs
        public IActionResult RegularWithParameter(string parameter1, string parameter2)
        {
            return View();
        }
```

12. Replace the code you selected with the following code
```cs
    public IActionResult RegularWithParameter(string parameter1, string parameter2)
    {
        return Content($"Parameter1 result: {parameter1} {Environment.NewLine}Parameter2 result: {parameter2}");
    }
```

13. On the **DEBUG** menu of the **HTMLHelpersExample –  Microsoft Visual Studio** window, click **Start Debugging**.
     > **Note**: The Home Controller's index action url path is: **http://localhost:[port]/**

14. In the **Microsoft Edge**, Index page, press the link that leads to the next controller.
     > **Note**:  The Main Controller's Normal Action url path is: **http://localhost:[port]/Main/Normal**

15. In the **Microsoft Edge**, Index page, press the link that leads to the next action.
     > **Note**:  The Main Controller's Index Action url path is: **http://localhost:[port]/Main**

16. In the **Microsoft Edge**, Index page, press the link that leads to the next action.
     > **Note**:  The Main Controller's RegularWithParameter Action url path is: **http://localhost:[port]/Main/RegularWithParameter?parameter1=Passing%20a%20value%20to%20the%20first%20parameter&parameter2=Passing%20a%20value%20to%20the%20second%20parameter**

17. In the **Microsoft Edge** window, click **Close**.