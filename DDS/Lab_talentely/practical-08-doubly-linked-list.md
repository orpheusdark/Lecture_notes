Practical: 8 - Implement binary search and interpolation search.
```
#include <iostream>
using namespace std;

int binarySearch(int arr[], int n, int target) {
    int low = 0, high = n - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] == target)
            return mid;
        else if (arr[mid] < target)
            low = mid + 1;
        else
            high = mid - 1;
    }
    return -1;
}

int interpolationSearch(int arr[], int n, int target) {
    int low = 0, high = n - 1;
    while (low <= high && target >= arr[low] && target <= arr[high]) {
        if (low == high) {
            if (arr[low] == target) return low;
            return -1;
        }
        int pos = low + ((double)(target - arr[low]) * (high - low)) / (arr[high] - arr[low]);
        if (arr[pos] == target)
            return pos;
        else if (arr[pos] < target)
            low = pos + 1;
        else
            high = pos - 1;
    }
    return -1;
}

int main() {
    int n, target;
    
    cin >> n;
    int arr[n];
    
    for (int i = 0; i < n; ++i)
        cin >> arr[i];
    cin >> target;

    int binIndex = binarySearch(arr, n, target);
    int interpIndex = interpolationSearch(arr, n, target);

    cout << "Binary Search Index: " << binIndex << endl;
    cout << "Interpolation Search Index: " << interpIndex << endl;

    return 0;
}
```
