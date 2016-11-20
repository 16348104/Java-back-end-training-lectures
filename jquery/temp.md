
11. Cancel the default action (click) of the first URL. 

  ```html
  <div style="background-color:yellow">
      <p>Click the button to change the background color of this paragraph.</p>
      <button>Click me!</button>
  </div>
  ```

12. Return previous values of custom events. 

  ```html
  <body>
  <button>Display event.result</button>
  <p></p>
  </body>
  ```

13. Display the tag's name on click. 

  ```html
  <body>
  <h1>Heading1</h1>
  <h2>Heading2</h2>
  <p>Paragraph</p>
  <button>Button</button>
  <div id="log"></div>
  </body>
  ```
    
14. Count the number of milliseconds between the two click events on a paragraph. 

  ```html
  <body>
  <h1>Heading1</h1>
  <h2>Heading2</h2>
  <p>Paragraph</p>
  <button>Button</button>
  <div id="log"></div>
  </body>
  ```
  
15. Display the event type on clicking all h1 elements. 

  ```html
  <body>
  <h1>This is header1</h1>
  <h1>This is another header1</h1>
  <h2>This is header2</h2>
  <h2>This is header3</h2>
  </body>
  ```    

16. Display the keyboard key which was pressed in a textbox:. 

  ```html
  <body>Input your name: <input type="text">
  <div></div>
  </body>
  ````    

17. Attach a function to the focus event. The focus event occurs (display a message regarding the text field) when the `input` field gets focus. 

  ```html
  <body>
  <p><input type="text"> <span>Input your first name</span></p>
  <p><input type="text"> <span>Input your last name</span></p>
  </body>
  ```

18. Set the focus to the first input box. 

  ```html
  <body>
  <p>First Name: <input type="text" id='field1'></p>
  <p>Last Name: <input type="password" id='field2'></p>
  </body>
  ```    

19. Test if an input has focus? 

  ```html
  <body>
  <div id="content">
      <input tabIndex="1">
      <select tabIndex="3">
          <option>select menu</option>
      </select>
      <p tabIndex="3">
          A Paragraph
  </div>
  </div>
  </body>
  ```

  ```css
  <style>
      .focused {
          background: green;
      }
  </style>
  ```

20. Set background color of an element when the element (or any elements inside it) gets focus or loses focus. 

  ```html
  <body>
  <div>
      First name: <input type="text"><br>
      Last name: <input type="text">
  </div>
  </body>
  ```

  ```css
  <style>
      .focusedin {
          background: green;
      }

      .focusedout {
          background: blue;
      }
  </style>
  ```

21. Display the tag name of the click element. 

  ```html
  <body>
  <p></p>
  <h2>This is a heading 2</h2>
  <div>
      First name: <input type="text"><br>
      Last name: <input type="text">
  </div>
  </body>
  ```

22. Count the number of specific elements. 

  ```html
  <body>
  <ul>
      <li>List - 1</li>
      <li>List - 2</li>
      <li>List - 3</li>
  </ul>
  <button>Display the number of li elements in console</button>
  </body>
  ```

23. Show texts when mouseup and mousedown event triggering. 

24. Display the window width while (or after) it is resized. 

  ```html
  <body>
  <p>Press mouse and release here.</p>
  </body>
  </title>
  </head>
  <body>

  </body>
  </html>
  ```