```python



#1
def isalpha1(s):
    if len(s)==0:
        return False
    for ch in s:
        if not(
            ('a'<=ch <='z') or
            ('A'<=ch<='Z')
        ):
            return False
    return True

def isdigit1(s):
    if len(s)==0:
        return False
    for ch in s:
        if not(
            ('0'<=ch<='9')
        ):
            return False
    return True

def split1(s):
    words=[]
    word=[]
    for ch in s:
        if ch!=" ":
            word+=ch
        else:
            if word!=" ":
                words.append(word)
                word=""
    if word !=" ":
        words.append(word)
    return words

def analyze_text(text):
    glasnie="eyuioa"
    text=text.lower()
    cleaned=""
    for i in range(len(text)):
        if isalpha1(text[i])==True or text[i]==" ":
            cleaned += text[i]
    find_glasniye=""
    for i in range(len(cleaned)):
        clean=cleaned[i]
        if clean in glasnie and clean not in find_glasniye:
            find_glasniye+=clean
    shitalka=len(find_glasniye)
    words=split1(cleaned)
    result=[]
    for i in range(len(words)):
        word=words[i]
        if len(word)>=5:
            if word[0]==word[-1]:
                if word not in result:
                    result.append(word)
    res=""
    for i in range(len(result)):
        res+=result[i]
        if i !=len(result)-1:
            res+=" "
    return (shitalka,res)

analyze_text("apple Monkey livel level ocean")
```




    (5, 'livel level')




```python
#2
process=lambda s: ' '.join(
    word[::-1]
    for word in filter(
        lambda w: isalpha1(w) and len(w) %2==0,
        split1(s)
    )
)
process("hello world1234 python java love")
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    Cell In[44], line 9
          1 #2
          2 process=lambda s: ' '.join(
          3     word[::-1]
          4     for word in filter(
       (...)
          7     )
          8 )
    ----> 9 process("hello world1234 python java love")


    Cell In[44], line 4, in <lambda>(s)
          1 #2
          2 process=lambda s: ' '.join(
          3     word[::-1]
    ----> 4     for word in filter(
          5         lambda w: isalpha1(w) and len(w) %2==0,
          6         split1(s)
          7     )
          8 )
          9 process("hello world1234 python java love")


    TypeError: <lambda>() takes 1 positional argument but 2 were given



```python
#3
def top_k_word(text,k):
    text=text.lower()
    clean=""
    punctuation="!.,/?!"
    for word in text:
        if word not in punctuation:
            clean+=word
    words=clean.split()
    count={}
    for w in words:
        if w:
            count[w]=count.get(w,0)+1
    wordlist=list(count.items())
    n=len(wordlist)
    for i in range(n-1):
        ma=i
        for j in range(i+1,n):
            if wordlist[j][1]>wordlist[ma][1]:
                ma=j
            elif wordlist[j][1]==wordlist[ma][1]:
                if wordlist[j][0]<wordlist[ma][0]:
                    ma=j
        wordlist[i],wordlist[ma]=wordlist[ma],wordlist[i]
    result=[]
    for i in range(k,len(wordlist)):
        result.append(wordlist[i][0])
    return result

top_k_word("monkey monkey cat cat cat dog",2)

```




    ['dog']




```python
#4
process_str=lambda s: ' '.join(
    word.lower() for word in s.split()
    if sum(1 for char in word if char.isupper())==1
    and not word[0].isupper()
    and not word[-1].isupper()
)
process_str("apple banana cHHerry dOg eLephant")
```




    'dog elephant'




```python
#5
def compress(text):
    if len(text)==0:
        return ""
    compressed=[]
    charr=text[0]
    count=1
    for i in range(1,len(text)):
        if text[i].lower() == charr.lower():
            count+=1
        else:
            compressed.append(charr)
            if count>1:
                compressed.append(str(count))
            charr=text[i]
            count=1
    compressed.append(charr)
    if count>1:
        compressed.append(str(count))
    return "".join(compressed)
compress("aaaaBBBBddd")
```




    'a4B4d3'




```python
#6
process_stra=lambda s: ' '.join(
    filter(
        lambda word: (
            len(word)>=4
            and isalpha1(word)
            and len(set(word.lower()))==len(word)
        ),
        s.split()
    )
)
process_stra("moon stars rain show")
```




    'rain show'




```python
#7
def polinidrom(text):
    text=text.lower()
    perepinaniya=["<",">",",",".","?","!","/"]
    clean1=""
    for c in text:
        if c not in perepinaniya:
            clean1+=c
    words=split1(clean1)
    clean2=[]
    for word in words:
        if word==word[::-1] and len(word)>=3 and word not in clean2:
            clean2.append(word)
    return clean2
