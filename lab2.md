# Lab Report #2
CSE 15L - Joe Politz - 10:00am - 11:50am | Manh Tri Nguyen | A17913483 | man026@ucsd.edu
### Code Block for `ChatServer`
```java
/**
 * Name: Manh Tri Nguyen
 * PID: A17913483
 * Email: man026@ucsd.edu
 * 
 * Implementing the URL Handler, the purpose of this code is to create an
 * add message tool to the URL store as a Query. As the user add more query
 * the output messages are increasing without losing the original outputs.
*/

import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {

    //Initializing ArrayList and MESSAGES and DESIRED_LENGTH variables
    final String MESSAGE = "Code by Manh Tri Nguyen, A17913483, CSE 15L" + 
    "\nPlease use /add-message?s=<MESSAGE>&user=<NAME> to add message";
    final String INPUT_ERROR_MESSAGE = "INVALID INPUT";
    final int DESIRED_LENGTH = 2;
    ArrayList<String> outputString = new ArrayList<>();
    
    /**
     * The method will return the inputs that you, the user included in the
     * parameters when using /add-message
     * 
     * @param url the url of the localhost
     * 
     * @return Lines of strings of <user>: <message> onto the webpage or errors
     */
    @Override
    public String handleRequest(URI url) {
        if (url.getPath().equals("/add-message")) {
            // Split at the &
            String[] queryParts = url.getQuery().split("\\&");
            if(queryParts.length != DESIRED_LENGTH) {
                return INPUT_ERROR_MESSAGE;
            }
            //Split at = for the first params and store it
            String[] messageParam = queryParts[0].split("=");
            String message = messageParam[1];

            //Split at = for the second params and store it
            String[] userParam = queryParts[1].split("=");
            String user = userParam[1];

            //Store in ArrayList and output all strings
            String output = user + ": " + message;
            outputString.add(output);
            String allStrings = String.join("\n", outputString);
            return allStrings;
        }
        return MESSAGE;
    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        final String PORT_ERROR_MESSAGE = "Missing port number!" + 
        "Try any number between 1024 to 49151";

        if(args.length == 0){
            System.out.println(PORT_ERROR_MESSAGE);
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```

### Screenshots of using `/add-message`
- After compiling the file with `javac ChatServer.java Server.java` and initialize the `ChatServer` with the port number `3350`,
  I am on the website greeted with the `MESSAGE` because the URL does not contain `/add-message` yet. A prompt will appear to guide the user
  to use `/add-message` to add their own custom messages.
#### Successfully Adding Messages
<img width="1256" alt="add-wrk" src="https://github.com/man3ng/cse15l-lab-reports/assets/141669725/88c1d07d-0a8e-49ae-8e4a-02befbea7c76">

- There were multiple attempts of using `/add-message` to demonstrate that web-page can output multiple lines of messages with the `<name>` and `<messages>` input
  at the query. When the user is typing  `/add-message?s=<MESSAGE>&user=<NAME>` with the parameter filled out and press enter, the website will not return the `MESSAGE`
  parameters. Instead, the `if` statement is now true and now we begin spliting the message with the regex `&`; there should be at least two elements present from the split
  in order to proceed.`queryParts` is updated with all the split strings.
- We split by the regex `=` for `queryParts[0]` to get the strings from the message and stored in `messageParam`. Then, we will store `messageParam[1]` in a String type object
  `message`. Then we will split by the regex `=` for `queryParts[1]` to get the strings from the user and stored in `userParam`. Then, we will store `userParam[1]` in the
  String object `user`. The reason I chose `messageParam[1]` and `userParam[1]` is because I want to ignore `s=` and `user=` at each respective split parameter.
- After all the field are set up, they will join as an `output` and is added to the ArrayList initialized at the beginning of the code. Using the `.join` method, we will
  return all the `Strings` that are stored in the `ArrayList` and output them on the screen with the correct formatting.
- Noted: everytime that the user decide to the add the messages all the reference from `queryParts`, `messageParam`, `message`, `userParam`, `user`, and `output` fields and
  arrays will change because those are temporary storage. Additionally, the `ArrayList` will be continuously updated with new messages with the original message preserved.

#### Failed Attempt Adding Messages
<img width="1262" alt="add-error" src="https://github.com/man3ng/cse15l-lab-reports/assets/141669725/bd22cac0-efee-413e-ac7e-d653a614521b">

