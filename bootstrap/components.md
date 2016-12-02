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
3. Tables `.table` +`.table-striped` +`.table-borderd` +`.table-hover` `.table-condensed`
  - **Responsive Tables** div  `.table-responsive`
4. Images `.img-rounded` `.img-circle` `.img-thumbnail`
  - **Responsive Images** `.img-responsive`
  - **Responsive Embeds** 
    - div 
        - `.embed-responsive` `.embed-responsive-16by9` `.embed-responsive-4by3` 
    - iframe embed video object
        - `.embed-responsive-item`  
5. Jumbotron `超大屏幕 - 巨幕` `.jumbotron`
  - inside container
  - outside container
6. Wells `浅容器` div `.well` +`.well-sm` +`well-lg`
7. Alerts 
  - div 
    - `.alert` +`.alert-success` +`.alert-info` +`.alert-warning` +`.alert-danger`
  - link in alert
    - a `.alert-link`
  - **Closing Alerts**
    - div +`alert-dissmissible` +`fade` +`in`
    - a `.close` `data-dismiss="alert"`
    
      ```html
      <div class="alert alert-success alert-dismissable">
          <a href="#" class="close" data-dismiss="alert">&times;</a>
          <strong>Success!</strong> a successful or positive action.
      </div>
      ```
    
8. Buttons `.btn`
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
   - `.active` `.disabled`
        
9. Button Groups 
  - `.btn-group`
  - `.btn-group-lg`
  - `.btn-group-xs`
  - `.btn-group-vertical`
  - `.btn-gropu-justified`
  - Dropdown Menus 
    - btn `.dropdown-toggle` `data-toggle="dropdown"`
      - span `.caret`
    - ul `.dropdown-menu` `role="menu"`
10. Glyphicons `字体图标` span `.glyphicon .glyphicon-*`
11. Badges/Labels `徽章、标签` `.badeg` `.label-default, .label-primary, .label-success, .label-info, .label-warning .label-danger`
12. Progress Bars `.progress` `.progress-bar` `style="width: 12%;"` 
13. Pagination ul `.pagination` `.active` `.disabled` `.pagination-lg` `.pagination-sm` ul `.breadcrumb`
14. Pager ul `.pager` li `.previous` `.next`
15. List Groups ul/div `.list-group` li/a `.list-group-item .list-group-item-*` `.active` `.disabled`
16. Panels `面板` `.panel` `.panel-*` `.panel-headind` `.panel-body` `.panel-footer` `.panel-group`
17. Dropdowns `下拉菜单` div `.dropdown` li `divider` `dropdown-header`
  - `caret`
18. Collapse `折叠板` `data-toggle="collapse"` `data-target="#demo"` `.collapse` `.in`
  - Accordion `手风琴` `.panel-group` `data-parent="#demo"` `.panel-collapse`
19. Tabs/Pills `list-inline` `nav` `nav-tabs` `nav-pills` `nav-stacked` `nav-justified` 
  - pill `胶囊`
  - Dynamic Tabs `data-toggle="tab"` `.tab-content` `.tab-pane`
  - Dynamic Pills `data-toggle="pill"`
20. Navbar nav `.navbar` `.navbar-default` `.navbar-inverse` `.navbar-fixed-*` `.navbar-header` `.navbar-brand` ul `.nav` `.navbar-nav` `navbar-right`
  - Collapsing Navigation Bar button `.navbar-toggle` `data-toggle="collapse"` `data-target="#navbar"` span `.icon-bar` div `collapse navbar-collapse`
21. Forms `.form-inline` `.form-horizontal` `.form-group` `.form-control` `.control-label` div `checkbox` `radio`
22. Inputs `.checkbox-inline` `radio-inline` `.form-control-static` `help-block`
23. Carousel `旋转木马` `carousel` `slide` `data-ride="carousel"` `carousel-indicators` `data-slide-to="0"` `carousel-inner` `itme` `carousel-caption` `left` `carousel-control` `data-slide="prev"`

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
24. Modal `模态框` button `data-toggle="modal"` `data-target="#modal"` div .`modal` `.fade` `.modal-dialog` `.modal-content` `.modal-header` `.modal-body` `.modal-footer` `.close` `data-dismiss="modal"` `.modal-sm` `.modal-lg`
25. Tooltip `提示工具` `data-toggle="tooltip"` `title=""` `data-placement="top"`

  ```javascript
  <script>
    $(document).ready(function(){
        $('[data-toggle="tooltip"]').tooltip(); 
    });
  </script>
  ```

26. Popover `弹出框` `data-toggle="popover"` `title=""` `data-content=""` `data-placement="top"` `data-trigger="focus"` `data-trigger="hover"`

  ```javascript
  <script>
    $(document).ready(function(){
        $('[data-toggle="popover"]').popover(); 
    });
  </script>
  ```

27. ~~Scrollspy `滚动监听`~~
28. ~~Affix `附加导航`~~