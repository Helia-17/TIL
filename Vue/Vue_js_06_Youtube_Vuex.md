[TOC]

# YouTube vuex

## 기본 구조

```vue
$ vue create vuex-youtube
```

```bash
$ vue add vuex
```

- 용량때문에 node.js 삭제했을 때
  - package.json을 읽어와서 필요한걸 설치해줌

```bash
$ npm i
```

- 필요없는거 지우기



- VideoSearchBar.vue

  - 이름 설정 +

  ```html
      <input type="text">
      <button>search</button>
  ```

- App.vue 연결
  - `  <VideoSearchBar/>`
  - `import VideoSearchBar from '@/components/VideoSearchBar'`
  - ` components: {  VideoSearchBar,`



- VideoListItem.vue
  - ` name: 'VideolistItem'`

- VideoList.vue와 연결

  - `import VideoListItem from '@/components/VideoListItem'`
  -   ` <VideoListItem/>`
  - `name: 'VideoList'`, components

  ```js
  import VideoListItem from '@/components/VideoListItem'
  
  export default {
    name: 'VideoList',
      components: {
        VideoListItem
      }
    }
  ```

- App.vue와 VideoList.vue와 연결
  -  ` <VideoList/>`
  - `import VideoList from '@/components/VideoList'`
  - `VideoList`



### 기능 구현

### 검색

- VideoSearchBar.vue

  - 클릭이벤트, query라는 데이터에 기록, 인풋값초기화도 미리 구현

  ```html
      <input type="text" v-model="query">
      <button @click="onSearch">search</button>
  ```

  ```js
  export default {
    name: 'VideoSearchBar',
    data: function () {
      return {
        query: ''
      }
    },
    methods: {
      onSearch: function () {
         console.log(this.query)
         this.query = ''
      }
    }
  }
  ```
  - action실행 위한 dispatch

  ```js
      onSearch: function () {
        console.log(this.query)
        this.$store.dispatch('onSearch', this.query)
         this.query = ''
      }
  ```

  - App.vue에서 axios쓰기

  ```bash
  $ npm i axios
  ```

- index.js에서 import

  ```js
  import axios from 'axios'
  ```

  ```js
  const API_URL = 'https://googleapis.com/youtube/v3/search'
  ```

  ```js
    actions: {
      onSearch: function () {
        axios({
          method: 'get',
          url: API_URL,
        })
      }
    },
  ```

  - apikey도 같이 보내주자

  ```js
  const API_KEY = process.env.VUE_APP_YOUTUBE_API_KEY
  ```

  - .env.local
    - 프로젝트 바로안에 있어야 함

  ```
  VUE_APP_YOUTUBE_API_KEY=AIzaSyDkN_W9-mb3saoil-E1BQCqIS-uNS0gs1Q
  ```

  - onSearch액션으로 params에 담아서 요청보내기 (context도 담아야 완성임)

  ```js
    actions: {
      onSearch: function (q) {
        const params = {
          part: 'snippet',
          key: API_KEY,
          type: 'video',
          q
        }
        axios({
          method: 'get',
          url: API_URL,
          params,
        })
          .then((res) => {
            console.log(res)
          })
      }
    },
  ```

  - context넣기
    - res로 결과를 받아오면 mutation으로 넘겨줌

  ```js
    actions: {
      onSearch: function (context, q) {
        const params = {
          part: 'snippet',
          key: API_KEY,
          type: 'video',
          q
        }
        axios({
          method: 'get',
          url: API_URL,
          params,
        })
          .then((res) => {
            context.commit('ADD_SEARCH_RESULT', res.data.items)
          })
      }
    },
  ```

  - state 작성

  ```js
    state: {
      searchResult: []
    },
  ```

  - mutation으로 state에 넣어주기

  ```js
    mutations: {
      ADD_SEARCH_RESULT: function (state, videos) {
        state.searchResult = videos
      }
    },
  ```

- VideoList.vue에서 출력

  ```html
  {{ this.$store.state.searchResult }}
  ```

**검색결과 보여주기**

- VideoList.vue

  - for문 돌리기, state 가져오기
  - `:video="video"`왼쪽은 자식 컴포넌트에서 받아온 것. 오른쪽은 출력할 v-for의 video

  ```html
      <VideoListItem
        v-for="video in $store.state.searchResult"
        :key="video.etag"
        :video="video"
      />
  ```

