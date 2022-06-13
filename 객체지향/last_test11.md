### 11장
```
#include <iostream>
#include <iomanip>
using namespace std;

/******************************************************************************
 * Class Point
 ******************************************************************************/
class Point {
	int x, y;  // 점의 x, y 좌표 값
public:
	Point() { x = 31; y = 15; }
	friend ostream& operator << (ostream& stream, Point a);
	friend istream& operator >> (istream& ins, Point& a);
};


// 여기에 필요한 연산자, 조작자 등의 함수를 구현하시오.
ostream& operator << (ostream& stream, Point a){
	cout << hex << showbase << setw(7) << setfill('*') << a.x << ", ";
	cout << oct << showbase << left << setw(6) << setfill('.') << a.y << ", ";
	if(a.x == a.y){
		cout << boolalpha << true;
	}
	else{
		cout << boolalpha << false;
	}
	cout << dec << noshowbase << noboolalpha << setfill(' ') << right;
	return stream;
}
ostream& leftp (ostream& stream){
	cout << "( ";
	return stream;
}

ostream& rightp (ostream& stream){
	cout << " )";
	return stream;
}

istream& operator >> (istream& ins, Point& a){
	cin >> a.x >> a.y;
	return ins;
}

istream& inmsg (istream& ins){
	cout << "x, y coordinate? ";
	return ins;
}
/******************************************************************************
 * 선택된 메인 메뉴 항목을 실행하는 함수들
 ******************************************************************************/
//------------------------------------------------------
// 경고: 아래 네 개의 함수는 주석을 제거하는 것 외는 수정하지 마시오.
//      만약 본인의 임의대로 아래 함수를 수정할 경우 0점 처리함.
//------------------------------------------------------

Point p;

void outPoint() {
	cout << setw(3) << 1 << 2 << 3 << true << endl;
	cout << p << endl;
	cout << setw(3) << 1 << 2 << 3 << true << endl;
}

void outMnpPoint() {
	cout << leftp << p << rightp << endl;
}

void inPoint() {
	cout << "input x and y: ";
	cin >> p;
	outMnpPoint();
}

void inMnpPoint() {
	cin >> inmsg >> p;
	outMnpPoint();
}

/******************************************************************************
 * menu_switch() 함수: 선택된 메인 메뉴 항목을 실행함
 ******************************************************************************/
string menuStr =
    "----------------------- I/O Stream -----------------------\n"
    "  0.exit 1.outPoint 2.outMnpPoint 3.inPoint 4.inMnpPoint  \n"
    "----------------------------------------------------------\n"
    "menu item? ";

void menu_switch(int menu)
{
    switch (menu) {
    case 1: outPoint();    break;
    case 2: outMnpPoint(); break;
    case 3: inPoint();     break;
    case 4: inMnpPoint();  break;
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
