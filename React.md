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
```
import React from 'react';
// Languageコンポーネントをインポートしてください
import Language from './Language'

class App extends React.Component {
  render() {
    return (
      <div>
        <h1>言語一覧</h1>
        <div className="language">
          {/* Languageコンポーネントを呼び出してください */}
          <Language />
          
        </div>
      </div>
    );
  }
}

export default App;
```
```
import React from 'react';
import Language from './Language';

class App extends React.Component {
  render() {
    return (
      <div>
        <h1>言語一覧</h1>
        <div className='language'>
          {/* HTML & CSSのpropsを渡してください */}
          <Language 
            name='HTML & CSS'
            image='https://s3-ap-northeast-1.amazonaws.com/progate/shared/images/lesson/react/html.svg'
            
          />
          {/* JavaScriptのpropsを渡してください */}
          <Language 
            name='JavaScript'
            image='https://s3-ap-northeast-1.amazonaws.com/progate/shared/images/lesson/react/es6.svg'
          />
          {/* Reactのpropsを渡してください */}
          <Language 
            name='React'
            image='https://s3-ap-northeast-1.amazonaws.com/progate/shared/images/lesson/react/react.svg'
          />
        </div>
      </div>
    );
  }
}

export default App;
```
```
import React from 'react';

class Language extends React.Component {
  render() {
    return (
      <div className='language-item'>
        {/* props名nameの値を表示するように書き換えてください */}
        <div className='language-name'>
        {this.props.name}
        </div>
        
        {/* src属性の値を、props名imageの値に書き換えてください */}
        <img 
          className='language-image'
          src={this.props.image}
        />
        
      </div>
    );
  }
}

export default Language;
```
```
import React from 'react';
import Language from './Language';

class App extends React.Component {
  render() {
    // 指定されたコードを貼り付けてください
    const languageList = [
      {
        name: 'HTML & CSS',
        image: 'https://s3-ap-northeast-1.amazonaws.com/progate/shared/images/lesson/react/html.svg'
      },
      {
        name: 'JavaScript',
        image: 'https://s3-ap-northeast-1.amazonaws.com/progate/shared/images/lesson/react/es6.svg'
      },
      {
        name: 'React',
        image: 'https://s3-ap-northeast-1.amazonaws.com/progate/shared/images/lesson/react/react.svg'
      },
      {
        name: 'Ruby',
        image: 'https://s3-ap-northeast-1.amazonaws.com/progate/shared/images/lesson/react/ruby.svg'
      },
      {
        name: 'Ruby on Rails',
        image: 'https://s3-ap-northeast-1.amazonaws.com/progate/shared/images/lesson/react/rails.svg'
      },
      {
        name: 'Python',
        image: 'https://s3-ap-northeast-1.amazonaws.com/progate/shared/images/lesson/react/python.svg'
      }
    ];

    return (
      <div>
        <h1>言語一覧</h1>
        <div className='language'>

          {/* mapメソッドを用いて、Languageコンポーネントを表示してください */}
          {languageList.map((languageItem) => {
            return (
              // Languageコンポーネントを呼び出し、その中でpropsを渡してください
             < Language
             name={languageItem.name}
              image={languageItem.image}
              />
            )
          })}
          
        </div>
      </div>
    );
  }
}

export default App;
```
```
import React from 'react';

class Lesson extends React.Component {
  render() {
    return (
      <div className='lesson-card'>
        <div className='lesson-item'>
          {/* props名nameの値を入れてください*/}
          <p>{this.props.name}</p>
          
          {/* src属性に、props名imageの値を指定してください */}
          <img src={this.props.image} />
          
        </div>
      </div>
    );
  }
}

export default Lesson;
```
```
import React from 'react';
import Lesson from './Lesson';

class Main extends React.Component {
  render() {
    const lessonList = [
      {
        name: 'HTML & CSS',
        image: 'https://s3-ap-northeast-1.amazonaws.com/progate/shared/images/lesson/react/html.svg',
      },
      {
        name: 'Sass',
        image: 'https://s3-ap-northeast-1.amazonaws.com/progate/shared/images/lesson/react/sass.svg',
      },
      {
        name: 'JavaScript',
        image: 'https://s3-ap-northeast-1.amazonaws.com/progate/shared/images/lesson/react/es6.svg',
      },
      {
        name: 'React',
        image: 'https://s3-ap-northeast-1.amazonaws.com/progate/shared/images/lesson/react/react.svg',
      },
    ];
    
    return (
      <div className='main-wrapper'>
        <div className='main'>
          <div className='copy-container'>
            <h1>Hello, World.</h1>
            <h2>プログラミングの世界へようこそ！</h2>
          </div>
          <div className='lesson-container'>
            <h3 className='section-title'>学べるレッスン</h3>
            {/* lessonListに対して、mapメソッドを用いてください */}
            {lessonList.map((lessonItem)=>{
              return(
              <Lesson
                  name={lessonItem.name}
                  image={lessonItem.image}
                />)
            })}
            
          </div>
        </div>
      </div>
    );
  }
}

export default Main;
import React from 'react';
import Lesson from './Lesson';

class Main extends React.Component {
  render() {
    const lessonList = [
      {
        name: 'HTML & CSS',
        image: 'https://s3-ap-northeast-1.amazonaws.com/progate/shared/images/lesson/react/html.svg',
      },
      {
        name: 'Sass',
        image: 'https://s3-ap-northeast-1.amazonaws.com/progate/shared/images/lesson/react/sass.svg',
      },
      {
        name: 'JavaScript',
        image: 'https://s3-ap-northeast-1.amazonaws.com/progate/shared/images/lesson/react/es6.svg',
      },
      {
        name: 'React',
        image: 'https://s3-ap-northeast-1.amazonaws.com/progate/shared/images/lesson/react/react.svg',
      },
    ];
    
    return (
      <div className='main-wrapper'>
        <div className='main'>
          <div className='copy-container'>
            <h1>Hello, World.</h1>
            <h2>プログラミングの世界へようこそ！</h2>
          </div>
          <div className='lesson-container'>
            <h3 className='section-title'>学べるレッスン</h3>
            {/* lessonListに対して、mapメソッドを用いてください */}
            {lessonList.map((lessonItem)=>{
              return(
              <Lesson
                  name={lessonItem.name}
                  image={lessonItem.image}
                />)
            })}
            
          </div>
        </div>
      </div>
    );
  }
}

export default Main;
```
```
import React from 'react';

class Lesson extends React.Component {
  // constructorを定義してください
  constructor(props) {
    super(props);
    // stateの初期値を定義してください
    this.state={isModalOpen:false}
    
  };
  
  render() {
    return (
      <div className='lesson-card'>
        <div className='lesson-item'>
          <p>{this.props.name}</p>
          <img src={this.props.image} />
        </div>
        <div className='modal'>
          <div className='modal-inner'>
            <div className='modal-header'></div>
            <div className='modal-introduction'>
              <h2>{this.props.name}</h2>
              <p>{this.props.introduction}</p>
            </div>
            <button className='modal-close-btn'>
              とじる
            </button>
          </div>
        </div>
      </div>
      
    );
  }
}
```
```
import React from 'react';

class Lesson extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isModalOpen: false};
  }
  
  // handleClickLessonメソッドを定義してください
  handleClickLesson(){
  this.setState({isModalOpen:ture});
  
  render() {
    let modal;
    if (this.state.isModalOpen) {
      modal = (
        <div className='modal'>
          <div className='modal-inner'>
            <div className='modal-header'></div>
            <div className='modal-introduction'>
              <h2>{this.props.name}</h2>
              <p>{this.props.introduction}</p>
            </div>
            <button className='modal-close-btn'>
              とじる
            </button>
          </div>
        </div>
      );
    }
    return (
      <div className='lesson-card'>
        {/* onClickイベントを追加してください */}
        <div
          className='lesson-item'
          onClick={()=>{this.handleClickLesson()}}
        >
          <p>{this.props.name}</p>
          <img src={this.props.image} />
        </div>
        {modal}
      </div>
    );
  }
}

export default Lesson;
```
export default Lesson;
```
```
import React from 'react';

