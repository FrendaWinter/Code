# Ruby

# General

Lib management of Ruby call `gem`

### ri

For read document

**Syntax:** ri {{lib}}

**Eg:** ri GC ri GC::enable ~ lib::function

### new

song1 = Song.new(“Ruby Tuesday”) 

song2 = Song.new(“Enveloped in Python”) 

song1 and song 2 have different object ID

**instance variables:** variables with values that are unique to each instance. **instance methods:**

It’s worth noting here a major difference between Ruby and most other languages. In (say) Java, you’d find the absolute value of some number by calling a separate function and passing in that number. You could write this:

`num = Math.abs(num) // Java code`

In Ruby, the ability to determine an absolute value is built into numbers—they take care of the details internally. You simply send the message abs to a number object and let it do the work:

`num = -1234 # => -1234` `positive = num.abs # => 1234`

The same applies to all Ruby objects. In C you’d write strlen(name), but in Ruby it would be name.length, and so on. This is part of what we mean when we say that Ruby is a genuine object-oriented language.

**Mutiple declare** a, b, c = 10, 20, 30

**Double-quoted case, Ruby does more work.** - First, it looks for substitutions `\n` - **Expression interpolation** `result = "Good night, #{name}"`

## Name

- Local variables, method parameters, and method names should all start with a lowercase letter or an underscore.
- Global variables are prefixed with a dollar sign ($), and instance variables begin with an “at” sign (@).
- Class variables start with two “at” signs (@@).
- Finally, class names, module names, and constants must start with an uppercase letter

## NULL

In many languages, the concept of `nil` (or `null`) means **“no object.”** **In Ruby, that’s not the case; nil is an object, just like any other, that happens to represent nothing.** ## Array

Short way to create string array `a = %w{ ant bee cat dog elk }` ~ `a = [ 'ant', 'bee', 'cat', 'dog', 'elk' ]`

## Hash

Key-value

```ruby
inst_section = {'cello' => 'string','clarinet' => 'woodwind',}
```

A hash by default returns `nil` when indexed by a key it doesn’tcontain -> Sometimes you’ll want to change this default

```ruby
histogram = Hash.new(0) # The default value is zero
histogram['ruby'] # => 0
histogram['ruby'] = histogram['ruby'] + 1
histogram['ruby'] # => 1
```

Keys in a particular hash must be unique

### Symbols

Like define in C++. In Ruby, 2 Way to declare

```ruby
NORTH = 1EAST = 2walk(NORTH)look(EAST)
```

```ruby
inst_section = {:cello => 'string',:clarinet => 'woodwind'}
# OR
inst_section = {cello: 'string',clarinet: 'woodwind'}
# Use
inst_section[:oboe]
inst_section[:cello]
```

### Control Structures

Ruby uses the keyword end to signify the end of a body of all the control structures:

```ruby
if radiation > 3000    puts "Danger, Will Robinson"end
```

Here it is again, rewritten using a statement modifier:

```ruby
puts "Danger, Will Robinson" if radiation > 3000
```

Most statements in Ruby return a value, which means you can use them as conditions

```ruby
while line = gets  # gets~Read input of user    
	puts line.downcase
end
```

### Regular expression

**Build in** The match operator `=~` .If the pattern is found in the string, `=~` returns its starting position; otherwise, it returns `nil`. This means you can use regular expressions as the condition in `if` and `while` statements `if line =~ /Perl|Python/` Use in Function

```ruby
newline = line.sub(/Perl/, 'Ruby') # replace first 'Perl' with 'Ruby'
```

## Blocks and Iterators

Block of code ~ Same same with closure in Java

Insert `yield` to call block in function

`yield` can call with argument like `(|params...|)`

E.g:

```ruby
def who_says_what
	yield("Dave", "hello")
	yield("Andy", "goodbye")
end

who_says_what {
	|person, phrase| 
	puts "#{person} says #{phrase}"
}
```

### Code blocks are used throughout the Ruby library to implement iterators

```ruby
animals = %w( ant bee cat dog ) 
# create an array
animals.each {|animal| puts animal } 
# Use code block to interator over all content
```

## Class

```ruby
class BookInStock    
	def initialize(isbn, price) 
		# initialize is a special method in Ruby programs        
		@isbn = isbn    
		# @isbn is instance variables        
		@price = Float(price)    
	end    
	def to_s 
	# Override to_s function to change default behaviour of puts        
	"ISBN: #{@isbn}, price: #{@price}" 
	# -> puts BookInStock -> ISBN: isbn1, price: 3.0    
	end
end
```

Noted `@isbn` and `@price` can use in to_s function. That shows how instance variables work—they’re stored with each object and available to all the instance methods of those objects.

### p method

