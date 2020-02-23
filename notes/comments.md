# Comments
### Comments don't make up for bad code
Clear and expressive code with few comments is far superior to cluttered and complex
code with lots of comments.

### Good comments | 什么时候comment
1. Legal comments
Copyright and authorship statements are necessary and reasonable things to put into a comment at the start of each source file.
2. Informative comments
举例：
```java
// format matched kk:mm:ss EEE, MMM dd, yyyy
Pattern timeMatcher = Pattern.compile("\\d*:\\d*:\\d* \\w*, \\w* \\d*, \\d*");
```
3. Explanation of intent
