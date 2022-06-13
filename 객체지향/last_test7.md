###7장
```
#include <iostream>
#include <string>
using namespace std;

/******************************************************************************
 * Person class
 ******************************************************************************/
class Person {
    string *name;  // 사람 이름
    int id;        // 고유한 ID 번호
    int hours;     // 일한 시간

public:
    Person(const string& name={}, int id=0, int hour=0); // 생성자
    ~Person();                                           // 소멸자
    void print(ostream& out) const;
    Person& operator += (int a);
    int operator () ();
    Person& operator = (const Person& p);
    Person operator + (int k);
    friend Person operator + (int k, const Person& p);
    bool operator == (const Person& a);
    Person& operator ++();
    Person operator++(int a);
    Person& operator << (int a);
};

Person::Person(const string& name, int id, int hours) {
    this->id = id;
    this->name = new string(name);
    this->hours = hours;
}

Person::~Person() {
    delete name;
}

void Person::print(ostream& out) const {
    out << "name(" << *name << ") ID(" << id << ") hours(" << hours << ")";
}

ostream& operator << (ostream& stream,const Person& a){
		a.print(stream);
		return stream;
}

Person& Person::operator += (int a){
	hours = hours + a;
	return *this;
}

int Person::operator () (){
	int k;
	k = hours * 8600;
	return k;
}

Person& Person::operator = (const Person& p){
	hours = p.hours;
	id = p.id;
	*name = *(p.name);
	return *this;
}

Person Person::operator + (int k){
	Person tmp;
	tmp = *this;
	tmp.hours = hours + k;
	return tmp;
}

bool Person::operator == (const Person& a){
	if(id == a.id && *name == *(a.name)){
		return true;
	}
	return false;
}

Person& Person::operator ++(){
	hours++;
	return *this;
}

Person Person::operator ++ (int a){
	Person tmp;
	tmp = *this;
	hours++;
	return tmp;
}

Person& Person::operator << (int a){
	hours = hours + a;
	return *this;
}
Person operator + (int k, const Person& p){
	Person tmp;
	tmp = p;
	tmp.hours = p.hours + k;
	return tmp;
}

/******************************************************************************
 * menu_switch() 함수: 선택된 메인 메뉴 항목을 실행함
 ******************************************************************************/
string menuStr =
    "---------------------- Operator ---------------------\n"
    "  0.exit  1. cout <<  2. +=  3. ()  4. =  5. +(int)  \n"
    "  6. +(int,Person)  7. ==  8. ++p  9. p++  10. p <<  \n"
    "-----------------------------------------------------\n"
    "menu item? ";

void menu_switch(int menu)
{
    Person p1("HongGD",    1, 10);
    Person p2("anonymous", 2);

    switch (menu) {
    case 1:
        cout << "p1: " << p1 << endl;
        break;
    case 2:
        cout << "p1            : " << p1 << endl;
        cout << "(p1 += 1) += 2: " << ((p1 += 1) += 2) << endl;
        cout << "p1            : " << p1 << endl;
        break;
    case 3:
        cout << "p1  : " << p1   << endl;
        cout << "p1(): " << p1() << endl;
        break;
    case 4:
        cout << "p1     : " << p1 << endl;
        cout << "p2 = p1: " << (p2 = p1) << endl;
        cout << "p2     : " << p2 << endl;
        break;
    case 5:
        cout << "p1        : " << p1 << endl;
        cout << "p1 + 3 + 4: " << p1 + 3 + 4 << endl;
        cout << "p1        : " << p1 << endl;
        break;
    case 6:
        cout << "p1          : " << p1 << endl;
        cout << "5 + (2 + p1): " << 5 + (2 + p1) << endl;
        cout << "p1          : " << p1 << endl;
        break;
    case 7:
       cout << boolalpha;
       cout << "p1      : " << p1 << endl;
       cout << "p2      : " << p2 << endl;
       cout << "p1 == p2: " << (p1 == p2) << endl;
       cout << "(p2 = p1) == p1: " << ((p2=p1) == p1) << endl;
       cout << "p2      : " << p2 << endl;
       break;
    case 8:
       cout << "p1  : " << p1   << endl;
       cout << "++p1: " << ++p1 << endl;
       cout << "p1  : " << p1   << endl;
       break;
    case 9:
       cout << "p1  : " << p1   << endl;
       cout << "p1++: " << p1++ << endl;
       cout << "p1  : " << p1   << endl;
       break;
    case 10:
       cout << "p1      : " << p1 << endl;
       cout << "p1 << 10: " << (p1 << 10) << endl;
       cout << "p1      : " << p1 << endl;
       break;
    }

    cout << endl;
}


/******************************************************************************
 * main() 함수
 ******************************************************************************/
int main()
{
    while (true) {
        int menu;
        cout << menuStr;
        cin >> menu;
        if (menu == 0) break;
        menu_switch(menu);
    }
    cout << "\nGood bye!!" << endl;
}
```
