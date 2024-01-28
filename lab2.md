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

    //Initializing ArrayList and MESSAGES
    final String MESSAGE = "Code by Manh Tri Nguyen, A17913483, CSE 15L" + 
    "\nPlease use /add-message?s=<MESSAGE>&user=<NAME> to add message";
    final String INPUT_ERROR_MESSAGE = "INVALID INPUT";
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
            if(queryParts.length <= 1) {
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
  in order to proceed. Then, for each index of the `queryParts`, we split by the regex `=` to get the desired information and store each of them in an array, and the part
  I desired in a field.
- After all the field are set up, they will join as an `output` and is added to the ArrayList initialized at the beginning of the code. Using the `.join` method, we will
  return all the `Strings` that are stored in the `ArrayList` and output them on the screen with the correct formatting.
- Noted: everytime that the user decide to the add the messages all the reference from `queryParts`, `messageParam`, `message`, `userParam`, `user`, and `output` fields and
  arrays will change because those are temporary storage. Additionally, the `ArrayList` will be continuously updated with new messages with the original message preserved.

#### Failed Attempt Adding Messages
<img width="1262" alt="add-error" src="https://github.com/man3ng/cse15l-lab-reports/assets/141669725/bd22cac0-efee-413e-ac7e-d653a614521b">
