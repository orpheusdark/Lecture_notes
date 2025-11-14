practical: 9 - Implement Bubble sort, selection sort, Insertion sort, quick sort ,merge sort.

#include <bits/stdc++.h>
using namespace std;

// -------------------- Bubble Sort --------------------
void bubbleSort(vector<int>& arr) {
    int n = arr.size();
    for(int i=0; i<n-1; i++) {
        for(int j=0; j<n-i-1; j++) {
            if(arr[j] > arr[j+1]) {
                swap(arr[j], arr[j+1]);
            }
        }
    }
}

// -------------------- Selection Sort --------------------
void selectionSort(vector<int>& arr) {
    int n = arr.size();
    for(int i=0; i<n-1; i++) {
        int minIndex = i;
        for(int j=i+1; j<n; j++) {
            if(arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        swap(arr[i], arr[minIndex]);
    }
}

// -------------------- Insertion Sort --------------------
void insertionSort(vector<int>& arr) {
    int n = arr.size();
    for(int i=1; i<n; i++) {
        int key = arr[i];
        int j = i-1;
        while(j >= 0 && arr[j] > key) {
            arr[j+1] = arr[j];
            j--;
        }
        arr[j+1] = key;
    }
}

// -------------------- Quick Sort --------------------
int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    for(int j=low; j<high; j++) {
        if(arr[j] <= pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i+1], arr[high]);
    return i+1;
}

void quickSort(vector<int>& arr, int low, int high) {
    if(low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi-1);
        quickSort(arr, pi+1, high);
    }
}

// -------------------- Merge Sort --------------------
void merge(vector<int>& arr, int l, int m, int r) {
    int n1 = m - l + 1, n2 = r - m;
    vector<int> L(n1), R(n2);
    
    for(int i=0; i<n1; i++) L[i] = arr[l+i];
    for(int j=0; j<n2; j++) R[j] = arr[m+1+j];
    
    int i=0, j=0, k=l;
    while(i<n1 && j<n2) {
        if(L[i] <= R[j]) arr[k++] = L[i++];
        else arr[k++] = R[j++];
    }
    while(i<n1) arr[k++] = L[i++];
    while(j<n2) arr[k++] = R[j++];
}

void mergeSort(vector<int>& arr, int l, int r) {
    if(l < r) {
        int m = l + (r-l)/2;
        mergeSort(arr, l, m);
        mergeSort(arr, m+1, r);
        merge(arr, l, m, r);
    }
}

// -------------------- Main --------------------
int main() {
    int N;
    cin >> N;
    vector<int> arr(N);
    for(int i=0; i<N; i++) cin >> arr[i];
    string algo;
    cin >> algo;

    if(algo == "bubble") {
        bubbleSort(arr);
    } else if(algo == "selection") {
        selectionSort(arr);
    } else if(algo == "insertion") {
        insertionSort(arr);
    } else if(algo == "quick") {
        quickSort(arr, 0, N-1);
    } else if(algo == "merge") {
        mergeSort(arr, 0, N-1);
    }

    for(int i=0; i<N; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
    return 0;
}
