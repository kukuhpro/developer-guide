## Frontend Styleguide

This frontend styleguide is compiled from respectable sources such as [Github Styleguide](https://github.com/styleguide), [Google Styleguide](https://code.google.com/p/google-styleguide/), etc.

---

#CSS

Welcome to our styleguide. Before continuing, you might want to get familiar with SCSS first.

##General

- Use soft-tabs with a two space indent. Spaces are the only way to guarantee code renders the same in any person's environment.
- Put spaces after `:` in property declarations.
- Put spaces before `{` in rule declarations.
- Put line breaks between rulesets.
- Place closing braces of declaration blocks on a new line.
- Each declaration should appear on its own line for more accurate error reporting.
- Separate each ruleset by a blank line.
- Whenever possible, avoid over qualifying class names with type selectors. Instead of `a.btn`, type `.btn`.

**Incorrect**

    .foo{
      width:100%; height:100%;
    }
    div.bar{
      font-size:12px;
    }

**Correct**

    .foo {
      width: 100%;
      height: 100%;
    }
    
    .bar {
      font-size: 12px;
    }

##Naming

- You should almost never need to use IDs for styling. Only use class for styling. Broken behavior due to ID collisions or specificity are hard to track down.
- Class names should be in lowercase, with words separated by dashes (this also applies to id names), except in components case (see **Components** for more detail).
- Image file names are lowercase with words separated by a dash, e.g., `icon-home.png` instead of  `iconHome.png`.
- Image file names are prefixed with their usage, e.g., `icon-home.png` or `bg-home.png`.
- As much as possible, write classes as specific as possible to encourage reusability and avoid specificity.
- Use double dashes for major component variation, e.g., `page--about` to differ it from component elements, e.g., `page-heading`.
- Use `.js-` prefixed class names for javascript selector purpose. **It should not, under any circumstances, be styled**.

**Not recommended**
    
    .componentName {
      .heading {
      
      }

      .componentName-content {
        p {
        
        }
      }
    }

**Recommended**
    
    .componentName {
      
    }

    .componentName-heading {
    
    }
    
    .componentName-content {
      p {
      
      }
    }

##Formatting

- Use lowercase and shorthand hex color codes `#fff` unless using `rgba()`.
- Avoid specifying unit for zero, e.g., `margin: 0;` instead of `margin: 0px;` except for `line-height` which should use unitless value, e.g., `line-height: 1.4;`
- Use single quote for property values, e.g., `content: '';`


##SCSS

- Avoid unnecessary nesting. As a rule of thumb, aim for at most three levels.

**Incorrect**  

    .main-container {
      .main-container-content {
        .main-container-content-sidebar {
          .main-container-content-sidebar-header {
            font-size: 19px;
          }
        }
      }
    }

**Correct**  
    
    .main-container {
      position: relative;
      
      .main-container-content {
        position: absolute;
      }
    }

    .main-container-content-sidebar-header {
      font-size: 19px;
    }

- Separate into many SCSS files and include those in `site.scss` or alike.

##Variables

Syntax: `<componentName>-<property>`

- To be discussed.
- Use 


**Example**

    

##Components

Syntax: `<componentName>[--modifierName|-descendantName]` or `<componentName>[-modifierName|-descendantName]`

- Component name must be written in camel case to avoid confusion with descendants or modifiers.
- A component modifier is a class that modifies the presentation of the base component in some form. Modifier names must be written in camel case and be separated from the component name preferably by two hyphens.
- A component descendant is a class that is attached to a descendant node of a component. It's responsible for applying presentation directly to the descendant on behalf of a particular component.
- If modifier and descendant are both necessary, always write modifier first before the descendant **or** use double hyphens for modifier and one hyphen for descendant.

**Not recommended**
    
    .component-name-modifier-name {
    }
    
    .panel-header-primary {
    }

**Recommended**
    
    .componentName-modifierName {
    }
    
    // or...

    .componentName--modifierName {
    }
    
    .panel-primary-header {
    }

    // or...
    
    .panel--primary-header {
    }


##Style Scopes & Namespacing

- Always look to abstract components. Think about writing styles in such a way that they can be reused in other parts of the app. For example, instead of `hompage-nav`, try instead `.nav` or `.nav-bar`. Always ask yourself if this component can be reused in another context.
- Components should belong to their own SCSS files.
- Page level overrides should be minimal and under a single page level class nest.

**Recommended**

    .page--home {
      .nav {
        margin-bottom: 10px;
      }
    }


##Comments

- Comments are strongly encouraged, especially if you are doing something that's still unstable.
- In SCSS files, use `//` instead of `/* */`

**CSS**

    /* Comment about this .foo. */
    .foo {
      width: 87.25%; /* Comment about why the width is such a random number */
    }

**SCSS**

    // Comment about this .foo.
    .foo {
      width: 87.25%; // Comment about why the width is such a random number
    }


#HTML

- Use HTML5 doctype `<!DOCTYPE html>`.
- Omit `type` attributes for style sheets and scripts since it is not necessary anymore in HTML5.

**Not recommended**

    <link rel="stylesheet" href="site.css" type="text/css">
    <script src="site.js" type="text/javascript"></script>

**Recommended**

    <link rel="stylesheet" href="site.css">
    <script src="site.js"></script>




#Workflows

- Write in SCSS, compile with GruntJS
- Optimize images with JPEGMini, imageAlpha and imageOptim