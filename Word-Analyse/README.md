# Analyzing a Phishing Word Document

## Steps 

1. Analyzing with [oledump.py](oledump/oledump.py)
   
```oledump.py a59fd8453397ed25525e90cad7d294b19fcd7459e237ca0eb20d189c72656ee1.doc```

2. Analyzing with [zipdump.py](zipdump.py)

```zipdump.py -D a59fd8453397ed25525e90cad7d294b19fcd7459e237ca0eb20d189c72656ee1.doc```

> Besides the 2 PNG files, it looks like there are only XML files inside. And the timestamps are all 1980-01-01, exactly what it should be for an OOXML file created with Office. It contains a word/document.xml file, so it's very likely a .DOCX file.

3. Looking for unusal URLs with [zipdump.py](zipdump.py) and [re-search.py](re-search/re-search.py)

```zipdump.py -D a59fd8453397ed25525e90cad7d294b19fcd7459e237ca0eb20d189c72656ee1.doc | re-search.py -u -n url -F officeurls```

4. Looking for hyperlink with [zipdump.py](zipdump.py) and [xmldump.py](xmldump.py)

```zipdump.py -s 4 -d a59fd8453397ed25525e90cad7d294b19fcd7459e237ca0eb20d189c72656ee1.doc | xmldump.py pretty``` 

So there is a hyperlink so it's probably a phishing document.

5. Looking at the text with [zipdump.py](zipdump.py) and [xmldump.py](xmldump.py)
   
```zipdump.py -s 3 -d  a59fd8453397ed25525e90cad7d294b19fcd7459e237ca0eb20d189c72656ee1.doc | xmldump.py wordtext``` 


## Source

- [Article Analyzing a phishing word document](https://isc.sans.edu/forums/diary/Analyzing+a+Phishing+Word+Document/28562)on SANS ISC InfoSec Forums from [Didier Stevens](https://blog.didierstevens.com/)
- Tools from [Didier Stevens](https://blog.didierstevens.com/)
  - [re-search.py](https://blog.didierstevens.com/2022/04/23/update-re-search-py-version-0-0-19/)
  - [oledump.py](https://blog.didierstevens.com/2022/03/29/update-oledump-py-version-0-0-64/)
  - [xlmdump.py](https://blog.didierstevens.com/2021/07/04/update-xmldump-py-version-0-0-7/)
  - [zipdump.py](https://blog.didierstevens.com/2020/12/25/update-zipdump-py-version-0-0-21/)
