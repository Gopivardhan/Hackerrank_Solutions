<h1 align="center">C++</h1>
<h2>Inherited Code</h2>

```C++
class BadLengthException{
  public:
    int x;
    BadLengthException(int n){
        x=n;
    }
    int what()
        {
        return x;
    }
    
};
```

<h2>Virtual Functions</h2>

```C++

class Person {
protected:
    string name;
    int age;
public:
    static int prof_id;
    static int stud_id;
    virtual void getdata()=0;
    virtual void putdata()=0;
};

int Person::prof_id = 1;
int Person::stud_id = 1;

class Student : public Person{
public:
    int marks[6];
    int cur_id;
    Student() {
        cur_id = stud_id++;
    }
    void getdata() {
        cin >> name >> age;
        for(int i = 0; i < 6; ++i) cin >> marks[i];
    }
    void putdata() {
        int sum = 0;
        for(int i = 0; i < 6; ++i) sum += marks[i];
        cout << name << ' ' << age << ' ' << sum << ' ' << cur_id << endl;
    }
};

class Professor : public Person{
public:
    Professor() {
        cur_id = prof_id++;
    }
    int publications;
    int cur_id;
    void getdata() {
        cin >> name >> age >> publications;
    }
    void putdata() {
        cout << name << ' ' << age << ' ' << publications << ' ' << cur_id << endl;
    }
};

```

<h2>Messages Order</h2>

```c++


class Message {
public: 
    Message() {}
    Message(const string& text, int id) : text_(text), id_(id) {}
    const string& get_text() {
        return text_;
    }
    bool operator<(const Message& rhs) const {
        return this->id_ < rhs.id_;
    }
private:
    string text_;
    int id_;
};

class MessageFactory {
public:
    MessageFactory() {}
    Message create_message(const string& text) {
        return Message(text, current_id++);
    }
private:
    int current_id = 0;
};

```

<h2>Operator Overloading</h2>

```c++

class Matrix {
  public:
    Matrix() {}
    Matrix(const Matrix& x) : a(x.a) {}
    Matrix(const vector<vector<int>>& v) : a(v) {}
    Matrix operator+(const Matrix&);
    vector<vector<int>> a;
};

Matrix Matrix::operator+(const Matrix& m){
    vector<vector<int>> vv = a;
    for (int i=0; i<vv.size(); i++){
        for (int j=0; j<vv[0].size(); j++){
            vv[i][j] += m.a[i][j];
        }
    }
    return Matrix(vv);
}

```

<h2>C++ Class Template Specialization</h2>

```c++

#include <string>

template <typename T> struct Traits
{
    static std::string name(int index) { return "unknown"; }
};

template<> struct Traits<Fruit>
{
    static std::string name(int index)
    {
        switch((Fruit)index) {
        case Fruit::apple:      return "apple";
        case Fruit::orange:     return "orange";
        case Fruit::pear:       return "pear";
        default:                return "unknown";
        }
    }
};

template<> struct Traits<Color>
{
    static std::string name(int index)
    {
        switch((Color)index) {
        case Color::red:        return "red";
        case Color::green:      return "green";
        case Color::orange:     return "orange";
        default:                return "unknown";
        }
    }
};

```

<h2></h2>

```c++


```

<h2></h2>

```c++


```

<h2></h2>

```c++


```



