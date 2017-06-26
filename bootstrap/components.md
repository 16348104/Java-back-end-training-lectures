# Chapter 3 常用组件

1. **Grid Basic** `栅格` `.col-*-`
  - xs (for phones)
  - sm (for tablets)
  - md (for desktops)
  - lg (for larger desktops)
  
  > [What is the difference among col-lg-*, col-md-* and col-sm-* in twitter bootstrap3?](http://stackoverflow.com/a/28654005/3414180)

2. Typography `排版`
  - h1-h6
  - small
  - mark
  - abbr
  - blockquote 
    - `.blockquote-reverse`
  - dl
  - code
  - kbd
  - pre
  - `.text-muted`, `.text-primary`, `.text-success`, `.text-info`, `.text-warning`, `.text-danger`
  - `.bg-primary`, `.bg-success`, `bg-info`, `bg-warning`, `.bg-danger`
3. Tables `.table` + `.table-striped` + `.table-borderd` + `.table-hover` `.table-condensed`
  - **Responsive Tables** div  `.table-responsive`
4. Images `.img-rounded` `.img-circle` `.img-thumbnail`
  - **Responsive Images** `.img-responsive`
  - **Responsive Embeds** 
    - div 
        - `.embed-responsive` + `.embed-responsive-16by9` + `.embed-responsive-4by3` 
    - iframe embed video object
        - `.embed-responsive-item`  
5. Jumbotron `超大屏幕 - 巨幕` `.jumbotron`
  - inside container
  - outside container
6. Wells `浅容器` div `.well` + `.well-sm` + `well-lg`
7. Alerts 
  - div 
    - `.alert`
    - \+ `.alert-success` + `.alert-info` + `.alert-warning` + `.alert-danger`
  - link in alert
    - a `.alert-link`
  - **Closing Alerts**
    - div + `alert-dissmissible` + `fade` + `in`
    - a `.close` `data-dismiss="alert"`
    
      ```html
      <div class="alert alert-success alert-dismissable">
          <a href="#" class="close" data-dismiss="alert">&times;</a>
          <strong>Success!</strong> a successful or positive action.
      </div>
      ```
    
8. Buttons button / input / a `.btn`
  - styles
 
    ```
    .btn-default
    .btn-primary
    .btn-success
    .btn-info
    .btn-warning
    .btn-danger
    .btn-link
    ```
    
  - sizes
 
    ```
    .btn-lg
    .btn-md
    .btn-sm
    .btn-xs
    ```
   - `.btn-block`
   - `.active` 
   - `.disabled`
        
9. Button Groups 
  - `.btn-group`
  - \+ `.btn-group-lg`
  - \+ `.btn-group-md`
  - \+ `.btn-group-sm`
  - \+ `.btn-group-xs`
  - \+ `.btn-group-vertical`
  - \+ `.btn-group-justified`
    - **each** `button` / `input` wrap div with .btn-group class
  - Dropdown Menus 
    - btn `.dropdown-toggle` `data-toggle="dropdown"`
      - span `.caret`
    - ul `.dropdown-menu` `role="menu"`

      ```html
      <div class="btn-group">
        <button class="btn btn-primary">Apple</button>
        <button class="btn btn-primary">Samsung</button>
        <div class="btn-group">
          <button class="btn btn-primary dropdown-toggle" data-toggle="dropdown">
            Sony <span class="caret"></span>
          </button>
          <ul class="dropdown-menu" role="menu">
            <li><a href="#">Tablet</a></li>
            <li><a href="#">Smartphone</a></li>
          </ul>
        </div>
      </div>
      ```
      
10. Glyphicons `[ɡlɪf]` `字体图标`
   - span 
      - `.glyphicon` 
      - \+ `.glyphicon-*`
11. Badges / Labels `徽章` `标签` 
  - badge span 
      - `.badge`
  - label span
      - `.label` 
      - \+ `.label-default, +.label-primary, .label-success, .label-info, .label-warning .label-danger`
12. Progress Bars 
  - outer div `.progress` 
  - inner div `.progress-bar` `style="width: 12%;"` 
      - `.progress-bar-success` `.progress-bar-info` `.progress-bar-warning` `.progress-bar-danger`
      - `.progress-bar-striped` `.active`
13. Pagination 
  - ul 
      - `.pagination` + `.pagination-lg` + `.pagination-sm` 
      - li
          - \+ `.active` + `.disabled`
  - ul 
      - `.breadcrumb`
14. Pager 
  - ul
      - `.pager` 
  - li
      - \+ `.previous` + `.next`
15. List Groups 
  - ul / div 
      - `.list-group` 
  - li / a 
      - `.list-group-item` + `.list-group-item-*` + `.active` + `.disabled`
16. Panels `面板` 
  - 1st div
      - `.panel-group`  
  - 2nd div
      - `.panel` + `.panel-*`
  - 3rd div
      -  \+ `.panel-headind` + `.panel-body` + `.panel-footer` 
17. Dropdowns `下拉菜单` 
  - div
      - `.dropdown` 
  - button
      - `.dropdown-toggle`
      - `data-toggle="dropdown"`
  - span
      - `.caret`
  - ul
      - `.dropdown-menu`
  - li
      - \+ `.divider`
      - \+ `.dropdown-header`

  ```html
  <div class="dropdown">
    <button class="btn btn-primary dropdown-toggle" data-toggle="dropdown">Dropdown Example
    <span class="caret"></span></button>
    <ul class="dropdown-menu">
      <li><a href="#">HTML</a></li>
      <li><a href="#">CSS</a></li>
      <li><a href="#">JavaScript</a></li>
    </ul>
  </div>
  ```

18. Collapse `折叠板` 
  - button 
      - `data-toggle="collapse"` 
      - `data-target="#demo"` or `<a href="#demo" data-toggle...`
  - div 
      - `id="demo"`
      - `.collapse` 
      - `.in`
  - Accordion `手风琴` `.panel-group` `data-parent="#demo"` `.panel-collapse`
  
    ```html
     <div class="panel-group" id="accordion">
      <div class="panel panel-default">
        <div class="panel-heading">
          <h4 class="panel-title">
            <a data-toggle="collapse" data-parent="#accordion" href="#collapse1">
            Collapsible Group 1</a>
          </h4>
        </div>
        <div id="collapse1" class="panel-collapse collapse in">
          <div class="panel-body">Lorem ipsum dolor sit amet, consectetur adipisicing elit,
          sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad
          minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea
          commodo consequat.</div>
        </div>
      </div>
      <div class="panel panel-default">
        <div class="panel-heading">
          <h4 class="panel-title">
            <a data-toggle="collapse" data-parent="#accordion" href="#collapse2">
            Collapsible Group 2</a>
          </h4>
        </div>
        <div id="collapse2" class="panel-collapse collapse">
          <div class="panel-body">Lorem ipsum dolor sit amet, consectetur adipisicing elit,
          sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad
          minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea
          commodo consequat.</div>
        </div>
      </div>
      <div class="panel panel-default">
        <div class="panel-heading">
          <h4 class="panel-title">
            <a data-toggle="collapse" data-parent="#accordion" href="#collapse3">
            Collapsible Group 3</a>
          </h4>
        </div>
        <div id="collapse3" class="panel-collapse collapse">
          <div class="panel-body">Lorem ipsum dolor sit amet, consectetur adipisicing elit,
          sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad
          minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea
          commodo consequat.</div>
        </div>
      </div>
    </div>
    ```
  
19. Tabs `选项卡` / Pills `胶囊` 
  - ul 
    - `.list-inline` 
    - `.nav` + `.nav-tabs` 
    - `.nav` + `.nav-pills` + `.nav-stacked` + `.nav-justified` 
  - Dynamic Tabs 
    - `data-toggle="tab"` `.tab-content` `.tab-pane`
    
    ```html
    <ul class="nav nav-tabs">
      <li class="active"><a data-toggle="tab" href="#home">Home</a></li>
      <li><a data-toggle="tab" href="#menu1">Menu 1</a></li>
      <li><a data-toggle="tab" href="#menu2">Menu 2</a></li>
    </ul>

    <div class="tab-content">
      <div id="home" class="tab-pane fade in active">
        <h3>HOME</h3>
        <p>Some content.</p>
      </div>
      <div id="menu1" class="tab-pane fade">
        <h3>Menu 1</h3>
        <p>Some content in menu 1.</p>
      </div>
      <div id="menu2" class="tab-pane fade">
        <h3>Menu 2</h3>
        <p>Some content in menu 2.</p>
      </div>
    </div>
    ```
    
  - Dynamic Pills `data-toggle="pill"`
  
  ```html
  <ul class="nav nav-pills">
    <li class="active"><a data-toggle="pill" href="#home">Home</a></li>
    <li><a data-toggle="pill" href="#menu1">Menu 1</a></li>
    <li><a data-toggle="pill" href="#menu2">Menu 2</a></li>
  </ul>

  <div class="tab-content">
    <div id="home" class="tab-pane fade in active">
      <h3>HOME</h3>
      <p>Some content.</p>
    </div>
    <div id="menu1" class="tab-pane fade">
      <h3>Menu 1</h3>
      <p>Some content in menu 1.</p>
    </div>
    <div id="menu2" class="tab-pane fade">
      <h3>Menu 2</h3>
      <p>Some content in menu 2.</p>
    </div>
  </div>
  ```
  
20. Navbar nav 
  - nav
      - `.navbar` 
      - \+ `.navbar-default` + `.navbar-inverse` + `.navbar-fixed-*` 
  - div
      - `.container-fluid`
  - div
      - `.navbar-header` 
  - a
      - `.navbar-brand` 
  - ul 
      - `.nav` `.navbar-nav` `navbar-right`
  - navbar with dropdown
    - li `.dropdown`
    - a `.dropdown-toggle` `data-toggle="dropdown"`
    - ul `.dropdown-menu`
  - button `navbar-btn`
  - form
    - `.navbar-form` `.navbar-left`
  - div
    - `.form-group` `.input-group`
  - input
    - `.form-control`
  - button
    ~~`.navbar-btn`~~
    - `input-group-btn`
  - i
    - `.glyphicon` + `.glyphicon-*`
  - Collapsing Navigation Bar 
    - button 
      - `.navbar-toggle` `data-toggle="collapse"` `data-target="#navbar"` 
    - span 
      - `.icon-bar` 
    - div 
      - `.collapse` 
      - `navbar-collapse`
      - `id="navbar"`
      
    ```html
    <nav class="navbar navbar-inverse">
      <div class="container-fluid">
        <div class="navbar-header">
          <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#myNavbar">
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span> 
          </button>
          <a class="navbar-brand" href="#">WebSiteName</a>
        </div>
        <div class="collapse navbar-collapse" id="myNavbar">
          <ul class="nav navbar-nav">
            <li class="active"><a href="#">Home</a></li>
            <li><a href="#">Page 1</a></li>
            <li><a href="#">Page 2</a></li> 
            <li><a href="#">Page 3</a></li> 
          </ul>
          <ul class="nav navbar-nav navbar-right">
            <li><a href="#"><span class="glyphicon glyphicon-user"></span> Sign Up</a></li>
            <li><a href="#"><span class="glyphicon glyphicon-log-in"></span> Login</a></li>
          </ul>
        </div>
      </div>
    </nav>
    ```
    
21. Forms 
  - form
    - `.form-inline` `.form-horizontal` 
  - div
    - `.form-group` `.has-success` `.has-warning` `.has-error`
  - label    
    - `for=""`
    - `.control-label` + `.col-*-`
  - input / textarea / select    
    - `.form-control` 
  - div 
    - `.checkbox` 
    - `.radio`
22. Inputs `.input-sm` `.input-lg`
  - label
    - `.checkbox-inline` 
    - `.radio-inline` 
  - file upload
    
    ```html
    <label class="btn btn-warning">
        <input type="file" style="display:none;">
    </label>
    ```
  
  - p
    - `.form-control-static` `help-block`
  - div
    - `.input-group` `.input-group-btn`
  - sapn
    - `.input-group-addon`
  - i
    - `.glphicon`
    
23. Media Object `媒体对象`
  - div
    - `.media`
    - `.media-left` `media-right`
    - `.media-body`
    - `.media-heading`
    - `.media-top` `.media-middle` `.media-botton`

24. Carousel `旋转木马` 
  - div
    - `id="myCarousel"` `.carousel` `.slide` `data-ride="carousel"` 
  - ol
    - `.carousel-indicators` 
  - li 
    - `data-target="myCarousel"` `data-slide-to="0"` 
  - div
    - `.carousel-inner` 
  - div
    - `.itme` 
  - div 
    - `.carousel-caption` 
  - a
    - `.left` `.carousel-control` `data-slide="prev / next"`
  
  ```html
  <div id="carousel" class="carousel slide" data-ride="carousel">
      <!-- Indicators -->
      <ol class="carousel-indicators">
          <li data-target="#carousel" data-slide-to="0" class="active"></li>
          ...
      </ol>
      <!-- Wrapper for slides -->
      <div class="carousel-inner" role="listbox">
          <div class="item active">
              <img src="img_1.jpg" alt="Chania">
              <div class="carousel-caption">
                  <h3>Chania</h3>
                  <p>The atmosphere in Chania has a touch of Florence and Venice.</p>
              </div>
          </div>
          ...
      </div>
      <!-- Left and right controls -->
      <a class="left carousel-control" href="#carousel" role="button" data-slide="prev">
          <span class="glyphicon glyphicon-chevron-left" aria-hidden="true"></span>
      </a>
      <a class="right carousel-control" href="#carousel" role="button" data-slide="next">
          <span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>
      </a>
  </div>
  ```
  
25. Modal `模态框` 
- button 
  - `data-toggle="modal"` `data-target="#modal"` 
- div 
  - `.modal` + `.fade` 
- div  
  - `.modal-dialog` + `.modal-sm` `.modal-lg`
- div  
  - `.modal-content` 
- div 
  - `.modal-header` `.modal-body` `.modal-footer` 
- botton
  - `.close` `data-dismiss="modal"` 
  
26. Tooltip `提示工具` `data-toggle="tooltip"` `title=""` `data-placement="top"`

  ```javascript
  <script>
    $(document).ready(function(){
        $('[data-toggle="tooltip"]').tooltip(); 
    });
  </script>
  ```

27. Popover `弹出框` `data-toggle="popover"` `title=""` `data-content=""` `data-placement="top"` `data-trigger="focus"` `data-trigger="hover"`

  ```javascript
  <script>
    $(document).ready(function(){
        $('[data-toggle="popover"]').popover(); 
    });
  </script>
  ```

28. ~~Scrollspy `滚动监听`~~
29. ~~Affix `附加导航`~~
