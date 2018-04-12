[用read4() API读取N个字符-单次调用](https://leetcode.com/problems/read-n-characters-given-read4/description/)

```
The API: int read4(char *buf) reads 4 characters at a time from a file.

The return value is the actual number of characters read. For example, it returns 3 if there is only 3 characters left in the file.

By using the read4 API, implement the function int read(char *buf, int n) that reads n characters from the file.

Note:
The read function will only be called once for each test case.
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
    char[] buffer = new char[4];
    int bufferPtr = 0, bufferCnt = 0;
    
    public int read(char[] buf, int n) {
        int cnt = 0;
        
        while (cnt < n) {
            if (bufferPtr == bufferCnt) {
                bufferCnt = read4(buffer);
                bufferPtr = 0;
            }
            
            if (bufferCnt == 0) {
                break;
            }
            
            while (cnt < n && bufferPtr < bufferCnt) {
                buf[cnt++] = buffer[bufferPtr++];
            }          
        }
        
        return cnt;
    }
}
```


