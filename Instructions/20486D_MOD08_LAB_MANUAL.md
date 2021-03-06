# Module 8: Using Layouts, CSS and JavaScript in ASP.NET Core MVC

# Lab: Using Layouts, CSS and JavaScript in ASP.NET Core

#### Scenario

You have been asked to add a slideshow to the homepage of the zooSite web application that will show some of the animals’ photos. The slideshow will display each photo in a large size. However, the slideshow will display only one photo at a time, and cycle through all the photos in order.

You want to use jQuery to create this slideshow because you want to cycle through the photos in the browser, without reloading the page each time. 

You have been also asked to add a purchase page to enable customers to buy adult, child and senior tickets to the zoo. To do calculations in the page you will use jQuery. You will also use client-side validation to validate the input typed by the users.

#### Objectives

After completing this lab, you will be able to:

- Apply a consistent look and feel to the web application.
- Use layouts to ensure that common interface features, such as the headers, are consistent across the entire web application.
- Render and execute JavaScript code in the browser.
- Use the jQuery script library to update and animate page elements.

### Lab Setup

Estimated Time: **60 minutes**

### Preparation Steps
1. Ensure that you have cloned the 20486D directory from GitHub. It contains the code segments for this course's labs and demos. (https://github.com/MicrosoftLearning/20486D-DevelopingASPNETMVCWebApplications/tree/master/Allfiles)

### Exercise 1: Applying a Layout and Link Views to it 

#### Scenario

To construct a consistent look and feel of a web application, a layout should be added to the web application. In this exercise you will create a layout and link views to it.

The main tasks for this exercise are as follows:

1. Create a layout.

2. Add a view and link it to a layout.

3. Add _ViewStart.cshtml.

4. Add existing views to the web application.

5. Add a section to the layout.

6. Run the application.


#### Task 1: Create a layout
1. From **Allfiles\Mod08\Labfiles\01_ZooSite_begin** open **ZooSite.sln**.

2. Create a new folder with the following information:

   - Parent folder: **Views**
   - Folder name: **Shared**

3. Add a new **Razor Layout** with the following information:

	- Folder: **Views/Shared**
	- Name: **_Layout**	

4. In the **_Layout.cshtml** file, in the **BODY** element, add a **UL** element with the following information:

	- Class: **nav**

5. In the **UL** element, add a **LI** element.

6. In the **LI** element, add an **A** element with the following information:

	- Href: **@Url.Action("Index", "Zoo")**
	- Content: **Attractions**

7. After the **LI** element, add a second **LI** element.

8. In the second **LI** element, add an **A** element with the following information:

	- Href: **@Url.Action("VisitorDetails", "Zoo")**
	- Content: **Visitor Info**

9. After the second **LI** element, add a third **LI** element.

10. In the third **LI** element, add an **A** element with the following information:

	- Href: **@Url.Action("BuyTickets", "Zoo")**
	- Content: **Tickets**

11. After the **UL** element, add a **DIV** element with the following information:

	- Class: **header-container**

12. In the **DIV** element, add an **H1** element with the following information:

	- Class: **content**
	- Content: **Welcome to Zoo Center**

13. After the **H1** element, add a **DIV** element with the following information:

	- Class: **slider-buttons**

14. In the **DIV** element, add an **IMG** element with the following information:

    - Src: **~/images/prevArrow.png**
	- Class: **prev**
    - Onclick: **prevImage()**

15. After the **IMG** element, add an **IMG** element with the following information:

	- Class: **next**
    - Src: **~/images/nextArrow.png**
    - Onclick: **nextImage()**


#### Task 2: Add a view and link it to a layout

1. In the **ZooController** class, right-click on the **Index** action name, and then click **Add View**. 

2. Create a new view using the **Add MVC View** dialog box, with the following information:

    - View Name: **Index**
    - Template: **Empty (without model)**
    - Create as Partial View: **False**
    - Use a layout page: **True**
    - Layout Page: **_Layout.cshtml**

3. Add a **@model** directive with the following information:

   - Type: **IEnumerable&lt;ZooSite.Models.Photo&gt;**


4.  Replace **_&lt;h2&gt;_Index_&lt;/h2&gt;_** with **H1** element, using the following information:

	- Class: **main-title**
    - Content: **Zoo Attractions**

