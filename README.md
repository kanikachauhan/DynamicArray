package a9;

import java.util.Arrays;

/**
 * A DynamicArray behaves like an array of strings, except that it can grow and
 * shrink. It is indexed beginning with zero. When a DynamicArray is created, it
 * is empty. Operations are provided to add, get, set, and remove elements at an index.
 * 
 */
public class DynamicArray {

	// Make the instance variable protected as the subclasses will be tightly
	// integrated with this class.
	protected String[] data; // the backing array
	protected int count; // The number of elements used in the data array
	/**
	 * Creates an empty dynamic array.
	 */
	public DynamicArray() {
		data = new String[0]; 
		count = 0;
	}

	/***
	 * Given an index i, returns a reference to an array that
	 * has space at i for a new value, and old values in the data 
	 * array copied into their appropriate locations. The count is 
	 * changed by 1 to account for the "opening" in the array.
	 * @param i
	 * @return
	 */
	public String[] growthStrategy(int i) {
		String[] newData;
		if (count == data.length) {
			newData = new String[data.length + 1];
		}
		else
			newData = data;

		for(int j = 0; j < i; j++) {
			newData[j] = data[j];
		}

		for(int j = size(); j > i; j--) {
			newData[j] = data[j - 1];
		}
		count++;
		return newData;
	}

	/**
	 * Adds a string s to the dynamic array at index i.
	 * 
	 * @param i
	 * @param s
	 */
	public void add(int i, String s) {
		if(i < 0 || i > size())
			throw new IndexOutOfBoundsException();

		// We have abstracted out the code that grows the array
		String[] newData = growthStrategy(i);
		newData[i] = s;
		data = newData;
	}

	/**
	 * Adds string s to end of the dynamic array.
	 * 
	 * @param s
	 */
	public void add(String s) {
		add(count, s);
	}

	/**
	 * Returns the string stored at index i in the dynamic array.
	 * 
	 * @param i
	 * @return the string stored at index i
	 */
	public String get(int i) {
		if(i < 0 || i >= size())
			throw new IndexOutOfBoundsException();

		return data[i];
	}

	/**
	 * Returns the number of elements in the dynamic array.
	 * 
	 * @return the number of elements
	 */
	public int size() {
		return count;
	}

	/**
	 * Changes the value of the string stored at index i in the dynamic array to
	 * s.
	 * 
	 * @param i
	 * @param s
	 */
	public void set(int i, String s) {
		if(i < 0 || i >= size())
			throw new IndexOutOfBoundsException();

		data[i] = s;
	}

	/***
	 * Given an index i, returns a reference to an array that
	 * has the value at i removed and the array values copied to their appropriate locations. 
	 * The count is changed by -1 to account for the "removal" in the array.
	 * @param i
	 * @return
	 */
	public String[] shrinkStrategy(int i) {
		String[] newData = new String[data.length - 1];
		count--;
		for(int j = 0; j < i; j++) {
			newData[j] = data[j];
		}

		for(int j = i; j < size(); j++) {
			newData[j] = data[j + 1];
		}

		return newData;
	}
	
	/**
	 * Removes the string at index i in the dynamic array.
	 * 
	 * @param i
	 */
	public void remove(int i) {
		if(i < 0 || i >= size())
			throw new IndexOutOfBoundsException();

		data = shrinkStrategy(i);
	}

	/**
	 * Returns the dynamic array as a formatted string.
	 * 
	 * @return the formatted string
	 */
	public String toString() {
		String result = "[";
		if(size() > 0) {
			result += get(0);
		}
		for(int i = 1; i < size(); i++) {
			result += ", " + get(i);
		}
		return result + "]"+" real length: " + data.length;
	}	
	
}
