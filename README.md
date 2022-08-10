# study-vue-js
Vue.js 시작하기

VSCode 플러그인 
- Vetur
코드 하이라이팅 위해서 사용합니다.

- Night Owl
색상조정

- Material Icon Theme
Material Icon을 VS코드로 가져온다.

- Live Server
파일을 저장하지 않고 실시간으로 변경가능
정적 및 동적 페이지에 대한 라이브

- ESLint
자바스크립트 문법 검사기.
코드에서 발견 된 문제 패턴을 식별하기 위한 정적 코드 분석 도구.
(코드품질과 코딩 스타일 문제를 모두 다룹니다.)

- Prettier
코드 포맷터

- Auto Close Tag
닫기 태그 자동 입력

- Atom Keymap
아톰에서 즐겨사용 하는 키보드 단축키를 사용할 수 있다.



- 객체 동작,속성 재정의 API ('대상객체' 객체의 속성{정의할 내용})
```c
        Object.defineProperty(viewModel, 'str', {
            //속성에 접근했을 때의 동작을 정의
            get: function () {
                console.log('접근');
            },
            //속성에 값을 할당했을 떄의 동작을 정의
            set: function (newValue) {
                console.log('할당',newValue);
                div.innerHTML = newValue;
            }
        });
```
- 즉시 실행 함수 
```c
(function () {
    //실행함수
})();
```

- 인스턴스에서 사용할 수 있는 속성 API 
```c
new Vue({
    el : 
    , template:
    , data:
    , methods:
    , created:
    , watch: 
})
```

-component 등록
```c
        Vue.component('컴포넌트 이름', {
            // '컴포넌트내용'
        })
```
-전역컴포넌트
```c
        Vue.component('app-header',{
            template:'<h1>Header</h1>'
        });
```
-지역컴포넌트
```c
        new Vue({
            el:'#app'
            //지역 컴포넌트 등록 방식
            ,  components:{
                // 'key:value'
                //컴포넌트 이름 : 컴포넌트 내용
                'app-footer':{
                    template: '<footer>footer</footer>'
                }
            }   
        })
```

# 상위 -> 하위 : props로 전달
# 하위 -> 상위 : event로 전달

-하위 컴포넌트 데이터 전달(props)
```c
    <div id="app">
        <!-- <app-header v-bind:프롭스 속성 이름 ="상위 컴포넌트의 데이터 이름"></app-header> -->
        <app-header v-bind:propsdata="message"></app-header>
    </div>
    var appHeader = {
        'app-header': {
            template: '<h1>header</h1>'
            , props:['propsdata']
        }
    };
```

-상위 컴포넌트 데이터 전달(event)
```c
    <div id="app">
        <p>{{num}}</p>
        <!-- <app-header v-on:하위컴포넌트에서 발생한 이벤트 이름="상위컴포넌트의 메서드"></app-header> -->
        <app-header v-on:pass="logText"></app-header>
        <app-content v-on:increase="increaseNumber"></app-content>
    </div>

         var appHeader = {
            template: '<button v-on:click="passEvent">클릭!</button>',
            methods: {
                passEvent: function(){
                    this.$emit('pass');
                }
            }
        }
        var appContent = {
            template: '<button v-on:click="addNumber">add</button>',
            methods:{
                addNumber : function(){
                    this.$emit('increase')
                }
            }
        }

        var vm  = new Vue({
            el: '#app'
            , components: {
                'app-header': appHeader,
                'app-content':appContent
            },
            methods:{
                logText:function(){
                    console.log('hi');
                },
                increaseNumber :function(){
                    this.num = ++this.num;
                }
                
            },
            data:{
                num : 10
            }
        });
```
-$emit() 이벤트 전달

-Vue CLI로 import 하여 사용 가능