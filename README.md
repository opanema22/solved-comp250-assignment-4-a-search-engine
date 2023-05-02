Download Link: https://assignmentchef.com/product/solved-comp250-assignment-4-a-search-engine
<br>
A search engine is software, usually accessed on the Internet, designed to carry out searches in a database of information according to the user’s query. The results provided are meant to best match what the user is trying to find and they are usually displayed in order of importance. The first search engine ever developed is considered to be Archie. It was named to resemble the word “archive”, and it was created in the 1990 by Alan Emtage, Bill Heelan and J. Peter Deutsch, computer science students at McGill. Today, there are many different search engines available on the Internet, each with their own abilities and features. The most popular of them all being Google.

A search engine performs the following tasks:

<ul>

 <li>Crawling and Indexing</li>

 <li>Ranking</li>

 <li>Searching</li>

</ul>

<strong>Crawling and Indexing </strong>Crawling is the process during which a search engine use programs, generally called <em>spiders </em>or <em>crawlers</em>, to collect information from web pages. By following links from a web page to another, the spiders find new content. Once a page is crawled, the data contained in the page is processed and indexed. Indexing is the process of storing and organizing the content found during the crawling. It generally involve associating words and other definable tokens found on web pages to a list of web pages that contain them. It also includes recording links to other pages. These associations are all stored in a database which is then used for web search queries. During this process the webgraph is created/updated. This is a directed graph where each node represents a page, and an edge represents an hyperlink from one page to another. This is also when what we refer to as the ‘word index’ is created. You can think of it as a mapping from single words to a list of urls containing them. Note that for actual search engine, this task (crawling and indexing) is never actually completed. Given the constantly changing nature of the Web, spiders are always crawling to keep the database up to date. <a href="https://www.google.com/search/howsearchworks/crawling-indexing/">The Google Search index</a> contains hundreds of billions of webpages.

<strong>Ranking </strong>How useful a search engine is depends on how relevant are the results obtained when we query it. There are millions of pages containing a specific word, but some pages are generally more relevant, or authoritative than others. To determine which pages to show in the search results and in what order, search engines use the data collected to perform a ranking. Different search engines use different algorithms to rank pages. Developed by Larry Page and Sergey Brin in 1996, <a href="http://infolab.stanford.edu/~backrub/google.html">PageRank </a>is one of the algorithms used at Google to rank webpages based on their importance. Using the webgraph, each webpage is assigned a numerical value that measure its relative importance. In simple terms, the rank of a webpage depends on the webpages that link to it. The contribution to the rank is higher if these linking webpages have a high rank themselves, while it’s lower if these linking webpage also link to a lot of other webpages.

<strong>Searching </strong>In this step, search engines receive a query from the user. Using the index created while crawling and the ranking based on the webgraph, the engine outputs a list of relevant web pages in order of importance. Do all search engines give the same results? Not necessarily. Search engines use different spiders to crawl and use different proprietary algorithms to index the data. Each index is therefore a search engine’s representation of how they see the web. Also the algorithms to rank and search the data are different, so every search engine has its own approach to finding what you’re trying to find. Finally, personalisation adapts the search to a specific computer/user. The results may be based on your geographical location, what else you’ve searched for, and what results were preferred by other users searching for the same thing, for example. Search engines might use and weigh all these factors in a unique way, which will lead to different search results.

The starter code contains four classes:

<ul>

 <li>XmlParser: This class has two methods: one to read the content of the xml database (which will serve as proxy for a web page for our assignment) given a url, and the other to extract information from it.

  <ul>

   <li>getContent(String url) returns an ArrayList of Strings corresponding to the set of words in the web page located at the given url. You will need to use this method while crawling in order to build your word index.</li>

   <li>getLinks(String url) returns an ArrayList of Strings containing all the hyperlinks going out of the given url. You will need this method to build the graph representing the data found while crawling.</li>

  </ul></li>

</ul>

