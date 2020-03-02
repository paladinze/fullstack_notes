# Markdown

## what is markdown
- a lightweight markup language to format plain text

## why markdown
- can be used for everything related to formatting plain text
- compatitable with any text editor
  - no vendor lockin (unlike ms word)
  - platform independent (linux, mac, windows)

## markdown processor
- convert markdown to html
- html + css for display or print

## Heading
- syntax
  ```markdown
  # Heading level 1
  ## Heading level 2
  ### Heading level 3
  #### Heading level 4
  ##### Heading level 5
  ###### Heading level 6
  ```
- best practice
  - seperate heading with content with blank line

## paragraph
- use blank line to seperate text
  ```markdown
  I really like using Markdown.

  I think I'll use it to format all of my documents from now on.
  ```

## line breaks
- end a line with two or more spaces, then return
  ```markdown
  Line 1  
  Line 2
  ```
- note: many markdown flavors don't require line breaks

## bold
- use ** to surround text
```markdown
**lovely potato**
Line 2
```

## italic
- use * without whitespace
```markdown
*lovely potato*
Line 2
```

## bold + italic
- use ***

## blockquotes
- use > before paragraph
```markdown
> Hello my friend
```

## unordered list
- add dashes (-), asterisks (*), or plus signs (+) in front of line items
  ```markdown
  + First item
  * Second item
  - Third item
  + Fourth item
  ```
- to nest element under a list item, just use indent
  ```markdown
  * line1
  * line2
    some more stuff
  ```

## ordered list
- add line items with numbers followed by periods
- numbering doesn't matter :)
  ```markdown
  3. line1
  2. line2
  1. some more stuff
  ```

## code blocks
- normally indented one tab
- when in list, indent them two tabs

## highlight code in sentence
```markdown
Hello my `friend`
```
Hello my `friend`

## horizontal Rules
```markdown
***
```
***

## links
- simple link
  ```markdown
  I like [Douban](https://www.douban.com/)
  ```
  I like [Douban](https://www.douban.com/)
- simple link with title (tooltip when hover over the link)
  ```markdown
  I like [Douban](https://www.douban.com/ "best place for movie reviews")
  ```
  I like [Douban](https://www.douban.com/ "best place for movie reviews")
- url as link
  ```markdown
  <https://www.douban.com>
  ```
  <https://www.douban.com>

## images
```markdown
![This is a pretty image](./nadia.jpg)
```
![This is a crazy image](./nadia.jpg)

## table
```markdown
col1 | col2 | col3
-----|-----|------
content1 | content2| content3
content4 | content5| content6
```
col1 | col2 | col3
-----|-----|------
content1 | content2| content3
content4 | content5| content6