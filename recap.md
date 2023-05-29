# RECAP

## #4 LOGIN 

```html
<form id="login-form" class="hidden">
  <input
    required
    maxlength="15" 
    type="text" 
    placeholder="What is your name?" 
  />
  <button>Log In</button>
</form>
<h1 id="greeting" class="hidden"></h1>
```

```css
.hidden {
  display: none;
}
```

```jsx
const loginForm = document.querySelector('#login-form');
const loginInput = document.querySelector ('#login-form input');
const greeting = document.querySelector('#greeting');

const HIDDEN_CLASSNAMES = "hidden"
const USERNAME_KEY = "username"

function onLoginSubmit(event) {
  event.preventDefault(); // submit의 기본 동작인 새로고침을 막음.
  loginForm.classList.add(HIDDEN_CLASSNAMES);
  const typedUsername = loginInput.value;
  localStorage.setItem(USERNAME_KEY, typedUsername) // 브라우저에 키(key)와 값(value) 저장(검사 -> application -> localStorage)
  paintGreetings(typedUsername);
}

function paintGreetings(abc) {
  greeting.innerText = `Hello ${abc}`; // '따옴표' 아니고 `백틱`
  greeting.classList.remove(HIDDEN_CLASSNAMES);
}

const savedUsername = localStorage.getItem(USERNAME_KEY); // getItem : 저장된 키(key)를 불러서 값(value)을 확인

if(savedUsername === null)  {
  loginForm.classList.remove(HIDDEN_CLASSNAMES);
  loginForm.addEventListener("submit", onLoginSubmit);
} else {
  paintGreetings(savedUsername);
}

// 처음 로그인 : typedUsername -> abc
// 이후 새로고침 : savedUsername -> abc
```