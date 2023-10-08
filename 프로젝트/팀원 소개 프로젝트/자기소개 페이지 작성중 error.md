firebase에서 받아온 데이터를 가지고
동적 tag생성 후 addevent가 안먹힘.
동적 tag생성 후 addevent를 했지만 async, await때문인지 적용되지않음.

```javascript
const searchComment = async () => {  
  const dataList = await getDocs(query(commentRef, orderBy("regDate", "desc")));  
  createCommentCard(dataList);  
};

const createCommentCard = dataList => {  
  dataList.forEach(item => {  
    let contentWrapper = document.createElement("div");  
    contentWrapper.classList.add("comment-card");  
    contentWrapper.innerHTML = `  
            <h2>${item.data().commentName}</h2>  
            <p>              ${item.data().commentContents}  
            </p>            <div class="comment-card__delete">              <button class="del-btn" value="${item.data().commentId}"></button>  
            </div>    `;  
    commentDiv.append(contentWrapper);  
  });  
  delBtnAddEvent();  
};

let delBtn = document.querySelectorAll(".del-btn");


const delBtnAddEvent = () => {  
  delBtn.forEach(buttons => {  
    buttons.addEventListener("click", event => {  
      event.preventDefault();  
      delModal.classList.toggle("active");  
    });  
  });  
};  
searchComment();
```

변경 후

```javascript
const searchComment = async () => {  
  const dataList = await getDocs(query(commentRef, orderBy("regDate", "desc")));  
  createCommentCard(dataList);  
};  
  
const createCommentCard = dataList => {  
  dataList.forEach(item => {  
    let contentWrapper = document.createElement("div");  
    contentWrapper.classList.add("comment-card");  
    contentWrapper.innerHTML = `  
            <h2>${item.data().commentName}</h2>  
            <p>              ${item.data().commentContents}  
            </p>            <div class="comment-card__delete">              <button class="del-btn" value="${item.data().commentId}"></button>  
            </div>    `;  
    commentDiv.append(contentWrapper);  
  });  
  delBtnAddEvent();  
};


const delBtnAddEvent = () => {  
  let delBtn = document.querySelectorAll(".del-btn");  
  delBtn.forEach(buttons => {  
    buttons.addEventListener("click", event => {  
      event.preventDefault();  
      delModal.classList.toggle("active");  
    });  
  });  
};  
searchComment();
```