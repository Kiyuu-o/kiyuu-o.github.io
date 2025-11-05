+++
date = '2025-11-04T21:54:56-07:00'
draft = true
title = 'Z Algorithm'
+++

## Code

Short and simple, come from [KACTL](https://github.com/kth-competitive-programming/kactl)
```cpp
#define rep(i, a, b) for (int i = (a); i < (b); i++)
using vi = vector<int>;
/**
 * Author: chilli
 * License: CC0
 * Description: z[i] computes the length of the longest common prefix of s[i:] and s,
 * except z[0] = 0. (abacaba -> 0010301)
 * Time: O(n)
 * Status: stress-tested
 */
#pragma once

vi Z(const string& S) {
	vi z(sz(S));
	int l = -1, r = -1;
	rep(i,1,sz(S)) {
		z[i] = i >= r ? 0 : min(r - i, z[i - l]);
		while (i + z[i] < sz(S) && S[i + z[i]] == S[z[i]])
			z[i]++;
		if (i + z[i] > r)
			l = i, r = i + z[i];
	}
	return z;
}
```

## Application

One application of the Z Algorithm is for the standard string matching problem of finding matches for a pattern T of length m in a string S of length n. We can do this in O(n + m) time by using the Z Algorithm on the string T Φ S (that is, concatenating T, Φ, and S) where Φ is a character that matches nothing. The indices i with Z[i] = m correspond to matches of T in S.