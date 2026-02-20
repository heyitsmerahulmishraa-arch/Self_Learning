## How Commands Get Executed

When you run a command in your terminal, the shell (like Bash or Zsh) takes care of interpreting and executing it. Here's a simplified overview of how this process works:
1. **Parsing the Command**: The shell reads the command you entered and breaks it down into its components (the command itself and any arguments or options).
2. **Finding the Command**: The shell looks for the command in its list of built-in commands. If it doesn't find it there, it searches through the directories listed in the `PATH` environment variable to find an executable file that matches the command name.
3. **Executing the Command**: Once the shell finds the command, it creates a new process to run the command. This involves loading the executable file into memory and starting its execution.
4. **Handling Input and Output**: The shell manages the input and output for the command. It can redirect input and output to files or other commands, allowing for powerful combinations of commands.
5. **Waiting for Completion**: The shell waits for the command to finish executing before it returns control to the user. If the command is a background process, the shell will allow you to continue using the terminal while it runs.
6. **Returning the Result**: After the command has finished executing, the shell returns the exit status of the command, which indicates whether it was successful or if an error occurred. This status can be used in scripts to make decisions based on the success or failure of commands.
Understanding this process can help you troubleshoot issues with commands and write more effective shell scripts.