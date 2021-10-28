# Be cautious when using vs-code debugger with symbolic link

Did some random coding today and tried to use a golang dlv-dap debugger to debug my golang code in a WSL2 environment.

All breakpoints didn't work at the beginning and caused me heavy confusion on the cause. At the beginning I thought it was due to the WSL2 + vscode combination (it ran into trouble before in GIT diff highlighting).

![image](https://user-images.githubusercontent.com/15870761/139293215-5b92a0c2-f751-4748-9e16-97fcdcf1e67a.png)

After doing some researching, I did find a possible cause: a breakpoint prompted this:

![image](https://user-images.githubusercontent.com/15870761/139292822-07db4622-e73e-4f90-9543-564eb9ed3314.png)

and it was indeed a symbolic link to this file. 

Seeing this could be a possible cause, I found a field `substitutePath` in <https://github.com/golang/vscode-go/blob/master/docs/debugging.md> which seemed to be relevant. I set this field to:
```json
"substitutePath":[
    {
        "from": "/home/ethernoy/code",
        "to": "/mnt/c/Users/ehapr/Documents/Code"
    }
]
```

The breakpoint issue was resolved.

Oct 28, 2021