5.  Add a **DIV** element with the following information:

	- Class: **container**

6. In the **DIV** element, create a **FOREACH** statement, with the following information:

	- Variable Type: **var**
	- Variable Name: **item**
	- Collection: **Model**

7. In the **FOREACH** statement block, Add a **DIV** element with the following information:

	- Class: **photo-index-card**

8. Create an **IF** statement that checks that the value of the **item.PhotoFileName** property is not **NULL**.

9. In the **IF** statement, add a **DIV** element with the following information:

	- Class: **image-wrapper**

10. In the **DIV** element, add an **IMG** element with the following information:

	- Class: **photo-display-img**
    - Src: **@Url.Action("GetImage", "Zoo", new { PhotoId = item.PhotoID })**

11. After the **IF** statement, add an **H3** element with the following information:

	- Class: **display-picture-title**
    - Content: **@Html.DisplayFor(modelItem  => item.Title)**

12. Add a **DIV** element.

13. In the **DIV** element, add a **SPAN** element with the following information:

	- Class: **display**
    - Content: **@Html.DisplayFor(model => item.Description)**

#### Task 3: Add _ViewStart.cshtml

1. Create a new **Razor View Start** file, with the following information:

    - Name: **_ViewStart**
    - Folder: **Views**

2. At the beginning of the **Index.cshtml** view, remove the **Layout** property with its value.

#### Task 4: Add existing views to the web application

1. Add existing **.cshtml** files to the **ZooSite** project, with the following information:

    - Source location: **Allfiles\Mod08\Labfiles\ZooViews**
	- Target location: **Allfiles\Mod08\Labfiles\01_ZooSite_begin\Zoo\Views**


#### Task 5: Add a section to the layout

1. In the **_Layout.cshtml** file, after the **DIV** element with **@RenderBody()** content, call the **RenderSection** method. 

2. Pass **"Scripts"** and **false** as parameters to the **RenderSection** method.


#### Task 6: Run the application

1. Save all the changes.

2. Start the application without debugging.

3. In the menu bar, click **Visitor Info**.

4. In the menu bar, click **Tickets**.

5. Close the **Microsoft Edge** window.

>**Results**: After completing this exercise, you will be able to add a layout and link views to it. You will also be able to use the **_ViewStart** file in the web application.  

### Exercise 2: Using CSS 

#### Scenario

To improve the appearance of the web application, a CSS should be used. In this exercise you will add a CSS file to the web application, and add a link from the layout to the CSS file.

The main tasks for this exercise are as follows:

1. Add existing CSS file to the project.

2. Link the layout to the CSS file.

3. Style the menu.

4. Style the photos section in Index.cshtml.

5. Style a form in BuyTickets.cshtml.

6. Run the application.

#### Task 1: Add existing CSS file to the project

1. Create a new folder with the following information:

	- Folder name: **css**
	- Parent folder: **wwwroot**

2. Add **zoo-style.css** file to the **ZooSite** project, with the following information:

	- Source location: **Allfiles\Mod08\Labfiles\ZooCSS**
	- Target location: **Allfiles\Mod08\Labfiles\01_ZooSite_begin\Zoo\wwwroot\css**

3. In **Startup** class, in the **Configure** method, after the call to the **zooContext.Database.EnsureCreated** method, call the **UseStaticFiles** method of the **app** parameter.

#### Task 2: Link the layout to the CSS file

1. In the **_Layout.cshtml** file, in the **HEAD** element, add a **LINK** element with the following information:

	- Type: **text/css**
	- Rel: **stylesheet**
	- Href: **~/css/zoo-style.css**

#### Task 3: Style the menu

1. In the bottom of the **zoo-style.css** file, add a **.nav** selector with the following properties:

	- list-style-type: **none**
	- margin: **0**
	- padding: **0**
	- overflow: **hidden**
	- background-color: **#85754e**
	- Position: **fixed**
	- top: **0**
	- left: **0**
	- width: **100%**

2. Add a **.nav li** selector with the following property:

	- float: **left**

3. Add a **.nav li a** selector with the following properties:

	- display: **block**
	- color: **white**
	- text-align: **center**
	- padding: **14px 16px**
	- text-decoration: **none**