class Lesson extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isModalOpen: false};
  }

  handleClickLesson() {
    this.setState({isModalOpen: true});
  }
  
  // handleClickCloseメソッドを定義してください
  handleClickClose(){
    this.setState({isModalOpen: false});
  }

  render() {
    let modal;
    if (this.state.isModalOpen) {
      modal = (
        <div className='modal'>
          <div className='modal-inner'>
            <div className='modal-header'></div>
            <div className='modal-introduction'>
              <h2>{this.props.name}</h2>
              <p>{this.props.introduction}</p>
            </div>
            {/* onClickイベントを追加してください */}
            <button
              className='modal-close-btn'
          　onClick={() => {this.handleClickClose()}}
            >
              とじる
            </button>
          </div>
        </div>
      );
    }

    return (
      <div className='lesson-card'>
        <div
          className='lesson-item'
          onClick={() => {this.handleClickLesson()}}
        >
          <p>{this.props.name}</p>
          <img src={this.props.image} />
        </div>
        {modal}
      </div>
    );
  }
}

export default Lesson;
```
```
import React from 'react';

class ContactForm extends React.Component {
  render() {
    return (
      <div className='contact-form'>
        <form>
          <p>メールアドレス（必須）</p>
          {/* inputタグを追加してください */}
          <input />
          
          <p>お問い合わせ内容（必須）</p>
          {/* textareaタグを追加してください */}
          <textarea />
          
          {/* 送信ボタンを追加してください */}
          <input
          type='submit'
          value='送信'
        </form>
      </div>
    );
  }
}

