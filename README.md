Sort an array according to the order defined by the other array
Here we will learn about Java program to Sort an array according to the order defined by another array which is discussed over here. We are given two arrays A [] and B [], sort A in such a way that the relative order among the elements will be the same as those are in B. The elements in array A has to be printed accordingly to the sequence of order of elements specified in array B, the rest of the elements, remaining in array A are printed at the end.

Java program to Sort an array according to the order defined by another array
Method Discussed :
Method 1 : Using Sorting and Binary searching.
Method 2 : By making customized comparator.
Method 1 :
Declare a temporary array temp of size m and copy the contents of arr1[] to it.
Declare another array visited[] and initialize all entries in it as false. visited[] is used to mark those elements in temp[] which are copied to arr1[].
Sort temp[] using any sorting technique
Declare the output index ind as 0.
Do following for every element of arr2[i] in arr2[] 
Binary search for all occurrences of arr2[i] in temp[], if present then copy all occurrences to arr1[ind] and increment ind. Also mark the copied elements visited[]
Copy all unvisited elements from temp[] to arr1[]
Method 1 : Code in Java

// Java program to sort an array according to the order defined by another array


import java.io.*;
import java.util.Arrays;

class PrepInsta 
       {

    // Binary search
    static int first(int arr[], int l, int h,
                     int x, int n)
    {
        if (h >= l)
        {
            int mid = l + (h-l)/2;

            if ((mid == 0 || x > array[mid-1]) &&
                array[m] == x)
                return mid;
            if (x > array[m])
                return first(arr, (m + 1), h,
                             x, n);
            return first(array, l, (m -1), x, n);
        }
        return -1;
    }

    // Sort according to the order defined by array 2 
    static void sort_according(int array1[], int array2[], int m,
                               int n)
    {

        int temp[] = new int[m1], visited[] = new int[m1];
        for (int i = 0; i < m1; i++)
        {
            temp[i] = array1[i];
            visited[i] = 0;
        }

        // Sort elements in temp
        Arrays.sort(temp);
        int ind = 0;

        for (int i = 0; i < n; i++)
        {

            int f = first(temp, 0, m1-1, array2[i], m);

            // If not present, no need to proceed
            if (f == -1) continue;

            // Copy all occurrences of arr2[i] to arr1[]
            for (int j = f; (j < m && temp[j] == arr2[i]);
                 j++)
            {
                arr1[ind++] = temp[j];
                visited[j] = 1;
            }
        }

        for (int i = 0; i < m1; i++)
            if (visited[i] == 0)
                arr1[ind++] = temp[i];
    }

    // Function to print an array
    static void print_array(int array[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(array[i] + " ");
        System.out.println();
    }

    public static void main(String args[])
    {
        int arr1[] = {1, 2, 3, 4, 3, 2, 4, 2, 5};
        int arr2[] = {4, 2, 1, 3};
        int m = arr1.l;
        int n = arr2.l;
        System.out.print("The Sorted array : ");
        sort_according(array1, array2, m1, n);
        print_array(arr1, m1);
    }
}
Output:-
4, 4, 2, 2, 2, 1, 3, 3, 5
Related Pages
Determine can all numbers of an array be made equal

Finding Minimum sum of absolute difference of given array

Replace each element of the array by its rank in the array

Finding equilibrium index of an array

Rotation of elements of array- left and right 

Method 2 :
In this method we will create our own customized compare method.
Method 2 : Code in Java
import java.io.*;
import java.util.Arrays;
import java.util.HashMap;
 
class Main {
 
    static void sortAccording(int[] A1, int[] A2, int m, int n)
    {
        HashMap index = new HashMap<>();
 
        for (int i = 0; i < n; i++) {
            if (!index.containsKey(A2[i]))
                index.put(A2[i], i + 1);
        }
 
        
        int[] tmp= Arrays.stream(A1).boxed().sorted((p1, p2) -> {
                      int idx1 = index.getOrDefault(p1, 0);
                      int idx2 = index.getOrDefault(p2, 0);
 
                      if (idx1 == 0 && idx2 == 0)
                          return p1 - p2;
 
                      if (idx1 == 0)
                          return 1;
 
                      if (idx2 == 0)
                          return -1;
 
                      return idx1 - idx2;
                  }).mapToInt(i -> i).toArray();
 
        // Sorted values are copied to the original
        // array
        for (int i = 0; i < m; i++) {
            A1[i] = tmp[i];
        }
    }
 
    // Driver program to test the above function
    public static void main(String[] args)
    {
        int arr1[] = { 20, 1, 20, 5, 7, 1, 9, 39, 6, 18, 18 };
        int arr2[] =  { 20, 1, 18, 39 };
        int m = arr1.length;
        int n = arr2.length;
        sortAccording(arr1, arr2, m, n);
        System.out.println(Arrays.toString(arr1));
    }
}
 
   
Output:-
[20, 20, 1, 1, 18, 18, 39, 5, 6, 7, 9]
