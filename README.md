Perfect 👍 Let’s go step by step and explain **everything** from above clearly, like a mini tutorial.

---

# 🟢 Step-by-Step Explanation of the News Headlines Web Scraper

---

## **Step 1: Install Required Packages**

Before writing the code, we need two external Python libraries:

* `requests` → To send an HTTP GET request and download the HTML page.
* `beautifulsoup4` → To parse the HTML and extract information.

Install them using:

```bash
pip install requests beautifulsoup4
```

This tells Python’s package manager (`pip`) to fetch these libraries from the Python Package Index (PyPI).

---

## **Step 2: Import Libraries**

```python
import requests
from bs4 import BeautifulSoup
```

* `requests` helps us get web pages.
* `BeautifulSoup` helps us understand the structure of the webpage (HTML) and find elements like `<h2>`.

---

## **Step 3: Define the Website URL**

```python
URL = "https://www.bbc.com/news"
```

Here, we set the target site. You can replace it with **any public news site** (NDTV, Reuters, etc.).

---

## **Step 4: Send an HTTP GET Request**

```python
headers = {"User-Agent": "Mozilla/5.0"}  
response = requests.get(URL, headers=headers)
```

* `requests.get()` fetches the page.
* `headers` contains a **User-Agent** string that makes our request look like it’s coming from a real web browser (otherwise some sites block bots).

---

## **Step 5: Check the Response Status**

```python
if response.status_code == 200:
```

* `200` means **Success**.
* If it’s `404` → page not found, `500` → server error.
  This check ensures we only continue if the site loaded correctly.

---

## **Step 6: Parse HTML with BeautifulSoup**

```python
soup = BeautifulSoup(response.text, "html.parser")
```

* `response.text` → contains raw HTML from the website.
* `"html.parser"` → built-in parser that converts HTML into a tree-like structure, so we can search for tags easily.

---

## **Step 7: Find Headlines**

```python
headlines = soup.find_all("h2")
```

* `.find_all("h2")` → searches all `<h2>` tags.
* On many news sites, **headlines are inside `<h2>` tags**.

---

## **Step 8: Clean Extracted Text**

```python
news_list = [h.text.strip() for h in headlines if h.text.strip()]
```

* `.text` → gets the actual text inside the tag (removes HTML).
* `.strip()` → removes unwanted spaces or newline characters.
* List comprehension collects only non-empty results.

---

## **Step 9: Save Headlines into a File**

```python
with open("headlines.txt", "w", encoding="utf-8") as f:
    for idx, headline in enumerate(news_list, start=1):
        f.write(f"{idx}. {headline}\n")
```

* `open("headlines.txt", "w")` → creates a new text file in **write mode**.
* `enumerate(..., start=1)` → adds numbering to headlines.
* Each headline is written into the file on a new line.

---

## **Step 10: Success or Failure Message**

```python
print(" Headlines scraped and saved to headlines.txt")
```

* If successful → prints confirmation.
* Else → shows an error message with the status .
