# Lesson 10 — Introduction to Web Scraping

## Overview

No overview provided

## Learning Objectives

- Students will gain a comprehensive understanding of web scraping, focusing on the fundamentals such as HTML structure, DOM representation, and using Python libraries like `Selenium` and `WebDriver Manager` to scrape and extract data from web pages. Additionally, students will explore the ethical aspects of web scraping, including adhering to guidelines provided by `robots.txt` and managing server requests responsibly.

## Topics Covered

- 1. Basics of HTML and DOM
- 2. Web Scraping Tool: `Selenium` and `WebDriver Manager`
- 3. Ethical Web Scraping: Understanding `robots.txt` and ethical considerations
- 4. Scraping Structured Data: Extracting specific data points
- 5. Managing Requests: Delays, retries, and handling errors
- 6. Saving Scraped Data to Files
- 7. Frailty in Scraping Programs

## Status

pending

## Assignment

Assignment for Lesson 10

### Objective

No objective specified

### Expected Capabilities

Expected capabilities will be defined as the lesson progresses.

### Instructions

Instructions will be provided when the lesson is generated.

### Tasks

#### Task 1: Task 1

# **Introduction to Web Scraping**

### **Objective**

You learn to harvest data from a live web site, scraping values from the HTML page and storing them in a CSV file.

## **Assignment Instructions**

You create the code for this assignment in the assignment10 folder within your python_homework folder.  Be sure to create an `assignment10` git branch before you start.  As usual, mark the code that completes each task with a comment line.

---

## **Overview**
This lesson introduces web scraping concepts and practices, including:
1. Understanding HTML and the DOM structure in a live web page.
2. Extracting content using Selenium.
3. Storing data in CSV and JSON files.
4. Ethical considerations in web scraping.


---

## **Tasks**

### **Task 1: Review robots.txt to Ensure Policy Compliance**

In this assignment, you collect data from the Durham County Library site.  As always, when you do web scraping, you need to review the policy described in robots.txt, to ensure that you comply.

