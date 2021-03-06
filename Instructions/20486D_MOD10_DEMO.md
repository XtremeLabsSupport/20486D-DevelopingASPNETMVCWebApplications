﻿
# Module 10: Testing and Troubleshooting

# Lesson 1: Testing MVC Applications

### Demonstration: How to Run Unit Tests

#### Preparation Steps

1. Ensure that you have cloned the **20486D** directory from GitHub. It contains the code segments for this course's labs and demos. (**https://github.com/MicrosoftLearning/20486D-DevelopingASPNETMVCWebApplications/tree/master/Allfiles**)

#### Demonstration Steps

1. Navigate to **Allfiles\Mod10\Democode\01_UnitTestingExample_begin**, and then double-click **UnitTestingExample.sln**.

2. In the **UnitTestingExample - Microsoft Visual Studio** window, In **Solution Explorer**, right-click **Solution 'UnitTestingExample'**, point to **Add**, and then click **New Project**.

3. In the **Add New Project** dialog box, in the navigation pane, expand **Installed**, expand **Visual C#**, and then click **.NET Core**.

4. In the **Add New Project** dialog box, in the result pane, click **MSTest Test Project (.NET Core)**.

5. In the **Add New Project** dialog box, in the **Name** text box, type **ProductsWebsite.Tests**, and then click **OK**.

6. In the **UnitTestingExample - Microsoft Visual Studio** window, In **Solution Explorer**, under **ProductsWebsite.Tests**, right-click **Dependencies**, and then click **Add Reference**.

7. In the **Reference Manager - ProductsWebsite.Tests** dialog box, in the navigation pane, expand **Projects**, and then click **Solution**.

8. In the **Reference Manager - ProductsWebsite.Tests** dialog box, in the result pane, check the **ProductsWebsite** check box, and then click **OK**.

9. In the **UnitTestingExample - Microsoft Visual Studio** window, In **Solution Explorer**, under **ProductsWebsite.Tests**, right-click **UnitTest1**, and then click **Rename**.

10. In the **UnitTest1.cs** text box, type **ProductControllerTest**, and then press Enter.

11. In the **Microsoft Visual Studio** dialog box, click **Yes**.

11. In the **UnitTestingExample - Microsoft Visual Studio** window, on the **TOOLS** menu, point to **NuGet Package Manager**, and then click **Package Manager Console**. 

12. In the **Package Manager Console** window, type the following text, and then press Enter.
```
    Install-Package Microsoft.AspNetCore.Mvc.ViewFeatures -ProjectName ProductsWebsite.Tests
```

13. In the **UnitTestingExample - Microsoft Visual Studio** window, In **Solution Explorer**, right-click **ProductsWebsite.Tests**, point to **Add**, and then click **New Folder**.

14. In the **NewFolder** text box, type **Mock**, and then press Enter.

15. In the **UnitTestingExample - Microsoft Visual Studio** window, In **Solution Explorer**, right-click **Mock**, point to **Add**, and then click **Class**.

16. In the **Add New Item - ProductsWebsite.Tests** dialog box, in the **Name** text box, type **FakeProductRepository**, and then click **Add**.

17. In the **FakeProductRepository.cs** code window, locate the following code:
```cs
    using System.Text;
```

18. Ensure that the cursor is at the end of the located code, press Enter, and then type the following code:
```cs
    using ProductsWebsite.Repositories;
    using ProductsWebsite.Models;
```

19. In the **FakeProductRepository.cs** code window, select the following code:
```cs
    class FakeProductRepository
```

20. Replace the selected code with the following code:
```cs
    internal class FakeProductRepository : IProductRepository
```

21. In the **FakeProductRepository.cs** code window, locate the following code:
```cs
    internal class FakeProductRepository : IProductRepository
    {
```

22. Ensure that the cursor is at the end of the located code, press Enter, and then type the following code:
```cs
    public IEnumerable<Product> GetProducts()
    {
        return new List<Product>()
        {
            new Product{ Id = 1, Name = "Product1's name", BasePrice = 1.1F, Description = "A description for product 1.", ImageName = "image-name-1" },
            new Product{ Id = 2, Name = "Product2's name", BasePrice = 2.2F, Description = "A description for product 2.", ImageName = "image-name-2" },
            new Product{ Id = 3, Name = "Product3's name", BasePrice = 3.3F, Description = "A description for product 3.", ImageName = "image-name-3" }
        };
    }
```

23. In the **ProductControllerTest.cs** code window, locate the following code:
```cs
    using Microsoft.VisualStudio.TestTools.UnitTesting;
```

