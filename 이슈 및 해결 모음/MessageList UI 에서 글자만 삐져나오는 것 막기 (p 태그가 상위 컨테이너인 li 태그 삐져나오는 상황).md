# 문제 상황 
![](https://i.imgur.com/NfpRhYz.png)


<br>

# 해결 방법 요약 
``` bash 
- min-w-0 으로, p 태그에게 최소한의 공간을 부여 한다. ('min-w-0')
- p 태그의 내용이 길어질 수 있으니, 길어지면 길어지는 만큼 내용물이 길어질 수 있는 여지가 있다. 
- 이때, 부모 컨테이너인 li 태그를 넘게 되면, 밑으로 떨어지라! 는 명령어를 준다. ('break-words')
	- 그러면, p 태그가 길어지다가, li 태그를 넘게 되는 찰나에 아래로 떨어진다. 
```



<br>

# 해결 코드 
``` js 
const MessageList = () => {
  return (
    <>
      <ul>
        {messageItem.map((item, index) => {
          return (
            <li className="flex p-3 mb-6 bg-stone-300">
              {/* <figure className="w-12 h-12 mr-2 bg-green-500 bg-top bg-cover border-2 rounded-2xl shrink-0 bg-[url('./assets/images/BJJTOM.jpg')]  "></figure> */}
              <figure
                className="w-12 h-12 mr-2 bg-green-500 bg-center bg-cover border-2 rounded-2xl shrink-0 "
                // style={{ backgroundImage: `url(${item.image})` }}
                style={{
                  backgroundImage: `url(${process.env.PUBLIC_URL}/assets/images/${item.image})`,
                }}
              ></figure>

              {/* 📛 삐져 나오는 코드  */}
              {/* <p className=" message-content">{item.desc}</p> */}

              {/* 🔵 해결 코드 */}
              <p className="min-w-0 break-words message-content">{item.desc}</p>
            </li>
          );
        })}
      </ul>
    </>
  );
};

```