export default ContactForm;
```
```
import React from 'react';

class ContactForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      /* isSubmittedというstateを定義してください */
      isSubmitted:false
    };
  }

  render() {
    /* 空の変数contactFormを定義してください */
    let contactForm;
    
    /* isSubmittedを条件式とするif文を作成してください */
    if (this.state.isSubmitted){
    contactForm=(
<div className='contact-submit-message'>
          送信完了
        </div>
      );
    } else {            
     contactForm = (
    
    <form>
          <p>メールアドレス（必須）</p>
          <input />
          <p>お問い合わせ内容（必須）</p>
          <textarea />
          <input
            type='submit'
            value='送信'
          />
        </form>
        );
    }
    return (
      <div className='contact-form'>
        {/* 以下を削除して、変数contactFormを表示してください */}
{contactForm}
      </div>
      
    );
  }
}

export default ContactForm;
```
```
import React from 'react';

class ContactForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isSubmitted: false,
    };
  }

  /* handleSubmitメソッドを定義してください  */
  handleSubmit(){
    this.setState({isSubmitted:true});
  }

  render() {
    let contactForm;
    if (this.state.isSubmitted) {
      contactForm = (
        <div className='contact-submit-message'>
          送信完了
        </div>
      );
    } else {
      contactForm = (
        /* formタグにonSubmitを追加してください */
        <form onSubmit={()=>{this.handleSubmit} }>
          <p>メールアドレス（必須）</p>
          <input />
          <p>お問い合わせ内容（必須）</p>
          <textarea />
          <input
            type='submit'
            value='送信'
          />
        </form>
      );
    }
    
    return (
      <div className='contact-form'>
        {contactForm}
      </div>
    );
  }
}

export default ContactForm;
```
```
import React from 'react';

class ContactForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isSubmitted: false,
      /* stateにemailを追加してください */
      email:'mail@prog-8.com'
    };
  }

  handleSubmit() {
    this.setState({isSubmitted: true});
  }

  render() {
    let contactForm;
    if (this.state.isSubmitted) {
      contactForm = (
        <div className='contact-submit-message'>
          送信完了
        </div>
      );
    } else {
      contactForm = (
        <form onSubmit={() => {this.handleSubmit()}}>
          <p>メールアドレス（必須）</p>
          {/* inputにvalue属性を加えてください */}
          <input  value={this.state.email}/>
          
          <p>お問い合わせ内容（必須）</p>
          <textarea />
          <input
            type='submit'
            value='送信'
          />
        </form>
      );
    }
    
    return (
      <div className='contact-form'>
        {contactForm}
      </div>
    );
  }
}

export default ContactForm;

```
```
import React from 'react';

class ContactForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isSubmitted: false,
      email: '',
    };
  }

  handleSubmit() {
    this.setState({isSubmitted: true});
  }

  render() {
    let contactForm;
    if (this.state.isSubmitted) {
      contactForm = (
        <div className='contact-submit-message'>
          送信完了
        </div>
      );
    } else {
      contactForm = (
        <form onSubmit={() => {this.handleSubmit()}}>
          <p>メールアドレス（必須）</p>
          {/* inputにonChangeイベントを追記してください */}
          <input
            value={this.state.email}
            onChange={(event)=>{console.log(event.target.value)}}
          />
          <p>お問い合わせ内容（必須）</p>
          <textarea />
          <input
            type='submit'
            value='送信'
          />
        </form>
      );
    }
    
    return (
      <div className='contact-form'>
        {contactForm}
      </div>
    );
  }
}

