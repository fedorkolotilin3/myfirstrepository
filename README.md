#include <iostream>

using std::cin;
using std::cout;

int ch_to_int(char x) {
  char nums[10] = {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9'};
  for (int i = 0; i < 10; i++) {
    if (x == nums[i]) {
      return i;
    }
  }
  return -1;
}

int main(int argc, char **argv) {
  int sum = 0;
  int mult = 1;
  int *pref_sums = new int[argc];
  int *inp = new int[argc];
  for (int i = 0; i < argc; i++) {
    inp[i] = ch_to_int(*argv[i]);
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
  int *idxs = new int[argc];
  for(int i = 0; i < argc; i++){
    idxs[i] = 0;
  }
  long long mega_sum = 0;
  for (int t = 0; t < mult; t++) {
    long long mega_mult = 1;
    for (int i = 0; i < argc; i++) {
      mega_mult *= (long long) arrays[pref_sums[i] + idxs[i]];
    }
    mega_sum += mega_mult;
    idxs[pos] += 1;
    while (pos <= argc && idxs[pos] == inp[pos]) {
      idxs[pos] = 0;
      pos += 1;
      idxs[pos] += 1;
    }
  }
  cout << mega_sum;
}

