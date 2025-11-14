Practical: 2 - Implement Infix to Postfix Expression Conversion using Stack

#include <iostream>
#include <stack>
#include <string>
using namespace std;

// Function to return precedence of operators
int precedence(char op) {
    if (op == '^') return 3;
    if (op == '*' || op == '/') return 2;
    if (op == '+' || op == '-') return 1;
    return 0;
}

// Function to check if character is operator
bool isOperator(char c) {
    return (c == '+' || c == '-' || c == '*' || c == '/' || c == '^');
}

// Infix to Postfix conversion
string infixToPostfix(string infix) {
    stack<char> st;
    string postfix = "";

    for (char c : infix) {
        // Operand → directly add to postfix
        if (isalnum(c)) {
            postfix += c;
        }
        // Left parenthesis → push
        else if (c == '(') {
            st.push(c);
        }
        // Right parenthesis → pop until '('
        else if (c == ')') {
            while (!st.empty() && st.top() != '(') {
                postfix += st.top();
                st.pop();
            }
            if (!st.empty()) st.pop(); // pop '('
        }
        // Operator
        else if (isOperator(c)) {
            while (!st.empty() && precedence(st.top()) >= precedence(c)) {
                // special case for right-associative ^
                if (c == '^' && precedence(st.top()) == precedence(c)) break;
                postfix += st.top();
                st.pop();
            }
            st.push(c);
        }
    }

    // Pop remaining operators
    while (!st.empty()) {
        postfix += st.top();
        st.pop();
    }

    return postfix;
}

// Driver
int main() {
    string infix;
    cin >> infix;

    string result = infixToPostfix(infix);
    cout << result << endl;

    return 0;
}
