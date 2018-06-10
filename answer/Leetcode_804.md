# Leetcode 804 Unique Morse Code Words 莫尔斯电码重复问题
题目描述：

International Morse Code defines a standard encoding where each letter is mapped to a series of dots and dashes, as follows: "a" maps to ".-", "b" maps to "-...", "c" maps to "-.-.", and so on.

For convenience, the full table for the 26 letters of the English alphabet is given below:

[".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."]
Now, given a list of words, each word can be written as a concatenation of the Morse code of each letter. For example, "cab" can be written as "-.-.-....-", (which is the concatenation "-.-." + "-..." + ".-"). We'll call such a concatenation, the transformation of a word.

Return the number of different transformations among all words we have.

Example:
Input: words = ["gin", "zen", "gig", "msg"]
Output: 2
Explanation: 
The transformation of each word is:
"gin" -> "--...-."
"zen" -> "--...-."
"gig" -> "--...--."
"msg" -> "--...--."

There are 2 different transformations, "--...-." and "--...--.".
Note:

The length of words will be at most 100.
Each words[i] will have length in range [1, 12].
words[i] will only consist of lowercase letters.
翻译：摩尔斯电码是使用.-来表示字母，如果直接将字符串转换成摩尔斯电码，而没有空格的话，那么不同的字符串可能有相同的摩尔斯电码，下面给出一系列字符串，给出这些字符串能够得到多少种不同类的摩尔斯电码。

思路：

    1.首先根据字母拼接对应的摩尔斯电码，然后将这一段电码做hash映射，可以看做是一段01串，直接转化成二进制即可（可能溢出int范围，但是没有关系，相同的字符串溢出后也是一样的）

    2.将一系列字符串对应的hash值排序，去重即可。

代码：

```
class Solution {  
public:  
    vector<string> mos={".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."};  
    string to_mos(string &word)  
    {  
        string ans="";  
        for(int i=0;i<word.size();i++)  
            ans += mos[word[i]-'a'];  
        return ans;  
    }  
    int removeDuplicates(vector<int>& nums)     
    {    
        int n=nums.size();    
        if(n < 2) return n;    
        int id = 1;    
        for(int i = 1; i < n; i++)     
            if(nums[i] != nums[i-1])     
                nums[id++] =nums[i];    
        return id;    
    }   
    int hash(string &m)  
    {  
        int ans=0;  
        for(int i=0;i<m.size();i++)  
        {  
            if(m[i]=='-') ans++;  
            ans*=2;  
        }  
        return ans;  
    }  
    int uniqueMorseRepresentations(vector<string>& words)   
    {  
        int n=words.size();  
        vector<string> mos_words(n);  
        for(int i=0;i<n;i++)  
            mos_words[i] = to_mos(words[i]);  
          
        vector<int> mos_words_hash(n,0);  
        for(int i=0;i<n;i++)  
            mos_words_hash[i] = hash(mos_words[i]);  
          
        sort(mos_words_hash.begin(),mos_words_hash.end());  
        return removeDuplicates(mos_words_hash);  
    }  
};  
```
