## Promo Codes On Scale

You need to design the server of a web page, which sells a product. The web page has a lot of visitors - more than 1 000 000 per month. The marketing team wants you to add a promo code, which is only for the first 10 000 people who claim it. The promo code will be available at a specific date and time. For example, October 10th, 12:00 PM. All the site's users will receive an e-mail newsletter about the promotion two days prior to that date so everyone knows about the code and the huge discount. Lots of people (more than 100 000) will start refreshing the site to try to purchase the product at the same time. How would you handle the server logic? How would you guarantee that exactly 10 000 people will receive the discount?

## Promo Codes On Scale Solution

There are two problems with the above requirements in a typical solution:

If we use a normal database, it may start returning timeouts from the huge load. Even if the database does not block, it will be difficult to check 10 000 promo codes exactly because of the asynchronous nature of the requests. We can use two approaches to fulfill the business requirements:

We can use atomic in-memory storage to save all the people who try to claim the promo codes. There are no chances of timeouts with such a persistence option. After we have more than 10 000 entries saved, we will just extract the first 10 000 of them and store them in the real database. We may create the in-memory storage by ourselves or we may use Redis as a third-party solution. If you are not familiar with Redis - I have a live class about it here in my mentorship feed. Another approach is to use an asynchronous queue with two threads. One thread will write to the queue, and another will read from it. The writing thread will push as many user requests as it can until there are more than 10 000 saved. The reading thread will take one entry at a time and store it in the database. It will do it in a slow and convenient manner so that the real database will not be overloaded with queries. If you are not familiar with multithreading - I have a step-by-step practical guidebook about it here is my mentorship feed. No matter the approach, we need to visualize a loading screen to the user, while the promo codes are processed. Then the browser will periodically poll the server to validate whether the user receives a discount or not.

## Huge Text File

You have a file containing 100 GB of text. Your machine has 8 GB of memory. Your task is to sort the file while keeping the performance in mind and do it as fast as possible. Provide three different solutions:

1. Sort it by characters.
2. Sort it by words.
3. Sort it by lines.

## Huge Text File Solution

It's a question about data structures. Let's see how we can solve it. Obviously, we do not have enough memory to read the whole file, so we need to read and process it in small chunks. 

1. Sorting the text by characters is quite easy. Our chunk size can easily be 1024 symbols or something similar. We can use a plain old sorted hash table to count each character in the text. For example, you will store that you have the symbol "a" 100 times, the symbol "b" 250 times, the symbol "c" 50 times, and so on. After you collect the data, you just need to loop through the data structure keys and write each symbol to the result file the number of times it has occurred.

2. Sorting the text by words is a bit more complicated. We need to consider what is defined as "word", but let's say it is a sequence of letters without any other symbol. There are two approaches to solve the task depending on the available memory. If we have enough memory (8 GB are more than enough if we have only the English alphabet), we can use the so-called Trie data structure. On each node, we can store how many times a specific word has occurred so far. After filling the trie, we can easily traverse it and save the sorted result in a file. The other approach is to use the external merge sort algorithm. The idea is straightforward - the elements cannot be sorted at once as the size is huge, so the data is divided into chunks and then sorted using merge sort. The sorted data is then dumped into multiple files. Then, we can read chunks from these files and perform merge sort on them. Repeating this process will produce a single sorted file.

3. Sorting the text by lines needs to be done with the external merge sort algorithm I explained in the previous point.

## Object Comparison

You need to implement a method which compares two objects. The method's signature is:

public Result AreEqual(object first, object second);

You need to compare the two objects by their data and not by their reference. If the data is the same, you should return a positive result.
Answer the following questions:
1. What kind of algorithm are you going to use to solve the task? 
2. What are the difficulties and the edge cases in this problem? 
3. If there is a difference in the data, how are you going to return the error message? 
4. What is your time estimation for writing a production-ready solution? 

## Object Comparison Solution

1. To compare the objects' data, we will need to traverse all their properties and check whether their values are equal. Since we are working with unknown classes - just generic "object" type, we will need to use reflection to extract what we need. Because objects can be nested - for example, a cat may have an owner, and an owner may have a hometown - we will need to use recursion and perform the same comparison algorithm on each nested object.

2. The edge cases here are quite a lot, and I do not expect people to mention them all without writing any code first, but you should be able to think of at least one or two. You need to consider collections, circular references (by storing somehow that we already visited an object), IComparable implementations, overridden Equals method, and more. Full implementation of the algorithm [here](https://github.com/pirocorp/CSharp-Playground/tree/main/03.%20Deep%20Equality%20Algorithm).

3. We may return simply "true" or "false". However, it will be difficult for the client code to understand where exactly the error is with bigger object hierarchies. For this reason, it is a good idea to have a result object to store the full path of the potential error. 

4. It is a difficult algorithm, so if you are not experienced enough, you should need at least 1 week with all the testing required.
