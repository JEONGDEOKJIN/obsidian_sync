
# 아키텍처 

https://www.figma.com/file/ES6ry06KdsFaf3OKT5NkPL/%5B240216%5D-%ED%8F%AC%ED%8A%B8%ED%8F%B4%EB%A6%AC%EC%98%A4-%EA%B0%9C%EC%A0%95_%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98-%EB%B0%8F-%EA%B5%AC%EC%A1%B0%EB%8F%84?type=whiteboard&node-id=7-2&t=DhPucNP0k5h1DSW8-4

- 수정 하기 📛 
![](https://i.imgur.com/fWWIrcS.png)








# filter, sort, tag, search  구현

## 1. 해당 기능이 동작할 때, '어떤 데이터' 를 기반으로 동작하게 할 것 인가. (의존관계)

- [예시] 첫 번째 filter 를 실행하고 -> 두 번째 sort 를 실행하는 경우 
``` bash
- '두 번째 sort' 는 '첫 번째 filter 의 결과를 기반' 으로 진행되어야 한다. 
- 따라서, '두 번째 sort 결과' 는 '첫 번째 filter 결과값' 에 '의존' 한다. 
```

<br>

- [예시] 첫 번째 filter 를 실행하고 -> 두 번째 search 를 실행하는 경우 
``` bash 
- '두 번째 search' 는 첫 번째 filter 의 결과값과 '상관없는(독립적)' 경우가 '많다.' 

- 물론, search 기능을, '첫 번째 filter 의 결과값' 을 기반으로 동작하게 할 수 있다. -> 이 것을 '결과 내 재검색' 기능으로 만들어진 것을 본 것 같다. 
- 그렇다면, '기본적으로는 filter 와 독립적' 으로 작동하게 될 것 이다. 
```

<br>

- [정리]
``` bash 
1. filter 와 sort 는 '최신 결과 데이터' 에 의존하게 만들어야 한다. 따라서, 상태관리 라이브러리를 고려해 볼 것. 
	- filter 와 sort 는 '언제나, 가장 최근의 결과 데이터' 를 기반으로 작업이 되어야 한다. 
	- filter 와 sort 의 결과물은 '최근 결과 데이터' 에 항상 반영될 수 있어야 한다. 
	- 이를 위해 
		- useMemo, useEffect 등을 사용할 수도 있고, 
		- 상태 관리 라이브러리(redux, recoil) 등을 사용할 수도 있다.

2. tag 기능과 search 기능은, '독립적' 으로 작동되게 한다. 
	- 즉, filter 를 하고, tag 를 쓰나, filter 를 안 하고 tag 를 쓰나, 동일하게 작동되게 한다. 

3. tag, search의 결과는 '최신 결과 데이터' 에 반영되어야 한다. 
	- 그래야, 검색 결과를 필터링 하고, sort 할 수 있다. 

🙌 결론
	-  filter, sort 는 '종속적 파이프라인(최신 결과 데이터에 의존적)', tag, search 는 '독립적 파이프라인' 으로 구성해보자. 

```

 


## 전역 관리가 필요한가? 아니면 다른 방법으로 뭘 할 수 있지? 

- recoil 
``` bash 
selector 는 atom 기반 
그리고 수정? 
```


- 전역 관리가 반드시 필요한가? 
``` bash 
- '캐싱' 기능이 필요한 경우, 전역 상태 말고, react-query 같은 캐싱을 사용하기도


```


- 전역 관리가 꼭 필요한 경우인지 생각하고 도입 
``` bash 
- 예시 
	- 로그인 권한, 사용자가 갖고 있는 정보를 전역 관리가 들고 있게 하기 
	- 쇼핑 카트 데이터 
	- 애플리 케이션 설정 ex) 다크 모드, 라이트 모드, 
	- 위젯 위에서 동시에 보여줄 때 -> 채팅창 같은 layout 같은 걸 써야 할 수도 
		- ex) 대시 보드, 뉴스 피드 등 

```


- 현재 구현해야 하는 것은 
``` bash 
filter, sort 기능을 구현할 때, 최근에 조작된 데이터, 가 들어가야 한다는 것. 
seacrh, tag 를 하면 -> 그 데이터를 기반으로 filter, sort 를 해야 함. 

그러면, 음... 어떻게 로컬로 관리하지? 

```


- react-query 에서 select 기능으로 필터링? 
``` bash 
- select 옵션으로, '데이터를 필터링' 해서 fetching 완료 data 로 전달할 수 있음. ⭐⭐
		- const { isLoading, error, data: userNames } = useQuery('users', fetchUsers, { select: data => data.map(user => user.name) });

- 생각
	- 1차 filter 기능 적용하고 -> 2차 filter, 3차 필터 까지는 안 되잖아. 
	- 그냥, data 로 부터 받아올 때의 단순 filter 임. 

```


<br>





## [캐싱] react-query (feat. 무한 스크롤, 필터링 기능)

### 꼭 알아야 하는 기능 
``` bash
- '캐싱' 을 어떻게 하는가 
	- const { isLoading, error, data } = useQuery('projects', fetchMetaData);
		- 받아오는 상태 구분 
			- isLoading : 받아지는 중 -> ✅로딩창
			- error : 받아올 때 에러난 경우 
			- data : 받아진 것 완료 
		- fetchProjects : axios 를 통해, 데이터 요청을 보내고, DB 에서 데이터를 받아오는 비동기 함수
		- 'projects' : 쿼리 키. 
			- ex) projects 쿼리키를 사용하면 -> 1) fetchMetaData 비동기 함수를 통해 받아온 동일한 데이터를 사용할 수 있고 2) fresh 데이터를 업데이트 하려면, 해당 쿼리키를 사용하면 됨


- '언제 캐싱' 이 실행돼? 
	- 만약, 기본 코드를 쳤다면, '해당 컴포넌트가 로드' 될 때 실행됨. 
	- 'useEffect 에서, 의존성 배열에 아무것도 없는 것' 과 동일하게 실행됨
	- 실행 순서 및 시간을 조절하고 싶으면 
		1. 시간 기반 조절 : 'staleTime' 옵션 사용 
		2. 특정 조건 조절 : 'enable' 옵션을 사용해서, 특정 조건일 때, fetch 하도록 설정


- 'fresh 데이터' 를 가져오려면 
	1. refetch 함수 사용 
		const { data, refetch } = useQuery('projects', fetchProjects);
		
		// 사용자가 버튼을 클릭하면 refetch 함수를 호출하여 데이터를 새로고침
		<button onClick={() => refetch()}>Refresh Data</button>

	2. 특정 시간 이후에, 자동 refetch
		const { data } = useQuery('projects', fetchProjects, {
		  staleTime: 5000, // 5초 동안 데이터를 신선하게 유지
		});

	3. 특정 쿼리키 무효화 
	- `queryClient.invalidateQueries('projects');`
		- 이렇게 하면, projects 키를 가진 캐싱이 모두 풀림 -> 언제나 fresh 데이터를 가져올 수 있음. 


- 추가 기능 
	- 무한 스크롤, 페이지네이션 기능 제공해줌 ⭐⭐
	- select 옵션으로, '데이터를 필터링' 해서 fetching 완료 data 로 전달할 수 있음. ⭐⭐
		- const { isLoading, error, data: userNames } = useQuery('users', fetchUsers, { select: data => data.map(user => user.name) });
	- 특정 조건에서만 쿼리 실행 (검색 기능) 에 활용 ⭐⭐
		- const { data: searchResults, isLoading, isError } = useQuery(['search', searchTerm], () => fetchSearchResults(searchTerm), { enabled: !!searchTerm, // 검색어가 있을 때만 쿼리 실행 });
```

<br>

### 사용 예시 
``` bash 
1. 서버에서 데이터 가져올 때. CRUD 작업 

2. 실시간 데이터 업데이트 
	- 'useQuery'의 'refetchInterval' 옵션

3. 의존성 있는 데이터 조회 ex) 검색 기능 ⭐⭐⭐  
	- 'useQuery' 의 'enabled' 옵션사용해서, 검색어가 있을 때만, 해당 쿼리를 실행

4. 받아온 데이터에, filter 해서, 렌더링이 필요한 경우 
	- 'useQuery' 의 'select' 옵션

5. 페이지 네이션, 무한 스크롤 
	- React Query의 'useInfiniteQuery'
```

<br>



## search 기능 

- search 기능 분석 (기능 명세, 세부 요건 파악)
``` bash 
- filter, sort 기능과의 관련 
	- 보통, search 를 하고 -> 나온 결과를 -> filter, sort 하는 경향이 있음. 
	- filter, sort 를 걸어놓고 -> search 를 하면 -> filter, sort 가 초기화 되는 경향이 있음. 
	- 아마도, DB 에서 데이터를 받아와서, 처음부터 렌더링 해서 그럴까? 
```


<br>


### 아키텍처 
- 링크 : https://bit.ly/49BjD8Q

![](https://i.imgur.com/OxrMoLU.png)


<br>

### 자주 만나게 되는 문제 

1. 검색 버튼을 눌러야만 검색이 되게 할지 vs 키워드를 넣는 와중에, 자동으로 검색되는 느낌을 주게 할지 
``` bash 
- 이건, useQuery 실행시 전달되는 'searchTerm' 값을 '언제 확정' 지을 것 인가의 문제 
- 즉, 지금 나는 'input 태그' 와 'input 의 submit' 태그를 사용중 
- ⭐⭐⭐ 각각 '고유한 이벤트' 를 갖고 있음 ⭐⭐⭐ 👉 따라서, '각 이벤트의 순간 중, 어디에서, 해당 searchTerm 을 설정해줄 것 인가' 의 문제임
	- handleSearchTermChange : 이 핸들러에서, 'query 될 검색어' 를 셋팅하면 -> 순간순간 보여짐 
	- handleSearchSubmit : 이 핸들러에서 'query 될 검색어' 를 셋팅하면 -> 제출을 눌러야 보여짐 
```


``` js 
  const handleSearchTermChange = (e) => {
    e.preventDefault();
    setSearchBarInput(e.target.value);      
          // input 창에서 검색어가 눌릴 때 마다, 저장하기
      // ⭐ 만약, 여기에 'setSearchTerm' 를 설정하면 -> 변경되는 단어가 실시간으로 검색이 된다.
      // ⭐ 이 로직만 따로 빼서, '검색 드롭다운' 만들면 될 것.
  
  const handleSearchSubmit = (e) => {
    e.preventDefault();

    setSearchTerm(searchBarInput)   // 입력된 검색어를 실제 검색어로 설정
    setIsSubmitClicked(true);   // 검색 실행 위한 상태 변경 -> 이게 있을 때, useQuery 에서 실제로 실행됨
    setSearchBarInput("");    // 검색 필드 초기화
  };

  return (
    <>
      <header>
        <h1>🐉</h1>
        <form className="flex w-3/4 h-12 ml-auto" onSubmit={handleSearchSubmit}>
          <input
            type="search"
            onChange={handleSearchTermChange}
            value={searchBarInput}
          />
          <input
            type="submit"
            value="찾기"
          />
        </form>
    </>
  );
};

export default SearchBar;

```


<br>


2. 의도치 않은, 재실행(재검색) 을 방지하기 
``` bash 
- 문제 상황
	- 에러가 난 경우, 그냥, 에러 페이지에 있게 하고 싶다. 
	- 그런데, 에러 페이지에서 아무런 클릭이나 했을 때, 재실행이 되어버리는 현상이 일어난다. 

- 해결방안 
	- 검색 useQuery 가 실행되는 조건은 3개의 상태 변수를 사용해서 컨트롤 한다.
	- 그리고, isSubmitClicked 를 초기화 ⭐⭐⭐⭐⭐ 
```

``` js 
  // 검색 useQuery
  const {
    data: searchResultData,
    isLoading: isSearchLoading,
    error: isSearchError,
  } = useQuery(
    ["search", searchTerm],
    () => getSearchResults(searchTerm), // searchTerm 이 있을 때, 실행되는 검색쿼리 처리 함수
    {
      enabled:
	  // 3개의 조건을 붙여서, 딱 그 순간에만 검색이 되게 함 ⭐⭐⭐⭐⭐⭐ 
        !!searchTerm && isSubmitClicked == true && searchBarInput != null,
    }
    // searchTerm 이 있을 때만 실행됨
    // isSubmitClicked != null : false 건, true 건 뭔가 들어가 있어야 한다.
    // isSubmitClicked == true
    // searchBarInput!= null : 검색단어가 뭐라도 있을 때 실행된다
  );

  // isSubmitClicked 제출 버튼 완료되면(true) -> 다시 false 로 버튼 초기화 하기⭐⭐⭐⭐⭐⭐ | 이걸 해야, 위의 3개 조건 적은게 완성이 됨 ⭐⭐⭐⭐⭐ 
  useEffect(() => {
    if (isSubmitClicked == true) setIsSubmitClicked(false);
  }, [isSubmitClicked, setIsSubmitClicked]);
```


<br>

3. 내가 만나게 되는 태그가 2개 이면, 2개 모두를 초기화 ⭐⭐⭐⭐⭐ 
``` bash 
- input 태그 초기화 
	- 이걸 해줘야, 검색이 완료되었을 때
		1. 다시 실행이 안 되고 
		2. 볼 때도 깔끔함 

- submit 버튼 제출 초기화 
	- 이걸 해줘야 
		1. submit 이 마음대로 실행되지가 않고, 내가 원하는 타이밍에만 실행됨 
		2. 이걸 안 하면, 다른 곳들 막 클릭해도 -> 재실행이 되어서 -> 그냥 검색이 되버림 
```







<br>

### 검색 기능 예시 코드 

- 프론트에서 검색 키워드 받아서, axios 로 요청 보내는 코드 
``` js 
import React, { useState } from 'react';
import { useQuery } from 'react-query';

// 서버에서 검색 결과를 가져오는 함수
const fetchSearchResults = async (searchQuery) => {
  if (!searchQuery.trim()) return [];
  const response = await fetch(`your-api-endpoint/search?query=${encodeURIComponent(searchQuery)}`);
  if (!response.ok) {
    throw new Error('Network response was not ok');
  }
  return response.json();
};

function SearchComponent() {
  const [searchTerm, setSearchTerm] = useState('');
  const { data: searchResults, isLoading, isError } = useQuery(['search', searchTerm], () => fetchSearchResults(searchTerm), {
    enabled: !!searchTerm, // 검색어가 있을 때만 쿼리 실행
  });

  return (
    <div>
      <input
        type="text"
        placeholder="검색..."
        value={searchTerm}
        onChange={(e) => setSearchTerm(e.target.value)}
      />
      {isLoading && <div>Loading...</div>}
      {isError && <div>Error occurred</div>}
      <ul>
        {searchResults?.map(result => (
          <li key={result.id}>{result.name}</li>
        ))}
      </ul>
    </div>
  );
}
```




- 범위 검색 예시 코드 : 이번에는 전문 검색만 사용 
``` js
// Sequelize Model을 사용한 범위 검색
sequelize.models.PortfolioMeta.findAll({
  where: {
    startDate: {
      [Op.gte]: startDate,
    },
    endDate: {
      [Op.lte]: endDate,
    },
  },
}).then(posts => {
  console.log('범위 검색 결과:', posts);
}).catch(error => {
  console.error(error);
});
```

<br>

- 전문 검색(full-text) 예시 코드 
``` js 
// 검색어
const searchQuery = '검색할 키워드';

// RAW 쿼리를 사용한 Full-Text 검색
sequelize.query(
  'SELECT * FROM `portfolioMetas` WHERE MATCH(title, summary, subTasks, stacks) AGAINST(:searchQuery IN NATURAL LANGUAGE MODE)',
  {
    replacements: { searchQuery },
    model: sequelize.models.PortfolioMeta, // 결과를 모델 인스턴스로 매핑
    mapToModel: true, // Raw 쿼리 결과를 모델 인스턴스로 매핑하도록 설정
    type: sequelize.QueryTypes.SELECT, // 쿼리 타입을 SELECT로 지정
  }
).then(posts => {
  console.log('Full-Text 검색 결과:', posts);
}).catch(error => {
  console.error(error);
});

```

<br>
- model 에서 full-text 인덱싱 설정하기 
``` js 
module.exports = (sequelize, DataTypes) => {
  const PortfolioMeta = sequelize.define('PortfolioMeta', {
    stacks: {
      type: DataTypes.STRING,
    },
    // 다른 필드 정의...
  }, {
    sequelize,
    modelName: "PortfolioMeta",
    tableName: "portfolioMetas", // 테이블 이름을 정확하게 지정
    indexes: [
      {
        type: 'FULLTEXT',
        name: 'text_idx',
        fields: ['title', 'summary', 'subTasks', 'stacks'],
      },
    ],
  });
  return PortfolioMeta;
};
```

<br>
- 범위 검색 
``` js 
module.exports = (sequelize, DataTypes) => {
  const PortfolioMeta = sequelize.define('PortfolioMeta', {
    // 필드 정의
  }, {
    sequelize,
    modelName: "PortfolioMeta",
    tableName: "portfolioMeta",
    indexes: [ // 인덱스 추가
    {
        fields: ['stacks'],
      },
      {
        fields: ['startDate', 'endDate'],
        using: 'BTREE', // 범위 검색에 적합한 B-TREE 인덱스 사용
      }
    ],
  });
  return PortfolioMeta;
};
```


![](https://i.imgur.com/X6ccxr1.png)
```
category_project
1번제목

roles_frontend
2024-02-01 00:00:00
2024-02-16 00:00:00

gradient_large_1708002761639.jpg

2024-02-15 08:42:48
2024-02-15 13:12:41



```



## 예시 코드 
- 설치 
```bash 
@ frontend 
npm i react-query 
```


- index.js 에서 queryClient 인스턴스를 생성해서, App 컴포넌트를 감싸주기 
	- 이렇게 해야, App 컴포넌트 및 그 자식에서, react-query를 자유롭게 사용할 수 있음 
``` js 
import React from "react";
import ReactDOM from "react-dom/client";
import "./index.css";
import App from "./App";
import { QueryClient, QueryClientProvider } from 'react-query'; ⭐⭐⭐

// QueryClient 인스턴스 생성 ⭐⭐⭐ 
const queryClient = new QueryClient();

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <QueryClientProvider client={queryClient}>
    <App />
  </QueryClientProvider>
);
```

<br>

- filter, sort, tag, search 기능 예시 코드 
``` js 
import React, { useState } from 'react';
import { useQuery } from 'react-query';

const fetchData = async () => {
  // 데이터 가져오기 로직 (가상)
  return [
    { id: 1, name: 'Item 1', category: 'Category 1', tag: 'New' },
    { id: 2, name: 'Item 2', category: 'Category 2', tag: 'Sale' },
    // 더 많은 아이템...
  ];
};

const ItemsList = () => {
  const [filter, setFilter] = useState('');
  const [sortOption, setSortOption] = useState('');
  const [selectedTag, setSelectedTag] = useState('');
  const [searchQuery, setSearchQuery] = useState('');

  // useQuery를 사용하여 데이터 가져오기
  const { data, isLoading, error } = useQuery('items', fetchData);

  // 데이터 처리 로직
  const filteredSortedData = data ? data
    .filter(item => {
      // 필터링 조건
      return (!filter || item.category === filter) &&
             (!selectedTag || item.tag === selectedTag) &&    
	             // 이건, item 중 tag 속성에서, 'selectedTag' 의 설정값과 동일한 놈만 보겠다는 의미 ⭐⭐⭐ 
	             // 만약, tag 를 filter, sort 와 독립적으로 움직이게 하고 싶다면, 이건 필요가 없음
             (!searchQuery || item.name.toLowerCase().includes(searchQuery.toLowerCase())); 
	             // 만약, 검색을 filter, sort 와 독립적으로 움직이게 하고 싶다면, 이건 필요가 없음
    })
    .sort((a, b) => {
      // 정렬 조건
      if (sortOption === 'NAME_ASC') {
        return a.name.localeCompare(b.name);
      } else if (sortOption === 'NAME_DESC') {
        return b.name.localeCompare(a.name);
      }
      return 0;
    }) : [];

  if (isLoading) return <div>Loading...</div>;
  if (error) return <div>An error has occurred: {error.message}</div>;

  // UI 컴포넌트와 이벤트 핸들러
  return (
    <div>
      {/* 결과 데이터를 나열하는 UI */}
      <ul>
        {filteredSortedData.map(item => (
          <li key={item.id}>{item.name} ({item.category}, {item.tag})</li>
        ))}
      </ul>
    </div>
  );
};

export default ItemsList;

```



- 검색 기능 예시 코드 
``` js 
import React, { useState } from 'react';
import { useQuery } from 'react-query';

// 서버에서 검색 결과를 가져오는 함수
const fetchSearchResults = async (searchQuery) => {
  if (!searchQuery.trim()) return [];
  const response = await fetch(`your-api-endpoint/search?query=${encodeURIComponent(searchQuery)}`);
  if (!response.ok) {
    throw new Error('Network response was not ok');
  }
  return response.json();
};

function SearchComponent() {
  const [searchTerm, setSearchTerm] = useState('');
  const { data: searchResults, isLoading, isError } = useQuery(['search', searchTerm], () => fetchSearchResults(searchTerm), {
    enabled: !!searchTerm, // 검색어가 있을 때만 쿼리 실행
  });

  return (
    <div>
      <input
        type="text"
        placeholder="검색..."
        value={searchTerm}
        onChange={(e) => setSearchTerm(e.target.value)}
      />
      {isLoading && <div>Loading...</div>}
      {isError && <div>Error occurred</div>}
      <ul>
        {searchResults?.map(result => (
          <li key={result.id}>{result.name}</li>
        ))}
      </ul>
    </div>
  );
}

```



## 알게 된 것 
#### 1. axios 로 받았을 때, 왜 response.data 로 적어야, 원하는 데이터가 나오는가 
``` bash 
- 결론
	결론은, '백엔드에서 send 의 인자로 들어가는 것' = '응답 본문' 에 담김
	axios 설계상, 응답 본문에 담긴 데이터를 가져오려면, 'response.data' 로 접근해야 함. 

- 예시 
	- 백엔드 코드
	export const getAllItem = async (req, res) => {
	  try {
	    const allItem = await db.PortfolioMeta.findAll();

	//⭐⭐⭐ 처리 완료된 데이터를 send 에 담음 -> 그러면, '응답 본문' 에 담김
	    if(allItem) return res.status(200).send(allItem) 
	  
	  } catch (error) {
	    console.log("getAllItem 오류 발생" , error)
	    return res.status(500).send(error.message)
	  }
	}

	- 프론트에서 받을 때 
	      const response = await axios.get(
	        `http://localhost:7070/meta_data/allMetaData`
	      );
	// ⭐⭐⭐ response.data 로 받아야, 응답 본문에 담긴 데이터를 온전히 받음.
	      if(response) return response.data
	      


```


<br>

### 2. 왜 필터 기능이 동작하는거지? (서로 의존적이지 않고, 독립적으로 동작한다고 이해해야 함.)
- 출처 : `C:\Users\user11\Desktop\dj_dev\portfolio_revise\frontend\src\components\CardList.jsx`


- 정리 
``` bash 
- 기존 문제 의식 
	- 현재, project 가 선택된 상태에서, all 을 클릭하면, 왜 category 에 있는 모든 데이터가 보이는 거지? 
	- 현재, feature 가 선택된 상태에서, 그 선택된 데이터를 넣어주지도 않았는데, 왜 project 를 클릭하면, 필터가 되는거지? 

- 대답 
	- 이 과정이 첫 번째 task 와 두 번째 task 가, 연동된게 아니라, 별도의 작업 이라고 생각하면 됨. 
	- 즉, 나는, 첫 번째 task 를 바탕으로, 누적되어, 두 번째 task 를 생각하지만, 그렇게 동작하지 않음. '별도' '독립적' 으로 동작함. 

```


- 필터 기능 
``` js 
  // 필터, 분류 기능
  const filteredSortedData = metaData
    ? metaData.filter((item) => {
        if(filterValue === 'all') return true
        return !filterValue || item.category === filterValue;
      })
    : [];
```

- Filter 컴포넌트 
``` js 
import React from "react";

const Filter = ({setFilterValue}) => {
  
  const handleViewProjectBtn = (e) => {
    e.preventDefault();
    setFilterValue(e.target.value)
  }
  
  return (
    <>
    <section className="flex mr-auto x-32">
        <button 
          className="p-2 mr-1 text-sm bg-gray-200 rounded-lg x-5 y-3"
          value={'all'}
          onClick={handleViewProjectBtn}  
        >
          전체 보기
        </button>

        <button 
          className="p-2 mr-1 text-sm bg-gray-200 rounded-lg x-5 y-3"
          value={'project'}
          onClick={handleViewProjectBtn}
          >
          project 별 보기
        </button>

        <button 
          className="p-2 mr-1 text-sm bg-gray-200 rounded-lg x-5 y-3"
          value={'feature'}
          onClick={handleViewProjectBtn}
          >
          기능 구현 보기
        </button>
        
    </section>
    </>
  );
};

export default Filter;
```


<br>

### 3. input 과 label 연결하기 

1. label 태그로 input 태그를 감싼다.  👉 컴포넌트로 만들기에는 이 방식이 던져줘야 하는 props 가 적어서, 더 편리함 ⭐⭐⭐
``` js 
  {/* [label input 연결 방식 1] label 로 감싸면, 라벨을 클릭해도 -> input 이 클릭될 수 있음.  */}
  <label>
	<input 
	  type ="checkbox" 
	  value = 'project'
	  onChange={handleCheckBoxInput}
	  checked={selectedItem.includes('project')}
	/>
	project 
  </label>
```

<br>

2. input 태그의 id 와 label 태그의 htmlFor 속성을 일치 시킨다.  
``` js 
{/* [label input 연결 방식 2] input 태그의 id 와 label 태그의 htmlFor 를 일치 시킨다. */}
<input
  id="projectCheckBox"
  type="checkbox"
  value="project"
  onChange={handleCheckBoxInput}
  checked={selectedItem.includes("project")}
/>
<label htmlFor="projectCheckBox">project</label>
```


<br>

### 4. 체크 박스 해제 로직 아직 어렵다 
``` js 
  const handleCheckBoxInput = (e) => {
    const value = e.target.value;
    const isChecked = e.target.checked;

    setSelectedFilterOptionArr(
      (prev) =>
        isChecked ? [...prev, value] : prev.filter((item) => item != value)
      // [...prev, value] : 체크가 되었다면 -> 기존 배열에 체크된 값을 넣어서, 새로운 배열을 생성
      // prev.filter(item => item != value) : ⭐체크가 해제되어서⭐, false 가 나왔으면 -> 기존 배열(selectedFilterOptionArr) 의 값을 꺼내서, 같지 않은 것만으로 새로운 배열 만들기
    );
  };
```

<br>

### 5. filter 와 sort 가 '동기적' 으로 처리된다는 걸 알게 됨 
``` bash 
- 이전의 생각 
	- 나는 filter 와 sort 가 동시에 처리되어야 할 것 같다고 느꼈음 
	- 그리고, '동시 처리' 라는 말이 굉장히 두루뭉실 하다는 걸 지금 느낌. 
	- 즉, filter 가 된 결과를 return 받아서, sort 할 수 있고, '동기적' 으로 처리할 수 있는데, 이 부분을 생각하지 못 했다. 

- 알게 된 점 
	1. 이번 필터 기능과 분류 기능에서 요구사항은 'filter 처리가 되면, 그 결과를 반영해서, sort 처리' 가 되어야 한다. 또한 반대로 'sort 처리가 되면, 그 결과를 반영해서, filter 처리' 가 되어야 한다. 
		- 이를 위해 '전역 상태 관리' 를 처음에 생각했다. 왜냐면, '하나의 데이터 store를 공유' 하고 있으면, 거기에서 데이터를 저장했다가, 빼는 식으로 사용하면 될 것 같아서였다.  
		- 물론 이것도 방법일 수 있겠으나, 필터와 분류 기능은 '리스트 페이지' 에만 국한될 수 있다는 점에서, '전역 상태 관리' 방식은 '필요 기능에 비해 큰 기술' 이라는 생각이 들었다. 
		- 따라서, 이를 위해, 'sort 처리 후 filter 를 처리' 하되, 체크한 옵션이 있는지 없는지를 체크함으로써, filter 만 체크한 상황에서도, 문제없이 sort 메소드를 통과할 수 있게 했다. 
	2. '특정 메서드가, 특정 데이터에 기반' 해서 동작하는 경우, 이렇게 '동기적' 인 파이프라인을 구성할 수 있다는 것을 알게 되었다. 
	3. 아키텍처를 구성할 때, '데이터 파이프라인' 이 어떻게 구성되어야 하는지에 대해서도, 고민해야 할 것 같다. 
```

<br>

### 6. 검색 기능을 구현할 때, encodeURIComponent 를 써서, 인자로 들어오는 텍스트를 인코딩 한다. 
``` js 
  const getSearchResults = async (searchTerm) => {

    try {
      if(!searchTerm.trim()) return [];   // 검색어가 없는 경우

	// encodeURIComponent ⭐⭐ 를 사용해서, 인코딩 한다. 
      const response = await axios.get(
        `http://localhost:7070/meta_data/search?query=${encodeURIComponent(searchTerm)}`
      )
  
      if(response) return response.data
      
    } catch (error) {
      console.log(error)
    }
  }
```


<br>

### 7. localeCompare 을 통해 비교하여, sort 한다. (⭐⭐⭐ 추가 학습 필요)
``` js 
  // 필터, 분류 기능
  const filteredSortedData = metaData
    ? metaData
        .filter((item) => {
          // all 을 클릭했거나, 아무것도 클릭 안 해서 배열이 비어있는 경우
          if (
            selectedFilterOptionArr.includes("all") ||
            selectedFilterOptionArr.length === 0
          )
            return true;

          const selectedCategories = selectedFilterOptionArr.filter((option) =>
            option.startsWith("category_")
          );
          const selectedRoles = selectedFilterOptionArr.filter((option) =>
            option.startsWith("roles_")
          );

          // 카테고리만 선택된 상황에서, 해당 item 의 콜백함수를 true 로 반환해서 필터링
          if (selectedCategories.length > 0 && selectedRoles.length === 0) {
            // selectedCategories 의 배열 안의 요소를 순회하면서,
            // 'item.category 의 각 요소의 문자열'이라면,  'clickedCategory 문자열' 과 동일한지 를 판단
            // 'item.category이 배열' 이라면, 각 배열 요소 안에, 'clickedCategory 문자열' 이 있는지를 판단.
            // 동일하다면, some 메서드는 true 를 반환한다.
            // 그러면, 현재, ⭐filter 함수의 콜백함수가 실행중인 상황이므로⭐, 현재 진행중인 콜백함수에는 true 가 반환된다.
            // 따라서, filter 함수로 돌아가서, 현재 진행중인 item 에 대해서는 true 이므로, filter 를 통과하게 된다.
            return selectedCategories.some((clickedCategory) =>
              item.category.includes(clickedCategory)
            );
          }

          // 역할만 선택된 상황에서, 해당 item 의 콜백함수를 true 로 반환해서 필터링
          if (selectedRoles.length > 0 && selectedCategories.length === 0) {
            return selectedRoles.some((clickedRole) =>
              item.roles.includes(clickedRole)
            );
          }

          // 위의 조건이 모두 아니면, '모두 선택된 상황' 이므로 -> 전부 다 필터링 한다.
          return (
            selectedCategories.some((clickedCategory) =>
              item.category.includes(clickedCategory)
            ) &&
            selectedRoles.some((clickedRole) =>
              item.roles.includes(clickedRole)
            )
          );

          // // '선택된 배열안에 있는 값' 과 'metaData 안의 category 속성이 일치' 하면, 그 metaData 아이템을 return 한다.
          // return (
          //   selectedFilterOptionArr.includes(item.category) ||
          //   selectedFilterOptionArr.includes(item.roles)
          // ); // roles 에도 있는지 확인하고 return
        })
        .sort((a, b) => {
          if (sortOption === "title_ascending") {
            // 'NAME_ASC' 같이 영어로 써야❓❓
            return a.title.localeCompare(b.title); // 이게 왜 오름 차순이지❓❓
          } else if (sortOption === "title_descending") {
            return b.title.localeCompare(a.title);
          } else if (sortOption === "date_ascending") {
            return a.endDate.localeCompare(b.endDate);
          } else if (sortOption === "date_descending") {
            return b.endDate.localeCompare(a.endDate);
          }
          return 0;
        })
    : [];
```

<br>