export default ContactForm;
```
```
import React from 'react';

class ContactForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isSubmitted: false,
      email: '',
    };
  }

  /* handleEmailChangeという名前のメソッドを定義してください */
  handleEmailChange(event){
    const inputValue=event.target.value;
    this.setState({email: inputValue});
  }

  handleSubmit() {
    this.setState({isSubmitted: true});
  }

  render() {
    let contactForm;
    if (this.state.isSubmitted) {
      contactForm = (
        <div className='contact-submit-message'>
          送信完了
        </div>
      );
    } else {
      contactForm = (
        <form onSubmit={() => {this.handleSubmit()}}>
          <p>メールアドレス（必須）</p>
          <input
            value={this.state.email}
            /* console.log(event.target.value) の部分を削除してください */
            /* handleEmailChangeを実行するようにしてください */
            onChange={(event) => {handleEmailChange(event)}}
          />
          <p>お問い合わせ内容（必須）</p>
          <textarea />
          <input
            type='submit'
            value='送信'
          />
        </form>
      );
    }
    
    return (
      <div className='contact-form'>
        {contactForm}
      </div>
    );
  }
}

export default ContactForm;
```
```
import React from 'react';

class ContactForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isSubmitted: false,
      email: '',
      /* hasEmailErrorを追加してください */
      hasEmailError:false,
    };
  }

  handleEmailChange(event) {
    const inputValue = event.target.value;
    this.setState({email: inputValue});
  }

  handleSubmit() {
    this.setState({isSubmitted: true});
  }

  render() {
    /* 変数emailErrorTextを定義してください */
   let emailErrorText;
    
    /* hasEmailErrorを条件にしたif文を作成してください */
    if (this.state.hasEmailError){
      emailErrorText=(
        <p className='contact-message-error'>
          メールアドレスを入力してください
        </p>
        );
    }

    let contactForm;
    if (this.state.isSubmitted) {
      contactForm = (
        <div className='contact-submit-message'>
          送信完了
        </div>
      );
    } else {
      contactForm = (
        <form onSubmit={() => {this.handleSubmit()}}>
          <p>メールアドレス（必須）</p>
          <input
            value={this.state.email}
            onChange={(event) => {this.handleEmailChange(event)}}
          />
          {/* emailErrorTextを表示してください */}
          {emailErrorText}
          
          <p>お問い合わせ内容（必須）</p>
          <textarea />
          <input
            type='submit'
            value='送信'
          />
        </form>
      );
    }

    return (
      <div className='contact-form'>
        {contactForm}
      </div>
    );
  }
}

export default ContactForm;
```
```
import React from 'react';

class ContactForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isSubmitted: false,
      email: '',
      hasEmailError: false,
    };
  }

  handleEmailChange(event) {
    const inputValue = event.target.value;
    /* 定数isEmptyを定義し、入力チェックの結果を代入してください */
    const isEmpty = inputValue==='';
    this.setState({
      email:inputValue,
      hasEmailError:isEmpty,
    });
    
    /* hasEmailErrorを更新してください */
    this.setState({email: inputValue});
    
  }

  handleSubmit() {
    this.setState({isSubmitted: true});
  }

  render() {
    let emailErrorText;
    if (this.state.hasEmailError) {
      emailErrorText = (
        <p className='contact-message-error'>
          メールアドレスを入力してください
        </p>
      );
    }

    let contactForm;
    if (this.state.isSubmitted) {
      contactForm = (
        <div className='contact-submit-message'>
          送信完了
        </div>
      );
    } else {
      contactForm = (
        <form onSubmit={() => {this.handleSubmit()}}>
          <p>メールアドレス（必須）</p>
          <input
            value={this.state.email}
            onChange={(event) => {this.handleEmailChange(event)}}
          />
          {emailErrorText}
          <p>お問い合わせ内容（必須）</p>
          <textarea />
          <input
            type='submit'
            value='送信'
          />
        </form>
      );
    }

    return (
      <div className='contact-form'>
        {contactForm}
      </div>
    );
  }
}

export default ContactForm;
```
