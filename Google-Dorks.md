# Google Dork(s) is an advanced search operator option used to identify and find specific information or values within a website.

Syntax          | Description              | Example
--------------- | ------------------------ | ------------
allintext      | Searches for occurrences of all the keywords given. | allintext:"value_here" |
intext      | Searches for the occurrences of keywords all at once or one at a time. | intext:"value_here" |
inurl      | Searches for a URL matching one of the keywords. | inurl:"value_here" |
allinurl      | Searches for a URL matching all the keywords in the query. | allinurl:"value_here" |
intitle      | Searches for occurrences of keywords in title all or one. | intitle:"value_here" |
allintitle      | Searches for occurrences of keywords all at a time. | allintitle:"value_here" |
site      | Specifically searches that particular site and lists all the results for that site. | site:"www.google.com" |
filetype      | Searches for a particular filetype mentioned in the query. | filetype:"pdf" |
link      | Searches for external links to pages. | link:"value_here" |
numrange      | Used to locate specific numbers in your searches. | numrange:321-325 |
before/after      | Used to search within a particular date range. | filetype:pdf & (before:2000-01-01 after:2001-01-01) |
allinanchor (and also inanchor)      | This shows sites which have the keyterms in links pointing to them, in order of the most links. | inanchor:rat |
allinpostauthor (and also inpostauthor)      | Exclusive to blog search, this one picks out blog posts that are written by specific individuals. | allinpostauthor:"value_here" |
related      | List web pages that are “similar” to a specified web page. | related:www.google.com |
cache      | Shows the version of the web page that Google has in its cache. | cache:www.google.com |
