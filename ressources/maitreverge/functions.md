---------------------------------------------------------------------------------

READLINE

The readline function is not a standard C function, but it's part of the GNU Readline library, which provides a set of functions for use by applications that allow users to edit command lines as they are typed in.

Function Description: readline reads a line from the terminal and returns it, allowing the user to edit the line with familiar key bindings and history capabilities.

Prototype: char *readline(const char *prompt);

Library: #include <readline/readline.h>

Example:

#include <stdio.h>
#include <readline/readline.h>

int main() {
	char *line = readline("Enter a line: ");
	printf("You entered: %s\n", line);
	free(line);  // Don't forget to free the memory allocated by readline
	return 0;
}

In this example, the program prompts the user to enter a line of text, then prints the entered line. The memory allocated by readline is freed after it's no longer needed.

---------------------------------------------------------------------------------

RL_CLEAR_HISTORY


The rl_clear_history function is part of the GNU Readline library, which provides a set of functions for use by applications that allow users to edit command lines as they are typed in.

Function Description: rl_clear_history clears the history list by freeing the memory of each element in the list and setting the length of the list to zero.

Prototype: void rl_clear_history(void);

Library: #include <readline/history.h>

Example:

#include <stdio.h>
#include <readline/readline.h>
#include <readline/history.h>

int main() {
	char *line;
	while ((line = readline("Enter a line: ")) != NULL) {
		if (*line) add_history(line);
		printf("You entered: %s\n", line);
		free(line);
	}
	rl_clear_history();
	return 0;
}

In this example, the program prompts the user to enter lines of text until an EOF (End Of File) character is received (Ctrl+D in Unix-like systems). Each entered line is added to the history.
After the loop, rl_clear_history is called to clear the history list.


---------------------------------------------------------------------------------
RL_ON_NEW_LINE

The rl_on_new_line function is part of the GNU Readline library, which provides a set of functions for use by applications that allow users to edit command lines as they are typed in.

Function Description: rl_on_new_line tells the readline library that the cursor is on a new line, so it should reset its idea of the cursor position. It's often used after a newline character has been printed or the readline input line has been cleared.

Prototype: int rl_on_new_line(void);

Library: #include <readline/readline.h>

Example:


#include <stdio.h>
#include <readline/readline.h>

int main() {
	char *line = readline("Enter a line: ");
	printf("You entered: %s\n", line);
	free(line);
	rl_on_new_line();
	return 0;
}

In this example, the program prompts the user to enter a line of text, then prints the entered line. After freeing the memory allocated by readline, rl_on_new_line is called to inform readline that the cursor is on a new line


---------------------------------------------------------------------------------
RL_REPLACE_LINE

The rl_replace_line function is part of the GNU Readline library, which provides a set of functions for use by applications that allow users to edit command lines as they are typed in.

Function Description: rl_replace_line replaces the contents of the current readline buffer with the string passed as an argument.

Prototype: int rl_replace_line(const char *text, int clear_undo);

Library: #include <readline/readline.h>

Example:

#include <stdio.h>
#include <readline/readline.h>

int main() {
	char *line = readline("Enter a line: ");
	rl_replace_line("This is a new line", 0);
	rl_redisplay();
	free(line);
	return 0;
}

In this example, the program prompts the user to enter a line of text. Then, rl_replace_line is called to replace the contents of the readline buffer with "This is a new line". The rl_redisplay function is then called to update the display.
The memory allocated by readline is freed after it's no longer needed.


---------------------------------------------------------------------------------
RL_REDISPLAY

The rl_redisplay function is part of the GNU Readline library, which provides a set of functions for use by applications that allow users to edit command lines as they are typed in.

Function Description: rl_redisplay causes readline to update the screen to reflect the current contents of the readline buffer.

Prototype: void rl_redisplay(void);

Library: #include <readline/readline.h>

Example:

#include <stdio.h>
#include <readline/readline.h>

int main() {
	char *line = readline("Enter a line: ");
	rl_replace_line("This is a new line", 0);
	rl_redisplay();
	free(line);
	return 0;
}

In this example, the program prompts the user to enter a line of text. Then, rl_replace_line is called to replace the contents of the readline buffer with "This is a new line". The rl_redisplay function is then called to update the display.
The memory allocated by readline is freed after it's no longer needed.


---------------------------------------------------------------------------------
ADD_HISTORY

The add_history function is part of the GNU Readline library, which provides a set of functions for use by applications that allow users to edit command lines as they are typed in.

Function Description: add_history adds the string passed as an argument to the history list.

Prototype: void add_history(const char *line);

Library: #include <readline/history.h>

Example:

#include <stdio.h>
#include <readline/readline.h>
#include <readline/history.h>

int main() {
	char *line = readline("Enter a line: ");
	if (*line) add_history(line);
	printf("You entered: %s\n", line);
	free(line);
	return 0;
}

In this example, the program prompts the user to enter a line of text. If the entered line is not empty, add_history is called to add the line to the history list. The entered line is then printed,
and the memory allocated by readline is freed after it's no longer needed.


---------------------------------------------------------------------------------
ACCESS

The access function is a standard C function that checks the file's accessibility.

Function Description: access checks whether the calling process can access the file pathname. It checks the file's permissions based on the mode parameter which can be F_OK (tests for the existence of the file), R_OK (tests for read permission), W_OK (tests for write permission), and X_OK (tests for execute or search permission).

Prototype: int access(const char *pathname, int mode);

Library: #include <unistd.h>

Example:

#include <stdio.h>
#include <unistd.h>

int main() {
	if (access("myfile.txt", F_OK) != -1) {
		printf("File exists.\n");
	} else {
		printf("File doesn't exist.\n");
	}
	return 0;
}

In this example, the program checks if the file myfile.txt exists. If the file exists,
it prints "File exists.", otherwise it prints "File doesn't exist.".

---------------------------------------------------------------------------------
OPEN

The open function is a standard C function that opens a file or device.

Function Description: open opens the file specified by pathname. The flags parameter determines the file access mode (read, write, read/write, create, etc.). It returns a file descriptor for the opened file, or -1 if an error occurs.

Prototype: int open(const char *pathname, int flags);

Library: #include <fcntl.h>

Example:

#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>

