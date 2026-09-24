# XPath select branch

```bash
$ xidel -s --printed-node-format="xml" --xpath "//book[year=(2004, 2005, 2013, 2020)]" books.xml
<book id="2" category="linux">
        <title lang="en">Understanding the Linux Kernel</title>
        <year>2005</year>
        <author>Daniel P. Bovet</author>
        <author>Marco Cesati</author>
</book>
<book id="3" category="novel">
        <title lang="en">A Game of Thrones</title>
        <year>2013</year>
        <author>George R. R. Martin</author>
</book>
```

[source](https://www.baeldung.com/linux/evaluate-xpath)