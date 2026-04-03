

```markdown
 Review 5: Java Resource Leaks & try-with-resources

Severity:** High  
Language:** Java

Original Task Given to AI

> Write a method that reads the first line from a file and returns it as a string.

## Buggy AI-Generated Code

```java
// ❌ BUGGY CODE
public String readFirstLine(String filePath) throws IOException {
    BufferedReader reader = new BufferedReader(new FileReader(filePath));
    String firstLine = reader.readLine();
    reader.close();
    return firstLine;
}
// ✅ CORRECTED CODE
import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;

public String readFirstLine(String filePath) throws IOException {
    if (filePath == null || filePath.isBlank()) {
        throw new IllegalArgumentException("File path cannot be null or blank");
    }
    
    Path path = Paths.get(filePath);
    
    if (!Files.exists(path)) {
        throw new FileNotFoundException("File not found: " + filePath);
    }
    
    // try-with-resources automatically closes the reader
    try (BufferedReader reader = Files.newBufferedReader(path, StandardCharsets.UTF_8)) {
        return reader.readLine();
    }
    // No need for finally block or manual close()
}

// Alternative: Files.readAllLines for small files
public String readFirstLineSimple(String filePath) throws IOException {
    if (filePath == null || filePath.isBlank()) {
        throw new IllegalArgumentException("File path cannot be null or blank");
    }
    
    return Files.lines(Paths.get(filePath), StandardCharsets.UTF_8)
        .findFirst()
        .orElse(null);
}
// This is what the AI's code ACTUALLY does:
public String buggyVersion(String filePath) {
    BufferedReader reader = null;
    try {
        reader = new BufferedReader(new FileReader(filePath));
        return reader.readLine();
    } catch (IOException e) {
        // reader is still open here — LEAK!
        throw new RuntimeException(e);
    } finally {
        if (reader != null) {
            try {
                reader.close();

// This is what the AI's code ACTUALLY does:
public String buggyVersion(String filePath) {
    BufferedReader reader = null;
    try {
        reader = new BufferedReader(new FileReader(filePath));
        return reader.readLine();
    } catch (IOException e) {
        // reader is still open here — LEAK!
        throw new RuntimeException(e);
    } finally {
        if (reader != null) {
            try {
                reader.close();
            } catch (IOException e) {
                // Swallowing exception — bad!
            }
        }
    }
}
            } catch (IOException e) {
                // Swallowing exception — bad!
            }
        }
    }
}