int main() {
	int fd = open("myfile.txt", O_RDONLY);
	if (fd == -1) {
		printf("Failed to open file.\n");
	} else {
		printf("File opened successfully.\n");
		close(fd);
	}
	return 0;
}

In this example, the program attempts to open the file myfile.txt in read-only mode. If the file is opened successfully, it prints "File opened successfully." and then closes the file.
If the file cannot be opened, it prints "Failed to open file.".

---------------------------------------------------------------------------------
READ

The read function is a standard C function that reads data from a file.

Function Description: read reads up to count bytes from the file referenced by the file descriptor fd, storing the results in the buffer.

Prototype: ssize_t read(int fd, void *buf, size_t count);

Library: #include <unistd.h>

Example:

#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>

#define BUF_SIZE 1024

int main() {
	int fd = open("myfile.txt", O_RDONLY);
	if (fd == -1) {
		printf("Failed to open file.\n");
	} else {
		char buf[BUF_SIZE];
		ssize_t bytesRead = read(fd, buf, BUF_SIZE - 1);
		if (bytesRead >= 0) {
			buf[bytesRead] = '\0';  // Null-terminate the string
			printf("Read from file: %s\n", buf);
		} else {
			printf("Failed to read from file.\n");
		}
		close(fd);
	}
	return 0;
}

In this example, the program attempts to open the file myfile.txt in read-only mode. If the file is opened successfully, it reads up to BUF_SIZE - 1 bytes from the file into a buffer, then prints the contents of the buffer. If the file cannot be read,
it prints "Failed to read from file.". After reading, the file is closed.


---------------------------------------------------------------------------------
CLOSE

The close function is a standard C function that closes a file descriptor.

Function Description: close closes a file descriptor, so that it no longer refers to any file and may be reused. It returns zero on success, or -1 if an error occurs.

Prototype: int close(int fd);

Library: #include <unistd.h>

Example:

#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>

int main() {
	int fd = open("myfile.txt", O_RDONLY);
	if (fd == -1) {
		printf("Failed to open file.\n");
	} else {
		printf("File opened successfully.\n");
		if (close(fd) == 0) {
			printf("File closed successfully.\n");
		} else {
			printf("Failed to close file.\n");
		}
	}
	return 0;
}

In this example, the program attempts to open the file myfile.txt in read-only mode. If the file is opened successfully, it prints "File opened successfully.". Then it attempts to close the file. If the file is closed successfully, it prints "File closed successfully.".
If the file cannot be closed, it prints "Failed to close file.".

---------------------------------------------------------------------------------
FORK

The fork function is a standard C function that creates a new process.

Function Description: fork creates a new process by duplicating the existing process. The new process, called the child, is an exact copy of the calling process, called the parent, except for a few values changed, including the process ID and parent process ID. It returns the process ID of the child process to the parent, and 0 to the child. If it fails, it returns -1.

Prototype: pid_t fork(void);

Library: #include <unistd.h>

Example:

#include <stdio.h>
#include <unistd.h>

int main() {
	pid_t pid = fork();

	if (pid < 0) {
		printf("Failed to fork.\n");
	} else if (pid == 0) {
		printf("This is the child process.\n");
	} else {
		printf("This is the parent process, child PID is %d.\n", pid);
	}
	return 0;
}

In this example, the program creates a new process using fork. If fork fails, it prints "Failed to fork.". If fork succeeds, the parent process prints its own process ID and the child's process ID,
and the child process prints "This is the child process.".



---------------------------------------------------------------------------------
WAIT

The wait function is a standard C function that makes a parent process wait until one of its child processes exits.

Function Description: wait suspends the calling process until one of its child processes exits. It returns the process ID of the child process that exited, or -1 if an error occurs. The exit status of the child process is stored in the integer pointed to by the status parameter.

Prototype: pid_t wait(int *status);

Library: #include <sys/wait.h>

Example:

#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
	pid_t pid = fork();

	if (pid < 0) {
		printf("Failed to fork.\n");
	} else if (pid == 0) {
		printf("This is the child process.\n");
	} else {
		int status;
		wait(&status);
		printf("This is the parent process, child has exited.\n");
	}
	return 0;
}

In this example, the program creates a new process using fork. If fork fails, it prints "Failed to fork.". If fork succeeds, the child process prints "This is the child process.", and the parent process waits for the child to exit
before printing "This is the parent process, child has exited.".



---------------------------------------------------------------------------------
WAITPID

The waitpid function is a standard C function that makes a parent process wait for a specific child process to exit.

Function Description: waitpid suspends the calling process until the specified child process exits. It returns the process ID of the child process that exited, 0 if the child is still running, or -1 if an error occurs. The exit status of the child process is stored in the integer pointed to by the status parameter.

Prototype: pid_t waitpid(pid_t pid, int *status, int options);

Library: #include <sys/wait.h>

Example:

#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
	pid_t pid = fork();

	if (pid < 0) {
		printf("Failed to fork.\n");
	} else if (pid == 0) {
		printf("This is the child process.\n");
	} else {
		int status;
		waitpid(pid, &status, 0);
		printf("This is the parent process, child has exited.\n");
	}
	return 0;
}

In this example, the program creates a new process using fork. If fork fails, it prints "Failed to fork.". If fork succeeds, the child process prints "This is the child process.", and the parent process waits for the specific child
to exit before printing "This is the parent process, child has exited.".



---------------------------------------------------------------------------------
WAIT3

The wait3 function is a standard C function that suspends the calling process until one of its child processes terminates.

Function Description: wait3 suspends the calling process until a child process terminates. It also returns resource usage information about the child in the structure pointed to by rusage. It returns the process ID of the child process that terminated, or -1 if an error occurs.

Prototype: pid_t wait3(int *status, int options, struct rusage *rusage);

Library: #include <sys/wait.h>

Example:

#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>
#include <sys/resource.h>

int main() {
	pid_t pid = fork();

	if (pid < 0) {
		printf("Failed to fork.\n");
	} else if (pid == 0) {
		printf("This is the child process.\n");
	} else {
		int status;
		struct rusage usage;
		wait3(&status, 0, &usage);
		printf("This is the parent process, child has exited.\n");
	}
	return 0;
}

