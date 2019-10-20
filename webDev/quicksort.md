# JavaScript的排序算法——快速排序

### 快速排序（Quicksort）
> 快速排序（Quicksort）是对[冒泡排序](https://www.jianshu.com/p/2fd84fadab5f)的一种改进。它的基本思想是：通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。

![快速排序（Quicksort）](https://upload-images.jianshu.io/upload_images/5701033-ca3cace10219b06d.gif?imageMogr2/auto-orient/strip)

### 复杂度
| 算法|最好情况|平均情况|最坏情况|空间复杂度|稳定性|
|:-------:|:------------:|:------------:|:------------:|:---------------:|:---------:|
|快速排序|O(n log n)|O(n log n)|O(n<sup>2</sup>)|O(log n)|不稳定|

### ES6 实现
```javascript
function QuickSort(array) {
 const sort = (arr, left = 0, right = arr.length - 1) => {
  if (left >= right) {
   return array;
  }
 let i = left;
 let j = right;
 const baseVal = arr[j] ;
 while (i < j) {
  while (i < j && arr[i] <= baseVal) {
   i++;
  }
  arr[j] = arr[i] ;
  while (j > i && arr[j] >= baseVal) { 
   j--;
 }
  arr[i] = arr[j] ;
 }
 arr[j] = baseVal ;
 sort(arr, left, j-1) ;
 sort(arr, j+1, right) ;
 }
 const newArr = array.concat() ;
 sort(newArr);
 return newArr;
}
```

### 参考
- [维基百科](https://en.wikipedia.org/wiki/Quicksort)
- [百度百科](https://baike.baidu.com/item/%E5%BF%AB%E9%80%9F%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/369842?fromtitle=%E5%BF%AB%E9%80%9F%E6%8E%92%E5%BA%8F&fromid=2084344&fr=aladdin)
