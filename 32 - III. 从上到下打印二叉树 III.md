<a name="KJI7y"></a>

## 解题思路

<a name="d61UJ"></a>

### 1. 层序遍历

在控制层数的基础上，判断是否反转当前层结果，可以借助最终返回值的长度进行判断

```go
func levelOrder(root *TreeNode) [][]int {
    q := make([]*TreeNode, 0)
    ans := make([][]int, 0)
    if root != nil {
        q = append(q, root)
    }
    for len(q) != 0 {
        size := len(q)
        layer := make([]int, 0)
        for i := 0; i < size; i++ {
            top := q[0]
            q = q[1:]
            layer = append(layer, top.Val)
            if top.Left != nil {
                q = append(q, top.Left)
            }
            if top.Right != nil {
                q = append(q, top.Right)
            }
        }
        // 需要反转
        if len(ans) % 2 == 1 {
            for i := 0; i < len(layer)/2; i++ {
                layer[i], layer[len(layer)-i-1] = layer[len(layer)-i-1], layer[i]
            }
        }
        ans = append(ans, layer)
    }
    return ans
}
```