- VideoListItem.vue에서 props주기, 출력해서 확인

  ```html
  <p>{{ video }}</p>
  ```

  ```js
    name: 'VideolistItem',
    props: {
      video: Object
    }
  ```

  - 정보 가져오기

  ```vue
  <template>
    <div>
      <p>{{ videoTitle }}</p>
      <p>{{ videoImage }}</p>
    </div>
  </template>
  
  <script>
  export default {
    name: 'VideolistItem',
    props: {
      video: Object
    },
    computed: {
      videoTitle: function () {
        return this.video.snippet.title
      },
      videoImage: function () {
        return this.video.snippet.thumbnails.default.url
      }
    }
  }
  </script>
  ```

  - unescape

  ```bash
  $ npm i lodash
  ```

  ```js
  import _ from 'lodash'
  ```

  ```js
      videoTitle: function () {
        return _.unescape(this.video.snippet.title)
      },
  ```

  - 출력

  ```html
      <img :src="videoImage" alt="">
      <p>{{ videoTitle }}</p>
  ```

  

**클릭이벤트**

- VideoListItem.vue

  - 메서드

  ```js
    methods: {
      selectVideo: function () {
        console.log('click')
      }
    }
  ```
  - 클릭된 정보를 App.vue까지 끌어올려야함
    - 원래는 VideoList.vue를 거쳐야했으나 이제는 데이터를 중앙관리하므로 한번에 가능
    - 보내보자
    - `selectVideo`라는 action, `this.video.`는 어떤 정보를 보내줄지

  ```js
  this.$store.dispatch('selectVideo', this.video)
  ```

- index.js

  - action 작성
    - `'SELECT_VIDEO'`: mutation의 이름

  ```js
      selectVideo: function (context, video) {
        context.commit('SELECT_VIDEO', video)
      }
  ```

  - mutation 작성
    - state의 selectVideo에 저장

  ```js
      SELECT_VIDEO: function (state, video) {
        state.selectVideo = video
      }
  ```

  - state 작성

  ```js
    state: {
      searchResult: [],
      selectVideo: null
    },
  ```

  - 순서 
    - VideoListItem에서 받으며 action 실행
    - muatation 실행
    - state에 저장

- VideoDetail.vue 생성, 이름설정
  - 필요한것만 연산을 해서 보여줄 수 있도록 getters 작성

- index.js

  - getters
    - 세가지 정보 가져오기

  ```js
    state: {
      searchResult: [],
      selectVideo: null
    },
    mutations: { ...
    },
    actions: { ...
    },
    getters: {
      videoURL: function () {
  
      },
      videoTitle: function() {
  
      },
      videoDescription: function() {
  
      }
    },
    modules: {
    }
  ```

  - `selectVideo`가 null일 수도 있으므로 if문 만들기
    - `state.selectVideo` 구조를 찍어보면 `state.selectVideo.id.videoId` 도달 가능
    - 주소에 videoId를 합해 반환
    - 인자로 state넣어줘야!

  ```js
      videoURL: function (state) {
        if (state.selectVideo) {
          const videoId = state.selectVideo.id.videoId
          return `https://www.youtube.com/embed/${videoId}`
        }
      },
  ```

  - 나머지도 Title, Description도 같음 구조 확인해서 쓰면 됨. 
  - 단, unescape 해야

  ```js
  import _ from 'lodash'
  ```

  ```js
    getters: {
      videoURL: function (state) {
        if (state.selectVideo) {
          const videoId = state.selectVideo.id.videoId
          return `https://www.youtube.como/embed/${videoId}`
        }
      },
      videoTitle: function(state) {
        if (state.selectVideo) {
          return _.unescape(state.selectVideo.snippet.title)
        }
      },
      videoDescription: function(state) {
        if (state.selectVideo) {
          return _.unescape(state.selectVideo.snippet.description)
          }
      }
    },
  ```



**mapgetters로 매핑**

- VideoDetail.vue

  - import

  ```js
  import { mapGetters } from 'vuex'
  ```

  - computed

  ```js
    computed: {
      ...mapGetters([
        'videoURL',
        'videoTitle',
        'videoDescription',
      ])
    }
  ```

  - iframe으로 출력

  ```js
      <iframe :src="videoURL" frameborder="0"></iframe>
      <h5>{{ videoTitle }}</h5>
      <p>{{ videoDescription }}</p>
  ```

- App.vue에서 임포트, 등록, 출력

  - `import VideoDetail from '@/components/VideoDetail'`

  - `  <VideoDetail/>`

  - ```js
      components: {
        VideoSearchBar,
        VideoList,
        VideoDetail,
      }
    ```