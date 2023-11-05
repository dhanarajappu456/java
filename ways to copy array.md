import java.util.*;
public class Main
{
	public static void main(String[] args) {
	     int[] a = {2, 3, 4, 5};
	    Arrays.copyOf(sourceArray, length to copy);
	    //returns the copied,
	   // remember copy always start with 0 indeex of the source, we can't specify the start
	   // ,only length to copy
	   //  int[] b = Arrays.copyOf(a,3); //[2,3,4]
	   
	   
	   // system.copy(srcArray, sourceStartIndex, destArray, destStartIndex, length to copy)
	   //doesn't return anything, copy made inplace to destArray specified
	   //int[] b = new int[10];
	   //System.arraycopy(a,1,b,2,2); //// [0, 0, 3, 4, 0, 0, 0, 0, 0, 0]
 	   System.out.println(Arrays.toString(b) );
	}
}
