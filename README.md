# CppSQL

<http://orlicz.top>

CppSQL,use Cpp call SQL

- Now,you can use "base<char,int>" to create a database.
- In this database,type of object1 is char,type of object2 is int.
- Type "base::addtab" to add a table.

# The following is a little description of the file directory. 

In the ***"/luogu/luogu"*** directory,
you can see that there are the following two  ***.h*** files. 
One of them is ***"BitIO.h"***, and the other is ***"CppIO.h"***.
You only need to place these two files under the same level directory as your ***cpp file***. 
    
When you want to use them, you only need to include ***"BitIO"***,***"CppIO"*** These two files will do. 
    
If you want to do this Development can be copied directly,go to the local directory and open it using **Visual Studio**.     

# Introduction to Main Classes 
## Class in CppIO
- ### table
    This is the basic unit in which data is saved.
    Where the ***data(void\*\*)*** attribute Saved all the information in this column. 
    ***cin/cout*** is its friend. 
    The method for packaging the same 
    ***(istream&)(istream& >> table&)***
    will be read in two order from the console ***data***.
    When calling the methods they encapsulate 
    ***(ostream&)(ostream& << table&)***,
    the data will be output to a console. 
    
<details>
<summary>
Functions  
</summary>
    
- ## addtab:
    This function can be used to create a new table in the database.
    
<details>
<summary>Source Code</summary>
    
```cpp
void addtab(table<T...> tab) {
        GetTyp<T...>(tab.data);
    }
```
</details>
    
- ## GetTab
    This function can match all tables that satisfy the condition. 
    
<details>
<summary>Source Code</summary>
    
```cpp
    template<typename r>
    vector<table<T...>> GetTab(string Name,r mb) {
        vector<table<T...>> ret;
        map<string, int> mm;
        cin.clear();
        cin.seekg(0L, ios::beg);
        string sgg("dsadsad");
        for (int i = 0; i < sizeof...(T); i++) {
            cin >> sgg;
            mm[sgg] = i+1;
            short a;
            cin >> a;
        }
        if (!(mm[sgg])) {
            throw string("There haven't name ") + Name;
        }
        table<T...> tab;
        for (ull re = 1; !(cin.eof()); re++) {
            cin >> tab;
            r id = tab.GetId<r>(mm[Name]-1);
            printf("RE:%llu Id:%c\n", re, id);
            if (id == mb) {
                ret.push_back(tab);
            }

        }
        return ret;
    }
```
    
</details>
</details>
    
# namespace Typ:
```cpp
template<typename X, typename Y>
void h(void** data, X g, Y t) {
    data[0] = new X(g);
    data[1] = new Y(t);

    //cout << g << endl<< t;
}


template<typename X, typename ...Y>
void h(void** data, X g, Y... t) {
    //cout << g << endl;

    data[0] = new X(g);
    h(data + 1, t...);
}
namespace Typ {
    template<typename T>
    void GetCall(T Call, bool flg) {
        cout << Call;
        if (flg)
            cout << endl; 
        else 
            cout << ' ';
        return;
    }

    template<typename... T>
    struct TypSiz;
    template <typename T>
    struct TypSiz <T>{
        ull size;
        TypSiz(void f(ull,void**&),void**& c) {
            size = sizeof(T);
            f(size,c);
        }
        TypSiz() {
            size = sizeof(T);
        }
    };
    template <typename T,typename... I>
    struct TypSiz<T,I...> {
        ull size;
        TypSiz(void f(ull,void**&),void**& c) {
            size = sizeof(T);
            f(size,c);
            TypSiz<I...> n(f,c);
            size += n.size;
        }
        TypSiz() {
            size = sizeof(T);
            TypSiz<I...> n;
            size += n.size;
        }
    };
    template<typename... T>
    struct GetTyp;

    template<typename T>
    struct GetTyp<T> {
        GetTyp(void** data) {
            GetCall<T>((*((T*)data[0])), 1);
        }
    };

    template<typename T, typename... I>
    struct GetTyp<T, I...> {
        GetTyp(void** data)
        {
            GetCall<T>((*((T*)data[0])), 0);
            GetTyp<I...> n(data + 1);
        }
    };

    template<typename... T>
    struct SetTyp;

    template<typename T>
    struct SetTyp<T> {
        SetTyp(void** data, istream& fin) {
            data[0] = new T;
            fin >> *((T*)data[0]);
        }
    };

    template<typename T, typename... I>
    struct SetTyp<T, I...> {
        SetTyp(void** data, istream& fin) {
            data[0] = new T;
            fin >> *((T*)data[0]);
            SetTyp<I...>(data + 1, fin);
        }
    };
}
```


# The following is a description of the functions of each function api interface. 
# CppIO
    

    
# BitIO
    
<details>
    <summary>open</summary>
    
- ## btab
    
</details>


未完待续（最好进去看一看