You should NOT modify this class at all.

<ul>

 <li>MyWebGraph: This class implements the data structure needed to store the data collected during the crawling phase. It has an inner class called WebVertex which is used to store data related to a specific web page. You should NOT modify this class at all.</li>

 <li>SearchEngine: This is one of the classes in which you will have to add your code. You will be implementing methods that performs the three tasks described above.</li>

 <li>Sorting: This is utility class containing methods that implement some sorting algorithm. You will be asked to implement one of them.</li>

</ul>

<h1>Your task</h1>

In this assignment you are going to write a search engine program that will:

<ol>

 <li>explore a portion of the web (which we’ll simulate through a database),</li>

 <li>build an index of the words contained in each web page,</li>

 <li>analyze the structure of the web graph to establish which web page should be ranked higher,</li>

 <li>use this analysis to perform simple searches where a query word is entered by the user and a sorted list of relevant web pages available is returned.</li>

</ol>

Although we are going to apply these tools using a local database, what you will develop is a simplified version of the what is used at Google to answer actual web queries.

To be able to implement the search engine program described above, we need a graph data structure that will allow us to store all the information related to the web pages. Such class is provided to you.

<strong>[Provided] </strong>The class MyWebGraph is an implementation of a directed graph using adjacency lists. You will be using this type of data structure to store the information your program collects in the crawling phase. Each node in the graph will store a String corresponding to the url of a webpage. The class has the following field:

<ul>

 <li>A HashMap storing all the vertices in the graph. Note that we’ll be labelling each vertex with the String corresponding to the url of the webpage represented by this vertex.</li>

</ul>

The class has also the following public methods:

<ul>

 <li>The constructor MyWebGraph() which does not take any input and initializes the field with an empty HashMap.</li>

 <li>An addVertex() method which takes as input a String representing a url. The method adds the corresponding vertex to the graph.</li>

 <li>An addEdge() method which takes as input two Strings, i.e. two urls. The method adds to the graph an edge from the vertex labelled with the first input to the vertex labelled with the second input.</li>

 <li>A getNeighbors() method which takes as input a String representing a url and returns an ArrayList of all the hyperlinks contained in the specified url.</li>

 <li>A getVertices() method which returns the list of all the urls represented in the graph.</li>

 <li>A getEdgesInto() method that takes as input a String representing a url. The method returns an ArrayList of Strings of all the pages that contains an hyperlink to the specified url.</li>

 <li>A getOutDegree() method which takes as input a String representing a url and returns the number of hyperlinks in the specified page.</li>

 <li>A getPageRank() method which takes as input a String representing a url and returns the rank of the specified page.</li>

 <li>A setPageRank() method which takes as input a String representing a url and a double representing its rank. The method assigns the input number as the rank of the specified page.</li>

 <li>A getVisited() method which takes as input a String representing a url and returns whether or not the specified page has been visited.</li>

 <li>A setVisited() method which takes as input a String representing a url and a boolean. The method assigns the input boolean to the visited field of the specified page.</li>

</ul>

<strong> </strong>The Sorting class is a utility class that at the moment contains a static method called slowSort(). This method takes as input a HashMap where the values are Comparable. The method returns an ArrayList containing all the keys in the map, sorted in descending

order based on the values they map to. The time complexity of slowSort is <em>O</em>(<em>n</em><sup>2</sup>), where <em>n </em>is the number of pairs in the map. Your task is to implement a method called fastSort which performs the same task as slowSort but with a time complexity of <em>O</em>(<em>n </em>· log(<em>n</em>)).

The SearchEngine class has the following fields:

<ul>

 <li>A HashMap called wordIndex used to represent the mapping from single words to a list of urls containing them.</li>

 <li>A MyWebGraph called internet which is used to store all relevant information regarding the structure of the webgraph.</li>

 <li>An XmlParser called parser which you should use to retrieve information for the database serving as a proxy for the web.</li>

</ul>

