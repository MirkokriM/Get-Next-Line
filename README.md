<img src="https://github.com/MirkokriM/42_Common_Core/blob/main/README.FILE/Copia%20di%20MirkokriM_github42_GNL.png">

## Table of Contents
- [Description](#description)
- [Usage](#usage)
- [Function Descriptions](#function-descriptions)
- [Bonus](#bonus)

## Description
The Get_Next_Line function is designed to read a single line from a file descriptor (`fd`) each time it is called. It stores the read line in a dynamically allocated string and returns that string. Subsequent calls to Get_Next_Line will continue reading the file from the previous position until reaching the end of the file.

The function prototype is defined as follows:
```c
char	*get_next_line(int fd);
```
The function takes an integer parameter `fd`, representing the file descriptor of the file to be read. It returns a pointer to a string that contains the line read from the file descriptor, or `NULL` if the end of the file has been reached or an error occurs.

The function uses a static variable to keep track of the file position and the content of the file that has been read but not yet returned to the caller. It reads a defined buffer size from the file descriptor and stores any remaining content in a static variable to be used in subsequent calls.

## Usage
To use the Get_Next_Line function in your project, follow these steps:

1. Copy the `get_next_line.c`, `get_next_line_utils.c`, and `get_next_line.h` files into your project directory.
2. Include the `get_next_line.h` header file in your source files where you want to use the function.
3. Compile your project, linking the `get_next_line.c` and `get_next_line_utils.c` files along with your other source files.
4. Call the `get_next_line` function with the desired file descriptor to read lines from that file.

Here is an example of how to use the Get_Next_Line function in a C program:
```c
#include "get_next_line.h"
#include <fcntl.h>
#include <stdio.h>

int main()
{
    int fd = open("file.txt", O_RDONLY);
    char *line;

    if (fd < 0)
    {
        perror("Error opening file");
        return 1;
    }

    while ((line = get_next_line(fd)) != NULL)
    {
        printf("%s\n", line);
        free(line);
    }

    close(fd);
    return 0;
}
```

## Function Descriptions
The Get_Next_Line project includes several additional functions to support the main functionality of reading lines from a file descriptor. Here is a brief description of each function:

### ft_read_to_left_str
```c
char *ft_read_to_left_str(int fd, char *left_str);
```
- This function is used internally by the `get_next_line` function to read from the file descriptor and append the read content to the existing content stored in the `left_str` variable.
- It returns a pointer to a new string that contains the concatenated content.

### ft_strchr
```c
char *ft_strchr(char *s, int c);
```
- This function is used internally by the `get_next_line` function to search for a specific character `c` in the string `s`.
- It returns a pointer to the first occurrence of the character `c`

 in the string `s`, or `NULL` if the character is not found.

### ft_strlen
```c
size_t ft_strlen(char *s);
```
- This function calculates the length of the string `s`.
- It returns the number of characters in the string.

### ft_strjoin
```c
char *ft_strjoin(char *left_str, char *buff);
```
- This function concatenates the string `left_str` with the string `buff`.
- It returns a pointer to a new string that contains the concatenated content.

### ft_get_line
```c
char *ft_get_line(char *left_str);
```
- This function extracts a line from the string `left_str`.
- It returns a pointer to a new string that contains the extracted line.

### ft_new_left_str
```c
char *ft_new_left_str(char *left_str);
```
- This function generates a new string that contains the remaining content after the extracted line from `left_str`.
- It returns a pointer to the new string.

## Bonus
The Get_Next_Line function also includes a bonus feature, allowing it to handle multiple file descriptors simultaneously. This is achieved by maintaining separate static variables for each file descriptor. The function prototype and usage remain the same as in the main implementation.

To use the Get_Next_Line function with multiple file descriptors, simply call the function with the desired file descriptor each time you want to read a line from that file.
