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
  
  
<h4>Screenshot 1:</h4> 	
![Image](https://i.imgur.com/rJk1583.png)\
In order to allow for this to happen, the `split()` method is being used three times at "&", and each of the "=" signs. Furthermore, `equals()` is being used in order to check if the given query is correct.\ 
  
The relevant arguments are `s=How are you` and `user=Diego`. In this case, both are strings, and are being treated as strings automatically.\
  
The values of each of the relevant fields aren't changing, however the program is parsing through to grab specific values from the argument, specifically what follows `s=` and `user=`. The values aren't changing because `getQuery()` is creating a string from the query, rather than any other types.  
  

<h4>Screenshot 2:</h4>
![Image](https://i.imgur.com/IEL7VMi.png)\
Once again, the `split()` method is being used three times at "&", and each of the "=" signs. `equals()` is also being used again in order to check if the given query is correct.\ 
  
The relevant arguments are `s=Okay` and `user=312`. In this case, the first value is normally a string, but 312 can be treated as an integer, yet both are being treated as strings automatically.\
  
The values of each of the relevant fields aren't changing, however the value following `user=` is being treated as a string. Once again, this is due to the use of `getQuery()` being used to create a string from the query, making an integer be treated as a string.\