4. Add a **.nav li a:hover:not(.active)** selector with the following property:

	- background-color: **#016b6b**

5. Add a **.active** selector with the following properties:

	- background-color: **#008484**		
	- color: **#fff**


#### Task 4: Style the photos section in Index.cshtml

1. Add a **.photo-index-card** selector with the following properties:

	- background-color: **#ffffff**
	- padding: **0**
	- margin: **10px 5px 15px 18px**
	- padding-bottom: **25px**
	- width: **355px**
	- border: **1px solid #d6d4d4**
	- border-radius: **10px**
	- overflow: **hidden**

#### Task 5: Style a form in BuyTickets.cshtml

1. Add a **.info .form-field** selector with the following property:

	- text-align: **left**

2. Add a **.info label** selector with the following properties:

	- width: **118px**
	- display: **inline-block**
	- margin-bottom: **10px**

3. Add a **.info input** selector with the following properties:

	- border-radius: **2px**
	- line-height: **20px**
	- border: **1px solid #ccc6c6**
	- background-color: **#f9f6f6**

4. Add a **input.submit-btn** selector with the following properties:

	- width: **100px**
	- margin-top: **12px**
	- height: **29px**
	- background-color: **orange**
	- font-weight: **bold**
	- box-shadow: **inset 0px 0px 4px #b77006**
	- border: **1px solid #a59797**

5. Add a **input.submit-btn[disabled]** selector with the following properties:

	- opacity: **0.8**
	- background-color: **whitesmoke**
	- box-shadow: **none**

#### Task 6: Run the application

1. Save all the changes.

2. Start the application without debugging.

3. On the **Zoo Attractions** page, in the header  click **right arrow**, and then click **left arrow**.

    >**Note:** The browser displays the **header** with the slider, but functionality is not applied yet.

4. In the menu bar, click **Visitor Info**.

5. In the menu bar, click **Tickets**.

6. On **Step 1 - Choose Tickets**, select the following:

	- Adult: **_&lt;As many tickets as you like&gt;_**
	- Child: **_&lt;As many tickets as you like&gt;_**
	- Senior: **_&lt;As many tickets as you like&gt;_**

    >**Note:** The browser displays **Step 1 - Choose Tickets**, but functionality is not applied yet.

7.  On **Step 2 - Buy Tickets**, type the following:

	- First Name: **_&lt;A first name of your choice&gt;_**
	- Last Name: **_&lt;A last name of your choice&gt;_**
	- Address: **_&lt;An address of your choice&gt;_**
	- Email: **_&lt;abcd&gt;_**
	- Phone Number **_&lt; A phone number of your choice&gt;_**

8. Click **Buy**.

    >**Note:** The browser displays **Step 2 - Buy Tickets**, but you cant buy the tickets and there is no validation, the functionality is not applied yet.

9. Close **Microsoft Edge**.

>**Results**: After completing this exercise, you will be able to add an existing CSS file to a web appllication, add a link form a layout to the CSS file and add new CSS selectors. 

### Exercise 3: Using JavaScript

#### Scenario

To calculate the total cost of the tickets, you have been asked to add a function in JavaScript. In this exercise you will add a JavaScript file and add a link to the JavaScript file from a view.

The main tasks for this exercise are as follows:

1. Add a JavaScript file.

2. Link a view to the JavaScript file.

3. Write the code of the JavaScript file.


#### Task 1: Add a JavaScript file

1. Create a new folder with the following information:

	- Folder name: **js**
	- Parent folder: **wwwroot**

2. Add a **JavaScript** **File** with the following information:

	- Folder: **js**
	- Name: **form-functions**	

#### Task 2: Link a view to the JavaScript file

1. In the **BuyTickets** view, in the **Scripts** section code block, add a **SCRIPT** element with the following information:

	- Src: **~/js/form-functions.js**

#### Task 3: Write the code of the JavaScript file
1. In the **form-functions.js** file, add a **function** with the following information:

	- Name: **calculateSum**

2. In the **calculateSum** function code block, add a new variable named **rows** with the value of **document.querySelectorAll("#totalAmount tr .sum")**.

3. Add a new variable named **sum** with the value of **0**.

4. Create a **FOR** loop, with the following information:

	- Initial Expression: **var i = 0**
	- Condition: **i < rows.length**
	- Increment Expression: **i++**