- With similar explanation as how this function work above, the reason that there is a error message is to let the user know that the query that you are trying to input
  after `/add-message?s=` is incorrect or not formatted correctly. The image above show that the user forget to add `<name>` to the query. Even though, the `queryParts`
  is splitting, the `queryParts` failed at the conditional because there must be 2 elements present in that field before proceeding with the next steps of spliting into
  other fields and adding the final string to the `ArrayList`.

### SSH Command Line
#### Absolute Path to Private SSH Key

```
trilosophe@Trilosophes-MBP-16 .ssh % pwd
/Users/trilosophe/.ssh
trilosophe@Trilosophes-MBP-16 .ssh % ls
id_rsa		id_rsa.pub	known_hosts
```
- This is a copy of my terminal, line-by-line. I am able to see my public key and private key storing location on my local device after `cd` into `.ssh`. I use
  `pwd` to show my absolute path and `ls` to show the contents inside my current directory.

#### Absolute Path to Public SSH Key

```
[man026@ieng6-201]:.ssh:67$ pwd
/home/linux/ieng6/oce/8o/man026/.ssh
[man026@ieng6-201]:.ssh:68$ ls
authorized_keys  id_rsa  id_rsa.pub
#skip forward a few unclean line of codes
[man026@ieng6-201]:.ssh:77$ ls
authorized_keys  id_rsa  id_rsa.pub
[man026@ieng6-201]:.ssh:78$ cat authorized_keys 
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDIIf9T0jKghBbORKJTCJjqxqQ6Q0SwIgd4l/4BFZuuHZxfaO1LHsHnp0NHLn20byeOMHdWpd90iPvLFFkDOUJE03xgq2PvCK87Sg9tAIUcXRBc5GX/YmkgchPnroOnjGNzmg3UMZoXP9X5PAqLK8VU+vUeJgy2NyXxPGKYH94nuJ424HScnW3XHE9WzpNkQSPzqJJYsVUAopoXI1ejNZ2gR8cuTQpBE4Kl2YS+BQVnjYqIzqCIP1skxazzLGm3GDZ1GLvhKWOfmHOtcapsFh2zIF4EcVQUX9u9DZzCiPf7wmbsatDMhz06X4ZqzTZLU7mSYQZGZBfwXOfrlHy4atUgWSrEojym/dFKXjx1jv/9i1ODpdxFnOPSFtkbGTUCDC57Av+LHN4zdbhnPSwHbjA+30dc13bM09Od1VMz09XQYF+U/46hdfVxheu2OM3hcddHET9TPMba7YE0M/ehz6MaARYj5czOVbMsLEFj7DNgSB8zY1z5pupmy+Z57IcOm6c= trilosophe@Trilosophes-MBP-16.local
[man026@ieng6-201]:.ssh:79$ 
```
- After successfully logging on to my `ieng6` virtual desktop without a password with my key, I can access the location where my `public key` is being stored.
  Using `ls -a` initially, I am able to locate the `.ssh` folder to move into. After that, I use `pwd` to show my absolute path and `ls` for content inside my
  current directory. Then, I use `cat` authorized_keys to see the key stored inside authorized_keys.

#### Terminal Interaction SSH-ing to `ieng6` without Password

```
trilosophe@Trilosophes-MBP-16 / % ssh man026@ieng6-201.ucsd.edu
Last login: Sun Jan 28 01:05:54 2024 from 100.91.160.47
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2024-01-12_0010: Stale file handle
Hello man026, you are currently logged into ieng6-201.ucsd.edu

You are using 0% CPU on this system

Cluster Status 
Hostname     Time    #Users  Load  Averages  
ieng6-201   17:50:01   49  1.70,  2.03,  2.09
ieng6-202   17:50:01   23  0.08,  0.18,  0.26
ieng6-203   17:50:01   28  4.07,  3.18,  3.02

 

To begin work for one of your courses [ cs15lwi24 ], type its name 
at the command prompt.  (For example, "cs15lwi24", without the quotes).
To see all available software packages, type "prep -l" at the command prompt,
or "prep -h" for more options.
[man026@ieng6-201]:~:53$ 
```
- Here is a snap shot of my terminal line-by-line of ssh-ing into the `ieng6` device without being asked to enter a password.

### Retrospect
- For week 2 and 3 for CSE15L course and lab, I have learned skills to manage my files using the terminal which is the skills that I was never confident of. Additionally,
  I learned how to use command line such as `scp`, `ssh`, and `curl` to manage content with the local host and the remote system. These are the skills that I consider
  essential and applicable in the future. Lastly, if you can't `ls` to see the all the contents on your remote desktop, one my groupmate at the lab introduced me with the
  command `ls -a` to see the hidden files; I assume this `-a` mean to include all the hidden files under the directory.