In this example, the program creates a new process using fork. If fork fails, it prints "Failed to fork.". If fork succeeds, the child process prints "This is the child process.", and the parent process waits for a child to exit and retrieves the child's
resource usage before printing "This is the parent process, child has exited.".



---------------------------------------------------------------------------------
WAIT4

The wait4 function is a standard C function that suspends the calling process until a specific child process terminates.

Function Description: wait4 suspends the calling process until the child process specified by pid terminates. It also returns resource usage information about the child in the structure pointed to by rusage. It returns the process ID of the child process that terminated, or -1 if an error occurs.

Prototype: pid_t wait4(pid_t pid, int *status, int options, struct rusage *rusage);

Library: #include <sys/wait.h>

Example:

#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>
#include <sys/resource.h>

int main() {
	pid_t pid = fork();

	if (pid < 0) {
		printf("Failed to fork.\n");
	} else if (pid == 0) {
		printf("This is the child process.\n");
	} else {
		int status;
		struct rusage usage;
		wait4(pid, &status, 0, &usage);
		printf("This is the parent process, child has exited.\n");
	}
	return 0;
}

In this example, the program creates a new process using fork. If fork fails, it prints "Failed to fork.". If fork succeeds, the child process prints "This is the child process.", and the parent process waits for the specific child to exit and retrieves the child's
resource usage before printing "This is the parent process, child has exited.".



---------------------------------------------------------------------------------
SIGNAL

The signal function is a standard C function that sets a function to handle a signal.

Function Description: signal sets a function to handle a signal. The function (or action) to be called when the signal occurs is passed as the second argument. It returns the previous action for the signal, or SIG_ERR if an error occurs.

Prototype: void (*signal(int sig, void (*func)(int)))(int);

Library: #include <signal.h>

Example:

#include <stdio.h>
#include <unistd.h>
#include <signal.h>

void handle_sigint(int sig) {
	printf("Caught signal %d\n", sig);
}

int main() {
	signal(SIGINT, handle_sigint);
	while (1) {
		printf("Running...\n");
		sleep(1);
	}
	return 0;
}


In this example, the program sets a function handle_sigint to handle the SIGINT signal
(usually generated by the Ctrl+C command). If the SIGINT signal is caught, the program prints "Caught signal 2". The program runs indefinitely, printing "Running..." every second, until it receives a SIGINT signal.


---------------------------------------------------------------------------------
SIGACTION

The sigaction function is a standard C function that allows you to examine and change a signal action.

Function Description: sigaction allows you to examine and change a signal action. It can be used to get or set the action to be taken by a process on receipt of a specific signal.

Prototype: int sigaction(int signum, const struct sigaction *act, struct sigaction *oldact);

Library: #include <signal.h>

Example:

#include <stdio.h>
#include <unistd.h>
#include <signal.h>

void handle_sigint(int sig) {
	printf("Caught signal %d\n", sig);
}

int main() {
	struct sigaction sa;
	sa.sa_handler = handle_sigint;
	sigemptyset(&sa.sa_mask);
	sa.sa_flags = 0;
	sigaction(SIGINT, &sa, NULL);
	while (1) {
		printf("Running...\n");
		sleep(1);
	}
	return 0;
}

In this example, the program sets a function handle_sigint to handle the SIGINT signal (usually generated by the Ctrl+C command) using sigaction. If the SIGINT signal is caught, the program prints "Caught signal 2". The program runs
indefinitely, printing "Running..." every second, until it receives a SIGINT signal.


---------------------------------------------------------------------------------
SIGEMPTYSET

The sigemptyset function is a standard C function that initializes a signal set to be empty.

Function Description: sigemptyset initializes a signal set to be empty. All signals are excluded from the set. It returns 0 on success, and -1 on error.

Prototype: int sigemptyset(sigset_t *set);

Library: #include <signal.h>

Example:

#include <stdio.h>
#include <signal.h>

int main() {
	sigset_t set;
	if (sigemptyset(&set) == 0) {
		printf("Signal set initialized to be empty.\n");
	} else {
		printf("Failed to initialize signal set.\n");
	}
	return 0;
}

In this example, the program initializes a signal set to be empty using sigemptyset. If sigemptyset succeeds, it prints "Signal set initialized to be empty.".
If sigemptyset fails, it prints "Failed to initialize signal set.".


---------------------------------------------------------------------------------
SIGADDSET

The sigaddset function is a standard C function that adds a specified signal to a signal set.

Function Description: sigaddset adds a specified signal to a signal set. It returns 0 on success, and -1 on error.

Prototype: int sigaddset(sigset_t *set, int signum);

Library: #include <signal.h>

Example:

#include <stdio.h>
#include <signal.h>

int main() {
	sigset_t set;
	sigemptyset(&set);
	if (sigaddset(&set, SIGINT) == 0) {
		printf("SIGINT added to the signal set.\n");
	} else {
		printf("Failed to add SIGINT to the signal set.\n");
	}
	return 0;
}

In this example, the program first initializes a signal set to be empty using sigemptyset. Then it adds SIGINT to the signal set using sigaddset. If sigaddset succeeds, it prints "SIGINT added to the signal set.".
If sigaddset fails, it prints "Failed to add SIGINT to the signal set.".



---------------------------------------------------------------------------------
KILL

The kill function is a standard C function that sends a signal to a specific process or a group of processes.

Function Description: kill sends a signal to a process or a group of processes. The pid parameter specifies the process or group to send to, and the sig parameter specifies the signal to send. It returns 0 on success, and -1 on error.

Prototype: int kill(pid_t pid, int sig);

Library: #include <signal.h>

Example:

#include <stdio.h>
#include <signal.h>
#include <unistd.h>

int main() {
	printf("Sending SIGSTOP to this process\n");
	kill(getpid(), SIGSTOP);
	return 0;
}

In this example, the program sends the SIGSTOP signal to itself using kill. This will cause the process to stop. Note that
you can continue the process with the fg command if you're running it in a terminal.



---------------------------------------------------------------------------------
EXIT

The exit function is a standard C function that terminates the calling process.

Function Description: exit terminates the calling process and returns the exit status to the parent process. The status parameter is the exit status of the process.

Prototype: void exit(int status);

Library: #include <stdlib.h>