5. In the **FOR** loop code block, assign the **sum** variable the value of **sum + parseFloat(parseFloat(rows[i].innerHTML.substring(1, rows[i].innerHTML.length)).toFixed(2))**.

6. Assign the **innerHTML** property of **document.getElementById("sum")** to **"Total: $" + sum**.

>**Results**: After completing this exercise, you will be able to add a **JavaScript File** and write JavaScript code. 

### Exercise 4: Using jQuery

#### Scenario

You have been asked to handle click events, modify elements and change the style of elements. You were also asked to apply client-side validation in the web application. In this exercise you will use npm to add several client-side packages to the web application, and you will use the packages to make various operations in the client-side.

The main tasks for this exercise are as follows:

1. Use npm to add jQuery.

2. Use jQuery to add event handlers.

3. Use jQuery to modify elements.

4. Client-side validation using jQuery.

5. Run the application.

#### Task 1: Use npm to add jQuery

1. Add a new **npm Configuration File** to the **ZooSite** project.

2. In the  **package.json** file, add the following key and value in the **dependencies** object:

	- Key: **"jquery"**
	- Value: **"3.3.1"**

3. Save **package.json**.

>**Note:** In **Solution Explorer**, under **Depenndencies**, a new folder named **npm** has been added which contains the **jquery** package.

4. In **Explorer Toolbar Options** click **Show All Files**.

      >**Note:** In the **ZooSite - Microsoft Visual Studio** window, in **Solution Explorer**, a new folder named **node_modules** has been added which contains the **jquery** package.

5. Create a new folder with the following information:

   - Folder name: **Middleware**

6. Add a new class with the following information:

	- Folder: **Middleware**
	- Name: **ApplicationBuilderExtensions**

7. In the **ApplicationBuilderExtensions** class, add **USING** statements for the following namespaces:

   - **System.IO**
   - **Microsoft.AspNetCore.Builder**
   - **Microsoft.Extensions.FileProviders**

8. Add a **static** keyword to the **ApplicationBuilderExtensions** class declaration.

9. Add a method with the following information:

    - Scope: **public**
	- Modifier: **static**
    - Return Type: **IApplicationBuilder**
    - Name: **UseNodeModules**
	- Parameters:
		- Parameter:
			- Type: **this IApplicationBuilder**
			- Name: **applicationBuilder**
		- Parameter:
			- Type: **string**
			- Name: **root**

10. In the **UseNodeModules** method, add a variable named **path** of type **var** with the value of **Path.Combine(root, "node_modules")**.

11. Add a variable named **fileProvider** of type **var** with the value of **new PhysicalFileProvider(path)**.

12. Add a variable named **options** of type **var** with the value of **new StaticFileOptions()**.

13. Assign the **RequestPath** property of the **options** variable the value of **/node_modules**.

14. Assign the **FileProvider** property of the **options** variable the value of **fileProvider** variable.

15. Call the **UseStaticFiles** method of the **applicationBuilder** parameter. Pass **options** variable as a parameter to the **UseStaticFiles** method.

16. Return the value of the **applicationBuilder** variable.

17. In the **Startup** class, add **USING** statement for the following namespace:

   - **ZooSite.Middleware**

18. In **Startup** class, in the **Configure** method, after the call to the **UseStaticFiles** method, call the **UseNodeModules** method of the **app** parameter and pass **env.ContentRootPath** as a parameter.

19. In the **_Layout.cshtml** file, in the end of the **HEAD** element, add a **SCRIPT** element with the following information:

	- Src:**~/node_modules/jquery/dist/jquery.min.js**

#### Task 2: Use jQuery to add event handlers
1. At the end of the **form-functions.js** file, call the **$** function. Pass an anonymous function as a parameter to the **$** function.

2. Move the **calculateSum** function inside the anonymous function.

3. At the beginning of the anonymous function code block, call the **$** function and pass **'.pricing select'** as a parameter. 

4. Chain a **change** function call to the **$** function call. Pass anonymous function as a parameter to the **change** function.

5. Change the signature of the anonymous function passed to the **change** method to accept an **event** parameter.

6. Inside the anonymous function passed to the **change** method, create a variable named **target** and assign it the value of **$(event.target)**.

