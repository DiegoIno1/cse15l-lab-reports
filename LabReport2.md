<h3>Code:</h3> 	

```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    
    String ChatLog = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("Current Chat:\n %s", ChatLog);
        } 
        else {
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("&");
                String[] parameters_string = parameters[0].split("=");
                String[] parameters_user = parameters[1].split("=");
                if (parameters_string[0].equals("s") && parameters_user[0].equals("user")) {
                    ChatLog += parameters_user[1] + ": " + parameters_string[1] + "\n";
                    return String.format("%s", ChatLog);
                }
            }
            return "404 Not Found!";
        }
    }
}
\
\
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

![Image](https://i.imgur.com/rJk1583.png)\
In order to allow for this to happen, the `split()` method is being used three times at "&", and each of the "=" signs. Furthermore, `equals()` is being used in order to check if the given query is correct.\ 
  
The relevant arguments are `s=How are you` and `user=Diego`. In this case, both are strings, and are being treated as strings automatically.\
  
The values of each of the relevant fields aren't changing, however the program is parsing through to grab specific values from the argument, specifically what follows `s=` and `user=`.

![Image](https://i.imgur.com/IEL7VMi.png)\
