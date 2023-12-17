---
title: Guestbook
description: 
slug: about
date: '2019-04-28'
aliases:
  - contact
menu:
    main: 
        weight: -80
        params:
            icon: coffee
---

  <!-- index.html or home.html -->
  <div id="text">
    <p style="font-size: 2rem; text-align: center; font-weight: bold; color: var(--card-text-color-secondary);"></p> 
  </div>
  <!-- ... other HTML content ... -->
  
  <script>
    let divTyping = document.querySelector('#text p');
    let i = 0,
      timer = 50,  // 修改为适当的时间间隔，以控制打字速度
      str = 'Hello! 如想和我交流，点击头像下的图标可跳转私人匿名提问箱（需魔法），或在下方评论区留言 ↓ ';  
  
    function typing() {
      if (i <= str.length) {
        divTyping.innerHTML = str.slice(0, i++) + '_';
        timer = setTimeout(typing, timer);
      } else {
        divTyping.innerHTML = str; // 结束打字，移除 _ 光标
        clearTimeout(timer);
      }
    }
  
    typing();
  </script>



    









