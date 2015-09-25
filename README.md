ScriptGenerator
===============

This project started with the aim of simplify the way we make scripts in JMeter. There are a lot of ways to create a JMeter script, and we find one that we think is awesome :). Also, we realized that we could extend this tool, not only for JMeter, and we are trying to include OpenSTA support.

Basically we have two main tools in this solution:
* FiddlerSessionComparer
* GeneratorFramework

1 - FiddlerSessionComparer
---------------------------
Fiddler Session Comparer (FSC) creates a tree view structure based on the "Fiddler sessions". As we know, when we request a page, the page invokes some resources (images, css, js) that it needs to show itself. So, we would say that the first HTTP request is the primary request and the other ones corresponding to additional resources like images, js and css are secondary requests. So, in this manner we would create a tree view for HTTP request.

FCS uses from two or more (nowadays, just two, we are working to add more) Fiddler Sessions files. After comparing two HTTP requests from Fiddler Sessions files, the comparer detect differences between requests. Each difference is a 'Parameter'. This parameters are reused along all the analysis.
 
2 - GeneratorFramework
---------------------------

We created a simple windows command line tool (and GUI) which uses [Fiddler](http://www.telerik.com/fiddler) sessions to create JMeter scripts. You can find our program [here](https://github.com/abstracta/ScriptGenerator/tree/master/Binaries%20.NET%204.5). You must record your sessions with Fiddler, pretty straightforward. While you are recording your sessiong mark with a comment every step of your session. For instance, let´s say that you are recording a test case consisting in search something in google. Your first step will be open www.google.com and then, the second one will be type your query in the search box and hit "search in google". To improve the JMeter generation and help the generator to understand your session, select all the request in your Fiddler session corresponding for the first step, and mark them with a comment, for example with the text "step 1". Then, select all the requests corresponding to your second step and mark them as well, and so on if you have more steps.

Finally execute the program to create the JMeter script in the following way

    Abstracta.ScriptGeneratorCLI_4.5.exe -h myapp.com -p 80 -a home -f C:\scripts\yourFiddlerSession1.saz -f C:\scripts\yourFiddlerSession2.saz -o C:\script\outputFolder\

The program will create the script and will store it in a file called _AutogeneratedName.jmx located at your output folder (in the example, C:\script\outputFolder\).

You can type help for more info or use the GUI if you feel more confortable

    -h, --host=VALUE           (required) host name where your web app is
                               hosted. Example: https://myapp.com/home, host =
                               myapp.com
    -p, --port=VALUE           port number where your web app is listening.
                               Example: https://myapp.com/home, port = 443
                               This must be an integer. By default the value is

                               80.
    -a, --app=VALUE            relative application name. Example:
                               https://myapp.com/home, app = home
    -o, --output=VALUE         (required) output path

    -f, --fiddlerPath=VALUE    (required) fiddler session path
      --help                 show this message and exit

Hope it helps someone


