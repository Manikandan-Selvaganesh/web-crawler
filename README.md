Web crawler is portion of search engine. The web crawler designed here
scans web pages looking for links. The web crawler is restricted to follow
and give links only of that particular domain. This web crawler outputs
a sitemap which has all the links of the given domain

Usage
=====
1) go run crawl.go <domain>
        Extract the golang.org/x/net/html to src folder if it is not automatically
        being pulled.
        crawl1.go - Extracts every URL(following up domains) from the domain
        crawl.go  - Limited to given domain(as mentioned in the task)
2) ./crawl <domain>

crawl -h: Help or shows the usage

Design
======
1) Read the start page of web page on which crawling should happen as a command
line argument.
2) In go http package which is available in the standard library helps us get
the http body and scans the links further.
3) Parsing hyperlinks can be done using regular expressions, since the www is
a lot of mess, we are using the standard http.Get which will parse the page and
return us slice of all the href links found.
4) The things will work fine if it is http and we need to take care of https,
the secured sites. Disabling SSL to perform the crawling.
5) The key thing to note is we need to store the links or already visited links
in a queue, otherwise we will end up exhausting all the resources across the
web. To achieve this, Go provides us with great alternative : channel. This is
a lightweight thread that functions much like a queue. In the program, we will
create a channel and whenever an URL is found, we will write into the channel.
All the relative links will be changed into absolute links using fixurl()
function.
6) What if the webpage points itself? There will be a loop, so we need to take
care of already visited pages. Making use of a map to store these details.

Testing
=======
Testing should be done considering the following points:
1) Validate the URL
        a. Check if its a valid URL. Validate the input
        b. Check if the site shows proper body or 'Page not found'
2) Validate the sitemap
        a. Check random URL's and see if it is a valid URL
        b. Count the number of URL's and check it.
        c. Validate against lot of loops in URL's
        d. Create a webpage with lot of special characters and check if
           extraction happens properly
        e. Export it to a sheet or database, run a query to check duplicate
           URL's.
        f. Check if it reaches other domains by running a script
        g. run against https site and http site and observe for any differences

More test cases will be uploaded.

While running the script, the exit condition is not specified, since it involves
regex, and I do not want to write a regex and spoil the code, I have not given the
exit condition, however in Python it has an exit condition. Since Go has lot
of concurrency, this is faster.

