# Programming Project #1
### By Yisheng Huang (PID yisheng9)
This blog will record some of my problems and solutions about the first project. This project consists of two major parts:

  - Roman Numeral/Arabic numeral converter using Go language
  - Domain-Specific Language for trading stocks in Java language

# Part I a

  - Read a Roman numeral and write the corresponding Arabic numeral to standard output.

You can also:
  - Input a correctly formatted Roman numeral and get the corresponding Arabic numeral as output.
  - Input a correctly formatted Arabic numeral and get the corresponding Roman numeral as output.
  - If the input is anything else, output "nulla"

I will assume that as long as your input comprises exclusively Roman numeric symbols or exclusively Arabic numeric symbols, the input is considered correctly formatted.

### How to Run

Just need to pass the Input to Part01A.exe and the program will work properly:
For example,
```sh
$ .\Part1A.exe III →  3
$ .\Part1A.exe 4→IV 
$ .\Part1A.exe X5V → nulla
$ .\Part1A.exe IX → 9
$ .\Part1A.exe Royal → nulla 
$ .\Part1A.exe 37 →XXXVII 
$ .\Part1A.exe MCMXCVIII → 1998
$ .\Part1A.exe 34X →nulla
```

# Part I b

  - On the basis of the previous, I added a few new rules

They are, respectively:
  - rule 1: The letters in a numeral must appear in this precedence order: M D C L X V I
Subtractive rules no longer apply .
  - rule 2: We can’t have the same letter repeated more than 4 times.
  - rule 3: We can’t repeat the characters V, L, and D.

In response display the following messages when break rules:
  - When the input breaks rule 1., my program will display: “You are a Royal 🐶”
  - When the input breaks rule 2., my program will display: “You are a Royal 🐴”
  - When the input breaks rule 3., my program will display: “You are a Royal 🐸”

### How to Run

Just need to pass the Input to Part01A.exe and the program will work properly:
For example,
```sh
$ .\Part1B.exe IIII  → 4
$ .\Part1B.exe XXXX  → 40
$ .\Part1B.exe XIIII → 14
$ .\Part1B.exe LXXVIIII → 79
$ .\Part1B.exe IV  → You are a Royal 🐶
$ .\Part1B.exe XXXXX → You are a Royal 🐴 
$ .\Part1B.exe L → 50
$ .\Part1B.exe MDCCCLXXXVIII → 1888
$ .\Part1B.exe MCMXCIX → You are a Royal 🐶
$ .\Part1B.exe MDCCCCLXXXXVIIII → 1999
$ .\Part1B.exe MDDCLXVII → You are a Royal 🐸
```


### Some thoughts on Part 1

Go language does not have the concept of classes and inheritance, instead of struct, interface and methods, so it looks different from Java or C++. Handling Roman numerals and Arabic numerals is easy to implement for the Go language. I can’t see emoticons in the CMD of windows, so I installed Windows Terminal. In general, the first part is easy to achieve.

# Part 2 a

  - Read a domain-specific language (DSL) for trading stocks and output SQL operations.

DSL will have the following grammar:
  - <stock_trade_requests> →  ‘For account' <acct_ident> ‘(' <trade> {‘,’ <trade>} ‘).’ 
  - <trade> → <number> <stock_symbol> ‘shares’ (‘buy at max' | ‘sell at min') <number>
  - <number> →  [1-9] {[0-9]}
  - <stock_symbol> → 'AAPL'|'HP'|'IBM'|'AMZN'|'MSFT'|'GOOGL'|'INTC'|'CSCO'|'ORCL'|'QCOM'
 -  <acct_ident> →  ‘“‘alpha_char { alpha_char | digit | ’_’} ‘“‘


The parser should output a sequence of SQL INSERT operations that would realize the requested trades:
```sql
INSERT INTO BuyRequests(NumShares, Symbol, MaxPrice, AccountID) VALUES(‘100’, ‘IBM’, ‘45’,  ‘Hokie123’)
INSERT INTO SellRequests(NumShares, Symbol, MinPrice, AccountID) VALUES(‘40’, ‘ORCL’, ‘25’, ‘Hokie123’)
```

### How to compile & run
For compile, we need use:
```sh
$ javac .\Part2A.java
```
I added a txt test file to run the test:
For example,
```sh
$ cat test2A.txt | java Part2A
```

# Part 2 B

  - Read a domain-specific language (DSL) for cancle all trading SQLs and output SQL operations.

DSL will have the following grammar:
 - <stock_trade_requests> →  ‘For account' <acct_ident> 'cancle (' <stock_symbol>  { ',' <stock_symbol> } ').'
 - <stock_symbol> → 'AAPL'|'HP'|'IBM'|'AMZN'|'MSFT'|'GOOGL'|'INTC'|'CSCO'|'ORCL'|'QCOM'
 - <acct_ident> →  '"'alpha_char { alpha_char | digit | '_'} '"'



The parser should output a sequence of SQL INSERT operations that would realize the requested trades and each stock symbol need 2 operations because we have 2 tables:
```sql
DELETE FROM BuyRequests WHERE (Symbol='GOOGL') AND (AccountID='Hokie123')
DELETE FROM SellRequests WHERE (Symbol='GOOGL') AND (AccountID='Hokie123')
```

### How to compile & run
For compile, we need use:
```sh
$ javac .\Part2B.java
```
I added a txt test file to run the test:
For example,
```sh
$ cat test2B.txt | java Part2B
```


### Some thoughts on Part 2

I wrote many lines of code for the second part. After I finished writing, I found that I don’t need a lot of useless judgments, I should use the helper method since many repeated judgments are not worthwhile and are prone to bugs. The hardest part is to determine the error location and output the "^" symbol. I started writing this project in a short period of only three days, and I should try to start it when it comes up. 😂😂😂

License
----

MIT
