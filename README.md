#include <iostream>

using std::cin;
using std::cout;

int main(int argc, char **argv) {
  int sum = 0;
  int mult = 1;
  int *pref_sums = new int[argc];
  int *inp = new int[argc];
  for (int i = 0; i < argc; i++) {
    inp[i] = (int) *argv[i];
  }
  for (int i = 0; i < argc; i++) {
    sum += inp[i];
    mult *= inp[i];
    if (i == 0) {
      pref_sums[i] = inp[i];
    } else {
      pref_sums[i] = pref_sums[i - 1] + inp[i];
    }
  }
  int *arrays = new int[sum];
  for (int i = 0; i < argc; i++) {
    for (int j = 0; j < inp[i]; j++) {
      cin >> arrays[pref_sums[i] + j];
    }
  }
  int pos = 0;
  int *idxs = new int[argc]{};
  long long mega_sum = 0;
  for (int t = 0; t < mult; t++) {
    idxs[pos] += 1;
    while (pos <= argc && idxs[pos] == inp[pos]) {
      idxs[pos] = 0;
      pos += 1;
      idxs[pos] += 1;
    }
    long long mega_mult = 1;
    for (int i = 0; i < argc; i++) {
      mega_mult *= (long long) idxs[i];
    }
    mega_sum += mega_mult;
  }
  cout << mega_sum;
}