1. Open [https://durhamcountylibrary.org/robots.txt]

2. Verify that the following steps are not in breach of policy.

### **Task 2: Understanding HTML and the DOM for the Durham Library Site**

You are going to find where in the HTML page the data you want is located.

1. Open [https://durhamcounty.bibliocommons.com/v2/search?query=learning%20spanish&searchType=smart]

2. Open your browser developer tools to show the HTML elements.  For Chrome, this is `shift-ctrl-J`.

3. Find the HTML element for a single entry in the search results list.  This is a little tricky.  When you select an element in the Chrome developer tools, that part of the web page is highlighted.  But, that typically only gets you to the main `div`.  There is a little arrow next to that div in the developer tools element window, and you click on that to open it up to show the child elements.  Then, you select the element that corresponds to the search results area.  Continue in this way, opening up divs or other containers and selecting the one that highlights the area you want.  Eventually, you'll get to the first search result.  Hint: You are looking for an `li` element, because this is an element in an unordered list.  Note the values for the class attribute of this entry.  You'll want to save these in some temporary file, as your program will need them.

3. Within that element, find the element that stores the title.  Note the tag type and the class value.  Your program will need this value too, so save it too.

4. Within the search results `li` element, find the element that stores the author.  Hint: This is a link.  Note the class value and save it.  Some books do have multiple authors, so you'll have to handle that case.

5. Within the search results `li` element, find the element that stores the format of the book and the year it was published.  Note the class value and save it.  Now in this case, the class might not be enough to find the part of the `li` element you want.  So look at the `div` element that contains the format and year.  You want to note that class value too.

### **Task 3: Write a Program to Extract this Data**

1. `get_books.py`. The program should import from selenium and webdriver_manager, as shown in your lesson.  You also need pandas and json.

2. Add code to load the web page given in task 2.

3. Find all the `li` elements in that page for the search list results.  You use the class values you stored in task 2 step 3.  Also use the tag name when you do the find, to make sure you get the right elements.

5. Within your program, create an empty list called `results`.  You are going to add `dict` values to this list, one for each search result.

6. Main loop: You iterate through the list of `li` entries.  For each, you find the entry that contains title of the book, and get the text for that entry.  Then you find the entries that contain the authors of the book, and get the text for each.  If you find more than one author, you want to join the author names with a semicolon `;` between each.  Then you find the `div` that contains the format and the year, and then you find the `span` entry within it that contains this information.  You get that text too.  You now have three pieces of text.  Create a `dict` that stores these values, with the keys being `Title`, `Author`, and `Format-Year`.  Then append that `dict` to your `results` list.

7. Create a DataFrame from this list of dicts.  Print the DataFrame.

**Hint** You can put little print statements in at each step, to see if that part works.  For example, when you find all the `li` entries, you could print out the length of the list.  Then, you could just implement the part of the main loop that finds the Title, and just print out that title.  In this way, you can get the program done incrementally.

**For Further Thought**  You are getting the search results from the first page of the search results list.  How would you get all the search results from all the pages?  How can you make the program do this regardless of how many pages you might have?  **Optional:** Change your program to page through the search results so as to get all of the results.  However! You need to make sure your program pauses between pages.  Fast screen scraping, where many requests are sent in short order, is an abuse of the privilege.

### **Task 4: Write out the Data**
Modify your program to do the following:

1. Write the DataFrame to a file called `get_books.csv`, within the assignment10 folder.  Examine the file to see if it looks right.

2. Write the `results` list out to a file called `get_books.json`, also within the assignment10 folder.  You should write it out in JSON format.  Examine the file to see if it looks right.

### **Task 5: Ethical Web Scraping**

**Goal**:  
Understand the importance of ethical web scraping and `robots.txt` files.

1. Access the `robots.txt` file for Wikipedia: [Wikipedia Robots.txt](https://en.wikipedia.org/robots.txt).
2. Analyze the file and answer the following questions.  Put your answers in a file called `ethical_scraping.txt` in your python_homework/assignment10 directory
   - Which sections of the website are restricted for crawling?
   - Are there specific rules for certain user agents?
3. Reflect on why websites use `robots.txt` and write 2–3 sentences explaining its purpose and how it promotes ethical scraping.  Put these in `ethical_scraping.txt` in your python_homework directory.


---

### **Task 6: Scraping Structured Data**

**Goal**:  
Extract a web page section and store the information.

1. Use your browser developer tools to view this page: [https://owasp.org/www-project-top-ten/].  You are going to extract the top 10 security risks reported there.  Figure out how you will find them.

2. Within your python_homework/assignment10 directory, write a script called `owasp_top_10.py`.  Use selenium to read this page.

3. Find each of the top 10 vulnerabilities.  Hint: You will need XPath.  For each of the top 10 vulnerabilites, keep the vulnerability title and the href link in a dict.  Accumulate these dict objects in a list.

4. Print out the list to make sure you have the right data.  Then, add code to the program to write it to a file called `owasp_top_10.csv`.  Verify that this file appears correct.

5. Create a file, `challenges.txt`, also within your lesson9 directory.  In this file, describe any challenges you faced in completing this assignment and how you resolved them.

---


### Submit Your Assignment on GitHub**  

📌 **Follow these steps to submit your work:**  

#### **1️⃣ Add, Commit, and Push Your Changes**  
- Within your python_homework folder, do a git add and a git commit for the files you have created, so that they are added to the `assignment10` branch.
- Push that branch to GitHub. 

#### **2️⃣ Create a Pull Request**  
- Log on to your GitHub account.
- Open your `python_homework` repository.
- Select your `assignment10` branch.  It should be one or several commits ahead of your main branch.
- Create a pull request.

#### **3️⃣ Submit Your GitHub Link**  
- Your browser now has the link to your pull request.  Copy that link. 
- Paste the URL into the **assignment submission form**. 

---

## **Resources**

- [Selenium Documentation](https://www.selenium.dev/documentation/webdriver/)
- [MDN Web Docs: Understanding the DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)
- [OWASP robots.txt](https://owasp.org/robots.txt)

---  


```

```

### Submission Instructions

Please submit on time

### Checklist

Checklist will be provided when the lesson is generated.

### Check for Understanding

Understanding checks will be provided when the lesson is generated.

## Subsections

### Lesson 10


# **Lesson 10 — Introduction to Web Scraping**

## **Lesson Overview**
**Learning objective:** Students will gain a comprehensive understanding of web scraping, focusing on the fundamentals such as HTML structure, DOM representation, and using Python libraries like `Selenium` and `WebDriver Manager` to scrape and extract data from web pages. Additionally, students will explore the ethical aspects of web scraping, including adhering to guidelines provided by `robots.txt` and managing server requests responsibly.

### **Topics:**
1. Basics of HTML and DOM
2. Web Scraping Tool: `Selenium` and `WebDriver Manager`
3. Ethical Web Scraping: Understanding `robots.txt` and ethical considerations
4. Scraping Structured Data: Extracting specific data points
5. Managing Requests: Delays, retries, and handling errors
6. Saving Scraped Data to Files
7. Frailty in Scraping Programs

**Why Do Web Scraping?**

There is a lot of information on the Internet, as you know, but it is in web pages that are provided so that humans can read them.  If you want to automate the process of searching or archiving some of this information, you need to extract it into a structured format and store it separately, so that you can then do SQL searches or the like on what you save.

Here are some examples:

- Finding the prices of airline flights to a given destination for multiple airlines.
- Finding all scholarly articles on a particular topic you want to research and saving this information for reference.
- Finding the schedule of public meetings for local government bodies.

---

## **9.1 Basics of HTML and DOM**

### **Overview**
HTML (Hypertext Markup Language) is the backbone of web pages, providing structure and content. The Document Object Model (DOM) is a tree structure that represents the page content. Understanding the structure of web pages and the DOM is essential for locating and extracting data during web scraping.  When you pull up a web page in your browser, a request is sent to a web server and an HTML document is returned.  Your browser then parses that document and presents the page.  When you do web scraping, you'll also parse that page, not for presentation, but to capture information from that page so that it can be stored in a structured way.  You need to understand HTML and the DOM structure to do screen scraping.  Many of you may already be familiar with HTML -- if so, skip ahead.

### Elements of an HTML Document

Each element of the DOM has the following:
- A tag, the name for the type of element.
- Attributes.  These are name-value pairs, and vary with the element type.  For example, a `class` attribute might describe the display style for the element.  For a link element, the `href` attribute describes web address to use for the link.  There are many others.
- Content.  This may be text, or it may be other elements.  As the DOM is a tree, some elements contain others.

### **Key HTML Elements:**
- **`<title>`**: The title of the page.
- **`<p>`**: Paragraphs of text.
- **`<h1>, <h2>, <h3>`**: Headers of varying levels.
- **`<a>`**: Links with `href` attributes pointing to URLs.
- **`<img>`**: Images with `src` attributes indicating the image source.

There are many others.

### For Further Reference

A good online refernce to HTML is available at [W3Schools](https://www.w3schools.com/html/).

### **Hands-On Activity:**

1. Open the Wikipedia page for "Web Scraping" ([Wikipedia - Web Scraping](https://en.wikipedia.org/wiki/Web_scraping)).
2. Open the developer tools for your browser.  For Chrome this is `Shift-Ctrl-J`.  Inspect the elements of the page.  In the Chrome developer tools, they are in the `Elements` tab. 
3. Traverse this collection of elements to:
   - Identify the title of the page.
   - Locate the first paragraph and examine its structure.
   - Explore headers (`<h1>, <h2>, <h3>`) and links (`<a>`).

When you are creating a web scraping program, this is often the first step.  Look at the page you want to scrape in the browser developer tools and find where the information you want resides within the DOM, so that you can write code to extract it.

### **How the DOM Is Structured:**
The DOM is a hierarchical tree structure. Here's an example:
```html
<html>
  <head>
    <title>Web Scraping</title>
  </head>
  <body>
    <h1>Introduction</h1>
    <p>This is an example paragraph.</p>
    <a href="https://example.com">Example Link</a>
  </body>
</html>
```

---

## **9.2 Web Scraping Tools: Selenium and WebDriver Manager**

### **Overview and Setup**

To scrape data from a web page, two primary libraries are commonly used in Python:
- **`Selenium`**: A library that executes the same actions as a web browser, and makes the resulting page available for subsequent operations.
- **`WebDriver Manager`**: Selenium requires a driver, which performs the actual web operations, just as a browser would.  This library makes the appropriate driver available to your program in an automated way.

You need to install these into your python_homework directory.  Within your VSCode terminal session for `python_homework` do:

```bash
pip install selenium
pip install webdriver-manager
```

### **Steps to Web Scraping:**
1. Initialize Selenium and the appropriate driver.  We'll use the Chromium driver, which is the same one as is in Chrome and other browsers.
2. Retrieve a web page.
3. Extract the desired elements using CSS selectors.

This is the initialization you'll need to do:

```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service as ChromeService
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.common.by import By

driver = webdriver.Chrome(service=ChromeService(ChromeDriverManager().install()))

```

Once you have a driver, you can fetch a web page, as follows:

```python
driver.get("https://en.wikipedia.org/wiki/Web_scraping")
```

### **Explanation: Why do we Need So Much Machinery?**

This may seem a pretty heavy collection of stuff just to scrape a web page.  However, most web pages these days are dynamic.  They contain JavaScript, and after the page loads, the scripts run to populate the page.  So, we need an engine that will not only get the page, but also run the JavaScript, and the JavaScript may itself make Ajax or Fetch calls to get more data.  A lot happens to create the appearance of the page you see.

Try the code above in your Python interative shell.  You'll see something a little odd.  A window will flash up with the actual page we are trying to scrape.  This can be interesting or annoying, depending on which side of the bed you got up on.  You can configure your driver to run in 'headless' mode, without a window, when you create the driver:

```python
options = webdriver.ChromeOptions()
options.add_argument('--headless')  # Enable headless mode
options.add_argument('--disable-gpu')  # Optional, recommended for Windows
options.add_argument('--window-size=1920x1080')  # Optional, set window size

driver = webdriver.Chrome(service=ChromeService(ChromeDriverManager().install()),options=options)

```

### **Finding Information**

A web page is comprised of HTML elements.  You can find elements within the page, and the most flexible way to find them is by CSS selector.  If you have done web page styling, you have used CSS selectors to specify which elements should have a particular style: font, color, background color, border, etc.  Selectors have various criteria.  Here are some examples:

```
Select by element name:

'p' : select all paragraphs
'h2' : select all h2 headings

Select by element class:

'.this-style-class' : All elements that have a class of this-style-class.  The . means select by class

Select by attribute:

'[src]' : All elements that have a value for the src attribute, such as img elements.
'[data-event="meeting"]' : All elements that have a value for the data-event attribute equal to "meeting".

There are others.  There are also combined selectors:

'div.main-container' : All div elements that have a class of main-container.
```

CSS selectors can be as complicated as need be, but typically you do not want to do complicated selection when web scraping, as this will make your scraping program frail.  If you want a full tutorial on CSS selectors, go here: [https://www.w3schools.com/css/css_selectors.asp]

Here are some examples.  Try them out in your Python interative shell (assuming you have already loaded the web page into your driver as shown above):

```python
from selenium.webdriver.common.by import By

title = driver.title # Find the title.  Parts of the header are accessed directly, not via find_element(), which only works on the body
print(title)

body = driver.find_element(By.CSS_SELECTOR,'body') # Find the first body element, typically only one
if body:
    links = body.find_elements(By.CSS_SELECTOR,'a') # Find all the links in the body.
    if len(links) > 0:
        print("href: ", links[0].get_attribute('href'))  # getting the value of an attribute



main_div = body.find_element(By.CSS_SELECTOR,'div[id="mw-content-text"]')
if main_div:
    bolds = main_div.find_elements(By.CSS_SELECTOR,'b')
    if len(bolds) > 0:
        print("bolds: ",bolds[0].text)

# Extract all images with their src attributes
images = [(img.get_attribute('src')) for img in body.find_elements(By.CSS_SELECTOR,'img[src]')] # all img elements with a src attribute
print("Image Sources:", images)
# hmm, this example uses a list comprehension.  We haven't talked about those.  This is the same as:
image_entries = driver.find_elements(By.CSS_SELECTOR,'img[src]')
images = []
for img in image_entries:
    images.append(img.get_attribute('src'))

print("Image Sources:", images)
# You can see that list comprehensions are a useful shortcut in Python!
```

Once you get an element, you can do the following (this is not an exhaustive list):

- Get the text value, if any.
- Get the value of any attributes.
- Search the descendants.

You can then close the browser connection with:

```python
driver.quit()
```

The `driver.get()` method can raise an exception.  It's a good idea to do it in a try block:

```python
try:
    driver.get("https://nonsense.never.com")
except Exception as e:
    print("couldn't get the web page")
    print(f"Exception: {type(e).__name__} {e}")
finally:
    driver.quit()
```

**Note:** Selenium is not used only for web scraping.  It can automate interaction with a browser page. One common use is to do end-to-end testing.  You can type into the fields of forms, you can click on submit buttons, you can refresh the page, you can hit the back button, and so on.  We won't do any of this for this lesson.

---

## **9.3 Ethical Web Scraping**

### **Overview**
While web scraping can be a powerful tool, it is important to follow ethical guidelines and respect website owners’ wishes to avoid excessive server load and legal issues.

### **Key Concepts:**
- **What is `robots.txt`?**
  - A file that specifies which sections of a website can or cannot be accessed by web crawlers.
- **Why is `robots.txt` important?**
  - It helps website owners control the traffic to their site and avoid server overload.
  - Ethical scraping involves reviewing and adhering to the rules set in `robots.txt`.

### **Activity: Explore `robots.txt` for Wikipedia**
1. Access the `robots.txt` file for Wikipedia: [Wikipedia Robots.txt](https://en.wikipedia.org/robots.txt).
2. Identify restricted sections of the site.
3. Discuss why these sections are restricted.

### **Example Code: Accessing `robots.txt`**
```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service as ChromeService
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.common.by import By

driver = webdriver.Chrome(service=ChromeService(ChromeDriverManager().install()))
robots_url = "https://en.wikipedia.org/robots.txt"
driver.get(robots_url)
print(driver.page_source)
driver.quit()

```

---

## **9.4 XPath to Traverse the DOM**

### **Overview**
After scraping basic data, you can refine your scraping strategy to focus on specific sections of a webpage.  Sometimes, though, the find by CSS selector approach does not suffice.  Have a look at the [Wikipedia Web Scraping page.](https://en.wikipedia.org/wiki/Web_scraping) Somewhere near the bottom, you see the `See also` section.  Suppose you want to scrape each of the links in that section.  You first open up the developer tools in your browser to see how you find the section.  Open up the elements tab and do a ctrl-f to find "See also".  The second hit gets you pretty close.  This is an `h2` element.  If you scroll down a little bit, you see a `div` further down in the page, and that div has the list of links you want.  But (sigh) there are no good identifiers like class or id or attribute to find this div.  So you go back to that h2 with "See also".  That h2 has the id of "See_also".  This helps some.  What you want to do is go up to the parent div, the one that contains that h2, call it parent_div.  Then you get the div that is the next div sibling of parent_div.  That's the one you want.

It is clear that finding by CSS selector won't work in this case.  You have to use another technique, called XPath.  There is an XPath tutorial [here.](https://www.w3schools.com/xml/xpath_intro.asp) We won't need most of XPath, but we do need to know the XPath axes, specifically parent and sibling.  Here's the code:

```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service as ChromeService
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.common.by import By

driver = webdriver.Chrome(service=ChromeService(ChromeDriverManager().install()))
driver.get("https://en.wikipedia.org/wiki/Web_scraping")  # this much you've seen before

see_also_h2 = driver.find_element(By.CSS_SELECTOR,'[id="See_also"]') # our starting point
links = []
if (see_also_h2):
    parent_div = see_also_h2.find_element(By.XPATH, '..') # up to the parent div
    if parent_div:
        see_also_div = parent_div.find_element(By.XPATH,'following-sibling::div' ) # over to the div with all the links
        link_elements = see_also_div.find_elements(By.CSS_SELECTOR, 'a')
        for link in link_elements:
            print(f"{link.text}: {link.get_attribute('href')}")
            name = link.text.strip()
            url = link.get_attribute("href")
            if name and url:
                links.append({"name": name, "url": url})


driver.quit()
```

### **Testing on Another Page:**

Test the script on different Wikipedia pages to ensure consistency and robustness.

---

## **9.5 Managing Requests and Handling Errors**

### **Overview**
When scraping large numbers of web pages, managing requests responsibly is essential. Techniques include delaying requests and handling connection errors.  

- The `driver.get()` operation may raise an exception. Sometimes this is a timeout.  Or perhaps the network might be down.  It may not help to retry the request in this case.
- The `driver.get()` operation may return an HTTP response code like 404 or 500.  Selenium does *not* raise an exception in this case.  Unfortunately, there is no easy way to access the HTTP response code in Selenium.  You can check if driver.title is the string you expect.
- You can do a subsequent driver.get() to scrape another page, but if you do, you want to pause between pages.  It is an abuse to drive excessive load by many rapid requests.
    ```python
    from time import sleep
    try:
        driver.get('https://acme.com/index.html')
        ... # extract data
        sleep(2) # wait 2 seconds
        driver.get('https://acme.com/another.html')
    except Exception as e:
        print(f"An exception occurred: {type(e).__name__} {e}")
    finally:
        driver.quit()

    ```
---

## **9.6 Saving Scraped Data**

### **Overview**
Once you've scraped valuable data, you may want to save it in a structured format, such as CSV or JSON.

### **Saving Data to CSV:**
```python
import csv

# Save extracted data to a CSV file
with open('scraped_data.csv', 'w', newline='') as file:
    writer = csv.writer(file)
    writer.writerow(["Name", "Link"])
    for link in links:
        writer.writerow([link["name"], link["url"]])
```

### **Saving Data to JSON:**
```python
import json

# Save data to a JSON file
data = {"links": links}
with open('scraped_data.json', 'w') as json_file:
    json.dump(data, json_file, indent=4)
```

### **Saving Data to an SQL Database**

Suppose you are scraping from multiple sites.  You may want to record different information from each site, and keep track of which site provided which information.  

For example, you may scrape airline sites for destinations, prices, and departure times.  You could create three tables, one for airlines, which would record the airline name and URL, and then three others for destinations, prices, and departure_times.  There would be a many-to-many relationship between airlines and destinations, which might have where_we_fly as a join table.  There would be a one-to-many relationship between where_we_fly entries and departure_times, and a one-to-many relationship between departure_times and prices (for economy, business, and first class). This is a little more complicated, to be sure -- but think about your data model when you get ready to store web scraping data!

## **9.7 Frailty in Web Scraping**

Web scraping programs can be frail.  The authors of the websites that you are accessing to scrape data can change the format of the page.  This can break the scraping logic, as the DOM may no longer be organized as you expect, or because the entries have different classes or ids.  Sometimes you can make your scraping more robust by finding known strings within the formatted page, and traversing from that point, but sometimes you can only log the error so as to trigger work on a fix.

---

## **Summary**

In this lesson, you learned:
1. How to understand the structure of web pages using HTML and the DOM.
2. How to use Python libraries `Selenium` and `WebDriver Manager` for web scraping.
3. Ethical considerations of web scraping, including respecting `robots.txt`.
4. Techniques for extracting specific data, handling errors, and managing requests.
5. How to save scraped data to CSV and JSON formats for future use.

### **Important Notes:**
- Always respect the website’s `robots.txt` file and terms of service.
- Avoid overloading a server with excessive scraping requests.
- Use appropriate delay and retry mechanisms to manage web traffic.

For further learning, explore the [Selenium Documentation](https://www.selenium.dev/documentation/webdriver/).


**Video URL:** No video available

**Code Examples:**

No code examples available

**External Links:**

No external links available

**Quizzes:**

No quizzes available

## Supplemental Videos

No supplemental videos available

## References

No references available

## Podcast URL

No podcast available