24. Ensure that the cursor is at the end of the located code, press Enter, and then type the following code:
```cs
    using System.Collections.Generic;
    using Microsoft.AspNetCore.Mvc;
    using ProductsWebsite.Controllers;
    using ProductsWebsite.Models;
    using ProductsWebsite.Repositories;
    using ProductsWebsite.Tests.Mock;
```

25. In the **ProductControllerTest.cs** code window, select the following code:
```cs
    public void TestMethod1()
    {
    }
```

26. Replace the selected code with the following code:
```cs
    public void IsIndexReturnsAllProducts()
    {
        // arrange
        IProductRepository fakeProductRepository = new FakeProductRepository();
        ProductController productController = new ProductController(fakeProductRepository);
        // act
        ViewResult viewResult = productController.Index() as ViewResult;
        List<Product> products = viewResult.Model as List<Product>;
        // assert
        Assert.AreEqual(products.Count, 3);
    }
```

27. In the **ProductControllerTest.cs** code window, locate the following code:
```cs
        Assert.AreEqual(products.Count, 3);
    }
```

28. Ensure that the cursor is at the end of the located code, press Enter twice, and then type the following code:
```cs
    [TestMethod]
    public void IsGetProductReturnsTheCorrectProduct()
    {
        // arrange
        var fakeProductRepository = new FakeProductRepository();
        var productController = new ProductController(fakeProductRepository);
        // act
        var viewResult = productController.GetProduct(2) as ViewResult;
        Product product = viewResult.Model as Product;
        // assert
        Assert.AreEqual(product.Id, 2);
    }
```

29. In the **UnitTestingExample – Microsoft Visual Studio** window, on the **FILE** menu, click **Save All**.

30. In the **UnitTestingExample - Microsoft Visual Studio** window, on the **TEST** menu, point to **Run**, and then click **All Tests**.
    >**Note:** The **Test Explorer** displays 1 failed test: **IsGetProductReturnsTheCorrectProduct**, and 1 passed test: **IsIndexReturnsAllProducts**.

31. In the **UnitTestingExample - Microsoft Visual Studio** window, In **Solution Explorer**, under **ProductsWebsite**, expand **Controllers**, and then click **ProductController.cs**. 

32. In the **ProductController.cs** code window, select the following code:
```cs
    var product = products.Where(p => p.Id != id).FirstOrDefault();
```

33. Replace the selected code with the following code:
```cs
    var product = products.Where(p => p.Id == id).FirstOrDefault();
```

34. In the **UnitTestingExample – Microsoft Visual Studio** window, on the **FILE** menu, click **Save All**.

35. In the **UnitTestingExample - Microsoft Visual Studio** window, on the **TEST** menu, point to **Run**, and then click **All Tests**.
    >**Note:** The **Test Explorer** displays 2 passed tests: **IsGetProductReturnsTheCorrectProduct** and **IsIndexReturnsAllProducts**.

36. In the **UnitTestingExample - Microsoft Visual Studio** window, on the **FILE** menu, click **Exit**.

# Lesson 2: Implementing an Exception Handling Strategy

### Demonstration: How to Configure Exception Handling
#### Preparation Steps

1. Ensure that you have cloned the **20486D** directory from GitHub. It contains the code segments for this course's labs and demos. (**https://github.com/MicrosoftLearning/20486D-DevelopingASPNETMVCWebApplications/tree/master/Allfiles**)

#### Demonstration Steps

1. Navigate to **Allfiles\Mod10\Democode\02_ErrorHandlingExample_begin**, and then double-click **ErrorHandlingExample.sln**.

2. In the **ErrorHandlingExample - Microsoft Visual Studio** window, on toolbar, click the arrow next to the **Start Debugging** button, and then click **Production**.​

3. In the **ErrorHandlingExample - Microsoft Visual Studio** window, on the **DEBUG** menu, click **Start Without Debugging**.

4. In **Microsoft Edge**, click **Close**.

6. In the **ErrorHandlingExample - Microsoft Visual Studio** window, on toolbar, click the arrow next to the **Start Debugging** button, and then click **Development**.​

7. In the **ErrorHandlingExample - Microsoft Visual Studio** window, on the **DEBUG** menu, click **Start Without Debugging**.

8. In **Microsoft Edge**, locate the following text:
 ```
    ErrorHandlingExample.Startup+<>c__DisplayClass1_0+<<Configure>b__0>d.MoveNext() in Startup.cs
	+	38.  cnt.IncrementRequestPathCount(context.Request.GetDisplayUrl());
 ```

9. In **Microsoft Edge**, click the **+** (plus) sign near **38**, and then inspect the code.

10. In **Microsoft Edge**, locate the following text:
 ```
    ErrorHandlingExample.Services.Counter.IncrementRequestPathCount(string requestPath) in Counter.cs
	+	19.            UrlCounter[requestPath]++;
 ```