Example:

#include <stdio.h>
#include <stdlib.h>

int main() {
	printf("Terminating this process\n");
	exit(0);
	return 0;  // This line will not be executed
}

In this example, the program terminates itself using exit. The printf statement after exit will not be executed because the process has already terminated.
The exit status of the process is 0, which usually indicates successful termination.


---------------------------------------------------------------------------------
GETCWD

The getcwd function is a standard C function that gets the current working directory of the process.

Function Description: getcwd gets the current working directory of the process. The buf parameter is a pointer to the buffer where the path is stored, and size is the size of the buffer. It returns a pointer to the buffer on success, and NULL on error.

Prototype: char *getcwd(char *buf, size_t size);

Library: #include <unistd.h>

Example:

#include <stdio.h>
#include <unistd.h>

int main() {
	char buf[1024];
	if (getcwd(buf, sizeof(buf)) != NULL) {
		printf("Current working directory: %s\n", buf);
	} else {
		printf("Failed to get current working directory.\n");
	}
	return 0;
}

In this example, the program gets the current working directory using getcwd and stores it in buf. If getcwd succeeds, it prints "Current working directory: " followed by the path.
If getcwd fails, it prints "Failed to get current working directory.".

---------------------------------------------------------------------------------
CHDIR

The chdir function is a standard C function that changes the current working directory of the process.

Function Description: chdir changes the current working directory of the process to the directory specified by path. It returns 0 on success, and -1 on error.

Prototype: int chdir(const char *path);

Library: #include <unistd.h>

Example:

#include <stdio.h>
#include <unistd.h>

int main() {
	if (chdir("/tmp") == 0) {
		printf("Changed the current working directory to /tmp\n");
	} else {
		printf("Failed to change the current working directory.\n");
	}
	return 0;
}

In this example, the program changes the current working directory to /tmp using chdir. If chdir succeeds, it prints "Changed the current working directory to /tmp".
If chdir fails, it prints "Failed to change the current working directory.".



---------------------------------------------------------------------------------
STAT

The stat function is a standard C function that gets file status.

Function Description: stat gets the status of the file specified by path and fills in the buffer pointed to by buf. It returns 0 on success, and -1 on error.

Prototype: int stat(const char *restrict path, struct stat *restrict buf);

Library: #include <sys/stat.h>

Example:

#include <stdio.h>
#include <sys/stat.h>

int main() {
	struct stat buf;
	if (stat("/tmp", &buf) == 0) {
		printf("Got the status of /tmp\n");
	} else {
		printf("Failed to get the status of /tmp.\n");
	}
	return 0;
}


In this example, the program gets the status of the directory /tmp using stat and stores it in buf. If stat succeeds, it prints
"Got the status of /tmp". If stat fails, it prints "Failed to get the status of /tmp.".


---------------------------------------------------------------------------------
LSTAT

The lstat function is a standard C function that gets file status, similar to stat, but if the file is a symbolic link, lstat returns information about the link itself, not the file it refers to.

Function Description: lstat gets the status of the file specified by path and fills in the buffer pointed to by buf. If the file is a symbolic link, lstat returns information about the link itself, not the file it refers to. It returns 0 on success, and -1 on error.

Prototype: int lstat(const char *restrict path, struct stat *restrict buf);

Library: #include <sys/stat.h>

Example:

#include <stdio.h>
#include <sys/stat.h>

int main() {
	struct stat buf;
	if (lstat("/tmp/symlink", &buf) == 0) {
		printf("Got the status of /tmp/symlink\n");
	} else {
		printf("Failed to get the status of /tmp/symlink.\n");
	}
	return 0;
}

In this example, the program gets the status of the symbolic link /tmp/symlink using lstat and stores it in buf. If lstat succeeds, it prints "Got the status of /tmp/symlink".
If lstat fails, it prints "Failed to get the status of /tmp/symlink.".



---------------------------------------------------------------------------------
FSTAT

The fstat function is a standard C function that gets the status of an open file.

Function Description: fstat gets the status of the open file associated with the file descriptor fd and fills in the buffer pointed to by buf. It returns 0 on success, and -1 on error.

Prototype: int fstat(int fd, struct stat *buf);

Library: #include <sys/stat.h>

Example:

#include <stdio.h>
#include <sys/stat.h>
#include <fcntl.h>

int main() {
	struct stat buf;
	int fd = open("/tmp/file", O_RDONLY);
	if (fd != -1) {
		if (fstat(fd, &buf) == 0) {
			printf("Got the status of /tmp/file\n");
		} else {
			printf("Failed to get the status of /tmp/file.\n");
		}
		close(fd);
	} else {
		printf("Failed to open /tmp/file.\n");
	}
	return 0;
}

In this example, the program opens the file /tmp/file and gets its status using fstat, storing the result in buf. If fstat succeeds, it prints "Got the status of /tmp/file". If fstat fails, it prints "Failed to get the status of /tmp/file.".
If the file fails to open, it prints "Failed to open /tmp/file.".



---------------------------------------------------------------------------------
UNLINK

The unlink function is a standard C function that removes a specified file.

Function Description: unlink removes the file at the path pathname. If the file is a symbolic link, the link is removed. The file is only actually removed if it is not open in any process. It returns 0 on success, and -1 on error.

Prototype: int unlink(const char *pathname);

Library: #include <unistd.h>

Example:

#include <stdio.h>
#include <unistd.h>

int main() {
	if (unlink("/tmp/file") == 0) {
		printf("Removed /tmp/file\n");
	} else {
		printf("Failed to remove /tmp/file.\n");
	}
	return 0;
}


In this example, the program removes the file /tmp/file using unlink.
If unlink succeeds, it prints "Removed /tmp/file". If unlink fails, it prints "Failed to remove /tmp/file.".


---------------------------------------------------------------------------------
EXECVE

The execve function is a standard C function that replaces the current process image with a new process image.

Function Description: execve replaces the current process image with a new process image specified by filename. The argv is an array of argument strings passed to the new program. The envp is an array of strings, conventionally of the form key=value, which are passed as environment to the new program. It does not return on success, and -1 on error.

Prototype: int execve(const char *filename, char *const argv[], char *const envp[]);

Library: #include <unistd.h>

Example:

#include <stdio.h>
#include <unistd.h>

int main() {
	char *argv[] = {"/bin/ls", "-l", NULL};
	char *envp[] = {NULL};
	if (execve("/bin/ls", argv, envp) == -1) {
		printf("Failed to execute /bin/ls.\n");
	}
	return 0;  // This line will not be executed if execve succeeds
}

In this example, the program replaces its own process image with the /bin/ls program using execve. If execve fails, it prints "Failed to execute /bin/ls.".
If execve succeeds, the rest of the program will not be executed because the process image has been replaced.



---------------------------------------------------------------------------------
DUP

The dup function is a standard C function that creates a copy of the file descriptor.

Function Description: dup creates a new file descriptor that is a copy of the old file descriptor. The new file descriptor is the lowest-numbered unused descriptor. It returns the new file descriptor on success, and -1 on error.

Prototype: int dup(int oldfd);

Library: #include <unistd.h>

Example:

#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>

int main() {
	int fd = open("/tmp/file", O_RDONLY);
	if (fd != -1) {
		int newfd = dup(fd);
		if (newfd != -1) {
			printf("Duplicated file descriptor: %d\n", newfd);
		} else {
			printf("Failed to duplicate file descriptor.\n");
		}
		close(fd);
	} else {
		printf("Failed to open /tmp/file.\n");
	}
	return 0;
}

In this example, the program opens the file /tmp/file and duplicates its file descriptor using dup, storing the new file descriptor in newfd. If dup succeeds, it prints "Duplicated file descriptor: " followed by the new file descriptor.
If dup fails, it prints "Failed to duplicate file descriptor.". If the file fails to open, it prints "Failed to open /tmp/file.".


---------------------------------------------------------------------------------
DUP2

The dup2 function is a standard C function that duplicates a file descriptor to a specified file descriptor.

Function Description: dup2 duplicates the file descriptor oldfd to newfd. If newfd was previously open, it is silently closed before being reused. If oldfd is not a valid file descriptor, then the call fails, and newfd is not closed. It returns the new file descriptor on success, and -1 on error.

Prototype: int dup2(int oldfd, int newfd);

Library: #include <unistd.h>

Example:

#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>

int main() {
	int fd = open("/tmp/file", O_RDONLY);
	if (fd != -1) {
		int newfd = dup2(fd, 10);
		if (newfd != -1) {
			printf("Duplicated file descriptor to: %d\n", newfd);
		} else {
			printf("Failed to duplicate file descriptor.\n");
		}
		close(fd);
	} else {
		printf("Failed to open /tmp/file.\n");
	}
	return 0;
}


In this example, the program opens the file /tmp/file and duplicates its file descriptor to descriptor 10 using dup2, storing the new file descriptor in newfd. If dup2 succeeds, it prints "Duplicated file descriptor to: " followed by the new file descriptor. If dup2 fails, it prints "Failed to duplicate file descriptor.".
If the file fails to open, it prints "Failed to open /tmp/file.".


---------------------------------------------------------------------------------
PIPE

The pipe function is a standard C function that creates a pipe, which is a unidirectional data channel that can be used for interprocess communication.

Function Description: pipe creates a pipe and places two file descriptors, one for reading and one for writing, into the array pointed to by pipefd. pipefd[0] is for reading, pipefd[1] is for writing. It returns 0 on success, and -1 on error.

Prototype: int pipe(int pipefd[2]);

Library: #include <unistd.h>

Example:

#include <stdio.h>
#include <unistd.h>

int main() {
	int pipefd[2];
	if (pipe(pipefd) == 0) {
		printf("Created a pipe. Read fd: %d, Write fd: %d\n", pipefd[0], pipefd[1]);
	} else {
		printf("Failed to create a pipe.\n");
	}
	return 0;
}

In this example, the program creates a pipe using pipe and stores the file descriptors in pipefd. If pipe succeeds, it prints "Created a pipe. Read fd: ", followed by the read file descriptor, ", Write fd: ",
followed by the write file descriptor. If pipe fails, it prints "Failed to create a pipe.".




---------------------------------------------------------------------------------
OPENDIR

The opendir function is a standard C function that opens a directory stream corresponding to the directory name, and returns a pointer to the directory stream. The stream is positioned at the first entry in the directory.

Function Description: opendir opens a directory stream corresponding to the directory name. The stream is positioned at the first entry in the directory. It returns a pointer to the directory stream. On error, NULL is returned.

Prototype: DIR *opendir(const char *name);

Library: #include <dirent.h>

Example:

#include <stdio.h>
#include <dirent.h>

int main() {
	DIR *dir = opendir("/tmp");
	if (dir) {
		printf("Opened the directory /tmp\n");
	} else {
		printf("Failed to open the directory /tmp.\n");
	}
	closedir(dir);
	return 0;
}

In this example, the program opens the directory /tmp using opendir and stores the directory stream in dir. If opendir succeeds, it prints "Opened the directory /tmp". If opendir fails, it prints "Failed to open the directory /tmp.".
After it's done with the directory, it closes the directory stream using closedir.



---------------------------------------------------------------------------------
READDIR

The readdir function is a standard C function that reads the next directory entry from the directory stream dir.

Function Description: readdir reads the next directory entry from the directory stream dir. It returns a pointer to a dirent structure representing the next directory entry in the directory stream pointed to by dir. It returns NULL on reaching the end of the directory stream or if an error occurred.

Prototype: struct dirent *readdir(DIR *dir);

Library: #include <dirent.h>

Example:

#include <stdio.h>
#include <dirent.h>

int main() {
	DIR *dir = opendir("/tmp");
	if (dir) {
		struct dirent *entry;
		while ((entry = readdir(dir)) != NULL) {
			printf("Found directory entry: %s\n", entry->d_name);
		}
	} else {
		printf("Failed to open the directory /tmp.\n");
	}
	closedir(dir);
	return 0;
}

In this example, the program opens the directory /tmp using opendir and reads all directory entries using readdir, printing each one. If opendir fails, it prints "Failed to open the directory /tmp.".
After it's done with the directory, it closes the directory stream using closedir.

---------------------------------------------------------------------------------
CLOSEDIR

The closedir function is a standard C function that closes a directory stream.