In this class, you should implement the following methods:

crawlAndIndex

This method takes a String as input representing a url. It will perform a graph traversal of the web, starting at the given url. You can use either a depth-first search or a breadthfirst search, and you can make it either recursive or non-recursive. For each url visited, the method should do the following:

<ul>

 <li>Update the web graph by adding the appropriate vertex and edges.</li>

 <li>Update the word index so that every word in the url just visited appear in the mapping.</li>

</ul>

Note that, it is possible for the graph to contain cycles. For instance, if it possible that two web pages link to each other. To prevent this method from getting stuck in an infinite loop, you should make sure to keep track of which web page has already been visited. This method should stop crawling once all web pages (in the database) have been visited.

assignPageRanks and computeRanks

The method computeRanks is a helper method for assignPageRanks. We specifically ask you to implement it so that our grader will be able to assign partial marks to your implementation. The purpose of assignPageRanks is to assign a rank to each vertex in the web graph. It will only be called after crawlAndIndex has been executed. Here are the ideas we will be using to assign a rank to a web page:

<ul>

 <li>Good web pages are cited by many other pages. If we think about it in terms of the webgraph, this means that we should prefer web pages (i.e. vertices) with a large in-degree.</li>

 <li>Web pages that link to a large number of other pages are less valuable. In terms of webgraph, this means that we will value less web pages (i.e. vertices) with a large out-degree.</li>

 <li>A link from a web page is more valuable if the web page is itself a good one. In graph terms, higher the rank of a web page (i.e. vertex), more valuable an in-edge from it would be.</li>

</ul>

Note that the rank of a page depends solely on the structure of the graph we have created while crawling. To represent the ideas just described, let

<ul>

 <li>the <em>pr</em>(<em>w</em>) be the page rank of a vertex <em>w</em></li>

 <li>the <em>out</em>(<em>w</em>) be the out-degree of a vertex <em>w</em></li>

 <li><em>w</em><sub>1</sub>, <em>w</em><sub>2</sub>, …, <em>w<sub>k </sub></em>be all the vertices in the graph that have an out edge going into <em>v</em>.</li>

</ul>

Then, the following equation determines the page rank of a vertex <em>v</em>:

The constant <em>d </em>is called the <em>damping factor </em>and it is added for technical reasons to account for the probability that an imaginary surfer who is randomly clicking on links will eventually stop clicking. For this assignment, we will be using a damping factor of 0<em>.</em>5. As you may notice, <em>pr</em>(<em>v</em>) is defined as a function of <em>pr</em>(<em>w<sub>i</sub></em>). If <em>N </em>is the total number of vertices in the graph (<em>v</em><sub>1</sub><em>,v</em><sub>2</sub><em>,…,v<sub>N</sub></em>), then we have a system of <em>N </em>linear equations in <em>N </em>variables. The unknown values, i.e. our variables, are the <em>pr</em>(<em>v<sub>i</sub></em>). To determine their values, we should solve the system of linear equations described above. To do so, we could use linear algebra, but the implementation of gaussian elimination runs in <em>O</em>(<em>n</em><sup>3</sup>). To improve the efficiency, we can instead use an iterative algorithm that approximate the result. The idea is the following:

<ul>

 <li>Start by initializing <em>pr</em>(<em>v<sub>i</sub></em>) to 1 for all 0 ≤ <em>i </em>≤ <em>N</em></li>

 <li>Repeat the following until convergence:</li>

</ul>

<strong>– </strong>compute <em>pr</em>(<em>v<sub>i</sub></em>) for all <em>i </em>using the formula above.

This single step is what the helper method computeRanks should be doing. The method takes as input an ArrayList&lt;String&gt; representing the urls in the web graph and returns an ArrayList&lt;double&gt; representing the newly computed ranks for those urls. Note that the double in the output list is matched to the url in the input list using their position in the list. That is, the page rank of the url stored in position <em>i </em>in the input list, can be found in position <em>i </em>in the output list.

