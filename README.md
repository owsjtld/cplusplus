# cplusplus
학교에서 배우는 코드 저장하는 곳


#include <iostream>
#include <string>

using namespace std;

#define MAX_STACK_SIZE 100

typedef struct {
    int student_id;
    string student_name;
} StudentRecord;

class StackType {
private:
    StudentRecord* data;
    int capacity;
    int top;
public:
    StackType() {
        top = -1;
        capacity = MAX_STACK_SIZE;
        data = new StudentRecord[capacity];
    }

    ~StackType() {
        delete[] data;
    }

    // 공백 상태
    int is_empty()
    {
        return (top == -1);
    }

    // 포화 상태
    int is_full()
    {
        return (top == capacity - 1);
    }

    // 삽입
    void push(StudentRecord item)
    {
        if (is_full()) {
            capacity *= 2;
            StudentRecord* temp = new StudentRecord[capacity];
            for (int i = 0; i <= top; i++) {
                temp[i] = data[i];
            }
            delete[] data;
            data = temp;
        }
        data[++top] = item;
    }

    // 삭제
	void pop(StudentRecord& item)
	{
		if (is_empty()) {
			throw "스택 공백 에러";
		}
		item = data[top--];
	}

};

int main(void) {
    StackType t;

    string Input;
    getline(cin, Input);
    int ID = stoi(Input.substr(0, Input.find(',')));
    string NAME = Input.substr(Input.find(',') + 1);

    StudentRecord a;
    a.student_id = ID;
    a.student_name = NAME;
    t.push(a);
    cout << a.student_id << endl;
    cout << a.student_name << endl;
	t.pop(a);
    cout << a.student_id << endl;
    cout << a.student_name << endl;
    return 0;
}
