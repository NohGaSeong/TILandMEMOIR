# JS 슬라이드 구현하기.

```
var slideWrapper = document.querySelector('.container');
var slides = document.querySelectorAll('.item');
var totalSlides = slides.length; // item의 갯수


var sliderWidth = slideWrapper.clientWidth; // container의 width
var slideIndex = 0;
var slider = document.querySelector('.slider');

slider.style.width = sliderWidth * totalSlides + 'px';

showSlides()

function showSlides() {
    for(var i=0;i<slides.length;i++){
        slider.style.left = -(sliderWidth * slideIndex) + 'px';    
    }
    slideIndex++;
    if (slideIndex === totalSlides) {
        slideIndex = 0;
    }
    setTimeout(showSlides, 2000);  //넘어가는 시간
}
```

## 아쉬운 점
마지막에서 다시 처음으로 갈떄 왼쪽으로 슉하고 넘어가는게 아쉬웠음. 다음엔 이걸 수정해서 한쪽 방향으로만 가게 구현해볼 예정.
