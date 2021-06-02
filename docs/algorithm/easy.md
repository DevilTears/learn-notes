# Easy

## 实现 createObj('a,b,c'); 输出 {a: {b: {c: null}}}

> 题目来源：2020.12-百度

```js
function createObj(str) {
  let arr = str.split(',')
  let current = null

  for (let i = arr.length - 1; i >= 0; i--) {
    const temp = {}

    temp[arr[i]] = current

    current = temp
  }

  return current
}

createObj('a,b,c');
```

## 实现 repeat(str, count)

> 题目来源：2020.12-百度

- repeat('s', 2) // 返回ss
- repeat('a', 3) // 返回aaa

```js
function repeat(str, count) {
  let result = ''

  for (let i = 0; i < count; i++) {
    result += str
  }

  return result
}

repeat('s', 2) // 返回ss
repeat('a', 3) // 返回aaa
```

## 有如下数据，修改其中id为“2-1”子节点的name属性值为 "childNode",请写实现的代码

> 题目来源：2020.12-好未来

```js
const obj = {
  id: 0,
  name: 'root',
  children: [
    {
      id: '0-1',
      name: '子节点1'
    },
    {
      id: '0-2',
      name: '子节点2',
      children: [
        {
          id: '2-1',
          name: '子节点5'
        }
      ]
    },
    {
      id: '0-3',
      name: '子节点3',
      children: [
        {
          id: '3-1',
          name: '子节点4'
        }
      ]
    }
  ]
}

function changeName(obj, id, value) {
  if (obj.id === id) {
    obj.name = value

    return
  }

  for (let i = 0; i < obj.children.length; i++) {
    changeName(obj[i], id, value)
  }

  return obj
}

changeName(obj, '2-1', 'childNode')
```

## 实现a，使得调用a.get('a').set('b'), 之后输出 'a get a and set b'

> 题目来源：2020.12-好未来

```js
class a {
  constructor {
    text: 'a'
  }

  get (t) {
    this.text = `${this.text} get ${t}`
    return this
  }

  set (t) {
    this.text = `${this.text} and set ${t}`
    return this
  }
}
```

## 实现一个简易的前端模板引擎

> 题目来源：2020.12-好未来

如下：

```js
tpl(`<div class="{%className%}">{%name%}</div>`, {className: 'hd',name:1323})
// 输出 `<div class="hd">1323</div>
```

解答

```js
function tpl (template, data) {

  for (let key in data) {
    template = template.replace(new RegExp('{%'+key+'%}','ig'), data[key])
  }

  return template
}
```

## 合并有序数组的最优解

> 题目来源：2020.12-好未来

- 标签：从后向前数组遍历
- 因为 nums1 的空间都集中在后面，所以从后向前处理排序的数据会更好，节省空间，一边遍历一边将值填充进去
- 设置指针 len1 和 len2 分别指向 nums1 和 nums2 的有数字尾部，从尾部值开始比较遍历，同时设置指针 len 指向 nums1 的最末尾，每次遍历比较值大小之后，则进行填充
- 当 len1<0 时遍历结束，此时 nums2 中海油数据未拷贝完全，将其直接拷贝到 nums1 的前面，最后得到结果数组

时间复杂度：O(m+n)O(m+n)

```js
var merge = function(nums1, m, nums2, n) {
  let len1 = m - 1;
  let len2 = n - 1;
  let len = m + n - 1;

  while(len1 >= 0 && len2 >= 0) {
    // 注意--符号在后面，表示先进行计算再减1，这种缩写缩短了代码
    nums1[len--] = nums1[len1] > nums2[len2] ? nums1[len1--] : nums2[len2--];
  }

  function arrayCopy(src, srcIndex, dest, destIndex, length) {
    dest.splice(destIndex, length, ...src.slice(srcIndex, srcIndex + length));
  }

  // 表示将nums2数组从下标0位置开始，拷贝到nums1数组中，从下标0位置开始，长度为len2+1
  arrayCopy(nums2, 0, nums1, 0, len2 + 1);
}
```