If using `p method` for class it will display more details

```ruby
b1 = BookInStock.new("isbn1", 3)p b1#<BookInStock:0x007fac4910f3e0 @isbn="isbn1", @price=3.0># if puts: <BookInStock:0x007fb424847468>
```

### Objects and Attributes

`Instance variables` is **private** ~ internal state `Attributes` is a member that can access from externally

- Long way

```ruby
# Class declare with @isbn and @pricedef isbn    @isbnend
```

- Short way

```ruby
class BookInStoc    
attr_reader :isbn, :price 
# attr_reader creates these attribute reader methods for you
```

### Writable att

Attribute can be write outside of object by creating a Ruby method whose name ends with an equals sign -> Can be use in assignments

```ruby
def price=(new_price)    
@price = new_priceend
# book.price = new_price
# Again, Ruby provides a shortcut for this
class BookInStock    
attr_reader :isbn    
attr_accessor :price # Set menthod
```

### Virtual Attributes

```ruby
class BookInStock    
	attr_reader :isbn    
	attr_accessor :price    
	def initialize(isbn, price)        
		@isbn = isbn       
		@price = Float(price)    
	end   
 
	def price_in_cents  
	# Virtual Attributes, def with name. You can call it like v ariable        
		Integer(price*100 + 0.5)    
	end    

	def price_in_cents=(cents) 
	# Can use set menthod to change this Virtual Attributes       
	 @price = cents / 100.0    
	end
end
```

**Why:** - Hiding the difference between `instance variables` and `calculated values` -> shielding other from the implementation of your class. You’re free to change how things work in the future without impacting the millions of lines of code that use your class - The internal state is held in `instance variables`. The external state is exposed through methods we’re calling `attributes`

### Call another lib

`require_relative 'book_in_stock'`

### Access

1. private
2. protected
3. public

## Variable

Is the referernt of object

```ruby
p1 = "a" # p1 is a reference for object string have value a
p2 = p1  
# p2 = p1 also is reference of that object
p1[0] = "b" 
# Change value of the referentp p1 
# bp p2 
# b -> p2 is referent of that so it have value b
```

But I have the code like

```ruby
p1 = "a" # p1 is a reference for object string have value a
p2 = p1  
# p2 = p1 also is reference of that objectp1 = "b" # Different here is it assign to new object, dettach from the previour onep p1 # b -> referent of new object so it is bp p2 # a -> p2 is referent of the old string so it have value b
```

## Operator

`defined?` -> returns `nil` if its argument (which can be an arbitrary expression) is not defined `&&` `||` `!=` And or not

```ruby
class T    
	def ==(other) 
	# Operator overloading        
	puts "Comparing self == #{other}"        
	other == "value"    
endend
```

`if` >< `unless`

```ruby
a, (b, c), d = 1,2,3,4 # a=1, b=2, c=nil, d=3a, (b, c), d = [1,2,3,4] # a=1, b=2, c=nil, d=4a, (b, c), d = 1,[2,3],4 # a=1, b=2, c=3, d=4a, (b, c), d = 1,[2,3,4],5 # a=1, b=2, c=3, d=5a, (b,*c), d = 1,[2,3,4],5 # a=1, b=2, c=[3, 4], d=5
```

## Exception

## Basic Input and Output

```ruby
file = File.new("testfile", "r") # Basic open file (1) file path (2) Mode r read / w write / r+ read-write# If exception throw,  garbage collection will eventually close it, but may take for a while.File.open("testfile", "r") do |file| # Using block after opening, if exception throw, it auto call close    # ... process the fileend
```

### Read iterator

```ruby
File.open("testfile") do |file|    
	file.each_line {|line| puts "Got #{line.dump}" } # use block to loop throught    
	file.each_line("e") {|line| puts "Got #{ line.dump }" } 
	# If pointer match "e", it break and create a line
end
=begin
	Got "This is line"
	Got " one"Got "\nThis is line"
	Got " two\nThis is line"
=end
IO.foreach("testfile") {|line| 
	puts line 
} 
# Closes the file automatically
str = IO.read("testfile") # Retrieve an entire file into a string
str[0, 30] # => "This is line one\nThis is line "arr = IO.readlines("testfile") # Retrieve an entire file into an array of linesarr[0] # => "This is line one\n"
```

### Write

`file.puts "Hello"` simple write `<<` Binary shift

### Network

**low lv:** TCP, UDP, SOCKS, and Unix domain sockets

**lib:** socket

```ruby
require 'socket'client = TCPSocket.open('127.0.0.1', 'www')client.send("OPTIONS /~dave/ HTTP/1.0\n\n", 0) # 0 means standard packetputs client.readlinesclient.close
```

**high lv:** FTP, HTTP, POP, SMTP, and telnet

