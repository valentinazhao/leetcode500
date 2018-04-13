[用read4()读取N个字符-多次调用](https://leetcode.com/problems/read-n-characters-given-read4-ii-call-multiple-times/description/)


```
The API: int read4(char *buf) reads 4 characters at a time from a file.

The return value is the actual number of characters read. For example, it returns 3 if there is only 3 characters left in the file.

By using the read4 API, implement the function int read(char *buf, int n) that reads n characters from the file.

Note:
The read function may be called multiple times.
```

```
宇宙问题: What is the difference between call once and call multiple times?

I think the difference is:
Call once: Assume you are always going to read from the start of the file/bufer.
Call multiple times: Start reading from where you left off. This means that you have to store the last place (ptr) where you stopped and store the read but uncopied bytes to the buffer.

I think code wise it should be same for both the cases except that the pointer from where to start reading the internal read4 buffer, the internal read4 buffer itself and the number of bytes to be read from that buffer, need to be stored in the 2nd case.

In plain C, I think if these fields are defined as static (int the 2nd case), then we will achieve the purpose.
```

```java
/* The read4 API is defined in the parent class Reader4.
      int read4(char[] buf); */

public class Solution extends Reader4 {
    /**
     * @param buf Destination buffer
     * @param n   Maximum number of characters to read
     * @return    The number of characters read
     */
    private int buffCnt = 4;
    private int buffPtr = 4;
    private char[] buff = new char[4];
    
    public int read(char[] buf, int n) {
        int ptr = 0;
        while (ptr < n) {
            if (buffPtr < buffCnt) {
                buf[ptr++] = buff[buffPtr++];
            } else if (buffPtr == buffCnt) {
                if (buffCnt < 4) {
                    break;
                }
                buffPtr = 0;
                buffCnt = read4(buff);
            }
        }
        
        return ptr;
    }
}
```
