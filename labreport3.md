# Lab Report 3
---
## Part 1 - Bugs

- Failure inducing input for the buggy program:
  ```
  @Test
  public void testReverseInPlaceEven(){
    int[] input1 = { 1, 2, 3, 4 };
    ArrayExamples.reverseinPlace(input1);
    assertArrayEquals(new int[]{ 4, 3, 2, 1 }, input1);
  }
  ```

- Input that doesn't induce failure:
  ```
  @Test 
	public void testReverseInPlaceSingle() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
  ```

- Symptom (Output of the running tests):
  ![Image](CSE15L LAB3 EX 1.1.png)
  ![Image](CSE15L LAB3 EX 1.2.png)

- The bug (before and after code):
  - BEFORE:
    ```
    // Changes the input array to be in reversed order
    static void reverseInPlace(int[] arr) {
      for(int i = 0; i < arr.length; i += 1) {
        arr[i] = arr[arr.length - i - 1];
      }
    }
    ```
 
  - AFTER:
    ```
    // Changes the input array to be in reversed order
    static void reverseInPlace(int[] arr) {
      for(int i = 0; i < arr.length / 2; i += 1) {
        int temp = arr[i];
        arr[i] = arr[arr.length - i - 1];
        arr[arr.length - i - 1] = temp;
      }
    }
    ```

- This fixes the program because before, there was no temp variable that allowed us to store the old elements of the array in order to
  place them in the appropriate indices of the array all the way through. Furthermore, we only iterate halfway through the length of the array
  in the `for ` loop (`arr/length / 2`), in order to preserve the other elements of the original array, and not lose them while iterating.

## Part 2 - Researching Commands
