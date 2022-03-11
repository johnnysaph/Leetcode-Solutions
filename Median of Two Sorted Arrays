from bisect import bisect_left

def locate_the_middle(A, B, l, r, half):
    while r - l > 1:
        middle = (r + l) // 2
        x = bisect_left(A, B[middle])
        if x + middle < half:
            l = middle
        elif x + middle > half:
            r = middle
        else:
            return middle
    return l, r

def processing_the_middle(middle, A, B, half):
    if type(middle) == tuple:
        l, r = middle
        x, y = bisect_left(A, B[l]), bisect_left(A, B[r])
        if x + l > half:
            return A[half]
        elif x + l == half:
            return B[l]
        elif y + r == half:
            return B[r]
        elif y + r < half:
            delta = half - (y + r + 1)
            return A[y+delta]
        else:
            delta = half - (x + l + 1)
            return A[x+delta]
    else:
        return B[middle]

def get_median_1_list(A):
    n = len(A)
    if n % 2 == 0:
        return (A[n//2] + A[n//2-1]) / float(2)
    else:
        return float(A[n//2])
    
def get_median_2_lists(A, B):
    n = len(A) + len(B)
    half = n // 2
    middle = locate_the_middle(A, B, 0, len(B)-1, half)
    right_median = processing_the_middle(middle, A, B, half)
    if n % 2 == 0:
        middle = locate_the_middle(A, B, 0, len(B)-1, half-1)
        left_median = processing_the_middle(middle, A, B, half-1)
        return (right_median + left_median) / float(2)
    else:
        return float(right_median)

class Solution:
    def findMedianSortedArrays(self, nums1, nums2):
        if not nums1:
            return get_median_1_list(nums2)
        elif not nums2:
            return get_median_1_list(nums1)
        else:
            return get_median_2_lists(nums1, nums2)
