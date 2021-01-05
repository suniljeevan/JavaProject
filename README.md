# JavaProject

Problem A 

Write a Java program to find Group anagrams ( Two words are anagram, if they have same characters but in different order e.g. ABC, BAC, CAB, CBA, BCA are anagrams)
    E.g. Words “CAT, “DOG”, “TAC”, ”MAD”, “DAM”, “AMD”, “GOD”, “SET”
         
Result should be in the form of : [CAT, TAC],  [DOG, GOD], [MAD, DAM, AMD], [SET]

Solution:
import java.util.*;
class ANARGRAMTEST {
 static List<Object> check(String[] S) {
 int size=S.length;
HashMap<String,ArrayList<String>> hm=new HashMap<String,ArrayList<String>>();
char[] arr;
for(int m=0;m<size;m++) {
arr=S[m].replaceAll("\\s","").toLowerCase().toCharArray();
Arrays.sort(arr);
String nw=new String(arr);
if(hm.containsKey(nw)){
hm.get(nw).add(S[m]);
}
else {
ArrayList<String> words=new ArrayList<String>();
words.add(S[m]);
hm.put(nw,words);
}
}
List<Object> big=new ArrayList<Object>();
for(String s:hm.keySet()) {
ArrayList<String> al=hm.get(s);
big.add(al);
}
return big;
}

public static void main(String args[]) {
int n;
System.out.println("Enter number of strings");
Scanner sc=new Scanner(System.in);
n=sc.nextInt();
String[] s=new String[n];
System.out.println("read input strings....");
for(int i=0;i<n;i++)
s[i]=sc.next();
System.out.println("ANARGRAM STRINGS ARE");
System.out.println(check(s));
}
}


Save the file with the name : ANARGRAMTEST.java
Compile the file : javac ANARGRAMTEST.java
Run the File : java ANARGRAMTEST
Enter number of strings
8
read input strings...
CAT
DOG
TAC
MAD
DAM
AMD
GOD
SET
ANARGRAM STRINGS ARE
[[CAT, TAC], [SET], [MAD, DAM, AMD], [DOG, GOD]]
 
---------------------------------------------------------------------------------------------------------------------------------------------------------------

Problem B
Given a phone directory, when user types name of person it should show suggestions for every character that is typed, create a library and a simple UI / CLI to test the output.

solution:
// Java Program to Implement a Dictionary

import java.util.*; 
class Node 
{ 
HashMap<Character,Node> child; 
boolean isLast; 
public Node() 
{ 
child = new HashMap<Character,Node>(); 
for (char i = 'a'; i <= 'z'; i++) 
child.put(i,null); 
isLast = false; 
} 
} 

class Dictionary
{ 
Node root; 
public void insertIntoDictionary(String contents[]) 
{ 
root = new Node(); 
int n = contents.length; 
for (int i = 0; i < n; i++) 
{ 
insert(contents[i]); 
} 
} 

public void insert(String s) 
{ 
int len = s.length(); 
Node itr = root; 
for (int i = 0; i < len; i++) 
{ 
Node nextNode = itr.child.get(s.charAt(i)); 
if (nextNode == null) 
{ 
nextNode = new Node(); 
itr.child.put(s.charAt(i),nextNode); 
} 
itr = nextNode; 
if (i == len - 1) 
itr.isLast = true; 
} 
} 

public void displayContentsUtil(Node curNode, String prefix)
{ 
if (curNode.isLast) 
System.out.println(prefix); 
		
for (char i = 'a'; i <= 'z'; i++) 
{ 
Node nextNode = curNode.child.get(i); 
if (nextNode != null) 
{ 
displayContentsUtil(nextNode, prefix + i); 
} 
} 
} 
	
void displayContents(String str) 
{ 
Node prevNode = root; 
String prefix = ""; 
int len = str.length(); 	
int i; 
for (i = 0; i < len; i++) 
{ 			
prefix += str.charAt(i); 			
char lastChar = prefix.charAt(i); 			
Node curNode = prevNode.child.get(lastChar); 			
if (curNode == null) 
{ 
System.out.println("No Results Found for "+ prefix  ); 			 
i++; 
break; 
} 
			
System.out.println("Suggestions based on "+ prefix + " are");  				
displayContentsUtil(curNode, prefix); 			
prevNode = curNode; 
} 
for ( ; i < len; i++) 
{ 
prefix += str.charAt(i); 
System.out.println("No Results Found for " + prefix  ); 							
} 
} 
} 

// Driver code 
class TestDictionary 
{ 
public static void main(String args[]) 
{ 
Dictionary dict = new Dictionary(); 
int n;
System.out.println("Enter size of Dictionary");
Scanner sc=new Scanner(System.in);
n=sc.nextInt();
String contents[] =new String[n];
System.out.println("Enter words to create Dictionary");
for(int i=0;i<n;i++)
contents[i]=sc.next();
dict.insertIntoDictionary(contents); 
String query ;	
System.out.println("Enter the word to search");
query=sc.next();
dict.displayContents(query); 
} 
} 

save the file as : TestDictionary.java
compile : javac TestDictionary.java
run the file : java TestDictionary
enter size of Dictionary
10
enter  words to create Dictionary
aaa
abc
abcde
fghji
ssss
ash
asha
xyz
sawe
pqr
Enter the word to search
as
Suggestions based on as are
ash
asha
