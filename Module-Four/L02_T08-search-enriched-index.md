# Exercise - Search the Margie's Travel index

To search the Margie's Travel index, you will use a web application that includes a form in which users can submit search expressions. Select your preferred language below, and then follow the steps below to query the Margie's Travel search solution.

### Using Python

1. In the **02-Create-an-enrichment-pipeline/Python** folder, expand the **enriched-search-client** folder. This folder contains a simple Flask-based web application for the Margie's Travel web site.
2. Open the **.env** file. This file contains environment variables for the web application.
3. Modify the values in the **.env** file to reflect the endpoint and query key for your Azure Cognitive Search resources (be sure to specify the *query* key, and not the *admin* key!). Then save the updated file.
4. Open the **app&#46;py** code file. This contains the code for the Flask web application. The code:
    - Loads the required Azure Cognitive Search credentials from environment variables.
    - Defines a function named **azsearch_query** that submits a query as a REST request to an Azure Cognitive Search endpoint.
    - Defines a route for the web site's home page (*/*) that displays a web page based on the **default.html** template. This template includes a basic search form.
    - Defines a route for the search results page (*/search*) that retrieves the query text from the search form, constructs parameters for the REST request, submits the query, and renders the results in the **search.html** template.
    - Defines a route for a more advanced search page (*/filter*) that includes filtering and sorting.
5. Right-click (Ctrl+click if using a Mac) the **Python/enriched-search-client** folder and select **Open in Integrated Terminal** to open a new bash terminal in this folder.
6. In the terminal for the **enriched-search-client** folder, enter the following command:
    ```bash
    flask run
    ```
7. When the following message is displayed, follow the `https://127.0.0.1:5000/` link to open the web application in a new browser tab:
    ```text
    * Environment: production
      WARNING: This is a development server. Do not use it in a production deployment.
      Use a production WSGI server instead.
   * Debug mode: off
   * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
   ```
8. Wait for the web site to open (the web site is being run in the development container, and port forwarding is used to make it available as a locally hosted site in your browser session - you may need to allow access through your firewall)
9. In the Margie's Travel website, enter **"Statue of Liberty"** (including the quotation marks to search for the whole phrase) into the search box and click **Search**.
10. Review the search results. They include the file name (with a hyperlink to the file URL), author, size, last modified date, and an extract of the file content with the search term (*Statue of Liberty*) emphasized.
11. Examine the extract of the file content with *Statue of Liberty* emphasized, and observe that the term was found as text in images and in the AI-generated caption of one of the images.
12. Try another search by entering the search term **skyscraper** in the search box at the top of the page and clicking **Search**.
13. Examine the results, observing that the term *skyscraper* is not used anywhere in the document contents, but is one of the suggested image tags for each of the results.
14. Try another search by entering the search term **"Tower of London"** (including the quotation marks) in the search box at the top of the page and clicking **Search**.
15. Examine the results, observing that the term *Tower of London* not only appears in the resulting documents, but is also identified as a key phrase and a location.
16. Try another search by entering the search term **quiet hotel in London** in the search box at the top of the page and clicking **Search**.
17. When the results are returned, change the **Sort by** option to **Positive to negative** and refine the results to list them in descending order of sentiment.
18. Close the browser tab containing the Margie's Travel web site and return to Visual Studio Code. Then in the Python terminal for the **enriched-search-client** folder (where the flask application is running), enter CTRL+C to stop the app.

### Using Csharp

1. In the **02-Create-an-enrichment-pipeline/Python/C-Sharp** folder, expand the **enriched-search-client** folder. This folder contains a simple ASP&#46;NET Core web application for the Margie's Travel web site.
2. Open the **appsettings.json** file. This file contains configuration values for the web application.
3. Modify the values in the **appsettings.json** file to reflect the service name (<u>without</u> the .*search&#46;windows&#46;net* suffix) and query key for your Azure Cognitive Search service (be sure to specify the *query* key, and not the *admin* key!). Then save the updated file.
4. In the **Pages** folder for the web application, open the **Index.cshtml** code file. This file defines the main page of the web application. The page contains a form in which users can submit search terms, and code to render the search results.
5. Open the **Index.cshtml.cs** code file, which contains C# code to support the web page. Review the **OnGet** function, which is called when the page is requested. It extracts parameters passed in the request, and then uses a **SearchServiceClient** object to submit a query to Azure Cognitive Search. The query includes the following parameters:
    - **Select**: The index fields to be included in the query results.
    - **SearchMode**: This value determines how the search query is applied. A value of **All** means that all of the specified search terms must be present for the document to be included in the results. A value of **Any** means that only one or more of the terms must be present.
    - **HighlightFields**: Fields that can be used to display a snippet of the document data with the search term highlighted. In this case, the results include extracts from the **content** field with up to three instances of the search term shown in context.
    - **Facets**: Fields that can be used to provide filters in the user interface, enabling users to "drill-down" into the results. In this case, the **author** field is specified, so the results can include navigation elements that enable users to further refine the query by selecting individual author values.
6. In the **Models** folder, open the **SearchResults.cs** code file. This defines a class for the search results - the query returns a list of these objects.
7. Right-click (Ctrl+click if using a Mac) the **C-Sharp/enriched-search-client** folder and select **Open in Integrated Terminal** to open a new bash terminal in this folder.
8. In the terminal for the **enriched-search-client** folder, enter the following command:
    ```bash
    dotnet run
    ```
9. When the following message is displayed, follow the `https://localhost:5000/` link to open the web application in a new browser tab:
    ```text
    info: Microsoft.Hosting.Lifetime[0]
    Now listening on: http://localhost:5000
    info: Microsoft.Hosting.Lifetime[0]
    Application started. Press Ctrl+C to shut down.
    info: Microsoft.Hosting.Lifetime[0]
    Hosting environment: Development
    info: Microsoft.Hosting.Lifetime[0]
    Content root path: /root/workspace/km/01-Create-a-search-solution/C-Sharp/search-client
   ```
10. Wait for the web site to open (the web site is being run in the development container, and port forwarding is used to make it available as a locally hosted site in your browser session - you may need to allow access through your firewall).
11. In the Margie's Travel website, enter **"Statue of Liberty"** (including the quotation marks to search for the whole phrase) into the search box and click **Search**.
12. Review the search results. They include the file name (with a hyperlink to the file URL), author, size, last modified date, and an extract of the file content with the search term (*Statue of Liberty*) emphasized.
13. Examine the extract of the file content with *Statue of Liberty* emphasized, and observe that the term was found as text in images and in the AI-generated caption of one of the images.
14. Try another search by entering the search term **skyscraper** in the search box at the top of the page and clicking **Search**.
15. Examine the results, observing that the term *skyscraper* is not used anywhere in the document contents, but is one of the suggested image tags for each of the results.
16. Try another search by entering the search term **"Tower of London"** (including the quotation marks) in the search box at the top of the page and clicking **Search**.
17. Examine the results, observing that the term *Tower of London* not only appears in the resulting documents, but is also identified as a key phrase and a location.
18. Try another search by entering the search term **quiet hotel in London** in the search box at the top of the page and clicking **Search**.
19. When the results are returned, change the **Sort by** option to **Positive to negative** and refine the results to list them in descending order of sentiment.
20. Close the browser tab containing the Margie's Travel web site and return to Visual Studio Code. Then in the terminal for the **enriched-search-client** folder (where the dotnet process is running), enter Ctrl+C to stop the app.
