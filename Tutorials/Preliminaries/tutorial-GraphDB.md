# Working with the GraphDB Triple Store

Starting from the third practical assignment, you will start working with triple stores. A triple store is just a specific type of graph database that stores RDF triples (subject, predicate, object), and allows their retrieval through semantic queries (e.g. using SPARQL).

There are a number of available triple stores created by different companies and institutions. In this course, we use the free edition of the [GraphDB](https://www.ontotext.com/products/graphdb/) triple store developed by [Ontotext](https://www.ontotext.com/), as it is free, easy to install, and supports all the features necessary in this course.  

This document presents a short tutorial on how to install and work with GraphDB for the purpose of this course. For additional information, please check the [GraphDB documentation](http://graphdb.ontotext.com/documentation/free/quick-start-guide.html).

### - *How to install the free edition of GraphDB?*

There are two ways to install GraphBB on your machine: either by 1) downloading the software and installing it on your device, or 2) by downloading a Docker image and running the software from a container.

#### Docker Container

Please follow these steps to run GraphDB from a container:

1. Download the tar file with the build script [here](https://surfdrive.surf.nl/files/index.php/s/Pm9b2r8FVVbds7c).
2. Extract the tar file in a new directory with `tar xf myTarFile.tar` or using a tool such as [7zip](https://www.7-zip.org/download.html).
3. Generate the GraphDB image as described in the supplied README file.
4. Start the container.

#### Manual Installation

Please follow these 5 simple steps to download and install GraphDB directly on your machine:

1. Open <https://ontotext.com/products/graphdb/graphdb-free/> in your browser
2. Fill in your information and provide a valid email address (e.g. your VU email address)
3. In less than 5 minutes, you should receive an email from the GraphDB team with a link for download (it is very probable that this email will end up in your SPAM/JUNK folder)
4. Choose the Operating System of your choice (Windows, Mac, deb based Linux, rpm based Linux)
5. Install GraphDB

### - *How to access the GraphDB web interface* -

Once started, the GraphDB web interface can be accessed by pointing your web browser to `127.0.0.1:7200`, which refers to the service (in our case GraphDB) which runs on port 7200 on your machine. Note that closing the tab or browser will not stop GraphDB from continue running in the background.

### - *How to create a local repository and load your own knowledge graph?*

After downloading and installing GraphDB, follow these steps to create your first repository and load your knowledge graph:

1. Launch the GraphDB Workbench (this step should open a new tab in your Web browser)
2. Create an empty local repository:
  * Go to the menu bar on the left of the page
  * Choose "Setup"
  * Choose "Repositories"
  * Choose "Create new repository"
  * Give it a simple Repository ID (e.g. *KnowledgeAndData*)
  * From the "Ruleset" options, choose the option **OWL-Max (Optimized)**
  * Choose "Create".
3. Now that your repository is created, you can see it on the top right of your window. It's time to import your knowledge graph into that repository:
  * Go to the menu bar on the left of the page
  * Choose "Import"
  * Choose "RDF" (then select the repository you want in case of several repositories)
  * Choose "Upload RDF files" and you should be able to select the .ttl file. Alternatively, you can directly copy-paste a small snippet by selecting the right option.
  * Select the file and choose "Import" (if another window appears, choose "Import" again)
  * If you go back to the main page (by clicking on the GraphDB logo on the top left), you will see that the number of total statements has increased, indicating that your knowledge graph has been successfully loaded into your repository.
4. [Optional] Assign a suitable prefix to the namespaces in your graph (e.g. `ex` instead of `ns1`) by choosing "Setup" and then "Namespaces".

### - *How to query both your local repository and DBpedia from GraphDB?*

You can write SPARQL queries inside of GraphDB, which is much more efficient than doing it in Jupyter Notebook over and over again. Get familiar with SPARQL, as you can from GraphDB query data in your local repository and other external repositories. It is even possible to query both local and external data in the same SPARQL query.

Try the following steps to query DBpedia from GraphDB:

1. Go to the menu bar on the left of the page
2. Choose "SPARQL"
3. Make sure you are in the repository that you want to query (or any repository if you're only interested in querying an external endpoint)
4. Execute the following SPARQL query in GraphDB, which returns 10 distinct and random official languages from DBpedia.

```turtle
    PREFIX dbo: <http://dbpedia.org/ontology/>
    SELECT DISTINCT ?language
    WHERE {
      SERVICE <https://dbpedia.org/sparql> {
        ?somePlace dbo:officialLanguage ?language .
      }
    } LIMIT 10
```
You can save your queries in GraphDB by clicking on the icon named "Create saved query", which you can find inside the query editor on the top right.

### - *How to get the SPARQL endpoint of your GraphDB local repository?*

Similarly to the DBpedia knowledge Graph which you can query in Yasgui or Python using its SPARQL endpoint: <http://dbpedia.org/sparql>, also you can query your GraphDB local repository. However, since your repository is local and not online, you can only query it if it hosted on the same machine. To get the SPARQL endpoint of your local repository, follow these steps:

1. Go to the menu bar on the left of the page
2. Choose "Setup
3. Choose "Repositories"
4. Next to the name of your repository, you can find on the right a set of different icons. Choose the first one from the left, named "Copy repository URL to clipboard"
5. You will find your local repository's SPARQL endpoint, which looks like this: http://127.0.0.1:7200/repositories/KnowledgeAndData

Now adapt some of the queries you tested on the DBpedia SPARQL endpoint to execute them on your local repository, by simply replacing the DBpedia SPARQL endpoint with this URL you just copied.