**lib:** lib/net **More advan lib** ~ recognize Link in file name, handles redirects automatically

```ruby
require 'net/http'http = Net::HTTP.new('pragprog.com', 80)response = http.get('/book/ruby3/programming-ruby-1-9')if response.message == "OK"    puts response.body.scan(/<img alt=".*?" src="(.*?)"/m).uniq[0,3]end
```

### HTML Parsing

1. regular expression -> Simple but not work all the time
2. Use lib nokogiri (Install rails)

```ruby
require 'open-uri'require 'nokogiri'doc = Nokogiri::HTML(open("https://www.youtube.com/?gl=VN"))puts "Page title is " + doc.xpath("//title").inner_html# Output the first paragraph in the div with an id="copyright"# (nokogiri supports both xpath and css-like selectors)puts doc.css('div#copyright p')# Output the second hyperlink in the site-links div using xpath and cssputs "\nSecond hyperlink is"puts doc.xpath('id("site-links")//a[2]')puts doc.css('#site-links a:nth-of-type(2)')
```

# Ruby and the Web

**Common Gateway Interface:** Is a protocol that defines how web servers communicate with external programs, also called CGI scripts. The CGI protocol enables web servers to execute these scripts and generate dynamic content on the fly, such as processing form data, creating database queries, and generating custom responses based on user input.

lib: cgi - Create html - Embed Ruby code into HTML - Cookie - Session IRL: No one use cgi, use rails instead to build web server

## Class

Inheritance `class Child < Parent`

# Regexp support

`=~` return the inddex of the first matching Eg: `/cat/ =~ dog and cat` => 8

`!~` Check if doesnt match

## Change string with regexp support

`str.sub(/reegex/, "String to replace")`

`sub` only replace the first occurrence `gsub` replace all (g for global)

`sub` and `gsub` create a copy and paste it to variable => You can use `sub!` or `gsub!` for changing the original string

`sub!` or `gsub!` only return when it match, nil when no match => Can use in `if` statement

Like other of ruby, Regex is instance of Regex class 3 way to declare regular expressions 1. `/md\/dd/` 2. Regexp.new(“mm/dd”) 3. %r{mm/dd}

### Match

match funtion return `MatchData` format

```ruby
/a/.match(name) # => #<MatchData "a">Regexp.new("all").match(name) # => #<MatchData "all">
```

`MatchData` => Assign to variables and can use `pre_match` or `post_match` functions

`"#{match.pre_match}->#{match[0]}<-#{match.post_match}"` => `show_regexp('very interesting', /t/) # => very in->t<-eresting`

# Exception Class

**Standard exception hierarchy**

```ruby
Exception
  NoMemoryError
  ScriptError
    LoadError
    NotImplementedError
    SyntaxError
  SecurityError
  SignalException
    Interrupt
  StandardError -- default for rescue
    ArgumentError
      UncaughtThrowError
    EncodingError
    FiberError
    IOError
      EOFError
    IndexError
      KeyError
      StopIteration
    LocalJumpError
    NameError
      NoMethodError
    RangeError
      FloatDomainError
    RegexpError
    RuntimeError -- default for raise
    SystemCallError
      Errno::*
    ThreadError
    TypeError
    ZeroDivisionError
  SystemExit
  SystemStackError
```

Use `begin` and `end` block to catch exceptions with keyword `rescue`

```ruby
begin    
# Code executerescue Exception    
# Handle exception    
STDERR.puts "Failed to download #{page}: #{$!}" 
# $! is the referent for error message    
raise # Call raise exception againend
```

When an exception is raised and independent of any subsequent exception handling, Ruby places a reference to the associated exception object into the global variable `$!`

After handle exception, we call `raise` with no parameters, which reraises the exception in `$!`. **This is a useful technique**, because it allows you to write code that filters exceptions, passing on those you can’t handle to higher levels. -> *It’s almost like implementing an inheritance hierarchy for error processing.*

We can use multiple `rescue` in `begin` and `end` block ~ Work like `case` statement. The match will like `parameter===$!`

### System Errors

Each System Errors s a subclass of `SystemCallError` `Errno` is module for System Errors

```ruby
Errno::EAGAIN::Errno # => 35
Errno::EPERM::Errno # => 1
Errno::EWOULDBLOCK::Errno # => 35
```

### Tidying Up

Sometimes you need to guarantee that some processing is done at the end of a block of code, regardless of whether an exception was raised.

Use `ensure`. `ensure` goes after the last rescue clause and contains a chunk of code that will always be executed as the block terminates

```ruby
begin    
# .. process    
rescue    
# .. handle error    
ensure    
# .. Ensure some actionend
```