11. In **Microsoft Edge**, click the **+** (plus) sign near **19**, and then inspect the code.

12. In **Microsoft Edge**, click **Close**.

13. In the **ErrorHandlingExample - Microsoft Visual Studio** window, in **Solution Explorer**, expand **Services**, and then click **Counter.cs**.

14. In the **Counter.cs** code window, select the following code:
```cs
    UrlCounter[requestPath]++;
```

15. Replace the selected code with the following code:
```cs
    if (UrlCounter.ContainsKey(requestPath))
    {
        UrlCounter[requestPath]++;
    }
    else
    {
        UrlCounter.Add(requestPath, 1);
    }
```

16. In the **ErrorHandlingExample - Microsoft Visual Studio** window, on the **FILE** menu, click **Save All**.

17. In the **ErrorHandlingExample - Microsoft Visual Studio** window, on the **DEBUG** menu, click **Start Without Debugging**.

18. In **Microsoft Edge**, click **16**.
     
19. In **Microsoft Edge**, locate the following text:
 ```
    ErrorHandlingExample.Controllers.HomeController.GetDividedNumber(int id) in HomeController.cs
	+	33.  DivisionResult divisionResult = _numberCalculator.GetDividedNumbers(id);
 ```

20. In **Microsoft Edge**, click the **+** (plus) sign near **33**, and then inspect the code.

21. In **Microsoft Edge**, locate the following text:
 ```
    ErrorHandlingExample.Services.DivisionCalculator.GetDividedNumbers(int number) in DivisionCalculator.cs
	+	20.  if (number % i == 0)
 ```

22. In **Microsoft Edge**, click the **+** (plus) sign near **20**, and then inspect the code.

23. In **Microsoft Edge**, click **Close**.

24. In the **ErrorHandlingExample - Microsoft Visual Studio** window, in **Solution Explorer**, under **Services**, click **DivisionCalculator.cs**.

25. In the **DivisionCalculator.cs** code window, select the following code:
```cs
    for (int i = 0; i < (number / 2) + 1; i++)
```

26. Replace the selected code with the following code:
```cs
    for (int i = 1; i < (number / 2) + 1; i++)
```

27. In the **ErrorHandlingExample - Microsoft Visual Studio** window, on the **FILE** menu, click **Save All**.

28. In the **ErrorHandlingExample - Microsoft Visual Studio** window, on toolbar, click the arrow next to the **Start Debugging** button, and then click **Production**.​

29. In the **ErrorHandlingExample - Microsoft Visual Studio** window, on the **DEBUG** menu, click **Start Without Debugging**.

30. In **Microsoft Edge**, click **16**.
    >**Note:** The browser displays the numbers that **16** can be divided by.

31. In **Microsoft Edge**, click **Close**.

32. In the **ErrorHandlingExample - Microsoft Visual Studio** window, on the **FILE** menu, click **Exit**.

# Lesson 3: Logging MVC Applications

### Demonstration: How to Log an MVC Application
#### Preparation Steps

1. Ensure that you have cloned the **20486D** directory from GitHub. It contains the code segments for this course's labs and demos. (**https://github.com/MicrosoftLearning/20486D-DevelopingASPNETMVCWebApplications/tree/master/Allfiles**)

#### Demonstration Steps

1. Navigate to **Allfiles\Mod10\Democode\03_LoggingExample_begin**, and then double-click **LoggingExample.sln**.

2. In the **LoggingExample - Microsoft Visual Studio** window, in **Solution Explorer**, click **Program.cs**. 

3. In the **Program.cs** code window, locate the following code:
```cs
    WebHost.CreateDefaultBuilder(args)
```

4. Place the cursor at the end of the located code, press Enter, and then type the following code:
```cs
    .ConfigureLogging((hostingContext, logging) =>
    {
        var env = hostingContext.HostingEnvironment;
        var config = hostingContext.Configuration.GetSection("Logging");

        logging.ClearProviders();

        if (env.IsDevelopment())
        {
            logging.AddConfiguration(config);
            logging.AddConsole();
        }
        else
        {
            logging.AddFile(config);
        }
    })
```

5. In **Solution Explorer**, expand **appsettings.json**, and then click **appsettings.development.json**.