7. Create a variable named **value** and assign it the value of **parseInt(target.val())**

8. Create a variable named **container** and assign it the value of **target.parent()**..

9. Create a variable named **price** and assign it the value of **container.prev()**.

10. Create a variable named **label** and assign it the value of **price.prev()**.

11. Call the **$** function and pass **"#" + label.text()** as a parameter. 

12. Chain a **remove** function call to the **$** function call. 


#### Task 3: Use jQuery to modify elements
1. At the end of the **$** function, add an **IF** statement that checks that value of **value** variable is not empty.

2. Inside the **IF** statement, call the **$** function and pass **'#summery'** as a parameter. 

3. Chain a **addClass** function call to the **$** function call. Pass **"display-div"** as a parameter to the **addClass** function.

4. Chain a **removeClass** function call to the **addClass** function call. Pass **"hidden-div"** as a parameter to the **addClass** function.

5. Create a variable named **correctCost** and assign it the value of **(price.text().substring(1, price.text().length))**.

6. Create a variable named **calc** and assign it the value of **parseInt(value * correctCost)**.

7. Create a variable named **msg** and assign it the value of **label.text() + " ticket - " + value.toString() + "x" + price.text() + " = &lt;span class='sum'&gt;" +'$' + calc +'&lt;/span&gt;'**.

8. Create a variable named **row** and assign it the value of **$("&lt;tr id='" + label.text() +"'&gt;")**.

9. Call the **append** method of the **row** variable. Pass **$("&lt;td&gt;")** as a parameter to the **append** function.

10.  Chain an **html** function call to the **append** function call. Pass **msg** as a parameter to the **append** function.

11. Call the **$** function and pass **'#totalAmount'** as a parameter. 

12. Chain an **append** function call to the **$** function call. Pass **row** as a parameter to the **append** function.

13. After the **IF** statement code block, add an **IF** statement that checkes if the value of **$("#totalAmount tr").length** is equal to **0**.

14. Inside the **IF** statement code block, call the **$** function and pass **'#summery'** as a parameter. 

15. Chain an **addClass** function call to the **$** function call. Pass **"hidden-div"** as a parameter to the **addClass** function.

16. Chain an **removeClass** function call to the **addClass** function call. Pass **"display-div"** as a parameter to the **removeClass** function.

17. Call the **$** function and pass **'#formButtons input'** as a parameter. 

18. Chain an **attr** function call to the **$** function call. Pass **"disabled"** and **"disabled"** as a parameters to the **attr** function. 

19. Call the **$** function and pass **'#comment'** as a parameter. 

20. Chain an **show** function call to the **$** function call. 

21. After the **IF** statement code block, add an **ELSE** statement. 

22. Inside the **ELSE** statement code block, call the **$** function and pass **'#formButtons input'** as a parameter. 

23. Chain a **removeAttr** function call to the **$** function call. Pass **"disabled"** as a parameter to the **removeAttr** function.

24. Call the **$** function and pass **'#comment'** as a parameter. 

25. Chain a **hide** function call to the **$** function call. 

26. After the **ELSE** ststement call block, call the **calculateSum** function.

27. Add a **JavaScript File** with the following information:

	- Folder: **js**
	- Name: **menubar-functions**	

28. In the beginning of the **menubar-functions.js** file, call the **$** function. Pass an anonymous function as a parameter to the **$** function.

29. At the beginning of the anonymous function code block, add a new variable named **path** with the value of **window.location.pathname**.

30. Call the **$** function and pass **'.nav li a'** as a parameter. 

31. Chain a **each** function call to the **$** function call. Pass anonymous function as a parameter to the **each** function.

32. Change the signature of the anonymous function passed to the **each** method to accept **index** and **value** parameters.

33. Inside the anonymous function passed to the **each** method, create a variable named **href** and assign it the value of **$(value).attr('href')**.

34. Create an **IF** statement that checks that the value of **path** is equal to **href**.

35. Inside the **IF** statement code block, call the **$** function and pass **this** as a parameter. 

36. Chain a **closest** function call to the **$** function call. Pass **'li'** to the **closest** function.

37. Chain a **addClass** function call to the **closest** function call. Pass **'active'** to the **addClass** function.

