<h1>Part 1</h1>
  
  
  
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
  
  
<h3>Screenshot 1:</h3>
  
![Image](https://i.imgur.com/rJk1583.png)
  
In order to allow for this to happen, the `handleRequest()` method is being used in order to read through the given information and actually apply it to the resulting string, while inside of it, the `split()` method is being used three times at "&", and each of the "=" signs. Furthermore, `equals()` is being used in order to check if the given query is correct.
  
The relevant arguments is the url. The code is parsing through the url's path (which has given by `URI url`), and uses it in order to find the inputs `s=How are you`, and `user=Diego`, which are treated as strings.
  
The values of each of the relevant fields is changing. Initially, it takes a `URI` variable. However, `getPath()` is used in order to treat the path as a string. This lets the program parse through the path and check the queries. Afterwards, it returns a string that is formatted in order to act as the chat log. Because of this, the relevant fields within the class change from a `URI` to a `String`.

<h3>Screenshot 2:</h3>
  
![Image](https://i.imgur.com/IEL7VMi.png)
  
Once again, the `handleRequest()` method is being used to parse and understand the given information, while inside of it, the `split()` method is being used three times at "&", and each of the "=" signs. `equals()` is also being used again in order to check if the given query is correct.
  
The relevant argument within `handleRequest()` is `URI url`. The code is parsing through the url's path (which has given by `URI url` alongside the method `getPath()`), and uses it in order to find the inputs `s=How are you`, and `user=Diego`, which are treated as strings.

are `s=Okay` and `user=312`. In this case, the first value is normally a string, but 312 can be treated as an integer, yet both are being treated as strings automatically.
  
Once again, the values of each of the relevant fields is changing. Initially, it takes a `URI` variable. However, to parse through it, it uses strings to easily compare the information. Afterwards, it returns a string that is formatted in order to act as the chat log. Because of this, the relevant fields within the class change from a `URI` to a `String`.
  
  
  
<h1>Part 2</h1>
  
  
<h3>Private Key on Local:</h3>
  
![Image](https://i.imgur.com/5HB5A6y.png)
  
In this image, `id_ed25519` refers to the private key, while `id_ed25519.pub` refers to the public key. Thus, the file path for the private key is `C:/Users/diego/.ssh/id_ed25519`.
  
<h3>Public Key on ieng6:</h3>
  
![Image](https://i.imgur.com/J1NA7gG.png)
  
In this image, `authorized_keys` refers to where the public key is, making the absolute file path `/home/linux/ieng6/oce/22/dinostroza/.ssh/authorized_keys`.
  
<h3>Logging in without a password:</h3>
  
![Image](https://i.imgur.com/osGwJKc.png)
  
  
  
<h1>Part 3</h1>
  
  
  
In lab 2 and lab 3, I learned a significant amount about the process of building and running web servers. Although I was aware of localhost and had used it a few times throughout my life, I had never used it to run anything on the web. For this reason, these labs have taught me a significant amount about how to build and run web servers locally, and how to use queuries in order to alter a page on a web server. Specifically, lab 3 has taught me how to properly add arguments to a web server in a way where things can be handeled, separated, and used in order to alter elements of the page. This can be done through a `Handler` method, which uses a url as an argument in order to split up the arguments givin within the url and uses them to manipulate an output that will be displayed. 
