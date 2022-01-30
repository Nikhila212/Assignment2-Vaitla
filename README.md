# Assignment2-Vaitla
I have created this repository as an assignment.
# NIKHILA CHOWDARY VAITLA
###### PARADISE
Paradise is loacted in Hyderabad, India. It is one of the best places which serves **biryani**. Many people come here for parties and get togethers. It is the best place with **tasty food** and **nice ambience**.

***
# Description on Restaurant    
1. Closest airport is Rajiv Gandhi international Airport.
     1. Take a right from airport parking. Travel for 2 Kms straight.
     2. Take a left and travel for 16kms on highway 25.
     3. From then take left and travel onto 8 kms and your destination will be on right.
* Recommended Food Items    
    * Haleem
    * Gulab Jamun
    * Prawns Biryani
    * Mutton Gohst
    * Apollo Fish

<https://github.com/Nikhila212/Assignment2-Vaitla/blob/main/AboutMe.md>

***
# Table
This table represents the sports that I want to try. This table consists of 3 columns. First column represents th ename of the sport/activity. Second column represents the location of where it can be played. Third column represents the amount that one spends on the personal equipment. 

| Sport Name | Location | Amount |
| ---------- |  ------  | ----- |
|  Cricket   |  Ground  | $150  |
| ---------- |  ------- | ----- |
|   Tennis   |  Court   | $250  |
| ---------- |  ------  | ----  |
| Foot Ball  |  Ground  | $180  |
| ---------- |  ------- | ----- |
| Badminton  |  Court   | $200  |

***
# Pithy Quotes
> "Life is either a great adventure or nothing." - *Helen Keller*
> 
> “Be thankful for what you have; you’ll end up having more. If you concentrate on what you don’t have, you will never, ever have enough.” — *Oprah Winfrey*

*** 
# Code Fencing
> Suffix tree is a compressed trie of all the suffixes of a given string. Suffix trees help in solving a lot of string related problems like pattern matching, finding distinct substrings in a given string, finding longest palindrome etc. In this tutorial following points will be covered:
>
> Compressed Trie
> Suffix Tree Construction (Brute Force)
> Brief description of Ukkonen's Algorithm

<https://www.hackerearth.com/practice/data-structures/advanced-data-structures/suffix-trees/tutorial/>

 ```
 string s;
int n;

struct node {
    int l, r, par, link;
    map<char,int> next;

    node (int l=0, int r=0, int par=-1)
        : l(l), r(r), par(par), link(-1) {}
    int len()  {  return r - l;  }
    int &get (char c) {
        if (!next.count(c))  next[c] = -1;
        return next[c];
    }
};
node t[MAXN];
int sz;

struct state {
    int v, pos;
    state (int v, int pos) : v(v), pos(pos)  {}
};
state ptr (0, 0);

state go (state st, int l, int r) {
    while (l < r)
        if (st.pos == t[st.v].len()) {
            st = state (t[st.v].get( s[l] ), 0);
            if (st.v == -1)  return st;
        }
        else {
            if (s[ t[st.v].l + st.pos ] != s[l])
                return state (-1, -1);
            if (r-l < t[st.v].len() - st.pos)
                return state (st.v, st.pos + r-l);
            l += t[st.v].len() - st.pos;
            st.pos = t[st.v].len();
        }
    return st;
}

int split (state st) {
    if (st.pos == t[st.v].len())
        return st.v;
    if (st.pos == 0)
        return t[st.v].par;
    node v = t[st.v];
    int id = sz++;
    t[id] = node (v.l, v.l+st.pos, v.par);
    t[v.par].get( s[v.l] ) = id;
    t[id].get( s[v.l+st.pos] ) = st.v;
    t[st.v].par = id;
    t[st.v].l += st.pos;
    return id;
}

int get_link (int v) {
    if (t[v].link != -1)  return t[v].link;
    if (t[v].par == -1)  return 0;
    int to = get_link (t[v].par);
    return t[v].link = split (go (state(to,t[to].len()), t[v].l + (t[v].par==0), t[v].r));
}

void tree_extend (int pos) {
    for(;;) {
        state nptr = go (ptr, pos, pos+1);
        if (nptr.v != -1) {
            ptr = nptr;
            return;
        }

        int mid = split (ptr);
        int leaf = sz++;
        t[leaf] = node (pos, n, mid);
        t[mid].get( s[pos] ) = leaf;

        ptr.v = get_link (mid);
        ptr.pos = t[ptr.v].len();
        if (!mid)  break;
    }
}

void build_tree() {
    sz = 1;
    for (int i=0; i<n; ++i)
        tree_extend (i);
}
```
<https://cp-algorithms.com/string/suffix-tree-ukkonen.html>   




