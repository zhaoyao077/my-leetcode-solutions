# Leetcode-Hot100 T1 两数之和
## 2022-04-12
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for(int i=0;;i++)
            for(int j=0;j!=i;j++){
                if( nums[i] + nums[j] == target){
                    return new int[]{i,j};
                }
            }
    }
}
```