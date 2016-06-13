# Draft SCSS Code style

Selector naming rule.

- `[BlockName]_[element]`
- `[childName]` - First word must be `element` name. and need to use child selector `>`.
- `-[modifier]`
- `is[state-name]` - State name must be start with `is`. (isActive, isCollapse, isOpen)

Example  - HTML

```html
<div class="UserBlock">
  <div class="UserBlock_fullname">Ratchagarn Naewbuntad</div>
  <div class="UserBlock_avatar">
    <img src="http://placehold.it/128x128" alt="" class="avatarImg" />
  </div>
  <ul class="UserBlock_info">    
    <li class="infoItem">Role: Frontend Engineer</li>
    <li class="infoItem">Age: 26</li>
  </ul>
  <div class="UserBlock_dropdown">
    <a href="#" class="dropdownTrigger js-trigger-dropdown">More</a>
    <ul class="UserBlock_dropdown_menu">
      <li class="menuItem"><a href="/change-password" class="menuLink">Change Password</a></li>
      <li class="menuItem"><a href="/logout" class="menuLink">Logout</a></li>
      <!--
      For about child, You can use Element style instead.
      So, If you use this style your selector don't need child selector.
      <li class="UserBlock_dropdown_menuItem"><a href="/change-password" class="menuLink">Change Password</a></li>
      <li class="UserBlock_dropdown_menuItem"><a href="/logout" class="menuLink">Logout</a></li>
      -->
    </ul>
  </div>
</div>
```


Example  - SCSS

```scss
.UserBlock {
  padding: 20px;
  border: 2px dashed #ccc;
  // ** Optinal/Suggestion ** (Need to commet for help about find in Editor)
  // `UserBlock_fullname`
  &_fullname {
    font-size: 1.2rem;
  }

  // `UserBlock_avatar`
  &_avatar {
    margin-top: 1rem;
    > .avatarImg {
      max-width: 100%;
    }
  }

  // `UserBlock_info`
  &_info {
    margin: 1rem 0 0 0;
    padding: 0;
    > .infoItem {
      padding: 1rem;
      border-bottom: 1px dotted #ccc;
      list-style: none;
    }
  }

  // `UserBlock_dropdown`
  &_dropdown {
    position: relative;
    margin-top: 1rem;
    > .dropdownTrigger {
      $bg-color: #0066CC !default;
      display: inline-block;
      padding: .5rem 1rem;
      background-color: $bg-color;
      color: white;
      text-decoration: none;
      border-radius: 4px;
      transition: background-color .2s;
      &:hover {
        background-color: lighten($bg-color, 10%);
      }
      &.-active {
        background-color: red;
      }
    }
    
    // NOTE: Need to find best solution than this.
    // state class    
    &.is-open {
      .UserBlock_dropdown_menu {
        display: block;
      }
    }
  }

  // `UserBlock_dropdown_menu`
  &_dropdown_menu {
    display: none;
    position: absolute;
    top: 100%;
    left: 0;
    z-index: 1000;
    min-width: 200px;
    margin: 0;
    padding: 0;
    border: 2px solid #ccc;
    background-color: white;
    border-radius: 4px;
    box-shadow: 0 0 5px rgba(0, 0, 0, .2);
    > .menuItem {
      list-style: none;
      > .menuLink {
        display: block;
        padding: .5rem;
        text-decoration: none;
        &:hover {
          background-color: #f6f6f6;
        }
      }
    }
  }
}
```


SCSS - Output (CSS)

```css
.UserBlock {
  padding: 20px;
  border: 2px dashed #ccc;
}
.UserBlock_fullname {
  font-size: 1.2rem;
}
.UserBlock_avatar {
  margin-top: 1rem;
}
.UserBlock_avatar > .avatarImg {
  max-width: 100%;
}
.UserBlock_info {
  margin: 1rem 0 0 0;
  padding: 0;
}
.UserBlock_info > .infoItem {
  padding: 1rem;
  border-bottom: 1px dotted #ccc;
  list-style: none;
}
.UserBlock_dropdown {
  position: relative;
  margin-top: 1rem;
}
.UserBlock_dropdown > .dropdownTrigger {
  display: inline-block;
  padding: .5rem 1rem;
  background-color: #0066CC;
  color: white;
  text-decoration: none;
  border-radius: 4px;
  transition: background-color .2s;
}
.UserBlock_dropdown > .dropdownTrigger:hover {
  background-color: #0080ff;
}
.UserBlock_dropdown > .dropdownTrigger.-active {
  background-color: red;
}
.UserBlock_dropdown.is-open .Userblock_dropdown_menu {
  display: block;
}
.UserBlock_dropdown_menu {
  display: none;
  position: absolute;
  top: 100%;
  left: 0;
  z-index: 1000;
  min-width: 200px;
  margin: 0;
  padding: 0;
  border: 2px solid #ccc;
  background-color: white;
  border-radius: 4px;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
}
.UserBlock_dropdown_menu > .menuItem {
  list-style: none;
}
.UserBlock_dropdown_menu > .menuItem > .menuLink {
  display: block;
  padding: .5rem;
  text-decoration: none;
}
.UserBlock_dropdown_menu > .menuItem > .menuLink:hover {
  background-color: #f6f6f6;
}
```

You can play live preview at [CodePen](http://codepen.io/ratchagarn/pen/gMrgNa)