a="Madam MADAM Rotator rotator"
polinidrom(a)
```




    [['m', 'a', 'd', 'a', 'm'], 'madam', 'rotator']




```python
#8
process=lambda s:' '.join(
    "vowel" if isalpha1(s) and s[0].lower() in "aeiuo"
    else "consonant" if isalpha1(s)
    else s
    for s in split1(s)
)
text="apple house car 456 orange"
process(text)
```




    'vowel consonant consonant 456 vowel'




```python
#9
def alternate_case_blocks(text, n):
    text_nospace=""
    for c in text:
        if c !=" ":
            text_nospace+=c
    result=""
    for i in range(0,len(text_nospace),n):
        b=text[i:i+n]
        if (i//n)%2==0:
            result+=b.upper()
        else:
            result+=b.lower()
    return result
a="Python Programming Language"
alternate_case_blocks(a,4)
```




    'PYTHon pROGRammiNG LanguAGE'




```python
#10
count=lambda s: [
    word for word in s.split()
    if any(isdigit1(c) for c in word)
    and not isdigit1(word[0])
    and len(word)>=5
]
a="hello123 world python3 code42 test a1b2c"
count(a)
```




    ['hello123', 'python3', 'code42', 'a1b2c']




```python
def common_unique_chars(s1, s2):
    charins2=set()
    for char in s2:
        if char!=" " and not isdigit1(char):
            charins2.add(char)
    result=[]
    chars=set()
    for char in s1:
        if(char in charins2 and char!=" " and not isdigit1(char) and char not in chars):
            result.append(char)
            chars.add(char)
    return ''.join(result)
s1 = "hello world"
s2 = "world hello"
result = common_unique_chars(s1, s2)
print(result)
```

    helowrd



```python
#12
filter=lambda s: [
    word for word in split1(s)
    if len(word)>3
    and word[0].lower()==word[-1].lower()
    and not word.lower()==word.lower()[::-1]
]
text1 = "hello level world radar mama test dad"
result1 = filter(text1)
print(result1)
```

    ['test']



```python
#13
def replace_every_nth(text, n, char):
    words=split1(text)
    forbid=set()
    for i,c in enumerate(words):
        if c==" " or isdigit1(c):
            forbid.add(i)
    pos=0
    for word in words:
      if len(word)<3:
          for j in range(len(word)):
              forbid.add(pos +1)
      pos+=len(word)+1
    result=list(text)
    for i in range(n-1,len(text),n):
        if i not in forbid:
            result[i]=char
    return ' '.join(result)
text1 = "hello world python programming"
result1 = replace_every_nth(text1, 3, '*')
print(result1)
```

    h e * l o * w o * l d * p y * h o *   p * o g * a m * i n *



```python
#14
filter_words= lambda s: ', '.join(
    word for word in s.split()
    if len(set(word.lower()))>3
    and not any (
        word.lower().count(v)>1 for v in "aiueo"
    )
)
text1 = "hello world python apple banana"
result1 = filter_words(text1)
print(result1)
```

    hello, world, python, apple



```python
#15
def word_pattern_sort(text):
    words=split1(text)
    vowels="aieou"

    group={}
    for word in words:
        lenght=len(word)
        if lenght not in group:
            group[lenght]=[]
        group[lenght].append(word)

    for lenght in group:
        listt=group[lenght]
        n=len(listt)

        for i in range(n-1):
            for j in range(n-1-i):
                vcj=sum(1 for c in listt[j] if c in vowels)
                vcj1=sum(1 for c in listt[j+1].lower() if c in vowels)
                if vcj<vcj1:
                    listt[j],listt[j+1]=listt[j+1],listt[j]
                elif vcj==vcj1:
                    if listt[j] > listt[j + 1]:
                        listt[j],listt[j+1]=listt[j+1],listt[j]
        group[lenght]=listt
    res=[]
    sorlen=sorted(group.keys())
    for lenght in sorlen:
        res.extend([lenght])
    return res
text1 = "hello world python apple banana"
result1 = word_pattern_sort(text1)
print(result1)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    Cell In[16], line 33
         31     return res
         32 text1 = "hello world python apple banana"
    ---> 33 result1 = word_pattern_sort(text1)
         34 print(result1)


    Cell In[16], line 24, in word_pattern_sort(text)
         22             listt[j],listt[j+1]=listt[j+1],listt[j]
         23         elif vcj==vcj1:
    ---> 24             if listt[j] > listt[j + 1]:
         25                 listt[j],listt[j+1]=listt[j+1],listt[j]
         26 group[lenght]=listt


    TypeError: '>' not supported between instances of 'list' and 'str'



```python
#16
def transform_list(nums):
    res=[]
    for num in nums:
        if num>0:
            if num%2==0:
                res.append(num**2)
            if num%2!=0:
                if num>10:
                    n=num
                    d=0
                    while n>0:
                        d+=n%10
                        n//=10
                    res.append(d)
                else:
                    res.append(num)
    return res
transform_list([1,2,3,4,5,6,7,8,9,10,11])

```




    [1, 4, 3, 16, 5, 36, 7, 64, 9, 100, 2]




```python
#17
transform_numbers=lambda nums: [
    x**2 for x in nums
    if (x%3==0 or x%5==0)
    and x%15!=0
    and len(str(abs(x)))%2!=0
]
nums1 = [3, 5, 15, 25, 30, 45, 50, 75, 100, 105]
result1 = transform_numbers(nums1)
print(result1)
```

    [9, 25, 10000]



```python
#18
def flatten_and_filter(lst):
    res=[]
    for num in lst:
        if num>0 and num%4!=0 and len(str(num))>1:
            res.append(num)
    return res
nums1 = [3, 5, 15, 25, 30, 45, 50, 75, 100, 105]
flatten_and_filter(nums1)
```




    [15, 25, 30, 45, 50, 75, 105]




```python
#19
find_matching_even=lambda list1,list2: [
    x for x,y in zip(list1,list2)
    if x==y and x%2==0
]
list1 = [1, 2, 3, 4, 5, 6]
list2 = [1, 2, 3, 4, 5, 7]
result1 = find_matching_even(list1, list2)
print(result1)
```

    [2, 4]



```python
#20
def max_subarray_sum(nums,k):
    n=len(nums)
    if k>n:
        return None
    max_sum=None
    for i in range(n-k+1):
        current_sum=0
        v=True
        for j in range(k):
            num=nums[i+j]
            if num <=0:
                v=False
                break
            current_sum+=num
        if v:
            if max_sum is None or current_sum>max_sum:
                max_sum=current_sum
    return max_sum
nums1 = [1, 2, 3, 4, 5, 6, 7, 8, 9]
result1 = max_subarray_sum(nums1, 3)
print(result1)
```

    24



```python
#21
filterrr=lambda stri: [
    x.upper() for x in stri
    if(
       isalpha1(x) and
                len(x)>4 and
                len(set(x.lower()))==len(x))
]
strings1 = ["hello", "world", "python", "java", "abc", "book", "mouse"]
result1 = filterrr(strings1)
print(result1)
```

    ['WORLD', 'PYTHON', 'MOUSE']



```python
#22
def group_by_parity_and_sort(nums):
    even=[]
    odd=[]
    for num in nums:
        if num%2==0:
            even.append(num)
        else:
            odd.append(num)
    for i in range(len(even)-1):
        for j in range(len(even)-1-i):
            if even[j]>even[j+1]:
                even[j],even[j+1]=even[j+1],even[j]
    for i in range(len(odd)-1):
        for j in range(len(odd)-1-i):
            if odd[j]>odd[j+1]:
                odd[j],odd[j+1]=odd[j+1],odd[j]
    return even+odd
nums1 = [3, 1, 4, 1, 5, 9, 2, 6, 5]
result1 = group_by_parity_and_sort(nums1)
print(result1)
```

    [2, 4, 6, 1, 1, 3, 5, 5, 9]



```python
#23
numbersss=lambda nums: [
    nums[i] for i in range(len(nums))
    if i>1 and all(i%d!=0 for d in range(2,int(i**0.5)+1))
    and nums[i]%2!=0
       and nums[i]>sum(nums)/len(nums)
]
nums1 = [10, 15, 20, 25, 30, 35, 40, 45, 50, 55]
result1 = numbersss(nums1)
print(result1)
```

    [35, 45]



```python
#24
def longest_increasing_sublist(nums):
    if not nums:
        return []
    current_start=0
    current_lenght=1
    best_start=0
    best_lenght=1
    for i in range(1,len(nums)):
        if nums[i]>nums[i-1]:
            current_lenght+=1
        else:
            if current_lenght>best_lenght:
                best_lenght=current_lenght
                best_start=best_lenght
            current_start=i
            current_lenght=1
    if current_lenght>best_lenght:
        best_lenght=current_lenght
        best_start=current_start
    return nums[best_start:best_start+best_lenght]
nums1 = [1, 2, 3, 2, 3, 4, 5, 1, 2]
result1 = longest_increasing_sublist(nums1)
print(result1)
```

    [3, 4, 5, 1]



```python
#25
filterr=lambda lists: [
    sum(inner)/len(inner) for inner in lists
    if len(inner)>=3 and sum(inner)%2==0
]
lists1 = [[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]]
result1 = filterr(lists1)
print(result1)
```

    [2.0, 8.0]



```python
#26
def remove_duplicates_keep_last(nums):
    count={}
    for num in nums:
        count[num]=count.get(num,0)+1
    result=[]
    for num in nums:
        count[num]-=1
        if count[num]==0:
            result.append(num)
    return result
nums1 = [1, 2, 3, 2, 3, 4, 5, 1, 2]
result1 = remove_duplicates_keep_last(nums1)
print(result1)
```

    [3, 4, 5, 1, 2]



```python
#27
sort_and_take_top=lambda stri: sorted(
    stri,
    key=lambda s:(-len(s),s.lower())
)[:5]
strings1 = ["apple", "banana", "cherry", "date", "elderberry", "fig", "grape", "honeydew"]
result1 = sort_and_take_top(strings1)
print(result1)
```

    ['elderberry', 'honeydew', 'banana', 'cherry', 'apple']



```python
#28
def moving_average(nums, k):
    n=len(nums)
    if not nums or k>n:
        return []
    result=[]
    for i in range(n-k+1):
        window=nums[i:i+k]
        has_negative=False
        for num in window:
            if num<0:
                has_negative=True
                break
        if not has_negative:
            window_sum=0
            for num in window:
                window_sum+=num
            average= window_sum / k
            result.append(average)
    return result
nums1 = [1, 2, 3, 4, 5, 6, 7, 8, 9]
result1 = moving_average(nums1, 3)
print(result1)
```

    [2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0]



```python
#29
filter=lambda list1,list2: [
    x for x in list1
    if x not in list2 and x>sum(list1)/len(list1)
]
list1 = [1, 2, 3, 4, 5, 6]
list2 = [1, 2, 3, 4, 5, 7]
result1 = filter(list1, list2)
print(result1)
```

    [6]



```python
#30
def analyze_strings_list(words):
    filtered=[]
    for word in words:
        has_digit=False
        for c in word:
            if isdigit1(c):
                has_digit=True
                break
        if not has_digit:
            filtered.append(word)
    process=[]
    for word in filtered:
        if len(word)%2==0:
            process.append(word[::-1])
        else:
            process.append(word.upper())
    res=[]
    seen=set()
    for word in process:
        if word not in seen:
            seen.add(word)
            res.append(word)
    return res
words1 = ["hello", "world", "python", "java", "script", "code"]
result1 = analyze_strings_list(words1)
print(result1)
```

    ['HELLO', 'WORLD', 'nohtyp', 'avaj', 'tpircs', 'edoc']



```python
#1
def invert_unique(d):
    inv={}
    for k,v in d.items():
        if v not in inv:
            inv[v]=[]
        if k not in inv[v]:
            inv[v].append(k)
    return inv
data = {
    "id1": "admin",
    "id2": "user",
    "id3": "admin",
    "id4": "guest",
    "id1": "admin"
}
result1 = invert_unique(data)
print(result1)
```

    {'admin': ['id1', 'id3'], 'user': ['id2'], 'guest': ['id4']}



```python
#2
filter=lambda s: {x for x in s if x>sum(s)/len(s) and x%2!=0 and x%5!=0} if s else set()
numbers = {1, 10, 15, 21, 23, 30, 45, 51}
print(filter(numbers))
```

    {51}



```python
#3
def merge_dicts_sum(d1,d2):
    inn=d1.copy()
    for k,v in d2.items():
        if k in inn:
            inn[k]+=v
        else:
            inn[k]=v
    return inn
dict_a = {'apples': 10, 'bananas': 5, 'orange': 8}
dict_b = {'apples': 3, 'pears': 12, 'orange': 2}
print(merge_dicts_sum(dict_a, dict_b))
```

    {'apples': 13, 'bananas': 5, 'orange': 10, 'pears': 12}



```python
#4
def filter_sets(sets_list):
    filtered=[]
    for s in sets_list:
        if len(s)<=3:
           continue
        nega=False
        for n in s:
            if n<0:
                nega=True
                break
        if nega:
            continue
        even=False
        for n in s:
            if n%2==0:
                even=True
                break
        if even:
            filtered.append(s)
    return filtered
data = [
    {1, 2, 3, 4, 5},
    {10, 20, 30},
    {1, 3, 5, 7, 9},
    {2, 4, 6, 8, -2},
    {10, 11, 13, 15, 17}
]
result1 = filter_sets(data)
print(result1)
```

    [{1, 2, 3, 4, 5}, {17, 10, 11, 13, 15}]



```python
#5
get_tops= lambda d: sorted(d.keys(), key=lambda k: (-d[k],k))[:5]
scores = {
    "banana": 10,
    "apple": 50,
    "cherry": 50,
    "date": 20,
    "elderberry": 5,
    "fig": 50,
    "grape": 40
}
result2 = get_tops(scores)
print(result2)
```

    ['apple', 'cherry', 'fig', 'grape', 'date']



```python
#6
def deep_sum(d):
    t=0
    for v in d.values():
        if isinstance(v,(int,float)):
            t+=v
        if isinstance(v,list):
            t+=sum(v)
        if isinstance(v,dict):
            t+=deep_sum(v)
    return t
data = {
    "a": 10,
    "b": [1, 2, 3],
    "c": {
        "d": 5,
        "e": [10, 20]
    },
    "f": 0.5
}
result3 = deep_sum(data)
print(result3)
```

    51.5



```python
#7
sum_even= lambda s1,s2:{x for x in (s1^s2) if x%2==0}
set_a = {1, 2, 4, 6, 8}
set_b = {4, 6, 10, 11, 12}
sum_even(set_a, set_b)
```




    {2, 8, 10, 12}




```python
#8
def sort_dict_by_value_length(d):
    i=list(d.items())
    sort=sorted(i,key=lambda p:(len(p[1]),p[0]))
    return sort
data = {
    "banana": "yellow",
    "apple": "red",
    "kiwi": "green",
    "cherry": "red",
    "sky": "blue"
}
result2 = sort_dict_by_value_length(data)
print(result2)
```

    [('apple', 'red'), ('cherry', 'red'), ('sky', 'blue'), ('kiwi', 'green'), ('banana', 'yellow')]



```python
#9
def common_elements_all(sets_list):
    if not sets_list:
        return set()
    com=sets_list[0].copy()
    for v in sets_list[1:]:
        com &= v
        if not com:
            break
    return com
data = [
    {1, 2, 3, 4, 5},
    {2, 3, 5, 8},
    {5, 10, 2, 0},
    {2, 5, 7}
]
result3 = common_elements_all(data)
print(result3)
```

    {2, 5}



```python
#10
filter_odd=lambda s: {
    k: sorted([x for x in v if x%2!=0])
    for k, v in s.items()
    if any(x%2!=0 for x in v)
}
data = {
    "numbers": [4, 1, 8, 3, 5, 2],
    "only_even": [2, 4, 6],
    "mixed": [11, 2, 7],
    "empty": []
}
result4 = filter_odd(data)
print(result4)
```

    {'numbers': [1, 3, 5], 'mixed': [7, 11]}



```python
#11
def group_by_length(w):
    res={}
    for i in w:
        length=len(i)
        if length not in res:
            res[length]=[]
        if i not in res[length]:
            res[length].append(i)
    return res
words_list = ["apple", "bat", "code", "apple", "cat", "python", "bat"]
result5 = group_by_length(words_list)
print(result5)

```

    {5: ['apple'], 3: ['bat', 'cat'], 4: ['code'], 6: ['python']}



```python
#12
fikter_set=lambda s: {
    x for x in s
    if x.isalpha() and len(x)>4 and len(set(x.lower()))==len(x)
}
data = {"Apple", "Python", "Table", "Bread", "12345", "Super", "Java"}
result6 = fikter_set(data)
print(result6)
```

    {'Table', 'Super', 'Python', 'Bread'}



```python
#13
def invers_dict_strict(d):
    vc={}
    for v in d.values():
        vc[v]=vc.get(v,0)+1
    inc={}
    for k,v in d.items():
        if vc[v]==1:
            inc[v]=k
    return inc
data = {
    "a": 10,
    "b": 20,
    "c": 10,
    "d": 30
}
result7 = invers_dict_strict(data)
print(result7)
```

    {20: 'b', 30: 'd'}



```python
#14
def top_k_frequent(nums,d):
    if not nums:
        return set()
    res={}
    for num in nums:
        if num not in res:
            res[num]=res.get(num,0)+1
    result=[]
    for k,num in res.items():
        if res[num]>=d:
            result.append(num)
    return result
numbers=[1,1,1,2,2,3,3,4,5,6,7,7]
result8 = top_k_frequent(numbers,2)
print(result8)

```

    []



```python
#15
filter_the_dict=lambda s: {
    k: v for k,v in s.items()
    if v>=(sum(s.values())/len(s)) and v%2!=0
} if s else {}
data = {
    "a": 10,
    "b": 21,
    "c": 10,
    "d": 30
}
result9 = filter_the_dict(data)
print(result9)
```

    {'b': 21}



```python
#16
def update_counts(d,items):
    for i in items:
        if i in d:
            d[i]+=1
        else:
            d[i]=1
    return d
current_inventory = {"apple": 2, "banana": 5}
new_arrivals = ["apple", "orange", "apple", "grape"]
update_counts(current_inventory, new_arrivals)
```




    {'apple': 4, 'banana': 5, 'orange': 1, 'grape': 1}




```python
#17
filter_set=lambda s1,s2,s3: (s1&s2)-s3
set_1 = {1, 2, 3, 4}
set_2 = {3, 4, 5, 6}
set_3 = {4, 7, 8}
filter_set(set_1, set_2, set_3)
```




    {3}




```python
#18
def sort_dict_by_value_sum(d):
    agg=[]
    for k,v in d.items():
        t=sum(v)
        agg.append((k,t))
    sorting=sorted(agg, key=lambda x: (-x[1], x[0]))
    return sorting
data = {
    "banana": [1, 2, 3],
    "apple": [10, 20],
    "cherry": [15, 15],
    "date": [5]
}
result10 = sort_dict_by_value_sum(data)
print(result10)
```

    [('apple', 30), ('cherry', 30), ('banana', 6), ('date', 5)]



```python
#19
def filter_by_digit_sum(nums):
    rsult=set()
    for num in nums:
        if num%2!=0:
            digit=0
            for di in str(abs(num)):
                digit+=int(di)
            if digit%2==0:
                rsult.add(num)
    return rsult
numbers = {13, 22, 25, 41, 107}
result11 = filter_by_digit_sum(numbers)
print(result11)
```

    {107, 13}



```python
#20
filter_by=lambda d: sorted(
    d.keys(),
    key=lambda k: (d[k],len(k))
)[:3]
data = {
    "elephant": 10,
    "dog": 2,
    "cat": 2,
    "mouse": 5,
    "ant": 2
}
result12 = filter_by(data)
print(result12)
```

    ['dog', 'cat', 'ant']



```python
#21
def count_leaf_values(d):
    count=0
    for v in d.values():
        if isinstance(v,dict):
            count+=count_leaf_values(v)
        else:
            count+=1
    return count
data = {
    "a": 1,
    "b": [10, 20, 30],
    "c": {
        "d": 5,
        "e": {
            "f": 100
        }
    }
}
result13 = count_leaf_values(data)
print(result13)
```

    4



```python
#22
filter_sets_lambda= lambda s1,s2: {
    x for x in (s1-s2)
    if x>(sum(s2)/len(s2))
} if s2 else s1
set_a = {10, 20, 30, 40, 50}
set_b = {5, 15, 25}
result14 = filter_sets_lambda(set_a, set_b)
print(result14)
```

    {40, 50, 20, 30}



```python
#23
def group_by_last_letter(words):
    group={}
    for word in words:
        if not word:
            continue
        last_letter=word[-1]
        if last_letter not in group:
            group[last_letter]=[]
        if word not in group[last_letter]:
            group[last_letter].append(word)
    return group
data = ["apple", "banana", "orange", "apple", "grape", "kiwi", "pear"]
result15 = group_by_last_letter(data)
print(result15)
```

    {'e': ['apple', 'orange', 'grape'], 'a': ['banana'], 'i': ['kiwi'], 'r': ['pear']}



```python
#24
def union_of_filtered_sets(sets_list):
    res=[]
    for s in sets_list:
        for w in s:
            if w>10 and w%2!=0:
                res.append(w)
    return res
data = [
    {1, 2, 3, 11, 5},
    {15, 3, 5, 8},
    {5, 10, 2, 13},
    {2, 5, 7}
]
result16 = union_of_filtered_sets(data)
print(result16)
```

    [11, 15, 13]



```python
#25
import math
process=lambda d: {
    k: math.prod(num)
    for k,v in d.items()
    if (num:=[x for x in v if x>0])
}
data = {
    "alpha": [1, 2, 3, -5],
    "beta": [-10, -20],
    "gamma": [10, 0, 5],
    "delta": []
}
result17 = process(data)
print(result17)
```

    {'alpha': 6, 'gamma': 50}



```python
#26
def remove_elements_with_common_digits(s):
    distrinution={}
    for num in s:
        unnums=set(str(abs(num)))
        for digit in unnums:
            distrinution[digit]=set()
        distrinution[digit].add(num)
    forbid={d for d,nums in distrinution.items() if len(nums)>1}
    res=set()
    for num in s:
        numdigit=set(str(abs(num)))
        if not (numdigit & forbid):
            res.add(num)
    return res
numbers = {12, 34, 56, 17}
result18 = remove_elements_with_common_digits(numbers)
print(result18)
```

    {56, 17, 34, 12}



```python
#27
simple=lambda d: {
    k: v for k,v in d.items()
    if len(k)%2!=0 and v>1 and all(v%i!=0 for i in range(2,int(v**0.5)+1))
}
data = {
    "apple": 7,
    "banana": 11,
    "pear": 13,
    "kiwi": 5,
    "lemon": 9,
    "cat": 3
}
result19 = simple(data)
print(result19)
```

    {'apple': 7, 'cat': 3}



```python
#28
def sorted_unique_chars(strings):
    all_ch=set()
    for string in strings:
        all_ch.update(string)
    filtered=[]
    for char in all_ch:
        if not char.isdigit() and char !=" ":
            filtered.append(char)
    filtered.sort()
    return filtered
words = ["apple 1", "banana 2", "cherry 3"]
result20 = sorted_unique_chars(words)
print(result20)
```

    ['a', 'b', 'c', 'e', 'h', 'l', 'n', 'p', 'r', 'y']



```python
#29
siplee=lambda d: sorted(
    d.keys(),
    key=lambda k: (d[k]%10,k)
)
data = {
    "zebra": 51,
    "apple": 42,
    "banana": 12,
    "cherry": 20
}
result21 = siplee(data)
print(result21)

```

    ['cherry', 'zebra', 'apple', 'banana']



```python
#30
def partition_by_sum_parity(s):
    s1={}
    for num in s:
        if num not in s1:
            s1[num]=0
        digits=[int(d) for d in str(abs(num)) ]
        s1[num]=sum(digits)
    a1=[]
    a2=[]
    for k,v in s1.items():
        if v%2==0:
            a1.append(k)
        else:
            a2.append(k)
    return a1,a2
nummmm={1,2,3,4,5,6,34,76,98,54,87654,7645}
print(partition_by_sum_parity(nummmm))
```

    ([2, 4, 6, 87654, 7645], [1, 3, 5, 34, 98, 76, 54])



```python
#31
filter_unique=lambda d: {
    k:v for k,v in d.items()
    if len(v)==len(set(v)) and all(len(s)>3 for s in v)
}
data = {
    "fruits": ["apple", "banana", "kiwi"],
    "pets": ["cat", "dog", "turtle"],
    "cities": ["Paris", "Berlin", "Paris"],
    "colors": ["blue", "green"]
}
result21 = filter_unique(data)
print(result21)
```

    {'fruits': ['apple', 'banana', 'kiwi'], 'colors': ['blue', 'green']}



```python
#32
def pair(sets_list):
    if len(sets_list)<2:
        return []
    res=[]
    for i in range(len(sets_list)-1):
        curr=sets_list[i]
        next_set=sets_list[i+1]
        inter=curr&next_set
        res.append(inter)
    return res
data = [
    {1, 2, 3},
    {2, 3, 4},
    {3, 4, 5},
    {5, 6}
]
result23 = pair(data)
print(result23)
```

    [{2, 3}, {3, 4}, {5}]



```python
#33
filter_by_avg = lambda d: (
    lambda total_sum, total_count:
        {k: v for k, v in d.items()
         if sum(v) / len(v) > total_sum / total_count}
)(sum(sum(lst) for lst in d.values()), sum(len(lst) for lst in d.values()))
data = {
    "group1": [10, 20, 30],
    "group2": [5, 15, 25],
    "group3": [100, 200, 300]
}


result = filter_by_avg(data)
print(result)
```

    {'group3': [100, 200, 300]}



```python
#34
def top_k_smallest_unique(nums, k):

    unique_nums = []
    for num in nums:
        if num not in unique_nums:
            unique_nums.append(num)


    sorted_nums = []
    for num in unique_nums:
        inserted = False
        for i in range(len(sorted_nums)):
            if num < sorted_nums[i]:
                sorted_nums.insert(i, num)
                inserted = True
                break
        if not inserted:
            sorted_nums.append(num)


    result = set()
    for i in range(min(k, len(sorted_nums))):
        result.add(sorted_nums[i])

    return result
print(top_k_smallest_unique([3, 1, 4, 1, 5, 9, 2, 6, 5], 3))
```

    {1, 2, 3}



```python
#35
filter_dict = lambda d: {k: v for k, v in d.items() if v % 3 != 0 and len(k) % 2 != 0}
data = {
    "a": 5,
    "bc": 6,
    "def": 9,
    "ghij": 10,
    "klmno": 12,
    "pqrstu": 14,
    "vwxyz": 7,
    "ab": 8,
    "c": 15
}

result = filter_dict(data)
print(result)
```

    {'a': 5, 'vwxyz': 7}



```python
#36

def all_subsets_of_size_k_v2(s, k):
    elements = list(s)
    result = []
    n = len(elements)


    for mask in range(1 << n):
        current = []
        for i in range(n):
            if mask & (1 << i):
                current.append(elements[i])

        if len(current) == k:
            result.append(set(current))

    return result
s = {1, 2, 3, 4}
print(all_subsets_of_size_k_v2(s, 2))
```

    [{1, 2}, {1, 3}, {2, 3}, {1, 4}, {2, 4}, {3, 4}]



```python
#37
transform_dict = lambda d: {k: (lambda n: 1 if n < 2 else n * __import__('functools').reduce(lambda x, y: x * y, range(1, n + 1)))(v) if v < 6 else v for k, v in d.items()}
data = {
    "a": 3,
    "b": 5,
    "c": 7,
    "d": 2
}

result = transform_dict(data)
print(result)
```

    {'a': 18, 'b': 600, 'c': 7, 'd': 4}



```python
#38
def multi_symmetric_difference_v2(sets_list):
    if not sets_list:
        return set()

    result = sets_list[0]
    for s in sets_list[1:]:

        diff = set()
        for elem in result:
            if elem not in s:
                diff.add(elem)
        for elem in s:
            if elem not in result:
                diff.add(elem)
        result = diff

    return result
sets = [{1, 2, 3}, {2, 3, 4}, {3, 4, 5}]
print(multi_symmetric_difference_v2(sets))
```

    {1, 3, 5}



```python
#39
vowels = set('aeiouAEIOUаеёиоуыэюяАЕЁИОУЫЭЮЯ')

sort_by_vowels_and_value = lambda d: sorted(d.keys(), key=lambda k: (sum(1 for ch in k if ch in vowels), -d[k]))
data = {
    "hello": 10,
    "world": 20,
    "python": 15,
    "java": 30,
    "code": 5
}

result = sort_by_vowels_and_value(data)
print(result)
```

    ['world', 'python', 'java', 'hello', 'code']



```python
#40
import string
def analyze_dict_keys(d):
    punctuation = set(string.punctuation)
    unique_chars = set()

    for key in d.keys():
        if isinstance(key, str) and not any(ch.isdigit() for ch in key):
            for ch in key:
                if ch != ' ' and ch not in punctuation:
                    unique_chars.add(ch)

    return unique_chars
d = {
    "hello": 1,
    "world123": 2,
    "python 3": 3,
    "hello!@#": 4,
    "test key": 5,
    123: 6,
    "data$%^": 7
}

result = analyze_dict_keys(d)
print(result)
```

    {'y', 'k', 'e', 'o', 's', 'a', 't', 'h', 'l', 'd'}



```python
#1
import string

def analyze_students(data):
    punctuation = set(string.punctuation)

    filtered_students = []

    for student in data:
        name = student["name"]
        has_digit = any(ch.isdigit() for ch in name)

        if not has_digit:
            student["name"] = name.title()
            filtered_students.append(student)


    for student in filtered_students:
        processed_grades = []

        for grade in student["grades"]:

            if grade <= 0:
                continue


            if grade % 2 != 0 and grade < 10:

                digit_sum = sum(int(d) for d in str(grade))
                processed_grades.append(digit_sum)


            elif grade % 2 == 0 and grade >= 10:
                processed_grades.append(grade ** 2)


            else:
                processed_grades.append(grade)

        student["processed_grades"] = processed_grades


    for student in filtered_students:
        all_comments = " ".join(student["comments"])
        cleaned_text = ""
        for ch in all_comments:
            if ch not in punctuation:
                cleaned_text += ch.lower()


        words = cleaned_text.split()


        unique_words = set()
        for word in words:
            if len(word) >= 4 and word != word[::-1]:
                unique_words.add(word)

        student["unique_words"] = unique_words


        vowels = set()
        vowels_set = set("aeiouаеёиоуыэюя")

        for word in unique_words:
            for ch in word:
                if ch in vowels_set:
                    vowels.add(ch)

        student["vowels_in_words"] = vowels


    word_student_count = {}

    for student in filtered_students:
        student_words = student.get("unique_words", set())

        for word in student_words:
            if word not in word_student_count:
                word_student_count[word] = set()
            word_student_count[word].add(student["name"])
    filtered_words = {
        word: len(students)
        for word, students in word_student_count.items()
        if len(students) >= 2
    }

    sorted_words = dict(
        sorted(filtered_words.items(), key=lambda x: (-x[1], x[0]))
    )


    all_vowels = set()
    for student in filtered_students:
        all_vowels.update(student.get("vowels_in_words", set()))


    students_by_avg = []
    for student in filtered_students:
        grades = student.get("processed_grades", [])
        if grades:
            avg_grade = sum(grades) / len(grades)
        else:
            avg_grade = 0

        students_by_avg.append((student["name"], avg_grade))


    students_by_avg.sort(key=lambda x: (-x[1], x[0]))
    students_by_avg_list = [name for name, _ in students_by_avg]


    students_by_name_length = {}
    for student in filtered_students:
        name = student["name"]
        name_length = len(name)

        if name_length not in students_by_name_length:
            students_by_name_length[name_length] = []


        if name not in students_by_name_length[name_length]:
            students_by_name_length[name_length].append(name)


    for length in students_by_name_length:
        students_by_name_length[length].sort()


    students_result = [
        {
            "name": student["name"],
            "processed_grades": student.get("processed_grades", [])
        }
        for student in filtered_students
    ]

    result = {
        "students": students_result,
        "word_counts": sorted_words,
        "all_vowels": all_vowels,
        "students_by_avg": students_by_avg_list,
        "students_by_name_length": students_by_name_length
    }

    return result

test_data = [
    {
        "name": "Alice123",
        "grades": [12, 9, 15, 8, -5, 0],
        "comments": ["Good work", "excellent effort", "Needs Improvement"]
    },
    {
        "name": "bob",
        "grades": [5, 10, 7, 14, 2],
        "comments": ["good job", "excellent", "keep going", "good work"]
    },
    {
        "name": "Charlie",
        "grades": [11, 8, 13, 6, 9],
        "comments": ["hello world", "good effort", "nice try"]
    },
    {
        "name": "diana99",
        "grades": [4, 6, 8, 10],
        "comments": ["excellent work", "perfect", "good job"]
    },
    {
        "name": "Eve",
        "grades": [3, 5, 7, 9],
        "comments": ["good", "bad", "average"]
    }
]


result = analyze_students(test_data)



print(result)
```

    {'students': [{'name': 'Bob', 'processed_grades': [5, 100, 7, 196, 2]}, {'name': 'Charlie', 'processed_grades': [11, 8, 13, 6, 9]}, {'name': 'Eve', 'processed_grades': [3, 5, 7, 9]}], 'word_counts': {'good': 3}, 'all_vowels': {'e', 'o', 'a', 'i'}, 'students_by_avg': ['Bob', 'Charlie', 'Eve'], 'students_by_name_length': {3: ['Bob', 'Eve'], 7: ['Charlie']}}



```python
import string

def analyze_students(data):
    punctuation = set(string.punctuation)

    filtered_students = []

    for student in data:
        name = student["name"]
        has_digit = any(ch.isdigit() for ch in name)

        if not has_digit:
            student["name"] = name.title()
            filtered_students.append(student)

    for student in filtered_students:
        processed_grades = []

        for grade in student["grades"]:
            if grade <= 0:
                continue

            if grade % 2 != 0 and grade < 10:
                digit_sum = sum(int(d) for d in str(grade))
                processed_grades.append(digit_sum)
            elif grade % 2 == 0 and grade >= 10:
                processed_grades.append(grade ** 2)
            else:
                processed_grades.append(grade)

        student["processed_grades"] = processed_grades

    for student in filtered_students:
        all_comments = " ".join(student["comments"])

        cleaned_text = ""
        for ch in all_comments:
            if ch not in punctuation:
                cleaned_text += ch.lower()

        words = cleaned_text.split()

        unique_words = set()
        for word in words:
            if len(word) >= 4 and word != word[::-1]:
                unique_words.add(word)

        student["unique_words"] = unique_words

        vowels = set()
        vowels_set = set("aeiouаеёиоуыэюя")

        for word in unique_words:
            for ch in word:
                if ch in vowels_set:
                    vowels.add(ch)

        student["vowels_in_words"] = vowels

    word_student_count = {}

    for student in filtered_students:
        student_words = student.get("unique_words", set())

        for word in student_words:
            if word not in word_student_count:
                word_student_count[word] = set()
            word_student_count[word].add(student["name"])

    filtered_words = {
        word: len(students)
        for word, students in word_student_count.items()
        if len(students) >= 2
    }

    sorted_words = dict(
        sorted(filtered_words.items(), key=lambda x: (-x[1], x[0]))
    )

    all_vowels = set()
    for student in filtered_students:
        all_vowels.update(student.get("vowels_in_words", set()))

    all_vowels_list = sorted(list(all_vowels))

    students_by_avg = []
    for student in filtered_students:
        grades = student.get("processed_grades", [])
        if grades:
            avg_grade = sum(grades) / len(grades)
        else:
            avg_grade = 0

        students_by_avg.append((student["name"], avg_grade))

    students_by_avg.sort(key=lambda x: (-x[1], x[0]))
    students_by_avg_list = [name for name, _ in students_by_avg]

    students_by_name_length = {}
    for student in filtered_students:
        name = student["name"]
        name_length = len(name)

        if name_length not in students_by_name_length:
            students_by_name_length[name_length] = []

        if name not in students_by_name_length[name_length]:
            students_by_name_length[name_length].append(name)

    for length in students_by_name_length:
        students_by_name_length[length].sort()

    students_result = [
        {
            "name": student["name"],
            "processed_grades": student.get("processed_grades", [])
        }
        for student in filtered_students
    ]

    result = {
        "students": students_result,
        "word_counts": sorted_words,
        "all_vowels": all_vowels_list,
        "students_by_avg": students_by_avg_list,
        "students_by_name_length": students_by_name_length
    }

    return result

test_data = [
    {
        "name": "Alice123",
        "grades": [12, 9, 15, 8, -5, 0],
        "comments": ["Good work", "excellent effort", "Needs Improvement"]
    },
    {
        "name": "bob",
        "grades": [5, 10, 7, 14, 2],
        "comments": ["good job", "excellent", "keep going", "good work"]
    },
    {
        "name": "Charlie",
        "grades": [11, 8, 13, 6, 9],
        "comments": ["hello world", "good effort", "nice try"]
    },
    {
        "name": "diana99",
        "grades": [4, 6, 8, 10],
        "comments": ["excellent work", "perfect", "good job"]
    },
    {
        "name": "Eve",
        "grades": [3, 5, 7, 9],
        "comments": ["good", "bad", "average"]
    }
]


result = analyze_students(test_data)


import json
print(json.dumps(result, indent=2, ensure_ascii=False))
```

    {
      "students": [
        {
          "name": "Bob",
          "processed_grades": [
            5,
            100,
            7,
            196,
            2
          ]
        },
        {
          "name": "Charlie",
          "processed_grades": [
            11,
            8,
            13,
            6,
            9
          ]
        },
        {
          "name": "Eve",
          "processed_grades": [
            3,
            5,
            7,
            9
          ]
        }
      ],
      "word_counts": {
        "good": 3
      },
      "all_vowels": [
        "a",
        "e",
        "i",
        "o"
      ],
      "students_by_avg": [
        "Bob",
        "Charlie",
        "Eve"
      ],
      "students_by_name_length": {
        "3": [
          "Bob",
          "Eve"
        ],
        "7": [
          "Charlie"
        ]
      }
    }



```python
import re

def analyze_orders(orders):
    vowels_set_global = set()
    word_order_count = {}
    unique_products = set()
    orders_processed = []

    def sum_of_digits(num):
        return sum(int(d) for d in str(abs(num)) if d.isdigit())

    for order in orders:
        if any(char.isdigit() for char in order["customer"]):
            continue

        order["customer"] = order["customer"].title()
        processed_items = []

        for item in order["items"]:
            price = item["price"]
            quantity = item["quantity"]

            if price <= 0:
                continue

            if price > 100 and quantity > 1:
                price = price * quantity

            if quantity % 2 == 1:
                price += sum_of_digits(int(round(price)))

            if price <= 0:
                continue

            processed_items.append({
                "name": item["name"],
                "price": price,
                "quantity": quantity
            })

            unique_products.add(item["name"])

        order["processed_items"] = processed_items

        notes_text = " ".join(order["notes"])
        notes_text = re.sub(r"[^\w\s]", "", notes_text)
        words = notes_text.lower().split()

        filtered_words = {w for w in words if len(w) >= 4 and w != w[::-1]}

        vowels = {c for c in "".join(filtered_words) if c in "aeiou"}
        vowels_set_global.update(vowels)

        for word in filtered_words:
            word_order_count[word] = word_order_count.get(word, 0) + 1

        orders_processed.append(order)

    word_counts_filtered = dict(filter(
        lambda item: item[1] >= 2,
        word_order_count.items()
    ))

    word_counts_sorted = dict(sorted(
        word_counts_filtered.items(),
        key=lambda x: (-x[1], x[0])
    ))

    def total_sum(order):
        return sum(item["price"] for item in order["processed_items"])

    orders_sorted = sorted(
        orders_processed,
        key=lambda o: (-total_sum(o), o["order_id"])
    )

    orders_by_total = [o["order_id"] for o in orders_sorted]

    orders_by_item_count = {}
    for order in orders_processed:
        count = len(order["processed_items"])
        if count not in orders_by_item_count:
            orders_by_item_count[count] = set()
        orders_by_item_count[count].add(order["order_id"])

    orders_by_item_count = {
        k: sorted(list(v)) for k, v in orders_by_item_count.items()
    }

    return {
        "orders": orders_processed,
        "word_counts": word_counts_sorted,
        "all_vowels": vowels_set_global,
        "unique_products": unique_products,
        "orders_by_total": orders_by_total,
        "orders_by_item_count": orders_by_item_count
    }
orders = [
    {
        "order_id": "A123",
        "customer": "john_doe",
        "items": [
            {"name": "Laptop", "price": 999.99, "quantity": 1},
            {"name": "Mouse", "price": 25, "quantity": 2}
        ],
        "notes": ["Deliver ASAP!", "fragile package", "handle with care"]
    },
    {
        "order_id": "B456",
        "customer": "anna",
        "items": [
            {"name": "Phone", "price": 500, "quantity": 3},
            {"name": "Case", "price": 20, "quantity": 1}
        ],
        "notes": ["fast delivery", "no delay", "handle with care"]
    }
]

result = analyze_orders(orders)

print(result)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    Cell In[46], line 119
         90     return {
         91         "orders": orders_processed,
         92         "word_counts": word_counts_sorted,
       (...)
         96         "orders_by_item_count": orders_by_item_count
         97     }
         98 orders = [
         99     {
        100         "order_id": "A123",
       (...)
        116     }
        117 ]
    --> 119 result = analyze_orders(orders)
        121 print(result)


    Cell In[46], line 59, in analyze_orders(orders)
         55         word_order_count[word] = word_order_count.get(word, 0) + 1
         57     orders_processed.append(order)
    ---> 59 word_counts_filtered = dict(filter(
         60     lambda item: item[1] >= 2,
         61     word_order_count.items()
         62 ))
         64 word_counts_sorted = dict(sorted(
         65     word_counts_filtered.items(),
         66     key=lambda x: (-x[1], x[0])
         67 ))
         69 def total_sum(order):


    TypeError: <lambda>() takes 1 positional argument but 2 were given

