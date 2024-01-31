# Lab Report 2
---
`ChatServer.java` Code
```
import java.io.IOException;
import java.net.URI;
import java.util.*;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.

    String chat = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format(chat);
        } else {
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("&");
                String message = parameters[0];
                message = message.substring(message.indexOf("=") + 1);

                String user = parameters[1];
                user = user.substring(user.indexOf("=") + 1);

                String fullString = String.format(user + ": " + message + "\n");

                chat = chat.concat(fullString);

                return chat;
            }
            return "404 Not Found!";
        }
    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```

Example 1 of `/add-message`:
![Image](CSE15L LAB2 EX1.1.png)

-Several methods are called in the code, including the methods:
```
.contains()
.getQuery()
.split()
.substring()
.indexOf()
.format()
.concat()
```

- Relevant argumens:
  1. for .contains() : the relevant arugement in .conatins() is `/add-message`
  2. for .getQuery() : the relevant argument is the `URI` variable `url` and it's associated value of the URL of the server page, which
                       in this instance would be the url query `/add-message?s=FINS UP!&user=mikeMcD`
  3. for .split() : there are two relevant arguements for this method, because it is used on two different occasions, once to
                    split the url query with the regular expression of `&` to seperate the strings `s=FINS UP!` and `user=mikeMcD` 
                    inputs in the query. It is used once more with the regular expression `=` to obtain the strings
  4. for .substring()
  5. for .indexOf()
  6. for .format()
  7. for .concat()
-Changed Values


Example 2 of `/add-message`:
![Image](CSE15L LAB2 EX1.2.png)

-Methods
-Relevant Arguments
-Changed Values
