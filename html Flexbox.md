ならびむきを指定  
折り返しを指定  
***
display: flexは指定した要素の子要素を横並びに  
横並びにしたい要素の親要素にdisplay: flex  
***
親要素の幅に合わせて伸ばしたい要素にflex: autoを指定  
***
flex-wrap: wrapを指定すると、子要素のサイズに応じて折り返す  
折り返したい要素の親要素にflex-wrap: wrapを指定  
折り返したい要素自身には列数に応じたwidthを指定  
今回は2列にしたいのでwidth: 50%を指定  
***
```
.flex-list {
  display: flex;
  /* flex-wrapを指定してください */
  flex-wrap: wrap
  
}
.flex-list li {
  flex: auto;
  /* widthを50％に指定してください */
  width:50%;
  
}
```
***
画面幅を狭めた時に2列に折り返すように 
```
@media (max-width: 1000px) {
  .flex-list {
    flex-wrap: wrap;
  }
  .flex-list li {
    width: 50%;
  }
}
```
***
画面幅を狭めた時に1列に並ぶように  
flex-direction: columnは子要素を上から下へ  
縦に並べたい要素の親要素にflex-direction: columnを指定  
margin: 0 autoとwidthを指定することで中央寄せに  
```
/* スマホ向けレイアウト */
/* ブレイクポイントが670px以下の時のメディアクエリを設定してください */
@media (max-width:670px) {
  /* .flex-listにflex-directionを指定してください */
  .flex-list{
    flex-direction: column;
  }
  /* .flex-list liにmarginを0 autoに指定してください */
  .flex-list li{
    margin:0 auto;
  }
}
```
***
