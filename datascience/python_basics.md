#Python

##Python Data Structures

    x = 36  # this is an integer
    x = 3.14  # a decimal number
    x = True  # Boolean ⋅⋅
    x = "This is a string"
    [ ] # list, mutable sequence
    ( ) # tuple, immutable
    { } # dictionary, mapping
    ([ ]) #set  
    print x[0]  #print first element
    top_teams.ix[['NYA','PIT']] #look up index


##Python Basics

    %time # tell you how long something takes to run
    \ #break line

    #list methods:
    l=[]
    l.append(obj) #add object to end of list
    l.count(obj) #returns int nbr of occurences of obj in list
    l.index(obj) #returns index of first occurence
    l.pop([index]) # returns item at specified index
    l.remove(obj) #remove first occurance of obj in list
    l.reverse() #reverse list
    l.sort() #sort list

    range() #creates range of integers
    xrange () #creates an iterator object
    for i, element in enumerate(l): 
       print "Element no", i, "is", element #returns tuple; this is called tuple unpacking; enumerate function lets you iterate both over the index and the elements 

    lambda #functions on the fly
    func = lambda x: 1 + .1 * (x - 4) ** 2 + 4 * np.random.random(len(x))

##Python Slicing

  print l # whole list
  print l[2] #third element
  print l[0:3] #elements 1 through 4
  print l[:3]# first 3 elements
  print l[3:] # elements after and including element 3
  print l[-1] #last element in array
  print l[-3:] #last three elements in array
  print l[:] #same as l, but it creates a copy
  print l[:-2]#everything but last two
  print l[::2] #every second
  print l[::-1] #reverse array

##Python Functions

    #If/else
    if x > 4:
        print "x"
    elif x == 4:
        print "y"
    else:
        print "z"
        
    #For loop
    l = []  # empty list
    for i in range(10):
        l.append(i ** 2)
    print l
    while loop

    #Function: 
    def func (x):
    if x > 4:
        print "x"
    elif x == 4:
        print "y"
    else:
        print "z"
    func(4)
    def f(x):
        return 3*x**2 - 2*x – 7