Sometimes it will be incorrect if you put some code that can cause exception right at beginning and it will be wrong to be execute the `ensure` -> Like `f.open` -> If open fail, file not open -> Ensure `f.close` will be wrong -> Use `else` statement. If present, it goes after the `rescue` clauses and before any `ensure`

Can use `retry` in `rescue` to run again the block if you have a way to fix

```ruby
rescue 
ProtocolError    
if @esmtp then        
	@esmtp = false        
retry    
else        
	raise
end
```

### Raising Exception

Use `raise` to raise an exception

```ruby
raise # Simplly return current exception or RuntimeError if no exception in stackraise "bad mp3 encoding" # Return RuntimeError with given Stringraise InterfaceException, "Keyboard failure", caller # Return give Exception with custom message
```

### Catch and throw

`catch` defines a block that is labeled with the given name (which may be a Symbol or a String). The block is executed normally until a `throw` is encountered. When Ruby encounters a `throw`, it zips back up the call stack looking for a catch block with a matching symbol. When it finds it, Ruby unwinds the stack to that point and terminates the block

```ruby
word_list = File.open("wordlist")catch (:done) do    
result = []    
while line = word_list.gets        
	word = line.chomp        
throw :done unless word =~ /^\w+$/        
	result << word    
end    
puts result.reverseend
```

## Regexp

**Options**

`i` Case insensitive `o` Substitute once `m` Multiline mode ~ dot `.` will match newline too `x` Extended mode ~ Allow new line space to make Complex regex readable

**Anchors**

The patterns `^` and `$` match the beginning and end of a line The sequence `\A` matches the beginning of a string, and `\z` and `\Z` match the end of a string The patterns `\b` and `\B`match word boundaries and nonword boundaries

**Character Classes**

`[]` Match char, `[aeiou]` match one of `aeiou` `[A-F]` Match from A -> F

- Use `^` to negate a character clas

```ruby
show_regexp('Price $12.', /[^A-Z]/) # => P->r<-ice $12.
show_regexp('Price $12.', /[^\w]/) # => Price-> <-$12.
show_regexp('Price $12.', /[a-z][^a-z]/) # => Pric->e <-$12.
```

**POSIX character classes** Special set of charater have a name

[:alnum:] Alphanumeric (Letter | Mark | Decimal_Number) [:alpha:] Uppercase or lowercase letter (Letter | Mark) [:ascii:] 7-bit character including nonprinting [:blank:] Blank and tab (+ Space_Separator) [:cntrl:] Control characters—at least 0x00–0x1f, 0x7f (Control | Format | Unassigned | Private_Use |Surrogate) [:digit:] Digit (Decimal_Number) [:graph:] Printable character excluding space (Unicode also excludes Control, Unassigned, and Surrogate) [:lower:] Lowercase letter (Lowercase_Letter) [:print:] Any printable character (including space) [:punct:] Printable character excluding space and alphanumeric (Connector_Punctuation | Dash_Punctuation | Close_Punctuation | Final_Punctuation | Initial_Punctuation | Other_Punctuation| Open_Punctuation) [:space:] Whitespace (same as ) [:upper:] Uppercase letter (Uppercase_Letter) [:xdigit:] Hex digit (0–9, a–f, A–F) [:xdigit:] Alphanumeric, underscore, and multibyte (Letter | Mark | Decimal_Number | Connector_Punctuation)

## Command Line

- Options
    - Have 2 forms
        - Short term: -d ~ Only one dash and one char ~ Can combine
        - Long form: –debug ~ 2 dash and long explain ~ Can’t combine
    - Have 2 type
        - Switches: On~Off option ~ not take arguments
        - Flags: Take arguments

Typically, if a switch is in the long-form (for example –foo), which turns “on” some behavior, there is also another switch preceded with no- (for example –no-foo) that turns “off” the behavior

Finally, long-form flags take their argument via an equal sign, whereas in the short form of a flag, an equal sign is typically not used.

`Command` ~ For larger and complex app ~ like `git push` ~ `push` is sub command ~ Need separate function for itS

Command-Suite ~ Command line with sub command

---

## Tip and tricks

- Details
    
    ```ruby
    # Ranges
    (1..10) # 1 to 10
    (1...10) # 1 up to 10
    (1..) # 1 to endless
     
    # Ranges bounds checking
    (1..10).cover?(7) # -> True
    
    # Looping in steps
    (10..100).steps(10) do |i|
    	puts i # 10 20 30 40 .. 100
    end
    
    # Ranges good for large amount of elements
    (1..100).last(10) # Get 10 last elements
    ```

## Troubleshoot

- Some issue when install Ruby
    
    ```bash
    # Solution for "cannot load such file -- openssl" on RVM
    https://gist.github.com/Irio/1496746
    ```