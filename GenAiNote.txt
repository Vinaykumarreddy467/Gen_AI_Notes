================================================================================
                         GEN AI STUDY NOTES
================================================================================

================================================================================
1. TEMPERATURE
================================================================================

Temperature (high and low): controls the creativity / randomness of the model.
  - High temperature  (0.8 - 1.0) -> more creative / random outputs
  - Low temperature   (0.0 - 0.3) -> more deterministic / focused outputs
  - Medium temperature (0.4 - 0.7) -> balanced between creativity and focus

Other sampling parameters:
  - Top-p (nucleus sampling): considers only tokens whose cumulative probability
    reaches p (e.g. top_p=0.9 means only the top 90% likely tokens are considered)
  - Top-k: limits the model to the k most likely next tokens
  - Top-p and temperature are often used together for finer control

================================================================================
2. PROMPT ENGINEERING
================================================================================

Prompts are the detailed instructions given to the models so that they can
understand what is expected.

Core Elements of Prompt Engineering:
  ~ Role / Persona      : who is using the model
  ~ Context / Background: the scenario
  ~ Task / Instructions : what to do
  ~ Format / Output     : expected response structure (JSON, markdown, etc.)
  ~ Constraints         : limits or rules (e.g. "200 words max", "no bullet points")

Types of Prompt Engineering:
  1. Zero-shot           : asking without any example
  2. Few-shot            : ask the model with examples (typically 2-5 examples)
  3. Chain-of-Thought    : step-by-step reasoning to achieve the desired output
                           (e.g. DeepSeek thinking, OpenAI o1)
  4. System Prompting vs User Prompting
  5. Role Prompting      : assigning a specific persona (e.g. "You are a senior
                           Python developer...")
  6. Tree-of-Thoughts    : explores multiple reasoning paths simultaneously and
                           evaluates them before choosing the best one
  7. ReAct (Reason + Act): interleaves reasoning steps with actions (tool calls)
                           to gather information before answering
  8. Iterative Prompting : refining prompts based on model responses

Prompt Engineering Best Practices:
  - Be specific and detailed
  - Break complex tasks into steps
  - Provide examples when possible
  - Use delimiters (""", ---, etc.) to separate instructions from input
  - Ask the model to think step-by-step for reasoning tasks
  - Specify the desired output format explicitly

================================================================================
3. EXPLICIT vs IMPLICIT PROGRAMMING
================================================================================

Explicit programming:
  The programmer needs to specify everything while programming (e.g. data types).
  Examples: Java, C, C++

Implicit programming:
  No need to specify data types; the interpreter recognizes types automatically.
  Examples: Python

Python was developed by Guido van Rossum.
Data structures: string, list, tuple

================================================================================
4. PYTHON PRACTICE QUESTIONS
================================================================================

# ==============================================================================
#                      PYTHON PRACTICE QUESTIONS — ANSWERS
# ==============================================================================
# ponytail: one-liners, stdlib only, no over-engineering

# --- SETS ANSWERS ---
# 1.  Create a set with values 10, 20, 30, 40.
s = {10, 20, 30, 40}  # {} literal, no set() needed
# 2.  Print all elements.
print(s)              # ponytail: print repr is fine for learning
# 3.  Add 50.
s.add(50)
# 4.  Remove 20.
s.remove(20)          # raises KeyError if missing; use discard() to ignore missing
# 5.  Length.
len(s)
# 6.  Check if 30 exists.
30 in s               # True / False
# 7.  Union of two sets.
s1 | s2               # or s1.union(s2)
# 8.  Intersection.
s1 & s2               # or s1.intersection(s2)
# 9.  Difference.
s1 - s2               # or s1.difference(s2) — items in s1 not in s2
# 10. Symmetric difference.
s1 ^ s2               # or s1.symmetric_difference(s2) — items in either, not both
# 11. Clear all.
s.clear()
# 12. Copy.
s2 = s1.copy()        # shallow copy
# 13. Convert list with duplicates to set.
set([1, 2, 2, 3])     # -> {1, 2, 3}; duplicates gone
# 14. Max value.
max(s)
# 15. Min value.
min(s)
# 16. Vowel check.
vowels = {'a','e','i','o','u'}; ch.lower() in vowels
# 17. Remove duplicates from list.
list(set([1, 2, 2, 3]))  # -> [1, 2, 3]; order not preserved
# 18. Count unique elements in a list.
len(set([1, 2, 2, 3]))   # -> 3
# 19. Check subset.
s1 <= s2 or s1.issubset(s2)
# 20. Check disjoint (no common elements).
s1.isdisjoint(s2)

# --- DICTIONARY ANSWERS ---
# 21. Create student dict.
student = {"name": "Alice", "age": 22}
# 22. Print all keys.
list(student.keys())  # or: for k in student: print(k)
# 23. Print all values.
list(student.values())
# 24. Access value by key.
student["name"]       # raises KeyError if missing; student.get("name") returns None
# 25. Add new key-value.
student["grade"] = "A"
# 26. Update existing key.
student["age"] = 23
# 27. Remove using pop().
age = student.pop("age")  # returns the value, raises KeyError if missing
# 28. Remove last inserted.
student.popitem()         # returns (key, value); Python 3.7+ order guaranteed
# 29. Check key exists.
"name" in student
# 30. Length.
len(student)
# 31. Loop all key-value pairs.
for k, v in student.items(): print(k, v)
# 32. Dict from two lists.
dict(zip(["name", "age"], ["Alice", 22]))
# 33. Get keys.
student.keys()        # dict_keys view, use list() to cast
# 34. Get values.
student.values()
# 35. Get items.
student.items()       # dict_items of (key, value) tuples
# 36. Nested dict.
students = {"s1": {"name": "A", "age": 20}, "s2": {"name": "B", "age": 21}}
# 37. Max value in dict.
max(d.values())
# 38. Min value in dict.
min(d.values())
# 39. Merge two dicts.
{**d1, **d2}          # Python 3.5+; d1.update(d2) modifies in-place
# 40. Char frequency in string.
from collections import Counter; Counter("hello")  # Counter({'l': 2, 'h': 1, 'e': 1, 'o': 1})
# ponytail: Counter is stdlib, one-liner, no custom loop needed

# --- IF-ELSE ANSWERS ---
# 41. Positive or negative.
"positive" if n > 0 else "negative"
# 42. Even or odd.
"even" if n % 2 == 0 else "odd"
# 43. Greater of two.
max(a, b)
# 44. Largest of three.
max(a, b, c)
# 45. Vote eligibility (18+).
"eligible" if age >= 18 else "not eligible"
# 46. Divisible by 5.
n % 5 == 0
# 47. Leap year.
(year % 4 == 0 and year % 100 != 0) or year % 400 == 0
# 48. Vowel or consonant.
"vowel" if ch.lower() in "aeiou" else "consonant"
# 49. Pass (marks >= 40).
"pass" if marks >= 40 else "fail"
# 50. Multiple of 3 and 5.
n % 3 == 0 and n % 5 == 0
# 51. Single/double/multi-digit.
"single" if -9 <= n <= 9 else "double" if -99 <= n <= 99 else "multi"
# ponytail: handles negatives; len(str(abs(n))) for digit-count-only
# 52. Positive, negative, or zero.
"positive" if n > 0 else "negative" if n < 0 else "zero"
# 53. Bonus: >50K -> 10%, else 5%.
bonus = salary * (0.1 if salary > 50000 else 0.05)
# 54. Uppercase or lowercase.
"upper" if ch.isupper() else "lower"
# 55. Between 1 and 100.
1 <= n <= 100          # Python chained comparison
# 56. Smallest of three.
min(a, b, c)
# 57. Senior citizen discount (60+).
"eligible" if age >= 60 else "not eligible"
# 58. Grade: 90+ A, 75-89 B, 50-74 C, <50 Fail.
"A" if marks >= 90 else "B" if marks >= 75 else "C" if marks >= 50 else "Fail"
# 59. Divisible by 2 and 3 (i.e. 6).
n % 2 == 0 and n % 3 == 0
# 60. Simple calculator.
ops = {"+": lambda a,b:a+b, "-": lambda a,b:a-b, "*": lambda a,b:a*b, "/": lambda a,b:a/b}
ops[op](a, b)          # ponytail: dict dispatch over if-elif chain, no eval

# --- INTERVIEW REVISION — ONE-LINE ANSWERS ---

# Sets:
# remove() vs discard(): remove() raises KeyError if missing, discard() silently does nothing.
# No duplicates: set uses hash table — duplicate hash = same slot, cannot store two identical items.
# Unordered: hash table doesn't preserve insertion order (Python <3.7); elements stored by hash, not position.
# union() vs update(): union() returns new set, update() adds items in-place (modifies original).
# difference() vs symmetric_difference(): difference = items in A not in B; symmetric = items in A or B but not both.

# Dictionaries:
# Keys unique: hash table — each key maps to exactly one value; second write overwrites the first.
# List as key? No — lists are unhashable (mutable); only immutable types (str, int, tuple) can be keys.
# get() vs dict[key]: get() returns None (or default) on missing key; dict[key] raises KeyError.
# pop() vs del: pop() returns the removed value; del just deletes (no return).
# Nested dict: a dict whose values are themselves dicts, e.g. {"s1": {"name": "A"}, "s2": {"name": "B"}}.

# If-Else:
# if vs if-else vs if-elif-else: if = one check; if-else = two branches; if-elif-else = many branches, first True wins.
# Multiple True conditions in elif chain: only the FIRST matching block runs; rest are skipped.
# == vs =: == compares values; = assigns a value to a variable.
# and / or / not: and = both True; or = at least one True; not = flips True/False.
# Nested if: when a condition only makes sense inside another condition (e.g. check age >= 18 before checking license).

================================================================================
5. PYTHON ESSENTIALS (Java Dev Edition)
================================================================================
# ponytail: Java→Python survival guide — one-liners, stdlib, no fluff

--- f-strings (vs Java String.format / concat) ---

name, age = "Alice", 30
f"Hello {name}, you are {age}"       # -> "Hello Alice, you are 30"
f"{2.5 * 2:.2f}"                      # -> "5.00" — format specifiers inline
# ponytail: f-strings are faster and cleaner than .format() or + concat
# Java: String.format("Hello %s", name) or "Hello " + name

--- List comprehensions (vs Java for-loop + add) ---

[x * 2 for x in range(10) if x % 2 == 0]  # -> [0, 4, 8, 12, 16]
# Java equivalent would be: loop, if-check, list.add() — 3+ lines
# ponytail: dict/set comprehensions too: {k: v for ...}, {x for x in ...}

--- Slicing (no Java equivalent) ---

lst = [0, 1, 2, 3, 4, 5]
lst[1:4]     # -> [1, 2, 3]       (start:end, exclusive end)
lst[:3]      # -> [0, 1, 2]        (start defaults to 0)
lst[::2]     # -> [0, 2, 4]        (step)
lst[::-1]    # -> [5, 4, 3, 2, 1, 0]  (reverse — no Java one-liner)
# Works on strings too: "hello"[::-1] -> "olleh"

--- Truthiness & None (vs Java null) ---

# Python: these are ALL falsy: None, False, 0, 0.0, "", [], {}, ()
# Everything else is truthy
if x:           # NOT "if x is not None and x is not empty"
    pass

x = None
x is None       # correct way to check None (not x == None)
# Java: null check is explicit; Python's truthiness handles 0/empty too

--- Mutable vs Immutable (common bug source for Java devs) ---

# IMMUTABLE (any change creates a new object):
#   int, float, str, tuple, bool

# MUTABLE (change in-place):
#   list, dict, set, bytearray

a = [1, 2, 3]
b = a           # b is a REFERENCE, not a copy
b.append(4)     # a is now [1, 2, 3, 4] too! — Java devs expect this, but easy to forget

b = a.copy()    # shallow copy — use .copy() or list(a) or a[:]
# ponytail: deepcopy(a) only when nested mutables, not needed for flat lists

--- *args and **kwargs (vs Java varargs) ---

def f(*args, **kwargs):
    print(args)    # tuple of positional args
    print(kwargs)  # dict of keyword args

f(1, 2, x=3, y=4)
# -> (1, 2)
# -> {'x': 3, 'y': 4}
# Java: void f(int... args) — positional only, no keyword equivalent

--- with statement - context manager (vs Java try-with-resources) ---

with open("file.txt") as f:
    content = f.read()   # file auto-closes after block, no finally needed
# Java: try (BufferedReader r = new BufferedReader(...)) { ... }

# Custom context manager in one line:
from contextlib import contextmanager
@contextmanager
def tag(name): print(f"<{name}>"); yield; print(f"</{name}>")
# ponytail: yield splits enter/exit; no __enter__/__exit__ boilerplate

--- self, __init__, __str__ (vs Java this, constructor, toString) ---

class Dog:
    def __init__(self, name):    # constructor
        self.name = name         # self = Java's "this", but EXPLICIT
    def __str__(self):           # toString()
        return f"Dog({self.name})"
    def __repr__(self):          # debug representation
        return self.__str__()

# ponytail: __init__ is NOT a constructor (object exists before __init__ runs)
# but conceptually it's the same for daily use

--- if __name__ == "__main__": (entry point) ---

# Python has no fixed main() like Java — every file can be run directly
# This idiom lets a file be BOTH a reusable module AND a runnable script:
def main():
    print("Running directly")

if __name__ == "__main__":
    main()

# Java: public static void main(String[] args)
# Python: __name__ == "__main__" when file is executed, not imported

--- Type Hints (optional, vs Java's mandatory types) ---

def add(x: int, y: int) -> int:   # hint: returns int
    return x + y

# Python does NOT enforce types at runtime — these are hints only
# Java: public int add(int x, int y) — compiler enforces it
# ponytail: add when code leaves a notebook; not needed for quick scripts
# Check with: mypy file.py

--- enumerate() / zip() (common iteration helpers) ---

for i, val in enumerate(["a", "b", "c"]):  # -> (0, 'a'), (1, 'b'), (2, 'c')
    print(i, val)

for a, b in zip([1, 2], ["x", "y"]):       # -> (1, 'x'), (2, 'y')
    print(a, b)

# Java: traditional index loop or Stream API + IntStream
# ponytail: enumerate/zip are simpler than Java's Indexed / zip-with-stream

--- import system (vs Java) ---

# Python:
from os.path import join, exists    # import specific names
import os                            # import module, use os.path.join()
# Java: import java.io.File; — similar, but Python uses filesystem paths

# Python has NO package-private / public — naming convention only:
_private_var = 1    # underscore = "please don't touch" (convention, not enforced)
__private = 2       # double underscore name-mangles (still accessible)

# ponytail: no public/private/protected keywords; we're all consenting adults

--- List vs Tuple vs Set (when to use) ---

[1, 2, 3]     # list — mutable, ordered, for collections that change
(1, 2, 3)     # tuple — immutable, ordered, for fixed data (like Java's record)
{1, 2, 3}     # set — mutable, unordered, unique, for membership/lookups

# Tuple as dict key? Yes — tuple is immutable. List? No.
d = {(1, 2): "point"}  # works
# Java has no direct equivalent of tuple-as-key

--- Virtual environments & pip (vs Maven/Gradle) ---

# Create & activate:
#   python -m venv .venv        # one-time setup
#   source .venv/bin/activate   # activate (Linux/Mac)
#   .venv\Scripts\activate      # activate (Windows)

# Install packages:
#   pip install requests        # installs globally (bad) or in venv (good)

# Freeze dependencies:
#   pip freeze > requirements.txt   # like pom.xml / build.gradle
#   pip install -r requirements.txt # restore

# ponytail: always use a venv — never pip install system-wide
# Java analogy: venv = project-specific JDK + local Maven repo

================================================================================
6. OOP CONCEPTS
================================================================================

class, object, interface, polymorphism, encapsulation, abstraction,
exception handling

================================================================================
7. JSON (JavaScript Object Notation)
================================================================================

Characteristics:
  - Small size (less bandwidth)
  - Fast to parse
  - Easy to read
  - Native array support
  - Direct mapping to programming objects
  - Lightweight
  - Readable
  - Supports complex nesting
  - Standard for Web APIs
  - Language independent

Golden Rules of JSON:
  - Start with { } for an object
  - Keys (strings) must be in double quotes
  - Separate items with commas
  - No comma after the last item

JSON Functions:
  json.loads()  --> parse JSON       : string -> dict/list
  json.dumps()  --> create JSON str  : dict/list -> string
  json.load()   --> load JSON file   : file -> dict/list
  json.dump()   --> write JSON file  : dict/list -> file

Access Patterns:
  Direct access      : print(api["data"])
  One level deep     : print(api["data"]["name"])

Core JSON Terms:
  Serialization   : converting JSON string to Python object  --> json.loads()
  Parsing         : processing the JSON structure             --> response.json()
  Nested          : objects or arrays inside the JSON data structure
  Key-Value Pair  : a key mapped to a value
  Root            : top-most level of the JSON, everything inside { }

JSON is built-in (no install needed).

Third-party libraries (for performance / validation):
  ijson, ujson, orjson, jsonschema

================================================================================
8. XML (eXtensible Markup Language)
================================================================================

XML is a markup language used to store, transport, and organize data in a
structured way. Unlike JSON, XML uses tags (<tag>) and attributes.

================================================================================
9. API (Application Programming Interface)
================================================================================

Methods:
  GET, POST, PUT, PATCH, DELETE

POST vs PUT vs PATCH:
  POST  - used to CREATE a new resource
  PUT   - used to REPLACE an entire resource (requires full object)
  PATCH - used to PARTIALLY UPDATE a resource (only changed fields)

Status Codes:
  200 : OK / Success
  201 : Created (resource successfully created)
  301 : The server redirects to another endpoint
  400 : Bad Request
  401 : Not Authorized (missing/invalid credentials)
  403 : Access Forbidden (valid credentials but no permission)
  404 : Resource Not Found
  429 : Too Many Requests (rate limited)
  500 : Internal Server Error
  503 : The server is not ready to handle the request

Example URL:
  https://weatherdata.com/forecast/v2/json/en/city=london/&temp=high/&precision=decimal/&unit=metric

Parts of the URL:
  Host URL  : https://api.weatherdata.com
  Service   : /forecast
  Version   : /v2
  Format    : /json
  Lang      : /en
  Dataset   : city=london
  Filters   : &temp=high
  Precision : &precision=decimal
  Unit      : &unit=metric

Headers (common):
  Content-Type : application/json
  Authorization: Bearer <token>  or  Basic <base64>
  Accept       : application/json

REST API Rules:
  - Uniform Interface
  - Client-Server
  - Stateless
  - Cacheable
  - Layered System
  - Code on Demand (optional)

================================================================================
10. PYTHON REQUESTS LIBRARY
================================================================================

The `requests` library is used to send HTTP requests in Python.

Installation:
  pip install requests

Basic Usage:
  import requests

  response = requests.get("https://api.example.com/data")
  response = requests.post("https://api.example.com/data", json={"key": "value"})
  response = requests.put("https://api.example.com/data/1", json={"key": "new"})
  response = requests.delete("https://api.example.com/data/1")

Common response attributes:
  response.status_code      # e.g. 200, 404
  response.text             # raw string response
  response.json()           # parse JSON -> dict/list
  response.headers          # response headers (dict)
  response.elapsed          # time taken for request

Passing parameters:
  params = {"key1": "value1", "key2": "value2"}
  response = requests.get(url, params=params)

Passing headers:
  headers = {"Authorization": "Bearer YOUR_API_KEY"}
  response = requests.get(url, headers=headers)

Error handling:
  try:
      response = requests.get(url, timeout=10)
      response.raise_for_status()    # raises exception for 4xx/5xx
      data = response.json()
  except requests.exceptions.Timeout:
      print("Request timed out")
  except requests.exceptions.HTTPError as e:
      print(f"HTTP error: {e}")
  except requests.exceptions.RequestException as e:
      print(f"Request failed: {e}")

================================================================================
11. API PRACTICE LAB
================================================================================

For the next 2:00pm - 3:00pm labs, we will work extensively with APIs.

Objective:
  1. Read API documentation.
  2. Identify available endpoints.
  3. Send API requests using Python (requests library) or Postman.
  4. Explore the JSON response.
  5. Identify objects, arrays, keys, and values.
  6. Extract specific information from the JSON response.
  7. Handle errors and status codes.
  8. Manage API keys securely (use environment variables, never hardcode).

--- Example API ---

ISS Current Location API
  Documentation: http://open-notify.org/Open-Notify-API/ISS-Location-Now/
  No API key required.

Questions:
  1. Fetch the current ISS location.
  2. Print latitude and longitude.
  3. Print the timestamp.
  4. Convert the timestamp to human-readable format.
  5. Store the response in a Python dictionary.
  6. Display all keys present in the JSON response.

--- Additional Free APIs (No Authentication Required) ---

### 1. JSONPlaceholder
  Documentation: https://jsonplaceholder.typicode.com/
  Resources:
    - /posts
    - /comments
    - /albums
    - /photos
    - /todos
    - /users
  Practice:
    - Fetch all users.
    - Get a single user.
    - Fetch posts of a specific user.
    - Create a new post using POST.
    - Update a post using PUT/PATCH.
    - Delete a post using DELETE.

### 2. ReqRes
  Documentation: https://reqres.in/
  Resources:
    - /users
    - /unknown
  Practice:
    - List users.
    - Get a specific user.
    - Create a user.
    - Update a user.
    - Delete a user.

### 3. FreeAPI
  Documentation:
  Resources:
    - Random Users
    - Quotes
    - Jokes
    - Products
    - Books
    - Meals
    - Dogs
  Practice:
    - Fetch random users.
    - Extract name, email, and country.
    - Create a formatted report from the response.

### 4. PokeAPI
  Documentation: https://pokeapi.co/
  Practice:
    - Get information about a Pokemon.
    - Extract abilities.
    - Extract height and weight.
    - List Pokemon types.

### 5. Dog API
  Documentation: https://dog.ceo/dog-api/
  Practice:
    - Get a random dog image.
    - Get images by breed.
    - Count returned URLs.

### 6. Bored API
  Documentation: https://www.boredapi.com/
  Practice:
    - Generate random activities.
    - Extract activity type and participants.
    - Create a recommendation system.

### 7. HTTPBin
  Documentation: https://httpbin.org/
  Practice:
    - Test GET requests.
    - Test POST requests.
    - Inspect headers.
    - Learn request/response structures.

### 8. Random User API
  Documentation: https://randomuser.me/
  Practice:
    - Fetch 10 users.
    - Extract names, emails, locations.
    - Store results in CSV format.

### 9. Countries API
  Documentation: https://restcountries.com/
  Practice:
    - Get country information.
    - Extract population, capital, currencies.
    - Find the largest country by population.

### 10. Universities API
  Documentation: http://universities.hipolabs.com/
  Practice:
    - Search universities by country.
    - Extract website URLs.
    - Count universities per country.

--- Deliverables ---

For each API:
  1. Read the documentation.
  2. Write Python code.
  3. Save the JSON response.
  4. Identify all keys and nested objects.
  5. Extract at least 5 useful fields.
  6. Handle exceptions.
  7. Print HTTP status codes.
  8. Document your observations.

Bonus:
  - Convert JSON into CSV.
  - Store API data in SQLite.
  - Create a small Flask API that consumes one of these APIs.

================================================================================
12. ENVIRONMENT VARIABLES & API KEY MANAGEMENT
================================================================================

Never hardcode API keys in your code! Use environment variables instead.

Setting environment variables:
  # Linux / Mac terminal
  export ANTHROPIC_API_KEY="sk-ant-xxxxx"

  # Windows terminal
  set ANTHROPIC_API_KEY=sk-ant-xxxxx

  # In Python
  import os
  api_key = os.getenv("ANTHROPIC_API_KEY")
  if not api_key:
      raise ValueError("ANTHROPIC_API_KEY not set in environment")

Using .env files (python-dotenv):
  1. pip install python-dotenv
  2. Create a .env file (DO NOT commit this to git):
       ANTHROPIC_API_KEY=sk-ant-xxxxx
       OPENAI_API_KEY=sk-xxxxx
  3. In Python:
       from dotenv import load_dotenv
       load_dotenv()
       api_key = os.getenv("ANTHROPIC_API_KEY")

.gitignore must include .env to prevent accidental commits.

================================================================================
13. ANTHROPIC SDK
================================================================================

The SDK helps us build tools efficiently and easily.
It simplifies communication between the user and the Anthropic server.
It manages operations in Anthropic (supports async and sync).

Installation:
  pip install anthropic

Why use the SDK?
  - Handle complex tasks: streaming responses, token counting, automatic retries,
    and error handling
  - Integrate with platforms
  - Use advanced AI features: tool use (function calling / tool calling),
    message batching, multiple responses

Authentication:
  Through API key (via environment variable)

Basic Usage:
  import anthropic

  client = anthropic.Anthropic(api_key=os.getenv("ANTHROPIC_API_KEY"))

  response = client.messages.create(
      model="claude-sonnet-4-20250514",
      max_tokens=1024,
      system="You are a helpful assistant.",
      messages=[{"role": "user", "content": "Hello!"}]
  )
  print(response.content[0].text)

Key Terms:
  - client
  - client.messages.create
  - system      : system prompt (sets the behavior/persona)
  - message     : individual turn in the conversation
  - role        : "user" or "assistant"
  - temperature : randomness control
  - model       : which model to use (e.g. claude-sonnet-4-20250514)
  - context     : the conversation history + system prompt
  - tokens      : units of text the model processes
  - prompt      : the input given to the model
  - max_tokens  : maximum length of the response
  - chain of thought (chaining)
  - memory

--- Streaming Responses ---

Streaming allows you to receive the response incrementally (token by token)
instead of waiting for the full response.

  stream = client.messages.create(
      model="claude-sonnet-4-20250514",
      max_tokens=1024,
      messages=[{"role": "user", "content": "Tell me a story"}],
      stream=True
  )
  for chunk in stream:
      if chunk.type == "content_block_delta":
          print(chunk.delta.text, end="")

Benefits of streaming:
  - Better user experience (visible progress)
  - Lower perceived latency
  - Can process partial results

--- Function Calling (Tool Use) ---

The model can request to call functions/tools, and the SDK handles the loop.

  tools = [
      {
          "name": "get_weather",
          "description": "Get the weather for a location",
          "input_schema": {
              "type": "object",
              "properties": {
                  "location": {"type": "string"}
              },
              "required": ["location"]
          }
      }
  ]

  response = client.messages.create(
      model="claude-sonnet-4-20250514",
      max_tokens=1024,
      messages=[{"role": "user", "content": "What's the weather in London?"}],
      tools=tools
  )

Response object methods:
  - response.content          : list of content blocks
  - response.stop_reason      : why generation stopped
  - response.usage            : token usage stats (input_tokens, output_tokens)

--- Message Batching ---

Anthropic supports sending multiple requests in a batch for cost savings.

  results = client.messages.batches.create(
      requests=[
          {"custom_id": "req1", "params": {"model": "...", "messages": [...]}},
          {"custom_id": "req2", "params": {"model": "...", "messages": [...]}},
      ]
  )

================================================================================
14. GIT & GITHUB
================================================================================

GIT - Version Control System (VCS)
  - Time travel (commit history)
  - Branching and merging
  - Distributed system (everyone has a full copy)
  - Centralized (GitHub acts as the central source of truth)

Why use Git?
  - No more broken code (rollbacks to any previous commit)
  - Complete visibility (who changed what and when)
  - Parallel development via branches

GITHUB - Cloud-based hosting server for Git repositories
  Features:
    - Centralized storage (cloud server)
  Uses:
    - Centralized backup
    - Asynchronous code review
    - Pull Request (PR) workflow
    - Automated CI/CD platform (GitHub Actions)

Basic Git Commands:
  Configure git first:
    git config --global user.name "Your Name"
    git config --global user.email "your.email@example.com"

  Common workflow:
    git init                    # initialize a new repo
    git add .                   # stage all changes
    git commit -m "message"     # commit staged changes
    git log --oneline           # view commit history
    git status                  # check current state

  Branching:
    git branch <name>           # create a branch
    git checkout <name>         # switch to a branch
    git merge <branch>          # merge a branch into current

  Remote:
    git remote add origin <url>
    git push origin main
    git pull origin main

  .gitignore:
    Create a .gitignore file to exclude files/folders from version control.
    Common entries:
      .env
      __pycache__/
      *.pyc
      .DS_Store
      venv/

================================================================================
15. BATCH PROCESSING, CHAINING, AND LOGGING
================================================================================

--- LOGGING IN PYTHON ---

Three core concepts in Python logging:
  1. Log Levels
  2. Timestamp (%asctime)
  3. Log Handler - creates the log file with the format provided

Basic logging setup:
  import logging

  logging.basicConfig(
      level=logging.INFO,
      format="%(asctime)s - %(levelname)s - %(message)s",
      handlers=[
          logging.FileHandler("app.log"),
          logging.StreamHandler()      # also print to console
      ]
  )

  logging.info("Application started")
  logging.error("Something went wrong")

Log Levels:
  DEBUG    (10) : Detailed diagnostic details during development.
  INFO     (20) : Normal operation confirmation messages.
  WARNING  (30) : Indications of unexpected events or upcoming issues.
  ERROR    (40) : Serious software issues preventing function runs.
  CRITICAL (50) : Severe failures where the program may crash.

--- BATCHING ---

Batching is the process of breaking down a large list of tasks or data into
smaller, manageable chunks (called batches).

When dealing with AI APIs, batching is necessary for two reasons:
  1. Rate-Limiting - APIs limit requests per minute; batching respects limits
  2. Memory and stability - smaller batches reduce memory pressure

Why Use Batch Processing?
  - Cost Efficiency: Major providers offer massive discounts (often up to 50%)
    for batch jobs.
  - Higher Rate Limits: Bypasses standard concurrent request limits by queuing
    tasks on the provider's servers.
  - Resource Optimization: Maximizes GPU/CPU utilization by processing inputs
    in bulk rather than handling sporadic requests.

Simple batch processing pattern:
  def process_in_batches(items, batch_size=10):
      for i in range(0, len(items), batch_size):
          batch = items[i:i + batch_size]
          results = process_batch(batch)
          time.sleep(1)    # rate limiting delay
      return results

--- CHAINING ---

Prompt chaining: linking multiple prompts/steps together where the output of
one step becomes the input of the next.

Why chaining?
  - Accuracy: each step focuses on one specific task
  - Debugging: easy to test and fix individual steps
  - Flexibility: steps can be reordered or replaced independently

Example of chaining:
  Step 1: Extract key points from a document
  Step 2: Summarize each key point
  Step 3: Combine summaries into a final report

================================================================================
16. LLM / AI / ML
================================================================================

AI -> ML -> Neural Networks -> Deep Learning -> Transformers -> Gen AI
  -> Generative Pre-trained Transformer (GPT)

AI:
  Supervised Learning Algorithms:
    - Linear Regression
    - Support Vector Machine (SVM)
    - K-Nearest Neighbors (KNN)
    - Decision Tree
    - Random Forest
    - Naive Bayes
    - Neural Networks

  Unsupervised Learning Algorithms:
    - Clustering algorithms (K-Means, DBSCAN, Hierarchical)
    - Association Mining (Apriori, FP-Growth)
    - Anomaly Detection algorithms (Isolation Forest, LOF)
    - Dimensionality Reduction (PCA, t-SNE, UMAP)

  Reinforcement Learning:
    - Q-Learning
    - Deep Q-Networks (DQN)
    - Policy Gradients (PPO, A2C)

--- Pre-training vs Fine-tuning ---

  Pre-training:
    - Training a model on a massive, general dataset (e.g. all of the internet)
    - Teaches the model language understanding, grammar, facts
    - Very expensive (millions of $, weeks of training)
    - Produces a "base model" (e.g. GPT-3 base, Llama base)

  Fine-tuning:
    - Taking a pre-trained model and training it further on a smaller,
      specific dataset
    - Teaches the model a specific task or style
    - Much cheaper and faster
    - Examples: fine-tuning on customer support chats, legal documents, etc.

  Instruction Tuning (RLHF / DPO):
    - A special type of fine-tuning that aligns the model to follow instructions
    - Uses human feedback (RLHF) or preference optimization (DPO)
    - Produces assistant-style models (e.g. ChatGPT, Claude)

================================================================================
17. TOKENIZATION
================================================================================

Tokenization is the process of converting text into smaller units (tokens)
that the model can process.

How it works:
  "Hello, how are you?" -> ["Hello", ",", " how", " are", " you", "?"]

Key points:
  - Tokens are NOT words. A word can be 1-4 tokens depending on complexity.
  - Common words: 1 token (e.g. "the", "is", "hello")
  - Rare words: more tokens (e.g. "antidisestablishment" -> 5 tokens)
  - Spaces and punctuation are often separate tokens
  - Different models use different tokenizers
    - GPT models: Byte-Pair Encoding (BPE)
    - Claude models: SentencePiece / BPE
    - Llama models: BPE

Token counts:
  - English text: ~1.3 tokens per word on average
  - 1000 tokens ~= 750 words
  - Model context limits are measured in tokens (e.g. 128K tokens for Claude)

Why tokenization matters:
  - Limits how much text you can send (context window)
  - Affects cost (APIs charge per token)
  - Different languages have different token efficiency
    - English: efficient (~1.3 tokens/word)
    - Other languages: may use more tokens for the same meaning

Token counting:
  import tiktoken                           # OpenAI's tokenizer
  encoder = tiktoken.get_encoding("cl100k_base")
  tokens = encoder.encode("Hello, world!")
  print(len(tokens))                        # token count

================================================================================
18. TRANSFORMERS & ATTENTION MECHANISM
================================================================================

The Transformer is the foundational architecture behind all modern LLMs (GPT,
Claude, Llama, Gemini, etc.). Introduced in the paper "Attention Is All You
Need" (Vaswani et al., 2017).

--- Key Components ---

  1. Attention Mechanism (Self-Attention):
     - Allows the model to look at ALL positions in the input simultaneously
     - Decides which words are most relevant to each other
     - Example: In "The cat sat on the mat because it was tired",
       the model learns that "it" refers to "cat", not "mat"
     - Multi-Head Attention: runs multiple attention operations in parallel
       to capture different types of relationships

  2. Encoder-Decoder Structure:
     - Encoder: reads the input and creates representations
     - Decoder: generates the output one token at a time
     - GPT uses only the Decoder (decoder-only architecture)
     - T5/BART use both (encoder-decoder architecture)

  3. Positional Encoding:
     - Since the model processes all tokens at once (not sequentially), it needs
       a way to know the position/order of words
     - Positional encodings are added to the token embeddings

  4. Feed-Forward Network (FFN):
     - After attention, each position goes through a neural network
     - Adds non-linear transformations to the representations

  5. Layer Normalization & Residual Connections:
     - Help stabilize training and allow deeper networks
     - Residual: skip connections that let gradients flow through directly

--- Why Transformers Replaced RNNs/LSTMs ---

  RNNs/LSTMs processed tokens one at a time in sequence (slow, couldn't
  parallelize). Transformers process all tokens simultaneously (parallel),
  making training much faster on GPUs.

--- Scaling Laws ---

  Performance of Transformers predictably improves with:
  - More parameters (bigger models)
  - More training data
  - More compute

  This is why we see models growing from GPT-1 (117M params) to GPT-4
  (estimated 1.8T params).

================================================================================
19. HALLUCINATION
================================================================================

Hallucination is when an LLM generates incorrect, nonsensical, or fabricated
information while sounding confident and plausible.

Types of Hallucination:
  1. Factual Hallucination: model states false information as fact
     (e.g. "The Eiffel Tower is in Rome")
  2. Source Hallucination: model invents sources/citations
     (e.g. making up a book title and author that doesn't exist)
  3. Logic Hallucination: model makes reasoning errors
     (e.g. incorrect math calculations)

Why Hallucinations Happen:
  - Models predict the next token based on patterns, not truth
  - Lack of real-world understanding or grounding
  - Training data contains inaccuracies
  - Model tries to be helpful even when it doesn't know the answer
  - Conflicting information in training data

How to Reduce Hallucinations:
  - Use RAG (Retrieval-Augmented Generation) - ground responses in real data
  - Lower temperature (less creative = fewer fabrications)
  - Ask the model to cite sources or show its reasoning
  - Use system prompts: "Only answer if you are certain"
  - Use Chain-of-Thought prompting
  - Implement human-in-the-loop verification for critical tasks
  - Use tools like web search or databases for factual lookups

Detection:
  - Cross-check facts against trusted sources
  - Look for vague or overly generic statements
  - Check for made-up citations (verify they exist)
  - Use another LLM to fact-check the response

================================================================================
20. RAG (Retrieval-Augmented Generation)
================================================================================

RAG combines information retrieval with text generation. Instead of relying
solely on the model's training data, RAG retrieves relevant information from
an external knowledge base and gives it to the model as context.

Why RAG?
  - Reduces hallucination (answers are grounded in retrieved documents)
  - Can access up-to-date information (not limited to training cutoff)
  - Can include private/proprietary data without fine-tuning
  - More transparent (can show which documents were used)

RAG Pipeline:

  Indexing Phase:
    Documents -> Split into chunks -> Generate embeddings ->
      Store in vector database

  Retrieval Phase:
    User query -> Generate query embedding ->
      Search vector DB for similar chunks ->
        Retrieve top-k most relevant chunks

  Generation Phase:
    Retrieved chunks + original query + system prompt -> LLM -> Final answer

Architecture:
                        User Query
                            |
                        Embedding
                            |
                    Vector Database ----[Indexed Documents]
                            |
                    Retrieve Top-K Chunks
                            |
            +-------------------------------+
            |  Prompt Template:             |
            |  "Using the following context,|
            |   answer the question: ..."   |
            +-------------------------------+
                            |
                           LLM
                            |
                       Final Answer

Key Decisions in RAG:
  Chunking strategy:
    - Size: 256-1024 tokens per chunk (depends on use case)
    - Overlap: 10-20% overlap between chunks to preserve context
    - Strategy: fixed-size, sentence-based, or semantic chunking

  Retrieval methods:
    - Dense retrieval (embedding similarity) - captures meaning
    - Sparse retrieval (BM25/keyword) - captures exact term matches
    - Hybrid (combines both) - best of both worlds

  Re-ranking:
    - After initial retrieval, use a cross-encoder to re-rank results
    - Improves relevance of top results

Advanced RAG:
  - Multi-hop RAG: break complex questions into sub-questions, retrieve for each
  - Agentic RAG: model decides when and what to retrieve
  - Graph RAG: uses knowledge graphs for structured relationships

================================================================================
21. AI AGENTS
================================================================================

An AI agent is an LLM-powered system that can:
  - Perceive its environment (receive user input, tool outputs)
  - Make decisions (plan, reason)
  - Take actions (call tools, browse web, run code)
  - Learn from feedback

Core Components:
  1. Model (LLM)       : the "brain" - reasoning and decision making
  2. Tools             : capabilities (web search, calculator, code execution,
                          file I/O, database queries)
  3. Memory            : context from previous interactions
  4. Planning          : breaking down complex tasks into steps
  5. Execution loop    : observe -> think -> act -> observe -> ...

Agent Loop:
  User Input -> LLM decides -> [if needs tool] -> Call tool ->
    Tool result -> LLM re-evaluates -> [until done] -> Final response

Types of Agents:
  - Simple Agent: single LLM call with tools (e.g. Chatbot with web search)
  - ReAct Agent: interleaves reasoning (thought) with actions (tool calls)
  - Multi-Agent: multiple specialized agents collaborating
  - Autonomous Agent: runs continuously until goal is reached

Tool Use (Function Calling):
  The model can request to call predefined tools. The application executes the
  tool and returns the result to the model.

  Example:
    User: "What's the weather in Tokyo?"
    Model: [thinks] -> calls get_weather(location="Tokyo")
    System: returns {"temperature": 22, "condition": "sunny"}
    Model: "The weather in Tokyo is 22 degrees and sunny."

Memory in Agents:
  - Short-term: current conversation context
  - Long-term: stored embeddings of past interactions
  - Episodic: specific past experiences
  - Persistent: user preferences, learned behaviors

================================================================================
22. EMBEDDINGS & VECTOR DATABASES
================================================================================

Embeddings:
  Numerical representation of text (or images, audio, etc.) as a dense vector
  of floating-point numbers. Similar texts have similar vectors.

  Used for: semantic search, similarity search, keyword search, recommendations,
  classification, clustering, and AI retrieval.

How Embeddings Work:
  text -> model -> vector (e.g. [0.12, -0.45, 0.78, ..., 0.33]) -> storage
  -> search operation

Creating embeddings in Python (OpenAI):
  import openai
  response = openai.embeddings.create(
      model="text-embedding-3-small",
      input="Your text here"
  )
  vector = response.data[0].embedding

Creating embeddings in Python (sentence-transformers - free/local):
  from sentence_transformers import SentenceTransformer
  model = SentenceTransformer('all-MiniLM-L6-v2')
  vector = model.encode("Your text here")
  print(vector.shape)   # (384,) for this model

Popular Vector DB / Indexing Libraries:
  FAISS        : Meta's library, best for local/high-performance (open source)
  ChromaDB     : Simple, Python-native, good for prototyping (open source)
  Pinecone     : Managed cloud service, scalable
  Weaviate     : Open source vector search engine
  Qdrant       : High-performance vector DB (open source)
  Milvus       : Enterprise-grade distributed vector DB (open source)

Embedding + Vector Database Pipeline:
  doc -> embedding -> vector DB -> query -> retrieval -> LLM answer

Similarity Measures:
  - Cosine Similarity: measures the angle between vectors (range -1 to 1)
  - Euclidean Distance: straight-line distance between vectors
  - Dot Product: similarity as the product of vector components
  - Cosine is most common for text embeddings

================================================================================
23. FAISS (Facebook AI Similarity Search)
================================================================================

FAISS is an open-source library developed by Meta for efficient similarity
search and clustering of dense vectors.

Indexing:
  The process of organizing and structuring vector data to enable fast and
  efficient similarity search without having to compare the query vector
  against every single vector in the database.

Key Factors:
  - Accuracy  : how close the results are to exact search
  - Speed     : how fast the search completes
  - Memory    : how much RAM the index uses

Techniques:

  FLAT (Brute Force):
    Searches records one by one, comparing every vector until the end. Finds
    the most similar vectors and picks the highest-probability vector.
    - 100% accuracy, but slow on large datasets

  IVF (Inverted File):
    Instead of storing everything in one big list, IVF first groups similar
    vectors into clusters (using K-Means). Search only compares against the
    closest clusters.
    - Fast, good accuracy, medium memory

  HNSW (Hierarchical Navigable Small World):
    Builds a multi-layer graph. Search starts at a random node and navigates
    to neighbors that are closer to the query. Repeats until no better neighbor
    exists. Like a highway system - express lanes (top layers) get you close
    fast, local roads (bottom layers) find the exact result.

    Example graph:
      Animals:   Dog ------ Cat
                      |
                 Wolf ------ Tiger

      Vehicles:  Car ------ Bus

      Fruits:    Apple ---- Orange

    Search Approach:  Puppy
                        |
                        v
                Start at random node
                        |
                        v
                      Dog
                     /   \
                  Cat    Wolf
                           |
                        Tiger
                           |
                     Closest Node
                           |
                           v
                    Return Result

  PQ (Product Quantization):
    Divides each high-dimensional vector into smaller subvectors, quantizes
    each subvector using a learned codebook, and stores only the corresponding
    code indices. During search, distances are approximated using lookup
    tables, enabling efficient ANN search with very low memory usage.

    Example:
      Original vector:
        [12, 45, 31, 77, 22, 63, 91, 18]

      Step 1: Split into 4 parts
        Part 1 -> [12, 45]    Part 2 -> [31, 77]
        Part 3 -> [22, 63]    Part 4 -> [91, 18]

      Step 2: Each part is mapped to the nearest code in a codebook

      Codebook for Part 1:         The vector becomes: [1, 1, 1, 1]
        Code 0: [10, 44]           (only the code indices are stored)
        Code 1: [12, 45]   <-- match
        Code 2: [90, 91]

      16 bytes stored instead of 8 floats (32 bytes) -> 50% memory reduction

--- Comparison Table ---

| **Index Type**                                | **Search Accuracy**               | **Search Speed**                                        | **Memory Usage**                              |
| --------------------------------------------- | --------------------------------- | ------------------------------------------------------- | --------------------------------------------- |
| **Flat**                                      | 100% (Exact Search)               | Slow (Scales linearly with the number of vectors)       | Medium (Stores raw vectors)                   |
| **IVF (Inverted File)**                       | High (Approximate Search)         | Fast (Narrows search space using clusters)              | Medium (Stores raw vectors + cluster list)    |
| **HNSW (Hierarchical Navigable Small World)** | Very High (Approximate Search)    | Blazing Fast (Logarithmic search complexity)            | Very High (Stores vectors + graph links)      |
| **PQ (Product Quantization)**                 | Low to Medium                     | Fast (Uses asymmetric distance on compressed vectors)   | Very Low (Compresses vectors heavily)         |

Combining techniques:
  IVF + PQ: common combination for large-scale similarity search
  IVF+HNSW: HNSW on top of IVF centroids for even faster search

================================================================================
24. MODEL EVALUATION & METRICS
================================================================================

Evaluating LLM outputs is challenging because there's no single "correct"
answer. Several approaches exist:

--- Automatic Metrics ---

  Perplexity:
    - Measures how "surprised" the model is by the text
    - Lower perplexity = better prediction
    - Mainly used during training, not for final evaluation

  ROUGE (for summarization):
    - Compares generated summary to reference summary
    - ROUGE-1: unigram overlap
    - ROUGE-2: bigram overlap
    - ROUGE-L: longest common subsequence

  BLEU (for translation):
    - Measures n-gram overlap between generated and reference text
    - Range: 0 (worst) to 1 (best)
    - Penalizes too-short translations (brevity penalty)

  BERTScore:
    - Uses BERT embeddings to compute semantic similarity
    - Captures meaning, not just exact word matches

--- Human Evaluation ---

  - Helpfulness: does the response address the user's need?
  - Honesty: is the model truthful about its limitations?
  - Harmlessness: does the response avoid harmful content?
  - Relevance: is the output on-topic?
  - Coherence: does the response flow logically?

--- LLM-as-a-Judge ---

  Using a strong LLM (e.g. GPT-4, Claude) to evaluate another model's outputs.
  Common for automated evaluation at scale.

  Example prompt:
    "Rate the following response on a scale of 1-5 for accuracy, relevance,
     and clarity. Response: [model output]"

================================================================================
25. MODEL QUANTIZATION
================================================================================

Quantization reduces the precision of model weights (e.g. from 32-bit floats
to 8-bit integers) to reduce memory usage and speed up inference.

Why Quantize?
  - Reduce model size (4x smaller for 8-bit vs 32-bit)
  - Faster inference (especially on consumer GPUs)
  - Enables running large models on smaller hardware
  - Lower power consumption

Common Quantization Formats:
  - FP32 (32-bit float): full precision (baseline)
  - FP16 / BF16 (16-bit): half precision, minimal quality loss
  - INT8 (8-bit integer): 4x smaller, slight quality loss
  - INT4 (4-bit): 8x smaller, more quality loss, used for extreme compression
  - NF4 (Normal Float 4): specially designed for LLM weights (QLoRA)

Techniques:
  - Post-Training Quantization (PTQ): quantize after training
  - Quantization-Aware Training (QAT): train with quantization in mind
  - GGUF / GGML: formats optimized for CPU inference (llama.cpp)
  - GPTQ: post-training quantization for GPU inference
  - AWQ: activation-aware weight quantization
  - BitsAndBytes: library for 4-bit/8-bit quantization in HuggingFace

Example (HuggingFace + BitsAndBytes):
  from transformers import AutoModelForCausalLM, BitsAndBytesConfig

  quant_config = BitsAndBytesConfig(
      load_in_4bit=True,
      bnb_4bit_compute_dtype=torch.float16
  )
  model = AutoModelForCausalLM.from_pretrained(
      "meta-llama/Llama-2-7b",
      quantization_config=quant_config
  )

================================================================================
26. RESPONSIBLE AI & ETHICS
================================================================================

Key principles for building and using AI responsibly:

  - Fairness: models should not discriminate against groups or individuals
  - Transparency: users should know they are interacting with AI
  - Accountability: someone must be responsible for AI outputs
  - Privacy: user data must be protected, not used for training without consent
  - Safety: models should refuse harmful requests
  - Robustness: models should handle unexpected inputs gracefully

Common Issues:
  - Bias: models reflect biases in training data (gender, race, cultural)
  - Misinformation: AI-generated content can spread false information
  - Jailbreaking: adversarial prompts designed to bypass safety controls
  - Prompt Injection: malicious instructions hidden in user input

Best Practices:
  - Always validate AI outputs for critical applications
  - Use content filtering / guardrails
  - Implement human-in-the-loop for high-stakes decisions
  - Be transparent about AI usage
  - Regularly audit for bias

================================================================================
27. ATTENTION MECHANISM
================================================================================

--- What is Attention? ---

Attention is the core innovation behind all modern LLMs (GPT, Claude, Llama,
Gemini). It allows the model to selectively focus on relevant parts of the
input when generating each word.

  Your note: "selective vision, dynamically, a weight blend"
  Explanation:
    Attention is NOT a fixed rule. It DYNAMICALLY (changes for every word)
    SELECTIVELY (picks only relevant words) creates a WEIGHTED BLEND (soft
    mixing, not hard cut) of information from all other words.

--- Self-Attention & QKV ---

  Your note:
    self attenction
      QKV explain
      attenction(Q,k,v)= softmax(Qk^t /  squrt(d _ k))x v

  Explanation:
    QKV stands for Query, Key, Value — think of it like a library search:

      Q (Query)  = what the current word is "looking for"
      K (Key)    = what each other word "offers" as a label
      V (Value)  = the actual information/content of each word

    Example: In "The cat sat on the mat because it was tired",
    when processing "it", the model:
      - Generates a Query from "it"
      - Compares it to Keys from every other word (cat, sat, mat, ...)
      - Finds "cat" has the highest match score
      - Blends "cat"'s information (Value) into "it"'s representation
    This is how the model knows "it" refers to "cat".

  The Formula — Step by Step:

    Attention(Q,K,V) = softmax( Q x K^T / sqrt(d_k) ) x V

    Step 1 — Q x K^T:
      Your note: "Qk^t - the similarity match 'matches'"
      Dot product between Query and every Key. High score = high relevance.
      This is the "matching" step — finding which words relate to each other.

    Step 2 — / sqrt(d_k):
      Your note: "%squart(d_k)"
      Divide by the square root of the Key vector dimension (e.g. 64 or 128).
      This is a SCALING FACTOR. Without it, large vectors produce huge dot
      products that make softmax too extreme (all probability on one word).
      The square root keeps scores balanced.

    Step 3 — softmax:
      Converts raw scores into a PROBABILITY DISTRIBUTION:
        - All values between 0 and 1
        - All values sum to 1
      Tells the model: "pay this much attention to each word."

    Step 4 — x V:
      Multiply the attention probabilities by each word's Value.
      Words with higher attention contribute more to the final output.

  Put simply:
    "Find relevant words (QxK), decide how much each matters (softmax),
     blend their information (xV)."

--- Multi-Head Attention ---

  Your note: "multi head"

  Explanation:
    Instead of one attention calculation, the model runs MULTIPLE in parallel
    (e.g. 8 to 96 heads). Each head learns a DIFFERENT type of relationship:

      - One head tracks position (word 3 -> word 7)
      - Another tracks grammar (subject -> verb)
      - Another tracks synonyms / related meaning
      - Another tracks negation ("not happy" -> unhappy)

    All heads' results are concatenated together. This is why Transformers
    understand language so richly — they see the text from many perspectives
    simultaneously.

--- Top-p & Top-k (Sampling) ---

  Your note:
    top-p
      if top-p=1 and top-p=0
    top-k
      key is liek how many records it should retrive from the top results

  Explanation:
    These belong under TEMPERATURE / SAMPLING, not Attention. They control
    how the model CHOOSES the next word during text generation:

    Top-p (Nucleus Sampling):
      - top-p = 1.0: consider ALL possible next words (most creative / risky)
      - top-p = 0.9: consider only the top 90% probability mass
      - top-p = 0.0: only the single most likely word (greedy / deterministic)

    Top-k:
      Your note is exactly right: limits how many top candidates are considered.
      - top-k = 50: only the 50 most-likely tokens can be chosen
      - top-k = 1: same as greedy (always pick the best)

--- Problems with RNNs (Before Transformers) ---

  RNNs/LSTMs processed text one word at a time in sequence. This caused
  three fundamental problems that Attention solves.

  1. Long-Range Dependencies:
     Your note: "informtion relayed hand to hand / vanishing"

     Explanation:
       In RNNs, information passes ONE STEP AT A TIME (hand to hand).
       For a 100-word sentence, word 1's signal must travel through 99
       steps to reach word 100. Like a game of telephone, the signal
       gets weaker and weaker (VANISHES) until it disappears entirely.
       This is called the "vanishing gradient problem."

  2. No Parallelization:
     Your note: "no parallelization"

     Explanation:
       RNNs must process token 1, then token 2, then token 3... in strict
       sequence. Token 50 waits for tokens 1-49 to finish. This means
       GPUs (which excel at parallel computation) are mostly idle.
       Training takes WEEKS instead of hours.

  3. Fixed-Context Bottleneck:
     Your note: "the fixed-context bottleneck"

     Explanation:
       RNNs compress the ENTIRE input sequence into one fixed-size vector
       (e.g. 1024 numbers). A 1000-word document gets squeezed into that
       same small vector. Most detail is LOST — hence "lossy."

--- What Attention Delivers (The Wishlist) ---

  Your note:
    "the wishlist for attenction delivers all three
       context any two direcly
       compute all position at once
       no lossy fixed size bottleneck"

  Explanation — these three solved everything wrong with RNNs:

    1. "Context any two directly":
       Any two words can connect DIRECTLY regardless of distance. Word 1
       communicates with Word 100 in a SINGLE step — no hand-to-hand relay,
       no vanishing signal. This solves long-range dependencies.

    2. "Compute all positions at once":
       FULL PARALLELISM. All token positions are computed simultaneously
       in one giant matrix multiplication. GPUs run at full speed. Training
       goes from weeks to hours. This solves the parallelization problem.

    3. "No lossy fixed-size bottleneck":
       The model can look back at EVERY original token's representation,
       not a compressed summary. Nothing is lost. This solves the context
       bottleneck.

  These three wins are why every modern LLM uses the Transformer
  architecture, and why RNNs/LSTMs are essentially obsolete.

================================================================================
28. PRETRAINING, FINE-TUNING & SELF-SUPERVISED LEARNING
================================================================================

--- Pretraining ---

  Your note:
    pretaining
      what is pretraining?

  Explanation:
    Pretraining is the FIRST phase of building an LLM. The model is trained
    on a MASSIVE amount of raw text (the entire internet — trillions of tokens)
    to learn the fundamentals of language:

      - Grammar and syntax
      - Word meanings and relationships
      - Facts about the world
      - General reasoning patterns

    This phase is EXTREMELY expensive — thousands of GPUs running for months,
    costing millions of dollars in compute alone.

    The model does NOT know how to answer questions or follow instructions yet
    at this stage. It only knows how to predict the next word in a sequence.

--- Fine-Tuning ---

  Your note:
    fine tuining:
      what is fine tuining?
      trainging the model according to the

  Explanation:
    Fine-tuning takes a pretrained model and trains it FURTHER on a smaller,
    specific dataset. The model already knows language — now we teach it
    WHAT TO DO with that knowledge.

    Types of fine-tuning:

      1. Instruction Fine-Tuning:
         - Train on (instruction, response) pairs
         - e.g. "Translate to French: Hello" -> "Bonjour"
         - Teaches the model to FOLLOW INSTRUCTIONS

      2. Chat Fine-Tuning:
         - Train on conversation format (multi-turn dialogue)
         - Teaches the model to be a helpful assistant
         - Uses techniques like RLHF (Reinforcement Learning from Human Feedback)

      3. Domain Fine-Tuning:
         - Train on specialized data (legal, medical, code)
         - Makes the model an expert in a specific field

    Fine-tuning is MUCH CHEAPER than pretraining:
      - Uses less data (thousands/millions of examples vs trillions)
      - Requires less compute (hours/days instead of months)
      - Often uses human-labeled data

--- Why Building Models Like GPT Takes So Long ---

  Your note:
    why is it takes so long to build models like GPT?
      computaion power?
      data
      supervised learing learning

  Explanation:
    Three key reasons:

    1. COMPUTATION POWER:
       - GPT-4 was estimated to use ~25,000 GPUs running for months
       - Requires specialized data centers with massive cooling and power
       - A single training run can cost $100M+
       - Most organizations simply cannot afford this

    2. DATA:
       - Models need TRILLIONS of tokens to learn effectively
       - Collecting, cleaning, filtering, and deduplicating data is huge work
       - Data quality matters as much as quantity (garbage in = garbage out)
       - Legal concerns (copyright, licensing) add complexity

    3. SUPERVISED LEARNING (The Old Bottleneck):
       - Before the Transformer era, every example needed a HUMAN label
       - "This email is spam" / "This image contains a cat"
       - Labeling trillions of examples is IMPOSSIBLE:
         * Too expensive (would cost billions of dollars)
         * Too slow (would take centuries)

--- Self-Supervised Learning (The Breakthrough) ---

  Your note:
    how to scale to trillions of examples if every single one requires an
    expensive human expert.
      solution: gpot
      breakthrough: self supervised learning (label itself)

  Explanation:
    Self-supervised learning is the INNOVATION that made modern LLMs possible.
    It removes the need for human labels entirely.

    How it works — Next Token Prediction:
      Input (to model):  "The cat sat on the ___"
      Correct answer:     "mat"
      The model predicts the next word. The ACTUAL next word IS the label.
      No human needed to create the label — the text itself provides it.

    This means:
      - Every sentence on the internet becomes a FREE training example
      - You can scale to trillions of examples AUTOMATICALLY
      - This is what "GPT" (Generative Pre-Training) is all about
      - Training data is essentially unlimited

    What the model learns:

      Your note: "to minimise the errors / concepts / facts / relations"

      The model's goal is to MINIMIZE PREDICTION ERROR. To predict the next
      word correctly, it MUST learn:

        - CONCEPTS: what words mean (e.g., "cat" = a small furry animal)
        - FACTS: how the world works (e.g., "cats drink milk", "Paris is in France")
        - RELATIONS: how words and ideas connect (e.g., "it" -> "cat")

      The error is measured by CROSS-ENTROPY LOSS:
        - Model predicts "mat" with 90% confidence -> small error
        - Model predicts "dog" with 60% confidence -> large error
        - Backpropagation adjusts billions of weights to reduce error
        - After trillions of examples, the model builds deep understanding

  Put simply:
    "Predict the next word. Get it wrong? Adjust. Repeat trillions of times.
     The result: a model that understands language."

--- Tokenization Types (Quick Reference) ---

  Your note:
    word tokenization
    chatector tokenization
    sub word tokanization

  (These are covered in detail in Section 16 above. This is a quick summary.)

  Word Tokenization:
    Split text by spaces and punctuation.
    Example: "I love AI" -> ["I", "love", "AI"]
    Vocabulary: MILLIONS of words (huge and inefficient)
    Problem: Cannot handle unknown words or typos

  Character Tokenization:
    Split into individual characters.
    Example: "I love AI" -> ["I", " ", "l", "o", "v", "e", " ", "A", "I"]
    Vocabulary: TINY (~100 characters) but sequences are VERY long
    Problem: Loses word-level meaning, inefficient for long texts

  Subword Tokenization (Used by ALL modern LLMs):
    Split into common subword units.
    Example: "I love AI" -> ["I", " love", " AI"]
    Example: "unhappiness" -> ["un", "happiness"]
    Algorithms: BPE (GPT), SentencePiece (Claude), WordPiece (BERT)
    Advantage: Best balance of vocabulary size and sequence length
    This is what "tokenization" means in practice for LLMs.

================================================================================
29. HOW LLMs WORK — LOGITS, SOFTMAX & CROSS-ENTROPY LOSS
================================================================================
# ponytail: one-liners, stdlib, no fluff

--- The Two Processes of an LLM ---

  Your note:
    two completely didtinct processes
    training: output probability => caluculates weights => learn
    generation: use probability => simple one token => create text

  Explanation:

    LLMs have TWO distinct modes that people often confuse:

    TRAINING:
      The model sees the correct answer, compares its prediction, and
      adjusts weights to get closer next time.
      Direction: text → probability → error → learn

    GENERATION (Inference):
      The model uses its trained weights to predict the next token,
      feeds it back, and repeats.
      Direction: probability → pick one token → append → repeat

    Both use the same math (logits → softmax → probabilities), but the
    GOAL is different: training reduces error, generation creates text.

--- Logits (Raw Scores) ---

  Your note:
    when model outputs a raw scope for every date token we call this score
	as LOGIT
    these LOGITs are just raw, not calibrated numbers, they cannot

    example:
      the cat sat on the
      Logit_score = {"mat": 3.2, "rug": 1.3, "moon": -2.1, ...}
      clear answer == "mat"

  Explanation:
    The model's final layer outputs ONE raw number (LOGIT) per token in
    the vocabulary. These are:
      - RAW: not yet probabilities (can be negative, >1, anything)
      - UNCALIBRATED: a logit of 3.2 doesn't mean "32% chance"
      - RELATIVE: only the ORDER matters at this stage (mat > rug > moon)

    Example — for "the cat sat on the ___":
      "mat"  logit = 3.2   (high = model thinks this is likely)
      "rug"  logit = 1.3   (medium = possible)
      "moon" logit = -2.1  (low = model thinks this is unlikely)

    "Clear answer == mat" — yes, because it has the HIGHEST logit.
    But logits alone can't tell us HOW confident the model is.
    That's what softmax does.

--- Softmax (Converting Logits to Probabilities) ---

  Your formula:
    s(x_i) = e^x_i / SUM(e^x_j for j=1 to n)

  What it does:
    Takes raw logits and turns them into PROBABILITIES that sum to 1.0

    Step 1: exponentiate each logit (e^logit) — makes all numbers positive
    Step 2: sum all exponentiated values
    Step 3: divide each by the sum — now they're probabilities

  Softmax Table for "the cat sat on the ___":

    Token    Logit     exp(logit)   / Sum     Probability
    ------   -----     ----------   ------    -----------
    mat      3.2       24.53        24.53/    ~0.892  (89.2%)
                                      27.49
    rug      1.3        3.67         3.67/    ~0.133  (13.3%)
                                      27.49
    moon    -2.1        0.12         0.12/    ~0.004  (0.4%)
                                      27.49
    other    ...        ...          ...      ~0.031  (3.1%)
    -----   -----     ----------   ------    -----------
    SUM     ---        27.49       1.0       1.000  (100%)

  Your note: "->messy data will be cleared"
    Yes — softmax TAMES the messy raw logits into clean probabilities
    that sum to 100%. This is the "clear answer."

  Key insight:
    Softmax is COMPETITIVE — raising one logit pushes others down
    (because probabilities must sum to 1.0). This forces the model
    to commit to the best answer.

--- Cross-Entropy Loss (How Models Learn) ---

  Your note:
    86.6% is official answer now.
    but here we need to cross verify for that we need a way to calculate
    a single error number
    this is the job of loss function
    for language model in this we use cross-entopy loss

  Explanation:
    From the softmax table, "mat" has 89.2% probability. But was this
    a GOOD prediction? We need a single number to measure error.

    Cross-entropy loss = -log(probability assigned to the CORRECT token)

    If the correct answer is "mat" (probability = 0.892):
      loss = -log(0.892) = 0.114   (LOW — model was confident and correct)

    If the correct answer were "moon" (probability = 0.004):
      loss = -log(0.004) = 5.52    (HIGH — model was wrong AND confident)

    The model's goal during TRAINING is to MINIMIZE this loss number
    across billions of examples. Lower loss = better predictions.

--- Surprise (Low vs High) ---

  Your note:
    low surpise:
    high surpise:

  Explanation:
    Cross-entropy loss IS a measure of SURPRISE:

    LOW SURPRISE (low loss = ~0.1):
      The model assigned high probability to the correct answer.
      "Of course it's 'mat' — cat sits on mat, obvious."
      Model learns very little here — it already knew.

    HIGH SURPRISE (high loss = ~5+):
      The model assigned low probability to the correct answer.
      "Wait, it was 'moon'?! I was so sure it was 'mat'!"
      Model learns A LOT here — this is where weight updates happen.

    During training, the model processes trillions of tokens. Each one
    generates a surprise score. Backpropagation uses these surprises to
    nudge weights in the right direction. Over time, high-surprise events
    become rare — the model gets better at predicting.

  Put simply:
    "Low surprise = model knew it. High surprise = model learned something.
     Training = minimize surprise across trillions of tokens."

================================================================================
30. LORA (LOW-RANK ADAPTATION)
================================================================================
# ponytail: fine-tune large models without training all parameters

--- What is LoRA? ---

  LoRA (Low-Rank Adaptation) is a technique that fine-tunes large language
  models by training only TINY "adapters" instead of all parameters.

  Instead of updating the full weight matrix W (billions of params):
    W_new = W + delta_W           (delta_W = A x B, two small matrices)

  Key insight:
    The weight updates during fine-tuning have LOW "rank" -- meaning they
    can be represented by multiplying two small matrices A and B.

  Result:
    - Trainable params: ~0.1% instead of 100%
    - Memory usage: drastically reduced
    - One base model + many LoRA adapters = many specialized models

--- Key Parameters ---

  Rank (r):
    Controls how much adaptation is allowed.
      r=8:    default starting point (good balance)
      r=1:    minimal changes (near-original behavior)
      r=64:   more adaptation (more parameters)
    Rule: start r=8, increase if model isn't learning, decrease if overfitting.

  Alpha (lora_alpha):
    Scaling factor for the LoRA update.
      alpha=16: default (usually 1-2x rank)
    Formula: output = Wx + (alpha/r) * A * B * x

  Dropout:
    Prevents overfitting on small datasets.
      dropout=0.05 or 0.1: typical values

  Target Modules:
    Which layers get the LoRA adapters.
      ["q_proj", "v_proj"]: attention layers (most common starting point)
      ["q_proj", "k_proj", "v_proj", "o_proj"]: all attention (more params)
      ["q_proj", "v_proj", "gate_proj", "up_proj", "down_proj"]: full fine-tune

  Task Type:
    CAUSAL_LM: for text generation (GPT, Llama)
    SEQ_CLS:   for classification tasks

--- LoRA in 2 Classes (from scratch) ---

  Example from your notes -- the core idea:

    class LoRALayer(nn.Module):
        def __init__(self, in_dim, out_dim, rank, alpha):
            super().__init__()
            # rank (r): the bottleneck dimension for the low-rank matrices.
            #   r=8: typical default. Each weight update is factorized into
            #   A: (in_dim x r) and B: (r x out_dim) instead of (in_dim x out_dim).
            #   Smaller r = fewer params, less adaptation. Larger r = more params, more adaptation.
            # alpha: scaling factor. The update gets multiplied by alpha/r.
            #   alpha=16 with r=8 gives scale=2. Higher alpha = stronger adaptation.
            self.A = nn.Parameter(torch.randn(in_dim, rank) * 0.01)
            # A: random small values (std=0.01). This is the "down-projection" — compresses input to rank.
            self.B = nn.Parameter(torch.zeros(rank, out_dim))
            # B: initialized to zeros. This is the "up-projection" — expands back to output dim.
            #    Starting B as zeros means LoRA adds NOTHING at first (delta_W = 0).
            #    Only gradients flow into A and B, not the frozen base weights.
            self.scale = alpha / rank
            # scale = alpha/r controls how much the LoRA path contributes.
            #   alpha=16, r=8  -> scale=2   (moderate adaptation)
            #   alpha=64, r=8  -> scale=8   (strong adaptation)
            #   alpha=8,  r=8  -> scale=1   (weak adaptation)
            # Rule: start alpha=16 for r=8. Increase if underfitting, decrease if overfitting.

        def forward(self, x):
            # Forward: scale * (x @ A @ B)
            # This equals scale * (x @ delta_W) where delta_W = A @ B
            return self.scale * (x @ self.A @ self.B)
            # x @ A: project input down to rank dimensions (compression)
            # (x @ A) @ B: project back up to output dimensions (expansion)
            # scale * result: apply the adaptation strength

    class LinearWithLoRA(nn.Module):
        def __init__(self, linear, rank, alpha):
            super().__init__()
            self.linear = linear
            for p in self.linear.parameters():
                p.requires_grad = False
                # Freeze the original linear layer — no gradients flow here.
                # Only the LoRA adapter (A and B matrices) gets trained.
                # This is why LoRA uses ~0.1% of the params vs full fine-tune.
            self.lora = LoRALayer(linear.in_features, linear.out_features, rank, alpha)
            # The LoRA adapter mirrors the linear layer's dimensions.
            # in_features -> rank -> out_features (bottleneck)

        def forward(self, x):
            # Combined forward: original_output + adapter_output
            # = W*x + (alpha/r) * (x @ A @ B)
            return self.linear(x) + self.lora(x)   # W*x + delta_W*x

  Forward pass: W*x + (alpha/r)*A*B*x
  A is initialized small (randn*0.01), B as zeros → delta_W = A@B = 0 at start.
  Training only updates A and B. The original W stays frozen.

--- Using LoRA with HuggingFace PEFT ---

  pip install peft transformers datasets

  from transformers import AutoModelForCausalLM
  from peft import LoraConfig, get_peft_model

  model = AutoModelForCausalLM.from_pretrained("meta-llama/Llama-2-7b-hf")

  lora_config = LoraConfig(
      # r (rank): the bottleneck dimension for low-rank decomposition.
      #   rank=8 means each adaptor matrix is (dim x 8) and (8 x dim).
      #   Why 8? It's the sweet spot: enough capacity to learn task-specific patterns,
      #   small enough to keep trainable params ~0.1% of total.
      #   Think of r as the "width of the information channel" for adaptation.
      r=8,

      # lora_alpha: scaling factor for the LoRA update.
      #   The actual update is: scale * A @ B  where scale = alpha / r.
      #   With alpha=16 and r=8: scale = 2. The LoRA path is amplified 2x.
      #   Why 16? Empirically works well as 2x the rank. Most papers use 8-32.
      #   Higher alpha = more aggressive adaptation (use if task is very different from pretraining).
      #   Lower alpha = more conservative (use for similar tasks to avoid catastrophic forgetting).
      lora_alpha=16,

      # target_modules: which linear layers in the transformer get LoRA adaptors.
      #   ["q_proj", "v_proj"] means ONLY the Query and Value projection matrices
      #   in each attention head get adapted. This is the most common and efficient choice.
      #   Why Q and V? Research shows adapting just Q and V captures most task-specific
      #   patterns while being parameter-efficient.
      #   Other options:
      #     ["q_proj", "k_proj", "v_proj", "o_proj"] — all attention (more params, more expressive)
      #     ["q_proj", "v_proj", "gate_proj", "up_proj", "down_proj"] — attention + FFN (full fine-tune)
      #   Rule: start with Q,V. Add K,O if underfitting. Add FFN if still underfitting.
      target_modules=["q_proj", "v_proj"],

      # lora_dropout: dropout rate applied to the LoRA adapter output.
      #   0.05 = 5% dropout. Helps prevent overfitting when fine-tuning on small datasets.
      #   Higher dropout (0.1-0.2) for very small datasets (<1000 examples).
      #   Lower dropout (0.0-0.05) for large datasets (>10000 examples).
      #   Why dropout on LoRA? Since LoRA has very few params, even 5% dropout provides
      #   meaningful regularization.
      lora_dropout=0.05,

      # bias: how to handle bias parameters during LoRA training.
      #   "none" = don't train bias terms at all (most efficient, recommended).
      #   "lora_only" = train only biases that belong to LoRA layers.
      #   "all" = train all bias parameters (defeats the purpose of LoRA efficiency).
      #   Why "none"? Biases are a tiny fraction of total params (~0.001%) and
      #   training them adds complexity with minimal benefit.
      bias="none",

      # task_type: what kind of model you're fine-tuning.
      #   CAUSAL_LM: causal language model (GPT, Llama, Mistral, Qwen) — predicts next token
      #   SEQ_CLS: sequence classification (BERT, RoBERTa) — classifies entire input
      #   SEQ2SEQ_LM: encoder-decoder (T5, BART) — sequence-to-sequence generation
      #   Why CAUSAL_LM? Llama-2 is a causal/decoder-only model. This tells PEFT to
      #   add LoRA adaptors to the correct layers for next-token prediction.
      task_type="CAUSAL_LM",
  )

  model = get_peft_model(model, lora_config)
  model.print_trainable_parameters()
  # trainable params: ~4.2M || all params: ~6.7B || trainable%: 0.06%
  # 4.2 million trainable out of 6.7 billion = only 0.06% of the model is being trained.
  # This is the entire point of LoRA — you can fine-tune a 7B model on a single GPU.

--- Full LoRA Training Script ---

  (from your notes -- runnable as-is)

  import torch
  from transformers import AutoModelForCausalLM, AutoTokenizer
  from peft import LoraConfig, get_peft_model, TaskType
  from datasets import Dataset
  from transformers import TrainingArguments, Trainer

  tokenizer = AutoTokenizer.from_pretrained("meta-llama/Llama-2-7b-hf")
  tokenizer.pad_token = tokenizer.eos_token
  model = AutoModelForCausalLM.from_pretrained(
      "meta-llama/Llama-2-7b-hf",
      torch_dtype=torch.float16,
      device_map="auto",
  )

  # r=8: bottleneck dim. 8 is the default sweet spot (enough capacity, minimal params).
  # lora_alpha=16: scale = 16/8 = 2. Controls how strongly LoRA adapts.
  # target_modules=["q_proj","v_proj"]: only Query & Value projections get adaptors.
  #   q_proj = the "what to attend to" weights in attention.
  #   v_proj = the "what information to carry" weights in attention.
  #   Together: LoRA learns better what to focus on (Q) and what to remember (V).
  # lora_dropout=0.05: 5% dropout for regularization on small datasets.
  # bias="none": don't train bias terms (tiny params, negligible benefit).
  # task_type=TaskType.CAUSAL_LM: tells PEFT this is a next-token prediction model.
  lora_config = LoraConfig(r=8, lora_alpha=16,
      target_modules=["q_proj", "v_proj"],
      lora_dropout=0.05, bias="none", task_type=TaskType.CAUSAL_LM)
  model = get_peft_model(model, lora_config)
  model.print_trainable_parameters()

  train_data = [{"text": "Once upon a time, there was a brave knight..."}]
  dataset = Dataset.from_list(train_data)

  def tokenize(examples):
      return tokenizer(examples["text"], truncation=True, padding="max_length", max_length=128)
  tokenized_dataset = dataset.map(tokenize, batched=True)

  trainer = Trainer(
      model=model,
      args=TrainingArguments(
          output_dir="./lora-llama2-output",
          num_train_epochs=3,
          per_device_train_batch_size=4,
          learning_rate=2e-4,
          fp16=True,
      ),
      train_dataset=tokenized_dataset,
  )
  trainer.train()
  model.save_pretrained("./lora-llama2-adapter")

--- QLoRA (Quantized Low-Rank Adaptation) ---

  # ponytail: like LoRA, but the base model is 4-bit quantized. Fit 70B on one GPU.

  --- What is QLoRA? ---

    QLoRA = Quantized LoRA. Same LoRA adapters on top, but the BASE MODEL is
    loaded in 4-bit (instead of 16-bit). This cuts memory by ~4x while adding
    only ~1% performance loss.

    LoRA alone:     7B model needs ~16GB VRAM (full 16-bit base + small adapters)
    QLoRA:          7B model needs ~5GB VRAM (4-bit base + same small adapters)
    QLoRA on 70B:   70B model fits on a single 48GB GPU (impossible with LoRA alone)

  --- Key Innovations (3 things make QLoRA work) ---

    1. 4-bit NormalFloat (NF4):
       A custom data type optimized for neural network weights.
       Normal distribution -> map to 16 evenly-spaced quantiles.
       Better than standard int4 because it allocates more precision
       to values near zero (where most weights live).
       Memory: 16-bit -> 4-bit = 4x reduction.

    2. Double Quantization (DQ):
       Quantize the quantization constants themselves (fp32 -> fp8).
       Saves ~0.5 bits per parameter on top of NF4.
       Why? Each 4-bit group needs a scaling constant in fp32.
       DQ quantizes those constants too, saving ~3GB on a 70B model.

    3. Paged Optimizers:
       Use CPU RAM as swap space for optimizer states.
       When GPU runs out of memory during training,
       optimizer pages move to CPU automatically.
       Prevents OOM errors without sacrificing throughput.

  --- LoRA vs QLoRA ---

    | Aspect         | LoRA                    | QLoRA                        |
    |----------------|-------------------------|------------------------------|
    | Base dtype     | float16 / bfloat16      | 4-bit NF4                    |
    | VRAM (7B)      | ~16GB                   | ~5GB                         |
    | VRAM (70B)     | ~140GB (needs 4 GPUs)   | ~48GB (1 GPU)                |
    | Speed          | faster (no quant/dequant)| slower (quant overhead)      |
    | Quality loss   | none                    | ~1% (NF4 is remarkably good) |
    | Trainable %    | ~0.1% (same as LoRA)    | ~0.1% (same adapters)        |

  --- QLoRA Training Script ---

    pip install bitsandbytes transformers peft

    import torch
    from transformers import AutoModelForCausalLM, AutoTokenizer, BitsAndBytesConfig
    from peft import LoraConfig, get_peft_model, TaskType
    from datasets import Dataset
    from transformers import TrainingArguments, Trainer

    # Step 1: 4-bit quantization config
    # This is what makes QLoRA different from LoRA
    bnb_config = BitsAndBytesConfig(
        load_in_4bit=True,                          # use 4-bit NF4 quantization
        bnb_4bit_quant_type="nf4",                  # NormalFloat (best for weights)
        bnb_4bit_compute_dtype=torch.float16,       # compute in fp16 for speed
        bnb_4bit_use_double_quant=True,             # quantize the quantization constants
    )

    # Step 2: Load model in 4-bit (not 16-bit like in LoRA)
    model = AutoModelForCausalLM.from_pretrained(
        "meta-llama/Llama-2-7b-hf",
        quantization_config=bnb_config,             # <-- QLoRA: 4-bit loading
        device_map="auto",
    )

    tokenizer = AutoTokenizer.from_pretrained("meta-llama/Llama-2-7b-hf")
    tokenizer.pad_token = tokenizer.eos_token

    # Step 3: LoRA config on top of 4-bit base (IDENTICAL to LoRA config)
    lora_config = LoraConfig(
        r=8,
        lora_alpha=16,
        target_modules=["q_proj", "v_proj"],
        lora_dropout=0.05,
        bias="none",
        task_type=TaskType.CAUSAL_LM,
    )

    # Step 4: Wrap with PEFT (same call as LoRA)
    model = get_peft_model(model, lora_config)
    model.print_trainable_parameters()

    # Step 5: Train (same as LoRA)
    train_data = [{"text": "Once upon a time..."}]
    dataset = Dataset.from_list(train_data)

    def tokenize(examples):
        return tokenizer(examples["text"], truncation=True, padding="max_length", max_length=128)
    tokenized_dataset = dataset.map(tokenize, batched=True)

    trainer = Trainer(
        model=model,
        args=TrainingArguments(
            output_dir="./qlora-output",
            num_train_epochs=3,
            per_device_train_batch_size=4,
            learning_rate=2e-4,
            fp16=True,
        ),
        train_dataset=tokenized_dataset,
    )
    trainer.train()
    model.save_pretrained("./qlora-adapter")

  --- The Critical Difference in 1 Sentence ---

    LoRA:     load model in 16-bit, freeze weights, add adapters
    QLoRA:    load model in 4-bit, freeze weights, add adapters

    Everything else (LoRA config, training loop, saving) is identical.
    The magic is that 4-bit base model takes 4x less VRAM.

  --- When to Use Which ---

    Use LoRA  when: you have enough VRAM (e.g., 7B on a 24GB card)
    Use QLoRA when: you want to fine-tune a larger model (e.g., 70B on one 48GB card)
                     or you only have a consumer GPU (e.g., 7B on an 8GB card)

================================================================================
31. MCP (MODEL CONTEXT PROTOCOL)
================================================================================

--- What is MCP? ---

  Your note: "wat is mcp?"

  MCP (Model Context Protocol) is an open standard that lets LLMs
  interact with EXTERNAL TOOLS AND DATA SOURCES in a structured way.

  Think of it as "USB-C for AI" -- a universal connector that lets any
  LLM work with any tool or data source without custom integrations.

--- Architecture ---

  Host/Client (OpenWork, Claude) <--> MCP Server (tools, resources, prompts)

--- Three Core Decorators ---

  1. @mcp.tool -- exposes a function as an ACTION the LLM can call
     Use for: API calls, calculations, file ops, DB queries

  2. @mcp.resource -- exposes READ-ONLY DATA via a URI
     Use for: files, config, DB records

  3. @mcp.prompt -- defines a reusable PROMPT TEMPLATE
     Use for: standard workflows, guided interactions

--- Key Benefits ---

  - Standardization: one protocol for all tool integrations
  - Security: host controls which MCP servers are allowed
  - Reusability: share MCP servers across different LLM apps
  - Simplicity: write a Python function, add a decorator, done

--- MCP Servers (Examples) ---

  Pre-built: Filesystem, GitHub, Database, Web, Slack, Puppeteer
  Custom: pip install mcp && decorate your functions

================================================================================
32. AGENTIC AI & RAG COMPONENTS
================================================================================
# ponytail: condensed overview -- see Sections 20, 21 for full detail

--- What is an AI Agent? ---

  Your note:
    "what is ai agent? an ai agent is a software program powered by an llm
     tha can percieve->reason->act->learn"

  An AI Agent is an LLM-powered system with a loop:
    Perceive -> Reason -> Act -> Learn

  Core equation (from your notes):
    LLM (brain) -> Tools (hands) -> Memory (context) -> Planner (strategy)

--- Why We Need AI Agents ---

  Problems agents solve:
    - Context Limit: agents retrieve only what's needed
    - Static Responses: agents can call APIs, run code
    - Tool Fragments: agents coordinate multiple tools
    - Repetitive Work: agents automate multi-step processes
    - Information Overload: agents filter before presenting

  Use cases: customer support, code generation, research automation,
  data analysis, DevOps, personal assistant

--- RAG Components ---

  Components:
    - Embedding Model:   converts text to vectors
    - Vector DB:         stores and searches vectors
    - Prompt Template:   "Using this context, answer..."
    - LLM:               generates the answer

  Phases:
    1. Query:            user asks a question
    2. Embed & Search:   convert query to vector, search Vector DB
    3. Build Context:    retrieved chunks + query + system prompt
    4. Generate:         LLM reads context and answers

--- Embeddings Definition ---

  Your note: "embeddings-turing text into vectors / defination"

  An embedding is a list of numbers (a vector) representing the MEANING
  of text. Similar texts have similar vectors. Typical: 384-3072 dimensions.

--- Vector Database Definition ---

  Your note: "vectordatabases:-fast similarity search / defination"

  A Vector DB stores embeddings and supports fast nearest-neighbor (ANN)
  search. Options: Chroma, FAISS, Pinecone, Weaviate, Qdrant, pgvector.
  All support: cosine/euclidean/dot-product, metadata, store original text.

--- Retrieval Definition ---

  Your note: "retrical--finding the right context / defination"

  Retrieval is finding relevant document chunks for a query.

  Strategies:
    - Similarity Search:     nearest neighbors by vector distance
    - MMR:                   balance relevance + diversity
    - Hybrid Search:         semantic (vector) + keyword (BM25)
    - Multi-Query:           multiple query variations
    - Recursive Retrieval:   retrieve, then retrieve more

--- Chunking ---

  Your note: "chunking---splitting documents intelligently"

  Splitting docs into pieces for embedding.
    Too small: loses context
    Too large: dilutes meaning

  Strategies:
    - Recursive Character Splitting: by newline -> period -> space
    - Semantic Chunking: at topic boundaries
    - Agentic Chunking: LLM decides where to split

  Rule of thumb: 256-1024 tokens per chunk, 10-20% overlap.

--- AI Agent Frameworks Comparison ---

  | Framework      | Language   | Best For                                      |
  |----------------|------------|-----------------------------------------------|
  | LangChain      | Python     | General agent & RAG pipelines                 |
  | LangGraph      | Python     | Stateful multi-agent workflows (graphs)       |
  | CrewAI         | Python     | Role-based multi-agent collaboration          |
  | LlamaIndex     | Python     | Data indexing & retrieval for RAG             |
  | AutoGen        | Python     | Multi-agent conversations & automation        |
  | Dify           | Python     | Low-code LLM app platform (visual builder)    |

--- Hands-On: Quick Examples ---

  # LangChain: simple RAG chain
  from langchain_core.prompts import ChatPromptTemplate
  from langchain_openai import ChatOpenAI
  prompt = ChatPromptTemplate.from_template("Answer using: {context}\nQ: {q}")
  chain = prompt | ChatOpenAI()
  # chain.invoke({"context": "...", "q": "your question"})

  # CrewAI: two agents collaborate
  from crewai import Agent, Task, Crew
  writer = Agent(role="Writer", goal="Write content", backstory="I write.", llm="gpt-4")
  editor = Agent(role="Editor", goal="Polish content", backstory="I edit.", llm="gpt-4")
  task = Task(description="Write about AI", agent=writer)
  crew = Crew(agents=[writer, editor], tasks=[task])
  # crew.kickoff()

  # LlamaIndex: query documents
  from llama_index.core import VectorStoreIndex, SimpleDirectoryReader
  docs = SimpleDirectoryReader("./docs").load_data()
  index = VectorStoreIndex.from_documents(docs)
  # index.as_query_engine().query("your question")

  # AutoGen: two-agent chat
  from autogen import AssistantAgent, UserProxyAgent
  assistant = AssistantAgent("assistant", llm_config={"config_list": [{"model": "gpt-4"}]})
  user = UserProxyAgent("user", code_execution_config={"work_dir": "coding"})
  # user.initiate_chat(assistant, message="Write a Python script")

  # Dify: uses visual builder (drag-and-drop), SDK for programmatic access
  # pip install dify-client
  # from dify_client import DifyClient
  # client = DifyClient("your-api-key")

================================================================================
33. LANGCHAIN DEEP DIVE
================================================================================
# ponytail: unified interface for 100+ LLMs, prompt templates, chains, memory, agents, RAG

--- What is LangChain? ---

  LangChain is an open-source framework (created by Harrison Chase, 2022, MIT)
  for building LLM-powered applications. It provides a UNIFIED INTERFACE over
  100+ LLM providers, prompt management, chains, memory, agents, and RAG.

  Core philosophy: "LLM applications are just chains of composable components."

--- Ecosystem ---

  | Library        | Purpose                                                |
  |----------------|--------------------------------------------------------|
  | langchain-core | Framework core: models, prompts, chains, memory, RAG   |
  | langgraph      | Stateful graph-based agent orchestration (cycles/branching) |
  | langsmith      | Debug, test, monitor, evaluate LLM apps + Prompt Hub   |
  | langfuse       | Open-source LLM observability (tracking, eval, cost)   |
  | langserve      | Deploy chains as REST APIs (auto UI, streaming)        |

--- #1: Models (LLMs & Chat Models) ---

  Two categories:
    LLMs:        text-in/text-out (string -> string)
    Chat Models: conversation with system/user/assistant message roles

  Supported: OpenAI, Anthropic, Google, Cohere, HuggingFace, Ollama, Azure, Bedrock...

  Common params: temperature, max_tokens, top_p, stop_sequences
  Supports: streaming, async, batch, function/tool calling

  # Basic chat model (your completed example)
  from langchain_openai import ChatOpenAI

  llm = ChatOpenAI(model="gpt-4", temperature=0.7)
  response = llm.invoke("Explain LoRA in one sentence")
  # "LoRA fine-tunes large models by training small adapter matrices instead of all parameters."

  # With messages
  from langchain_core.messages import HumanMessage, SystemMessage
  messages = [
      SystemMessage("You are a helpful AI tutor"),
      HumanMessage("What is QLoRA?"),
  ]
  print(llm.invoke(messages).content)

--- #2: Prompts & Prompt Templates ---

  Components:
    PromptTemplate:           parameterized string template
    ChatPromptTemplate:       structured message template (system/human/ai roles)
    FewShotPromptTemplate:    few-shot learning examples baked in
    PipelinePromptTemplate:   compose multiple prompts together
    MessagesPlaceholder:      dynamic message injection (e.g., chat history)

  Best practices: be specific, provide context, use examples, format constraints,
  define output structure.

  # PromptTemplate example
  from langchain_core.prompts import PromptTemplate

  template = PromptTemplate.from_template(
      "Explain {topic} as if I'm a {audience}. Use {num_examples} examples."
  )
  prompt = template.invoke({"topic": "LoRA", "audience": "5-year-old", "num_examples": 2})
  # "Explain LoRA as if I'm a 5-year-old. Use 2 examples."

  # ChatPromptTemplate with roles
  from langchain_core.prompts import ChatPromptTemplate

  chat_template = ChatPromptTemplate.from_messages([
      ("system", "You are a {role} expert. Answer concisely."),
      ("human", "{question}"),
  ])
  prompt = chat_template.invoke({"role": "GenAI", "question": "What is QLoRA?"})

--- #3: Output Parsers ---

  Parsers turn unstructured LLM text into structured data:

    PydanticOutputParser:           JSON with Pydantic validation
    CommaSeparatedListOutputParser: "a, b, c" -> ["a", "b", "c"]
    JsonOutputParser:               raw JSON parsing
    StructuredOutputParser:         dict with typed fields
    DateTimeOutputParser:           date/time string -> datetime
    EnumOutputParser:               string -> Enum
    OutputFixingParser:             auto-fix malformed output (retry with error msg)

  # Pydantic parser example
  from langchain_core.prompts import PromptTemplate
  from langchain_core.output_parsers import PydanticOutputParser
  from pydantic import BaseModel, Field

  class StudyNote(BaseModel):
      topic: str = Field(description="topic name")
      summary: str = Field(description="one-line summary")
      difficulty: int = Field(description="difficulty 1-5")

  parser = PydanticOutputParser(pydantic_object=StudyNote)
  prompt = PromptTemplate(
      template="Generate a study note about {topic}.\n{format_instructions}",
      partial_variables={"format_instructions": parser.get_format_instructions()},
  )
  # chain = prompt | llm | parser
  # result = chain.invoke({"topic": "LoRA"})  # returns a StudyNote object

--- #4: Chains & LCEL (LangChain Expression Language) ---

  Chains = sequences of calls: LLM -> parser -> tool -> LLM -> ...

  LCEL uses the | (pipe) operator to compose chains:
    chain = prompt | model | parser
    # Automatic: streaming, async, batch, retry, fallbacks

  Chain types:
    LLMChain:            prompt -> model -> parser
    SequentialChain:     multiple steps in sequence (output of step 1 -> input of step 2)
    RouterChain:         route input to specialized chains
    RunnablePassthrough: pass data through unchanged (for side-effects or debugging)
    RunnableParallel:    run branches in parallel (merge results)

  # Simple chain with LCEL
  from langchain_core.output_parsers import StrOutputParser

  chain = ChatPromptTemplate.from_template("Explain {topic} in one line") | llm | StrOutputParser()
  print(chain.invoke({"topic": "QLoRA"}))
  # "QLoRA loads the base model in 4-bit, cutting VRAM by 4x with only ~1% quality loss."

  # Parallel chain (two questions at once)
  from langchain_core.runnables import RunnableParallel

  chain1 = ChatPromptTemplate.from_template("Explain {topic}") | llm | StrOutputParser()
  chain2 = ChatPromptTemplate.from_template("Give an example of {topic}") | llm | StrOutputParser()
  parallel = RunnableParallel(explanation=chain1, example=chain2)
  result = parallel.invoke({"topic": "LoRA"})
  # result["explanation"] = "...", result["example"] = "..."

--- #5: Memory ---

  Memory lets your LLM app remember past conversation — chat history,
  state persistence across turns.

  Types (from your notes):
    ConversationBufferMemory:         stores ENTIRE history (grows unbounded)
    ConversationBufferWindowMemory:   last K turns only (fixed window size)
    ConversationSummaryMemory:        periodically summarizes old messages
    ConversationSummaryBufferMemory:  hybrid = summary of old + recent verbatim
    VectorStoreRetrieverMemory:       retrieves relevant memories by similarity
    ZepMemory:                        long-term persistent memory (uses Zep server)

  # Buffer memory example
  from langchain.memory import ConversationBufferMemory
  from langchain.chains import ConversationChain

  memory = ConversationBufferMemory()
  chain = ConversationChain(llm=llm, memory=memory)
  chain.predict(input="Hi I'm Mike")    # stores in memory
  chain.predict(input="What's my name?") # retrieves "Mike" from memory

--- #6: Agents & Tools ---

  Agents = LLMs that DECIDE which tools to call, in what order, with what args.

  Three components:
    - Tool:      function the agent can invoke (search, calculator, API, code exec)
    - Agent:     the LLM that reasons about which tool to use
    - Executor:  runs the agent-tool loop (think -> act -> observe -> repeat)

  Agent types:
    Tool-Calling Agent:      LLM natively supports function/tool calling (GPT-4, Claude)
    ReAct Agent:             Reason + Act loop (thought -> action -> observation)
    Plan-and-Execute Agent:  first plan all steps, then execute each one

  # Tool-calling agent example
  from langchain.agents import create_tool_calling_agent, AgentExecutor
  from langchain.tools import tool

  @tool
  def multiply(a: int, b: int) -> int:
      """Multiply two numbers."""
      return a * b

  tools = [multiply]
  prompt = ChatPromptTemplate.from_messages([
      ("system", "You are a helpful assistant"),
      ("human", "{input}"),
      ("placeholder", "{agent_scratchpad}"),
  ])
  agent = create_tool_calling_agent(llm, tools, prompt)
  executor = AgentExecutor(agent=agent, tools=tools)
  executor.invoke({"input": "What is 7 times 8?"})