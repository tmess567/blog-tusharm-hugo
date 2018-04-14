---
title: 'Apache SYNCOPE Eclipse Plugin: Update #3'
author: tusharm
type: post
date: 2016-07-21T12:11:08+00:00
url: /?p=174
image: /wp-content/uploads/2016/03/wallhaven-2842171-1200x675.jpg
categories:
  - Apache SYNCOPE (GSOC Project)
tags:
  - apache
  - api
  - eclipse
  - google summer of code
  - gsoc
  - plugin
  - project
  - rest
  - syncope

---
## Editors

The editor displays the content of the mail and report templates, but to display all the available formats of a template, the editor needs to be a multi-page editor. This is done by the TemplateEditor class which extends the MultiPageEditorPart class to allow multiple text editors to be displayed in a single view. The input to these pages is provided by the TemplateEditorInput class which accepts the title, type and content of the template from the SyncopeView class. To provide basic editor capabilities such as syntax highlighting and content assist, specific editor classes are used which will be discussed in a future post.

The templates with HTML format are made available with HTMLEditor while other formats are displayed using StructuredTextEditor available as a part of Structured Source Editing (SSE) UI Component of Eclipse.

### TemplateEditor

&nbsp;

#### init() method

The method accepts an editorInput argument which is then typecasted into TemplateEditorInput which provides the content for the multi-page editors. This content is saved in global variables which are then used by the editors.

#### createPage() and createPages() methods

The createPages() method is called when initializing the display for the multi-page editor. This method in turn passes the fetched editor titles and content to the createPage() method. This method checks if the format for the template is HTML or others and opens the appropriate Editor as a page in the multi-page editor.

#### doSave() method

The execution of this method follows the following list

  1. Get the active editor and the content of that editor
  2. Create a new job to interrupt UI while saving the template content
  3. Determine the format of the current template
  4. Call static methods of the SyncopeView class to send the content to the deployment server
  5. Check if a deleted template is being saved (lost concurrency) close the editor and display error
  6. Call the parent doSave() method to ensure saved status is passed to the editor and reflected in the UI

### TemplateEditorInput

The constructor for this class accepts the following arrays:

  * **inputStringList: **Content of the template
  * **titleList: **Template format names
  * **tooltipList: **Template key names

These arrays are then used by the TemplateEditor to pass them on to the individual editors. Most of the rest of the class is generic methods except for the getStorage() method.

#### getStorage() method

Since the data is being fetched from a String instead of a file, the generic functionality of this method needed to be changed. This method accepts the String of the template content and converts it into a  ByteArrayInputStream which is the standard input for the editors in eclipse.
