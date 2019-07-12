# 排序相关

## 冒泡排序

```ts
function bubbleSort (arr: number[]): void {
  for (let i = 0; i < arr.length -1; i++) {
    for (let j = arr.length -1; j > i; j--) {
      if (arr[j] < arr[i]) {
        [arr[i], arr[j]] = [arr[j], arr[i]]
      }
    }
  }
}

```

## 选择排序

```ts
function selectSort (arr: number[]): void {
  let minIndex = 0
  for (let i = 0; i< arr.length -1; i++) {
    minIndex = i
    for (let j = i+1; j< arr.length; j++) {
      if (arr[j] < arr[minIndex]) {
        minIndex = j
      }
    }
    if (minIndex != i) {
      [arr[i], arr[j]] = [arr[j], arr[i]]
    }
  }
}

```

## 插入排序

```ts
function insertSort (arr: number[]) {
  for (let i = 1; i< arr.length; i++) {
    let j = i
    let target = arr[i]
    // 后移
    while (j >0 && target < arr[j-1]) {
      arr[j] = arr[j-1]
      j--
    }
    // 插入
    arr[j] = target
  }
}
```

## 快速排序
```ts

```

## 希尔排序
```ts

```