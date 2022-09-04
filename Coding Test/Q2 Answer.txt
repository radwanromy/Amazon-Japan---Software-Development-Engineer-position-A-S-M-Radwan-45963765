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
    public static long findTotalImbalance(List<Integer> rank) {
    long m_imbalance = 0;
          int r  = 0;           
          TreeSet<Integer> m_set = new TreeSet<>();  
          while ( r < rank.size()-1) {
              m_set.clear();
              m_set.add(rank.get(r));
              long curm_imbalance = 0;
              for (int i = r + 1; i < rank.size();i++) {
                  Integer e = rank.get(i);
                  m_set.add(e);
                  Integer f = m_set.lower(e);
                  Integer c = m_set.higher(e);
                  if (f == null) {
                      curm_imbalance += ((c-e)>1?1:0);
                  } 
                  else if (c == null) {
                      curm_imbalance += (((e-f)>1)?1:0);
                  }  
                  else {
                      curm_imbalance += (c-f)>1?-1:0;
                      curm_imbalance += (((c-e)>1)?1:0);
                      curm_imbalance += ((e-f))>1?1:0;
                  }
                  m_imbalance += curm_imbalance;
              }
              r ++;
          }      
          return m_imbalance;     
    }
}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));
        int rankCount = Integer.parseInt(bufferedReader.readLine().trim());
        List<Integer> rank = IntStream.range(0, rankCount).mapToObj(i -> {
            try {
                return bufferedReader.readLine().replaceAll("\\s+$", "");
            } catch (IOException ex) {
                throw new RuntimeException(ex);
            }
        })
            .map(String::trim)
            .map(Integer::parseInt)
            .collect(toList());
        long result = Result.findTotalImbalance(rank);
        bufferedWriter.write(String.valueOf(result));
        bufferedWriter.newLine();
        bufferedReader.close();
        bufferedWriter.close();
    }
}
