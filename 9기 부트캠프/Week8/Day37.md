# Day37 요약

## css

```html
<link rel="stylesheet href="global.css> // blue

<style>
    #texst {
        ... // red
    }
</style>

<body>
    <input ... style="color:yellow">    // yellow
</body>
```

* css 는 같은 것을 정의한 순위대로 엎어치게됨
* 1. <input> 태그, 2. <style> 태그, 3. <link> 태그 

**inline, inline-block**

* inline 은 컨텐츠 영역만큼만 크기를 가짐. (width, height 적용 X)
* inline-block은 크기를 명시적으로 지정 가능함. (width, height 적용 O)

**position**

* static
* relative
* absolute
* fixed
* sticky