Convergence is reached when  for all <em>i</em>, where <em>pr<sup>j</sup></em>(<em>v<sub>i</sub></em>) represents the computation of <em>pr</em>(<em>v<sub>i</sub></em>) in the <em>j</em>-th iteration, and <em> </em><strong>is the input to the method</strong>. Note that, you can assume that the web graph does not contain self loops and every vertex in the graph has at least one outgoing edge.

Consider the following web graph:

Suppose we’d like to compute the page rank assigned to each vertex with an <em> </em>equal to

0<em>.</em>01. We start by assigning value 1 to each of them:

<ul>

 <li><em>pr</em>(<em>A</em>) = 1</li>

 <li><em>pr</em>(<em>B</em>) = 1</li>

 <li><em>pr</em>(<em>C</em>) = 1</li>

 <li><em>pr</em>(<em>D</em>) = 1</li>

</ul>

Then we need to use the following formula (same as the formula above, but with damping factor of 0<em>.</em>5) to recompute the page ranks for each vertex, until convergence.

After the first iteration we get:

<ul>

 <li><em>pr</em>(<em>A</em>) = 1<em>/</em>2 + 1<em>/</em>2 ∗ (1<em>/</em>3 + 1) = 7<em>/</em>6 = 1<em>.</em>166</li>

 <li><em>pr</em>(<em>B</em>) = 1<em>/</em>2 + 1<em>/</em>2 ∗ (1<em>/</em>2) = 3<em>/</em>4 = 0<em>.</em>75</li>

 <li><em>pr</em>(<em>C</em>) = 1<em>/</em>2 + 1<em>/</em>2 ∗ (1<em>/</em>2 + 1<em>/</em>3 + 1) = 17<em>/</em>12 = 1<em>.</em>416</li>

 <li><em>pr</em>(<em>D</em>) = 1<em>/</em>2 + 1<em>/</em>2 ∗ (1<em>/</em>3) = 4<em>/</em>6 = 0<em>.</em>666</li>

</ul>

After the second iteration we get:

<ul>

 <li><em>pr</em>(<em>A</em>) = 1<em>/</em>2 + 1<em>/</em>2 ∗ (0<em>.</em>75<em>/</em>3 + 1<em>.</em>416) = 1<em>.</em>333</li>

 <li><em>pr</em>(<em>B</em>) = 1<em>/</em>2 + 1<em>/</em>2 ∗ (1<em>.</em>166<em>/</em>2) = 0<em>.</em>791</li>

 <li><em>pr</em>(<em>C</em>) = 1<em>/</em>2 + 1<em>/</em>2 ∗ (1<em>.</em>166<em>/</em>2 + 0<em>.</em>75<em>/</em>3 + 0<em>.</em>666) = 1<em>.</em>25</li>

 <li><em>pr</em>(<em>D</em>) = 1<em>/</em>2 + 1<em>/</em>2 ∗ (0<em>.</em>75<em>/</em>3) = 0<em>.</em>625</li>

</ul>

After 5 iterations we reach convergence since the difference between the rank values in the 4th iteration and the rank values in the fifth iteration is smaller than . The ranks at the end are:

<ul>

 <li><em>pr</em>(<em>A</em>) = 1<em>.</em>270</li>

 <li><em>pr</em>(<em>B</em>) = 0<em>.</em>819</li>

 <li><em>pr</em>(<em>C</em>) = 1<em>.</em>274</li>

 <li><em>pr</em>(<em>D</em>) = 0<em>.</em>636</li>

</ul>

getResults

This method takes as input a String representing a single-word query. It then returns an ArrayList of urls that contain such word, ordered based on their rank from most relevant to least relevant. This method will be called only after both crawlAndIndex and assignPageRanks have been executed. This method should use one of the sorting algorithms from the Sorting class. Ideally, it should use fastSort(), but if you did not implement it, you can use slowSort().