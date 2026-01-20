Below are the two items to drop into your doc.

# When Hash Maps Beat Arrays (with examples)

- **Keys are unknown, sparse, or unbounded**
  - Arrays require a dense 0..N index range. If keys are large (IDs, values, words), arrays waste memory or are impossible.
  - Example: Two Sum on arbitrary integers. A hash map from `value → index` gives O(1) average lookup; an array would need size proportional to value range.

- **Keys are not integers**
  - Arrays can’t index by strings/tuples/objects.
  - Example: Group Anagrams by a signature key (e.g., sorted word or 26-count tuple). Use a map `signature → list of words`.

- **Need O(1) “have we seen this?” membership**
  - Example: Detect duplicates or visited nodes: use a set/map for O(1) average membership checks.

- **Frequency counting with unknown alphabet**
  - Example: Ransom Note with Unicode. Use `Counter`/dict for counts. An array only works when the alphabet is small and fixed.

- **Building associations or inverted indexes**
  - Example: Map `category → items`, `user → last_seen_time`, `node → neighbors`. Arrays don’t model these relations unless keys are small ints.

- **When arrays win instead**
  - Keys are a small, fixed, dense range (e.g., 26 lowercase letters, 10 digits, ≤256 ASCII).
  - Example: Valid Anagram over lowercase letters: a 26-length array is faster and uses less overhead than a dict.

- **Rule of thumb**
  - Small dense integer domain → array.
  - Anything else (sparse, large, dynamic, or non-integer keys) → hash map.

# Template Code for Frequency Counting

- **General-purpose dict (default-zero via get)**

```python
def count_freq(iterable):
    freq = {}
    for x in iterable:
        freq[x] = freq.get(x, 0) + 1
    return freq
```

- **Consume pattern (fail fast when missing)**

```python
def can_construct(need, have):
    # have/need are iterables of tokens (chars, words, etc.)
    from collections import Counter
    supply = Counter(have)
    for x in need:
        if supply.get(x, 0) == 0:
            return False
        supply[x] -= 1
    return True
```

- **Fixed alphabet (lowercase a–z)**

```python
def count_lowercase(s):
    base = ord('a')
    cnt = [0] * 26
    for c in s:
        cnt[ord(c) - base] += 1
    return cnt
```

- **One-liner comparisons (when appropriate)**

```python
from collections import Counter
def same_multiset(a, b):
    return Counter(a) == Counter(b)
```

Notes:

- All counting templates run in O(n) time.
- Array-based variant is O(1) extra space for fixed alphabets; dict/Counter is O(k) where k is number of distinct keys.