Function Description: closedir closes the directory stream associated with dir. A successful call to closedir also closes the underlying file descriptor associated with dir. The directory stream descriptor dir is not available after this call. It returns 0 on success, and -1 on error.

Prototype: int closedir(DIR *dir);

Library: #include <dirent.h>

Example:

#include <stdio.h>
#include <dirent.h>

int main() {
	DIR *dir = opendir("/tmp");
	if (dir) {
		struct dirent *entry;
		while ((entry = readdir(dir)) != NULL) {
			printf("Found directory entry: %s\n", entry->d_name);
		}
		if (closedir(dir) == 0) {
			printf("Closed the directory /tmp\n");
		} else {
			printf("Failed to close the directory /tmp.\n");
		}
	} else {
		printf("Failed to open the directory /tmp.\n");
	}
	return 0;
}

In this example, the program opens the directory /tmp using opendir, reads all directory entries using readdir, and then closes the directory using closedir. If closedir succeeds, it prints "Closed the directory /tmp". If closedir fails, it prints "Failed to close the directory /tmp.".
If opendir fails, it prints "Failed to open the directory /tmp.".




---------------------------------------------------------------------------------
STRERROR

The strerror function is a standard C function that returns a string describing the error code passed in the argument errno.

Function Description: strerror returns a pointer to a string that describes the error code passed in the argument errnum. The string is actually a static buffer that is overwritten by each call to strerror.

Prototype: char *strerror(int errnum);

Library: #include <string.h>

Example:

#include <stdio.h>
#include <string.h>
#include <errno.h>

int main() {
	FILE *file = fopen("/nonexistent", "r");
	if (!file) {
		printf("Error: %s\n", strerror(errno));
	}
	return 0;
}

In this example, the program tries to open a non-existent file. When the fopen call fails,
it prints the error message associated with the current errno value using strerror.

---------------------------------------------------------------------------------
PERROR

The perror function is a standard C function that prints a descriptive error message to stderr.

Function Description: perror produces a message on the standard error output, describing the last error encountered during a call to a system or library function. It takes a string argument which is printed, followed by a colon and a space, and then the error message and a new line.

Prototype: void perror(const char *str);

Library: #include <stdio.h>

Example:

#include <stdio.h>

int main() {
	FILE *file = fopen("/nonexistent", "r");
	if (!file) {
		perror("Error opening file");
	}
	return 0;
}

In this example, the program tries to open a non-existent file. When the fopen call fails, it prints the error message associated with the current errno value using perror.
The output will be something like "Error opening file: No such file or directory".


--------------------------------------------------------------------------------
ISATTY

The isatty function is a standard C function that checks if a file descriptor refers to a terminal.

Function Description: isatty checks if the file descriptor fd refers to a terminal. It returns 1 if fd is an open file descriptor referring to a terminal; otherwise 0 is returned, and errno is set to indicate the error.

Prototype: int isatty(int fd);

Library: #include <unistd.h>

Example:

#include <stdio.h>
#include <unistd.h>

int main() {
	if (isatty(STDOUT_FILENO)) {
		printf("STDOUT is a terminal.\n");
	} else {
		printf("STDOUT is not a terminal.\n");
	}
	return 0;
}

In this example, the program checks if the standard output (STDOUT) is a terminal using isatty. If isatty returns 1, it prints "STDOUT is a terminal.".
If isatty returns 0, it prints "STDOUT is not a terminal.".




---------------------------------------------------------------------------------
TTYNAME

The ttyname function is a standard C function that returns a pointer to a string which describes the terminal device that is open on the file descriptor fd.

Function Description: ttyname returns a pointer to a string which describes the terminal device that is open on the file descriptor fd. The string is a static buffer that is overwritten by each call to ttyname. If fd is not an open file descriptor or if it is not associated with a terminal, NULL is returned.

Prototype: char *ttyname(int fd);

Library: #include <unistd.h>

Example:

#include <stdio.h>
#include <unistd.h>

int main() {
	char *name = ttyname(STDOUT_FILENO);
	if (name) {
		printf("Terminal name: %s\n", name);
	} else {
		printf("STDOUT is not a terminal.\n");
	}
	return 0;
}

In this example, the program gets the name of the terminal associated with the standard output (STDOUT) using ttyname. If ttyname returns a name, it prints "Terminal name: " followed by the name.
If ttyname returns NULL, it prints "STDOUT is not a terminal.".


---------------------------------------------------------------------------------
TTYSLOT

The ttyslot function is a standard C function that returns the index of the current user's terminal in the system's utmp file (a record of all logins and logouts).

Function Description: ttyslot returns the index of the current user's terminal in the system's utmp file. If the user is not logged in, or the process is not attached to a terminal, or an error occurred, it returns 0.

Prototype: int ttyslot(void);

Library: #include <unistd.h>

Example:

#include <stdio.h>
#include <unistd.h>

int main() {
	int slot = ttyslot();
	if (slot > 0) {
		printf("The terminal slot in the utmp file: %d\n", slot);
	} else {
		printf("The process is not attached to a terminal, or an error occurred.\n");
	}
	return 0;
}

In this example, the program gets the terminal slot in the utmp file using ttyslot. If ttyslot returns a slot greater than 0, it prints "The terminal slot in the utmp file: " followed by the slot number. If ttyslot returns 0,
it prints "The process is not attached to a terminal, or an error occurred.".


---------------------------------------------------------------------------------
IOCTL

The ioctl function is a standard C function that provides a generic interface for various I/O operations.

Function Description: ioctl manipulates the underlying device parameters of special files. In particular, many operating characteristics of character special files (e.g., terminals) may be controlled with ioctl requests. The argument fd must be an open file descriptor. The second argument is a device-dependent request code. The third argument is usually zero, or a pointer to a structure.

Prototype: int ioctl(int fd, unsigned long request, ...);

Library: #include <sys/ioctl.h>

Example:

#include <stdio.h>
#include <unistd.h>
#include <sys/ioctl.h>

int main() {
	struct winsize w;
	if (ioctl(STDOUT_FILENO, TIOCGWINSZ, &w) == 0) {
		printf("Terminal size: %d rows, %d columns\n", w.ws_row, w.ws_col);
	} else {
		perror("ioctl");
	}
	return 0;
}

