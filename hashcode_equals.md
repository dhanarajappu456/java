The hashcode and equals from the objects are based on references, by default 


that is hashcode generated is  based on memory address not content and equals check for ,  refernces are same not content

if you need it based on content you need to override it with necessary logic, 

consider how equals and hashcode behave  differently   in case of array and other collections

# for Arrays 
  _________________
the Arrays.equals and Arrays.hahscode ovveride it based  on content 

if you had a set with array as element and checking presence of same array  would give false, since by defualt the equals and hahscod of object class is called
which is not overriden for array ,
```
// Create a Set of arrays
        Set<int[]> set = new HashSet<>();

        // Create the array to check
        int[] arrayToCheck = {1, 2};

        // Add some arrays to the Set
        int[] array1 = {1, 2};
        int[] array2 = {3, 4};
        set.add(array1);
        set.add(array2);

        System.out.println("The Set contains the array [1, 2]." + " "+ set.contains(new int[]{1,2}));
```
so you need to override  equals  and  hashcode , based on content , for  which you can use Array.equals and Arrays.hashcode when overriding the equals and hashcode, 



# for collectionss
for collections , remember the equals and hashcode is already overriden based on content ,  you can directly use contains without worrying

```
import java.util.*;

public class Main {
    public static void main(String[] args) {
        // Create a Set of Lists
        Set<List<Integer>> set = new HashSet<>();

        // Create the List to check
        List<Integer> listToCheck = new ArrayList<>();
        listToCheck.add(1);
        listToCheck.add(2);

        // Add some Lists to the Set
        List<Integer> list1 = new ArrayList<>();
        list1.add(1);
        list1.add(2);

        List<Integer> list2 = new ArrayList<>();
        list2.add(3);
        list2.add(4);

        set.add(list1);
        set.add(list2);

        // Check if the Set contains the List
        boolean containsList = set.contains(listToCheck);

        if (containsList) {
            System.out.println("The Set contains the list [1, 2]."); 
        } else {
            System.out.println("The Set does not contain the list [1, 2].");
        }
    }
}
```
this returns true
