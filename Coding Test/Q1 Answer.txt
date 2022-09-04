import java.io.*;
import java.math.*;
import java.security.*;
import java.text.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.function.*;
import java.util.regex.*;
import java.util.stream.*;
import static java.util.stream.Collectors.joining;
import static java.util.stream.Collectors.toList;

class Result {
    public static int minSwapsRequired(String s) {
     int countOne = 0;
        int countZero = 0;  
        for(char c : s.toCharArray()) {
            if(c == '0') {
                countZero++;
            } else {
                countOne++;
            }
        }
        if(countOne%2 == 1 && countZero%2 == 1) {
            return -1;
        }   
        int mismatchedIndexes = 0;
        for(int i=0; i<(s.length()/2); i++) {
            if(s.charAt(i) != s.charAt(s.length()-1-i)) {
                mismatchedIndexes++;
            }
        }
        int countSwaps = mismatchedIndexes/2;
        if(mismatchedIndexes%2 == 1) {
            countSwaps++;
        }
        return countSwaps;
    }
}
public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));
        String s = bufferedReader.readLine();
        int result = Result.minSwapsRequired(s);
        bufferedWriter.write(String.valueOf(result));
        bufferedWriter.newLine();
        bufferedReader.close();
        bufferedWriter.close();
    }
}
