--- 
layout: post
title: Parsing command line arguments with JOpt Simple 
tags: 
- Java
status: publish
type: post
published: true
--- 

The other day whilst doing some programming for my final year project I stumbled across a really useful library for parsing command line arguments from a Java program.

[JOpt Simple][1] is a Java library for parsing command line options, like the type you might give to ls or find. The supported syntax is very similar to Unix option syntax provided by getopt() and getopt_long(), which pretty much translates to standard Unix argument syntax: --name David, -N 6 and so on In order to parse some particular options, setup is pretty simple: 
    
    OptionParser parser = new OptionParser( "aB?" );
    
OptionParser is provided in the package joptsimple. This one line creates a parser that will accept options -a, -B and -? To parse some string containing the arguments, for example the args[] array from the main method of any Java class you simply run the parsers parse method on the array of Strings: [code lang="java" light="true"] OptionSet options = parser.parse("-a", "-B"); [/code] You can now just use the has() method on the option set in order to see whether a certain argument has been set, for example: [code lang="java" light="true"] options.has("a"); [/code] So that's a very brief overview, I'm going to skip over the middleground of examples, which you can find 

[here][2], and present a more specific use-case which I found particularly applicable. 
#### Converting Option Arguments to Other Types 

Whilst this is detailed in the on the [examples][2] page of the Jopt Simple website, I wanted to present it here because I found it so useful. 

[code lang="java" light="true"] OptionParser parser = new OptionParser(); parser.accepts( "count" ).withRequiredArg().ofType( Integer.class ); parser.accepts( "file" ).withRequiredArg().ofType( File.class ); [/code] 

The above code constructs a parser that accepts the long arguments --count and --file. Both options have a required argument. Since both Integer and File contain a constructor method which takes a String, JOpt Simple can use this to convert the value of the option to your preferred type when parsing. 

Following the above example, if I wanted to parse in a File - for reading perhaps - I would simple put that as the value of the --file argument. For example --file myFile.txt Once I have created the OptionSet by parsing the array containing the Strings corresponding to the arguments, I can use options.valueOf("file") in order to directly access the file created from the string "myFile.txt", like so: [code lang="java" light="true"] File parsedFile = options.valueOf("file"); [/code]

The ultimate use I had for JOpt Simple was to create an "Arguments" class, which encapsulated all this processing. I constructed the parser inside a static block, then I could simple create a new parser and give it the string[] of arguments that I had received inside my main method. I then had calls which allowed me to get specific items from the arguments - a file, a string, and some integer values. This encapsulation allowed me to reuse the object in multiple location whenever I needed to parse some options from the command line. I highly recommend JOpt Simple for it's great API, good documentation, and most of all, its ease of use.

 [1]: http://jopt-simple.sourceforge.net
 [2]: http://jopt-simple.sourceforge.net/examples.html
