Download Link: https://assignmentchef.com/product/solved-cs3516-programming-assignment-1-socket-programming
<br>






<strong>Programming Assignment 1: Socket Programming</strong>







<strong>Total Points </strong>

100 (One Hundred)







<h1>Goal</h1>

In this assignment you will be asked to implement an HTTP client and server running a simplified version of the HTTP/1.1 protocol. This project will be completed in either C/C++ using the Unix Socket commands. The program has to run without errors in any CCC machine.




<strong>Step 1: The HTTP Client  </strong>




<em>Execution:</em> Your client should take command line arguments and the GET method to download a web-page. The arguments are as follows:

<ul>

 <li>The <strong>server URL</strong> (<u>http://www.server.com/path/to/file</u>) or an IP address</li>

 <li>The <strong>port</strong> <strong>number</strong> on which to contact the server</li>

 <li>The <strong>options </strong>that which add functionality to the client o –p: prints the RTT for accessing the URL on the terminal before server’s response (i.e., the webpage)</li>

</ul>

For example

./http_client [-options] server_url port_number







<em>Workflow:</em> The client should work as follows:

<ul>

 <li>Connect to the server via a TCP socket</li>

 <li>Submit a valid HTTP/1.1 GET request for the supplied URL.

  <ul>

   <li>Note that: HTTP expects all lines in a request to be terminated with a r
. The last line of the request should only contain a r
 (i.e., empty line)</li>

   <li>Read the server’s response and display it on the terminal</li>

  </ul></li>

 <li>Submit a valid HTTP/1.1 GET request for the supplied URL with the –p option.

  <ul>

   <li>Print the RTT for accessing the URL on the terminal o Read the server’s response and display it on the terminal</li>

  </ul></li>

</ul>




<em>Testing:</em> Use the client to get a file of your choosing from an actual webserver on the Internet. For example,

./http_client www.google.com 80




Use the client to get the provided index.html from your own server program. For example,




./http_client cccworks4.wpi.edu/index.html 7890




Use the client to get a file of your choosing an <em>actual</em> webserver (of your choosing) on the Internet and <em>your own</em> web server using the –p option to compute the RTT between you and the webserver. For example,

./http_client –p www.google.com 80

./http_client –p cccworks4.wpi.edu/index.html 7890

<ul>

 <li>Do this 10 times and compute the average RTT time for both cases. Create a table and show each of the RTT values and the average value.</li>

 <li>You should print the RTT value in milliseconds.</li>

</ul>

<em> </em>




<strong>Step 2: The HTTP Server  </strong>




<em>Execution</em>: Your server should start first (i.e., before the client) and take a command line argument specifying a port number. For example,

./http_server 7890




<em>Workflow</em>: The basic workflow of the server is as follows

<ul>

 <li>Start the server in an infinite loop (you must interrupt your server with a termination signal (e.g., SIGTERM) to stop it)</li>

 <li>Wait for a client connection on the port number specified by command line argument.</li>

 <li>When a client connection is accepted, read the HTTP request.</li>

 <li>Construct a valid HTTP response including status line, any headers you feel are appropriate, and, of course, the requested file in the response body.

  <ul>

   <li>For example, if the server receives the “GET index.html HTTP/1.1” request, it sends out “200 OK” to the client, followed by the file index.html.</li>

   <li>The file index.html has been provided.</li>

   <li>If the requested file doesn’t exist, the server sends out “404 Not Found” response to the client.</li>

  </ul></li>

 <li>Close the client connection and loop back to wait for the next client connection to arrive.</li>

 <li>Make sure your server code shuts down gracefully when terminated. That means closing any open sockets, freeing allocated memory, etc.</li>

 <li><strong>[BONUS POINTS:] </strong>Make the server multi-threaded, which means it can handle as multiple clients at the same time. We will test with at least 5 to 10 clients. (10 extra points)</li>

 <li>The link to the file <strong>html </strong>to be downloaded from your implementation of the web server is available in project documents. Use this as your index.html file at the server.</li>

</ul>




<em>Testing: </em>Use an ordinary browser such as Firefox or Chrome to get an html file from your server. For example, your server is running at host cccworks4.wpi.edu on port number 7890, and there is a file index.html (or TMDG.html) in the current directory. In the URL box of the web browser, type in cccworks4.wpi.edu:7890/index.html or cccworks4.wpi.edu:7890/TMDG.html, the browser should fetch the file and display it. <em> </em>

<strong> </strong>

<strong> </strong>




<h1>Notes</h1>

<ul>

 <li>The HTTP 1.1 standard is available at <u>http://www.w3.org/Protocols/rfc2616/rfc2616.html</u>. Use this to make your client robust in handling the responses you get from different sites while displaying the page. For example, some site specify the size of the page they are returning in the header instead of strictly following the /r/n rule mentioned above.</li>

 <li>Remember we may not test the client with <u>google.com</u> but any arbitrary site.</li>

 <li>Beej’s is an excellent tutorial for socket programming the old-fashioned way</li>

</ul>

(<u>http://beej.us/guide/bgnet/</u>). Check it out.

<ul>

 <li>You must chose a server port number larger that 1023 (to be safe, choose a server port number larger than 5000).</li>

 <li>When you       connect             to         wpi.edu,      you       may      get        hostnames         other     than cccworks4.ccc.wpi.edu (as given the examples above). Please use the command hostname to find out where you are connected.</li>

 <li>The gettimeofday() system call can be used to determine and record the time prior to your call to connect() and to determine the time after connect() has completed. The difference between these two times is an estimate of the RTT.</li>

</ul>

o    You will have to do conversion from the second and microsecond fields used by gettimeofday()

<ul>

 <li>I would strongly suggest that everyone begin by writing a client and getting its test cases to work. Then write the web server and test it with your client.</li>

 <li>In writing your code, make sure to check for an error return from your system calls or method invocations, and display an appropriate message. In C this means checking and handling error return codes from your system calls.</li>

 <li>If you need to kill a background process after you have started it, you can use the UNIX <em>kill</em> Use the UNIX <em>ps</em> command to find the process id of your server</li>

 <li>Make sure you perform error handling and close every socket that you use in your program.</li>

 <li>If you abort your program, the socket may still hang around and the next time you try and bind a new socket to the port ID you previously used (but never closed), you may get an error.</li>

 <li>On UNIX systems, you can run the command “netstat” to see which port numbers are currently assigned.</li>

</ul>





