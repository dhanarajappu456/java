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


# map with custom  object as the key, - u need to override the hashcode and equals for the class of object which is the key



```
import java.util.*;

class HelloWorld {
    public static void main(String[] args) {
     
        
         Map<A,Integer> mp= new HashMap<>();
    //each time you put a element to hashamp , its hash is calcculated , based on which 
    //the bucket is detemined
    
    mp.put(new A(100),100);
     mp.put(new A(200),200);
     // when you check for contains or get, it calls hashcode to get the bucket, then 
     // for all the element in the bucket calls equals , that determines the mathching element
     System.out.println(mp.containsKey(new A(100)));
  

    }
    
   
}

class A{
  
  int a;
  A(int val){
    this.a = val;
  }
  
  @Override
  public boolean equals(Object o){
    System.out.println("secondly the equals is checked");
    if (this == o){
      return true;
    }
    if(o ==null || this.getClass() != o.getClass()){
      return false;
      
    }
    A obj = (A)o;
    return this.a == obj.a;
    
  }
  @Override
  public int hashCode(){
      System.out.println("first hashcode checked ");
  # note the static hashcode method  of Objects class, used to get hashcode of any object
  #there is another method in this class which is equals used to compare two objects even passing null as one argument
    return Objects.hashCode(a);
  }
}
```

# Arraylist with custom objects -
here equals on individual object  is called  when we compare two lists 
eventough the hashcode is not used  here, it is best practice to overrdie both equals and hashcode always for 
custom objects

```
import java.util.ArrayList;
import java.util.List;


public class Main {
    public static void main(String[] args) {
        List<CustomObject> list1 = new ArrayList<>();
        list1.add(new CustomObject(1));
        list1.add(new CustomObject(2));
        list1.add(new CustomObject(3));

        List<CustomObject> list2 = new ArrayList<>();
        list2.add(new CustomObject(1));
        list2.add(new CustomObject(2));
        list2.add(new CustomObject(3));

        // Check equality using equals method
        System.out.println(list1.equals(list2));  // true
    }
}
class CustomObject {
    int value;

    CustomObject(int value) {
        this.value = value;
    }

    @Override
    public boolean equals(Object obj) {
      System.out.println("equals called");  // true
        if (this == obj) {
            return true;
        }
        if (obj == null || getClass() != obj.getClass()) {
            return false;
        }
        CustomObject other = (CustomObject) obj;
        return value == other.value;
    }

    @Override
    public int hashCode() {
      System.out.println("hash called");  // true
        return Integer.hashCode(value);
    }
}

Output:

equals called
equals called
equals called
true
