# crud 해보기
## GET
```.js
fetch('/data.json')
  .then(response => response.json())
  .then(data => {
    console.log(data)
  })
```
## POST
```.js
fetch(url, {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
        },
        body: JSON.stringify(data)
    })
    .then(response => response.json())
    .then(data => {
        console.log(data)
     })
```
## DELETE
```.js
fetch('http://백엔드 주소/cart', {
        method: 'DELETE',
        headers: {
          Authorization: localStorage.getItem('access_token'),
        },
        body: JSON.stringify({
          //삭제하고싶은 데이터의 물건 id
          cart_id: data.cart_id,
        }),
```
## PUT
```.js
fetch('http://백엔드 주소/cart', {
      method: 'PATCH',
  //http는 stateless성을 띄기 때문에 항상 토큰값을 넣어 백엔드에 요청해야한다.
      headers: { authorization: localStorage.getItem('access_token') },
  // 바디에 수정하고싶은 값을 넣어 보내줘야한다, JSON.stringify는 보내는값을 컴퓨터가 읽을수있는 문자로 바꿔준다고 생각하면됨.
      body: JSON.stringify({
        cart_id: cartListCopy[selectedIdx].cart_id,
        // 수량을 변경하고싶은 물건 id
        quantity: cartListCopy[selectedIdx].quantity,
        // 변경하고자 하는 수량.
      }),
    });
```
