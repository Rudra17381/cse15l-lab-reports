# Lab Report Week 3

[Index Page](https://rudra17381.github.io/cse15l-lab-reports/index.html)

In this week's Lab Report we will learn how to implement group choice questions from [Lab 5](https://docs.google.com/document/d/1NQ17hecUPFKeoFyrEvK9DBlCS1JkDbMW6Ygrf_CJJJU/edit).

## Streamlining ```ssh``` Configuration

In previous labs and lab reports, we have taken a lot at how to use remote pcs to do our work using ieng6. Having to access it often, it becomes a tedious and annoying task.

```ssh cs15lsp22zzz@ieng6.ucsd.edu```

First you need to remember the course name, then your account specific name and not to mention type it all out perfectly in one go (Almost an impossible task) 

If only there could be a way to automatically type this from a smaller command- obviously there is a way since all of us programmers are lazy and find any and every excuse to automate stuff.

### To do so, follow these steps:
**On your client PC**
1. Open up Terminal
2. Open up your ```ssh``` config file using the command: ```open .ssh/config```
    * If the ```ssh``` file does not exist, you can create it using ```touch .ssh/config.txt```
3. Add the following lines to the config file:
    ```
        Host ieng6
        HostName ieng6.ucsd.edu
        User cs15lsp22zzz (use your username)
      ```

Done! You have now made it easier to log into your ieng6 account. To log in, use the following command: 
```ssh ieng6```

If this does not work then add a line to your config file explicitly refering to the id_rsa file using the following command:
```echo     IdentityFile ~/.ssh/id_rsa >> .ssh/config``` or just open the file and manually edit in the line ```IdentityFile ~/.ssh/id_rsa```

Below are screenshots for the lab report and to help you out if you're a little stuck
1. ```.ssh/config``` File and how I accessed it
    * Accessing the file
    * The file and its text contents

2. Logging in using ```ssh ieng6```

3. Copying files using ```scp file ieng6```

## Set up Github Access from ieng6
