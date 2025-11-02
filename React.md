```
import React from 'react';

class App extends React.Component {
  render() {
    return (
      <h1>Hello React</h1>
    );
  }
}

export default App;
```
<div>タグで囲んで、1つの要素に  
  JSXを{/* */}で囲むと、その部分はコメントに  
```
```
import React from 'react';

class App extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello World</h1>
        <p>一緒にReactを学びましょう！</p>
        {/* <img>タグを用いて、画像を表示してください */}
        <img src='https://s3-ap-northeast-1.amazonaws.com/progate/shared/images/lesson/react/ninjawanko.png'/>
        
      </div>
    );
  }
}

export default App;

```
```
// Reactをインポートしてください
import React from 'react';

// Appクラスを定義してください
class App extends React.Component{ 
render(){
return (
      <h1>Hello React</h1>
    );
}
// Appクラスをエクスポートしてください
}
export default App;
```
```
イベント名={() => { 処理 }}
```
```
import React from 'react';

class App extends React.Component {
  // constructorを貼り付けてください
  constructor(props) {
    super(props);
    // stateを定義してください
    this.state = {name:'にんじゃわんこ'};
    
  }
  
  render() {
    return (
    	<div>
    	  <h1>こんにちは、にんじゃわんこさん！</h1>
        <button onClick={() => {console.log('ひつじ仙人')}}>ひつじ仙人</button>
        <button onClick={() => {console.log('にんじゃわんこ')}}>にんじゃわんこ</button>
      </div>
    );
  }
}

export default App;
```
```
import React from 'react';

class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = {name: 'にんじゃわんこ'};
  }
  
  render() {
    return (
    	<div>
        {/* 「こんにちは、にんじゃわんこさん！」の名前の部分をstateを使って置き換えてください */}
    	  <h1>こんにちは、{this.state.name}さん！</h1>
    	  
        <button onClick={() => {console.log('ひつじ仙人')}}>ひつじ仙人</button>
        <button onClick={() => {console.log('にんじゃわんこ')}}>にんじゃわんこ</button>
      </div>
    );
  }
}

export default App;

```
```
import React from 'react';

class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = {name: 'にんじゃわんこ'};
  }
  
  render() {
    return (
    	<div>
    	  <h1>こんにちは、{this.state.name}さん！</h1>
    	  {/* onClickの処理に、stateを変更する処理を加えてください */}
        <button onClick={() => {this.setState({name:'ひつじ仙人'})}}>ひつじ仙人</button>
        
        {/* onClickの処理に、stateを変更する処理を加えてください */}
        <button onClick={() => {this.setState({name:'にんじゃわんこ'})}}>にんじゃわんこ</button>
        
      </div>
    );
  }
}

export default App;
```
```
import React from 'react';

class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = {name: 'にんじゃわんこ'};
  }
  
  // handleClickメソッドを定義してください
  handleClick(name){
    this.setState({name:name});
  }
  
  render() {
    return (
    	<div>
    	  <h1>こんにちは、{this.state.name}さん！</h1>
    	  {/* onClickイベント内の処理を、handleClickメソッドを呼び出す処理に書き換えてください*/}
        <button onClick={() => {this.handleClick('ひつじ仙人')}}>ひつじ仙人</button>
        
    	  {/* onClickイベント内の処理を、handleClickメソッドを呼び出す処理に書き換えてください*/}
        <button onClick={() => {this.handleClick('にんじゃわんこ')}}>にんじゃわんこ</button>
        
      </div>
    );
  }
}

export default App;
```
```
import React from 'react';

class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = {count: 0};
  }
  
  // handleClickメソッドを定義してください
  handleClick(){
    this.setState({count: this.state.count + 1});
  }
  
  render() {
    return (
      <div>
        <h1>
          {this.state.count}
        </h1>
        {/* <button>タグ内でonClickイベントを追加してください */}
        <button onClick={()=>{this.handleClick()}}>+</button>
        
      </div>
    );
  }
}

export default App;
```
```
import React from 'react';
import ReactDOM from 'react-dom';
import App from './components/App';
// 以下に指定されたコードを貼り付けてください 
ReactDOM.render(<App />, document.getElementById('root'));
```
```
コンポーネントは「部品」や「パーツ」という意味です。  
Reactでは、見た目を機能ごとにコンポーネント化して、  
コンポーネントを組み合わせることでWebサイトの見た目を作ります。  
```
