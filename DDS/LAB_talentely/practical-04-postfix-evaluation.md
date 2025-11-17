Practical: 4 - Implement Towers of Hanoi using Stack.

#include <bits/stdc++.h>
using namespace std;

struct Stack {
    stack<int> s;
    char name;
};

void moveDisk(Stack &src, Stack &dest) {
    int pole1Top = src.s.empty() ? INT_MAX : src.s.top();
    int pole2Top = dest.s.empty() ? INT_MAX : dest.s.top();

    if (pole1Top < pole2Top) {
        dest.s.push(src.s.top());
        src.s.pop();
        cout << "Move disk " << pole1Top << " from rod " << src.name 
             << " to rod " << dest.name << endl;
    } else {
        src.s.push(dest.s.top());
        dest.s.pop();
        cout << "Move disk " << pole2Top << " from rod " << dest.name 
             << " to rod " << src.name << endl;
    }
}

void tohIterative(int num_of_disks, Stack &src, Stack &aux, Stack &dest) {
    int total_moves = pow(2, num_of_disks) - 1;

    // Larger disks pushed first
    for (int i = num_of_disks; i >= 1; i--)
        src.s.push(i);

    // If number of disks is even, swap destination and auxiliary
    if (num_of_disks % 2 == 0)
        swap(dest.name, aux.name);

    for (int i = 1; i <= total_moves; i++) {
        if (i % 3 == 1)
            moveDisk(src, dest);
        else if (i % 3 == 2)
            moveDisk(src, aux);
        else if (i % 3 == 0)
            moveDisk(aux, dest);
    }
}

int main() {
    int n;
    cin >> n;

    Stack src, aux, dest;
    src.name = 'A';
    aux.name = 'B';
    dest.name = 'C';

    tohIterative(n, src, aux, dest);

    return 0;
}