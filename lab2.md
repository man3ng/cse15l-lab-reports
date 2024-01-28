# Lab Report #2
CSE 15L - Joe Politz - 10:00am - 11:50am | Manh Tri Nguyen | A17913483 | man026@ucsd.edu

Your identification has been saved in /Users/trilosophe/.ssh/id_rsa
Your public key has been saved in /Users/trilosophe/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:MSlqloZ0Qb+m75AF1xPs8zdcn4EIaadxrKirGAau79g trilosophe@Trilosophes-MBP-16.local

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
