# myrepository
// Program of randomized select in c++
#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;
class Random_Select
{
	public:
		Random_Select();
		~Random_Select();
		int *arr,n,i;
		void input();
		int partition(int,int);
		int random_partition(int,int);
		int randomized_select(int,int,int);
};
Random_Select::Random_Select()
{
	cout << "Enter the number of elements in the array: ";
    cin >> n;
	arr=new int[n];
}
Random_Select::~Random_Select()
{
	delete []arr;
}
int Random_Select::random_partition(int p,int r)
{
    srand(time(0));
    int part=rand()%r+p;
    //cout<<"random partition "<<part;
    swap(arr[part],arr[r]);
    return partition(p,r);
}
void Random_Select:: input()
{
	//int i;

   cout<<"Enter the elements in the array:";
    for(int j=0;j<n;j++)
    {
        cin>>arr[j];
    }
    cout << "The array is: ";
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
    cout << "Enter the value of i (1 <= i <= n): ";
    cin >> i;
    int ith_smallest = randomized_select(0, n-1, i);
    cout << "The i-th smallest element is: " << ith_smallest << endl;	
}
int Random_Select::partition( int p, int r) {
    int pivot = arr[r];
    int i = p - 1;
    for (int j = p; j < r; j++) {
        if (arr[j] <= pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i+1], arr[r]);
    return i+1;
}

int Random_Select::randomized_select(int p, int r, int i) {
    if (p == r) {
        return arr[p];
    }
    int q = random_partition(p, r);
    int k = q - p + 1;
    if (i == k) {
        return arr[q];
    }
    else if (i < k) {
        return randomized_select(p, q-1, i);
    }
    else {
        return randomized_select(q+1, r, i-k);
    }
}

int main() {
    Random_Select obj;
    obj.input();
    return 0;
}