In this example, the program gets the size of the terminal using ioctl with the TIOCGWINSZ request. If ioctl succeeds, it prints "Terminal size: " followed by the number of rows and columns.
If ioctl fails, it prints an error message using perror.




---------------------------------------------------------------------------------
GETENV

The getenv function is a standard C function that retrieves the value of an environment variable.

Function Description: getenv searches the environment list provided by the host environment (the operating system, in most cases) to find the environment variable name, and returns a pointer to the value of the variable, or NULL if the variable is not found.

Prototype: char *getenv(const char *name);

Library: #include <stdlib.h>

Example:

#include <stdio.h>
#include <stdlib.h>

int main() {
	char *path = getenv("PATH");
	if (path) {
		printf("PATH: %s\n", path);
	} else {
		printf("PATH environment variable not found.\n");
	}
	return 0;
}

In this example, the program gets the value of the "PATH" environment variable using getenv. If getenv returns a value, it prints "PATH: " followed by the value.
If getenv returns NULL, it prints "PATH environment variable not found.".


---------------------------------------------------------------------------------
TCSETATTR

The tcsetattr function is a standard C function that sets the parameters associated with the terminal.

Function Description: tcsetattr sets the parameters associated with the terminal (unless support is required from the underlying hardware that is not available) from the termios structure referred to by termios_p. fd is the file descriptor of the terminal. The change is made immediately. If any requested change could not be successfully carried out, the function returns -1 and leaves the state of the terminal unchanged.

Prototype: int tcsetattr(int fd, int optional_actions, const struct termios *termios_p);

Library: #include <termios.h>

Example:

#include <stdio.h>
#include <termios.h>
#include <unistd.h>

int main() {
	struct termios term;
	if (tcgetattr(STDIN_FILENO, &term) == 0) {
		term.c_lflag &= ~ECHO;
		if (tcsetattr(STDIN_FILENO, TCSANOW, &term) != 0) {
			perror("tcsetattr");
		}
	} else {
		perror("tcgetattr");
	}
	return 0;
}

In this example, the program first gets the current terminal parameters using tcgetattr. Then it modifies the parameters to disable echoing of input characters. Finally, it sets the new terminal parameters using tcsetattr. If tcsetattr fails, it prints an error message using perror.
If tcgetattr fails, it also prints an error message using perror.





---------------------------------------------------------------------------------
TCGETATTR

The tcgetattr function is a standard C function that gets the parameters associated with the terminal.

Function Description: tcgetattr gets the parameters associated with the terminal and stores them in the termios structure referenced by termios_p. fd is the file descriptor of the terminal. The function returns 0 on success, and -1 on failure.

Prototype: int tcgetattr(int fd, struct termios *termios_p);

Library: #include <termios.h>

Example:

#include <stdio.h>
#include <termios.h>
#include <unistd.h>

int main() {
	struct termios term;
	if (tcgetattr(STDIN_FILENO, &term) == 0) {
		printf("Got terminal attributes successfully.\n");
	} else {
		perror("tcgetattr");
	}
	return 0;
}

In this example, the program gets the current terminal parameters using tcgetattr and stores them in a termios structure. If tcgetattr succeeds, it prints "Got terminal attributes successfully.".
If tcgetattr fails, it prints an error message using perror.


---------------------------------------------------------------------------------
TGETENT

The tgetflag function is a part of the termcap library in Unix-like operating systems that checks for the existence of a boolean capability in the termcap entry.

Function Description: tgetflag checks for the existence of a boolean capability id in the termcap entry. It returns 1 if the capability is found, and 0 if it is not found.

Prototype: int tgetflag(char *id);

Library: #include <termcap.h>

Example:

#include <stdio.h>
#include <termcap.h>

int main() {
	char term_buffer[1024];
	char *term_type = getenv("TERM");
	if (tgetent(term_buffer, term_type) > 0) {
		if (tgetflag("am")) {
			printf("The terminal has automatic margins.\n");
		} else {
			printf("The terminal does not have automatic margins.\n");
		}
	} else {
		printf("Failed to load termcap entry for %s.\n", term_type);
	}
	return 0;
}

In this example, the program gets the termcap entry for the terminal type specified by the "TERM" environment variable using tgetent. If tgetent returns a value greater than 0, it checks if the terminal has the "am" (automatic margins) capability using tgetflag. If tgetflag returns 1, it prints "The terminal has automatic margins.". If tgetflag returns 0, it prints "The terminal does not have automatic margins.". If tgetent returns a value less than or equal to 0,
it prints "Failed to load termcap entry for " followed by the terminal type.



---------------------------------------------------------------------------------
TGETFLAG

The tgetflag function is a part of the termcap library in Unix-like operating systems that checks for the existence of a boolean capability in the termcap entry.

Function Description: tgetflag checks for the existence of a boolean capability id in the termcap entry. It returns 1 if the capability is found, and 0 if it is not found.

Prototype: int tgetflag(char *id);

Library: #include <termcap.h>

Example:

#include <stdio.h>
#include <termcap.h>

int main() {
	char term_buffer[1024];
	char *term_type = getenv("TERM");
	if (tgetent(term_buffer, term_type) > 0) {
		if (tgetflag("am")) {
			printf("The terminal has automatic margins.\n");
		} else {
			printf("The terminal does not have automatic margins.\n");
		}
	} else {
		printf("Failed to load termcap entry for %s.\n", term_type);
	}
	return 0;
}

In this example, the program gets the termcap entry for the terminal type specified by the "TERM" environment variable using tgetent. If tgetent returns a value greater than 0, it checks if the terminal has the "am" (automatic margins) capability using tgetflag. If tgetflag returns 1, it prints "The terminal has automatic margins.". If tgetflag returns 0, it prints "The terminal does not have automatic margins.". If tgetent returns a value less than or equal to 0,
it prints "Failed to load termcap entry for " followed by the terminal type.



---------------------------------------------------------------------------------
TGETNUM

The tgetnum function is a part of the termcap library in Unix-like operating systems that retrieves the numeric value of a capability from the termcap entry.

Function Description: tgetnum retrieves the numeric value of the capability id from the termcap entry. It returns the numeric value if the capability is found, and -1 if it is not found.