6. Place the cursor after the **{** (opening braces) sign, press Enter, and then type the following code:
```cs
    "Logging": {
       "LogLevel": {
         "Default": "Trace"
       }
    }
```

7. In **Solution Explorer**, under **appsettings.json**, click **appsettings.production.json**.

8. Place the cursor after the **{** (opening braces) sign, press Enter, and then type the following code:
```cs
    "Logging": {
      "PathFormat": "myLog.txt",
      "LogLevel": {
        "Default": "Warning"
      }
    }
```

9. In **Solution Explorer**, expand **Controllers**, and then click **HomeController.cs**. 

10. In the **HomeController.cs** code window, locate the following code:
```cs
    ICounter _counter;
```

11. Place the cursor at the end of the located code, press Enter, and then type the following code:
```cs
    ILogger _logger;
```

12. In the **HomeController.cs** code window, select the following code:
```cs
    public HomeController(IDivisionCalculator numberCalculator, ICounter counter)
```

13. Replace the selected code with the following code:
```cs
    public HomeController(IDivisionCalculator numberCalculator, ICounter counter, ILogger<HomeController> logger)
```

14. In the **HomeController.cs** code window, locate the following code:
```cs
    _numberCalculator = numberCalculator;
```

15. Place the cursor at the end of the located code, press Enter, and then type the following code:
```cs
    _logger = logger;
```

16. In the **HomeController.cs** code window, select the following code:
```cs
    _counter.IncrementNumberCount(id);
    ViewBag.NumberOfViews = _counter.NumberCounter[id];
    ViewBag.CounterSucceeded = true;
```

17. Replace the selected code with the following code:
```cs
    try
    {
        _counter.IncrementNumberCount(id);
        ViewBag.NumberOfViews = _counter.NumberCounter[id];
        ViewBag.CounterSucceeded = true;
    }
    catch (Exception ex)
    {
        _logger.LogError(ex, $"An error occured while trying to increase or retrieve the page display count. Number parameter is: {id}");
    }
```

18. In the **LoggingExample - Microsoft Visual Studio** window, on the **FILE** menu, click **Save All**.

19. In the **LoggingExample - Microsoft Visual Studio** window, on toolbar, click the arrow next to the **Start Debugging** button, and then click **Production**.​

20. In the **LoggingExample - Microsoft Visual Studio** window, on the **DEBUG** menu, click **Start Without Debugging**.

21. In **Microsoft Edge**, click **16**.
    >**Note:** The browser displays the numbers that **16** can be divided by.

22. In **Microsoft Edge**, click **Close**.

23. In **File Explorer**, navigate to **Allfiles\Mod10\Democode\03_LoggingExample_begin\LoggingExample**, and then double-click **myLog-XXXXXXXX.txt**.
    >**Note**: Inspect the **KeyNotFoundException** stack trace.

24. In **myLog-XXXXXXXX.txt** window, click **Close**.

25. In **Solution Explorer**, expand **Services**, and then click **Counter.cs**. 

26. In the **Counter.cs** code window, select the following code:
```cs
    NumberCounter[number]++;
```

27. Replace the selected code with the following code:
```cs
    if (NumberCounter.ContainsKey(number))
    {
        NumberCounter[number]++;
        _logger.LogDebug($"The number of time the page was displayed for the number {number} was increased to {NumberCounter[number]}.");
    }
    else
    {
        NumberCounter.Add(number, 1);
        _logger.LogDebug($"The number {number} was added to the page display count dictionary.");
    }
```
28. In the **LoggingExample - Microsoft Visual Studio** window, on the **FILE** menu, click **Save All**.

29. In the **LoggingExample - Microsoft Visual Studio** window, on toolbar, click the arrow next to the **Start Debugging** button, and then click **Development**.​

30. In the **LoggingExample - Microsoft Visual Studio** window, on the **DEBUG** menu, click **Start Without Debugging**.

31. In the **LoggingExample - Microsoft Visual Studio** window, in the **Output** tab, click the **Output** pane.

32. In the **LoggingExample - Microsoft Visual Studio** window, on the **Output** tab, in the **Show output from** list, select **ASP.NET Core Web Server**, and then click the **Clear All** button.

33. In **Microsoft Edge**, click **16**.

34. In the **LoggingExample - Microsoft Visual Studio** window, on the **Output** tab, locate the following text:
```
    The number 16 was added to the page display count dictionary.
```

35. In **Microsoft Edge**, click **Close**.

36. In the **LoggingExample - Microsoft Visual Studio** window, on the **FILE** menu, click **Exit**.

©2018 Microsoft Corporation. All rights reserved.

The text in this document is available under the [Creative Commons Attribution 3.0 License](https://creativecommons.org/licenses/by/3.0/legalcode), additional terms may apply. All other content contained in this document (including, without limitation, trademarks, logos, images, etc.) are  **not**  included within the Creative Commons license grant. This document does not provide you with any legal rights to any intellectual property in any Microsoft product. You may copy and use this document for your internal, reference purposes.

This document is provided &quot;as-is.&quot; Information and views expressed in this document, including URL and other Internet Web site references, may change without notice. You bear the risk of using it. Some examples are for illustration only and are fictitious. No real association is intended or inferred. Microsoft makes no warranties, express or implied, with respect to the information provided here.