38. Add a **JavaScript File** with the following information:

	- Folder: **js**
	- Name: **slider-functions**	

39. In the beginning of the **slider-functions.js** file,  add a new variable named **images** with the value of **['/images/header.jpg', '/images/waters.jpg']**.

40. Add a new variable named **current** with the value of **0**.

41. Add a new **function** with the following information:
    - Name: **nextImage**

42. In the **nextImage** function code block, increment the **current** variable by 1.

43. Create an **IF** statement that checks that the value of **current** is equal to **images.length**.

44. Inside the **IF** statement code block, assign the **current** variable the value of **0**.

45. After the **IF** statement code block, call the **$** function and pass **'.header-container'** as a parameter. 

46. Chain a **css** function call to the **$** function call. Pass **'background-image'** and **'url(' + images[current] + ')'** as a parameters to the **css** function. 

47. Add a new **function** with the following information:
    - Name: **prevImage**

48. In the **prevImage** function code block, decrement the **current** variable by 1.

49. Create an **IF** statement that checks that the value of **current** is smaller than **0**.

50. Inside the **IF** statement code block, assign the **current** variable the value of **images.length-1**.

51. After the **IF** statement code block, call the **$** function and pass **'.header-container'** as a parameter. 

52. Chain a **css** function call to the **$** function call. Pass **'background-image'** and **'url(' + images[current] + ')'** as a parameters to the **css** function. 

53. In the **_Layout.cshtml** file, in the bottom of the **HEAD** tag code block, add a **SCRIPT** element with the following information:

	- Src: **~/js/menubar-functions.js**

54. Add a **SCRIPT** element with the following information:

	- Src: **~/js/slider-functions.js**


#### Task 4: Client-side validation using jQuery

1. In the  **package.json** file, add the following key and value in the **dependencies** object:

	- Key: **"jquery-validation"**
	- Value: **"1.17.0"**

2. In the  **package.json** file, add the following key and value in the **dependencies** object:

	- Key: **"jquery-validation-unobtrusive"**
	- Value: **"3.2.10"**

3. Save **package.json**.

    >**Note:** In **Solution Explorer**, under **Dependencies**, under **npm** new packages have been added named **jquery-validation**, and **jquery-validation-unobtrusive**.

4. In the **BuyTickets** view, in the beginning of the **Scripts** section code block, add a **SCRIPT** element with the following information:

	- Src: **~/node_modules/jquery-validation/dist/jquery.validate.min.js**

5. Add a **SCRIPT** element with the following information:

	- Src: **~/node_modules/jquery-validation-unobtrusive/dist/jquery.validate.unobtrusive.min.js**

#### Task 5: Run the application

1. Save all the changes.

2. Start the application without debugging.

3. On the **Zoo Attractions** page, in the header  click **right arrow**, and then click **left arrow**.

    >**Note:** The browser displays the **header** with the slider, and the slider functionality is applied.

4. In the menu bar, click **Visitor Info**.

5. In the menu bar, click **Tickets**.

    >**Note:** The **Buy** button is disabled, and there is a message **Please Choose Tickets** under the button.

6. On **Step 1 - Choose Tickets**, select the following:

	- Adult: **_&lt;As many tickets as you like&gt;_**
	- Child: **_&lt;As many tickets as you like&gt;_**
	- Senior: **_&lt;As many tickets as you like&gt;_**

    >**Note:** The **Buy** button is enabled, and the message under the button disappeared.

7.  On **Step 2 - Buy Tickets**, type the following:

	- First Name: **_&lt;A first name of your choice&gt;_**
	- Last Name: **_&lt;A last name of your choice&gt;_**
	- Address: **_&lt;An address of your choice&gt;_**
	- Email: **_&lt;abcd&gt;_**

    >**Note:** Client side validation applied.

8. On **Step 2 - Buy Tickets**, type the following:

	- Email: **_&lt;An email of your choice&gt;_**
	- Phone Number **_&lt; A phone number of your choice&gt;_**

9. Click **Buy**.

10. Close **Microsoft Edge**.

11. Close **Microsoft Visual Studio**.

>**Results**: After completing this exercise, you will be able to add jQuery to a web application using npm, modify HTML elements using jQuery, preform client-side validation and handle JavaScript events. 