Prototype: int tgetnum(char *id);

Library: #include <termcap.h>

Example:

#include <stdio.h>
#include <termcap.h>

int main() {
	char term_buffer[1024];
	char *term_type = getenv("TERM");
	if (tgetent(term_buffer, term_type) > 0) {
		int cols = tgetnum("co");
		if (cols >= 0) {
			printf("The terminal has %d columns.\n", cols);
		} else {
			printf("The number of columns is not defined for this terminal.\n");
		}
	} else {
		printf("Failed to load termcap entry for %s.\n", term_type);
	}
	return 0;
}

In this example, the program gets the termcap entry for the terminal type specified by the "TERM" environment variable using tgetent. If tgetent returns a value greater than 0, it retrieves the number of columns ("co") using tgetnum. If tgetnum returns a value greater than or equal to 0, it prints "The terminal has " followed by the number of columns. If tgetnum returns a value less than 0,
it prints "The number of columns is not defined for this terminal.". If tgetent returns a value less than or equal to 0, it prints "Failed to load termcap entry for " followed by the terminal type.





---------------------------------------------------------------------------------
TGETSTR

The tgetstr function is a part of the termcap library in Unix-like operating systems that retrieves the string value of a capability from the termcap entry.

Function Description: tgetstr retrieves the string value of the capability id from the termcap entry. It returns a pointer to the string if the capability is found, and NULL if it is not found.

Prototype: char *tgetstr(char *id, char **area);

Library: #include <termcap.h>

Example:

#include <stdio.h>
#include <termcap.h>

int main() {
	char term_buffer[1024];
	char cap_buffer[1024];
	char *term_type = getenv("TERM");
	char *cap_ptr = cap_buffer;
	if (tgetent(term_buffer, term_type) > 0) {
		char *clr_eol = tgetstr("ce", &cap_ptr);
		if (clr_eol) {
			printf("The clear-to-end-of-line sequence is: %s\n", clr_eol);
		} else {
			printf("The clear-to-end-of-line sequence is not defined for this terminal.\n");
		}
	} else {
		printf("Failed to load termcap entry for %s.\n", term_type);
	}
	return 0;
}


In this example, the program gets the termcap entry for the terminal type specified by the "TERM" environment variable using tgetent. If tgetent returns a value greater than 0, it retrieves the clear-to-end-of-line ("ce") sequence using tgetstr. If tgetstr returns a non-null pointer, it prints "The clear-to-end-of-line sequence is: " followed by the sequence. If tgetstr returns a null pointer, it prints "The clear-to-end-of-line sequence is not defined for this terminal.". If tgetent returns a value less than or equal to 0,
it prints "Failed to load termcap entry for " followed by the terminal type.



---------------------------------------------------------------------------------
TGOTO

The tgoto function is a part of the termcap library in Unix-like operating systems that formats a cursor addressing string.

Function Description: tgoto formats a cursor addressing string cm with the row destcol and column destline. It returns a pointer to a static area containing the escape sequence to move the cursor to the specified position.

Prototype: char *tgoto(const char *cm, int destcol, int destline);

Library: #include <termcap.h>

Example:

#include <stdio.h>
#include <termcap.h>

int main() {
	char term_buffer[1024];
	char cap_buffer[1024];
	char *term_type = getenv("TERM");
	char *cap_ptr = cap_buffer;
	if (tgetent(term_buffer, term_type) > 0) {
		char *cursor_move = tgetstr("cm", &cap_ptr);
		if (cursor_move) {
			char *goto_str = tgoto(cursor_move, 10, 20);
			printf("The sequence to move the cursor to (10, 20) is: %s\n", goto_str);
		} else {
			printf("The cursor move sequence is not defined for this terminal.\n");
		}
	} else {
		printf("Failed to load termcap entry for %s.\n", term_type);
	}
	return 0;
}

In this example, the program gets the termcap entry for the terminal type specified by the "TERM" environment variable using tgetent.
If tgetent returns a value greater than 0, it retrieves the cursor move ("cm") sequence using tgetstr.
If tgetstr returns a non-null pointer, it formats the sequence to move the cursor to the position (10, 20) using tgoto and prints "The sequence to move the cursor to (10, 20) is: " followed by the sequence. If tgetstr returns a null pointer, it prints "The cursor move sequence is not defined for this terminal.". If tgetent returns a value less than or equal to 0, it prints "Failed to load termcap entry for " followed by the terminal type.



---------------------------------------------------------------------------------
TPUTS

The tputs function is a part of the termcap library in Unix-like operating systems that outputs a termcap string to the terminal.

Function Description: tputs outputs the termcap string str to the terminal. It uses the function putc to output each character. The affcnt argument is the number of lines affected by the operation, or 1 if not applicable. The putc argument is a pointer to a function that takes a single character and outputs it to the terminal.

Prototype: int tputs(const char *str, int affcnt, int (*putc)(int));

Library: #include <termcap.h>

Example:

#include <stdio.h>
#include <termcap.h>

int putch(int ch) {
	return putchar(ch);
}

int main() {
	char term_buffer[1024];
	char cap_buffer[1024];
	char *term_type = getenv("TERM");
	char *cap_ptr = cap_buffer;
	if (tgetent(term_buffer, term_type) > 0) {
		char *cursor_move = tgetstr("cm", &cap_ptr);
		if (cursor_move) {
			char *goto_str = tgoto(cursor_move, 10, 20);
			tputs(goto_str, 1, putch);
		} else {
			printf("The cursor move sequence is not defined for this terminal.\n");
		}
	} else {
		printf("Failed to load termcap entry for %s.\n", term_type);
	}
	return 0;
}

In this example, the program gets the termcap entry for the terminal type specified by the "TERM" environment variable using tgetent. If tgetent returns a value greater than 0, it retrieves the cursor move ("cm") sequence using tgetstr.
If tgetstr returns a non-null pointer, it formats the sequence to move the cursor to the position (10, 20) using tgoto and outputs it to the terminal using tputs. If tgetstr returns a null pointer, it prints "The cursor move sequence is not defined for this terminal.". If tgetent returns a value less than or equal to 0,
it prints "Failed to load termcap entry for " followed by the terminal type.


---------------------------------------------------------------------------------

