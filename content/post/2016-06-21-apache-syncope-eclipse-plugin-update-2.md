---
title: 'Apache SYNCOPE Eclipse Plugin: Update #2'
author: tusharm
type: post
date: 2016-06-21T10:00:49+00:00
url: /?p=169
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
The tree viewer was almost complete by the last post. The only thing required to be added was a reset button for re-fetching the keys to allow the user to refresh the list. Simple enough, I added the same functionality used after login. I wanted to list a few things that might be worth mentioning to anyone looking at the <a href="https://github.com/tmess567/SYNCOPE-809/blob/master/bundles/org.apache.syncope.ide.eclipse.plugin/src/main/java/org/apache/syncope/ide/eclipse/plugin/views/SyncopeView.java" target="_blank">SyncopeView.java</a> file.

## Details about SyncopeView.java

  1. There is an invisible root to ensure that the tree view consists of 2 visible roots, namely Mail Templates and Report Templates.
  2. If you are &#8220;Reading the code&#8221; the main part starts at the **initialize** method. It does the following: 
      * Check username and password for **null or empty** values.
      * Create the **visible roots**, Mail Templates and Report Templates.
      * Generate a **SyncopeClient** instance from the provided username, password and deployment url
      * Fetch **lists of keys** for both Mail and Report Templates from the above instance
      * Generate a **TreeObject** for each of these instances and populate them in the visible roots
  3. User interactions are handled within the createPartControl() method. 
      * **makeActions()** creates the anonymous classes for each action to be done on user interaction.
      * **hookContextMenu()** populates and assigns actions to the context menu (right click menu for TreeObjects).
      * **hookDoubleClickAction()** as the name suggests, assigns actions to double click events on TreeObjects.
      * **contributeToActionBars()** populates and assigns actions to the action bar
  4. Make Actions makes the following action anonymous classes 
      * **loginAction**: Open Login dialog and update TreeViewer once the user clicks OK
      * **refreshAction**: Update the TreeViewer. This action is disabled by default and enabled only when TreeViewer is already populated.
      * **doubleClickAction**: Calls openTemplateInEditor on the currently selected TreeObject.
      * **readAction**: Same as above. Only available to context menu.
      * **addAction**: Opens up a dialog for the key name and once entered, creates a new TemplateTO object and refreshes the TreeViewer
      * **removeAction**: Deletes the currently selected TreeObject from the deployments and refreshes the TreeViewer.
  5. To open template content in an editor, the openTemplateInEditor() method is called. It does the following: 
      * There are separate code blocks for Mail and Report templates because of 2 reasons: 
          * TemplateService for the 2 templates are named differently, MailTemplateService and ReportTemplateService
          * The formats used by MailTemplates and ReportTemplates are both different in name and number.
      * Each of the above code blocks, opens up a dialog to block UI while fetching template content from the deployment url.
      * The content of the template for any particular format is fetched by the **getStringFromTemplate()** method which opens an InputStream to read the template format content
      * Upon opening the editor with TemplateEditorInput, 3 arrays are passed to it 
          1. **templateData**: content of each of the formats supported by the template
          2. **editorTitles**: The format names of the template such as TEMPLATE\_FORMAT\_HTML
          3. **editorToolTips**: The name of the current TreeObject
  6. To restrict the available of SyncopeClient instance to just this class, it contains the **setMailTemplateContent and setReportTemplateContent public static methods** which allow the editor classes to set content for any template format without having to deal with SyncopeClient instance generation (since it requires values such as username which would not be directly available to them).

## Why did I use

  * **display.syncExec** : Any changes to the UI in eclipse must be made on the UI thread
  * **Jobs** : The UI must be blocked while performing background tasks to ensure that the user is aware of the task.
  * **Public Template Format names** : (such as TEMPLATE\_FORMAT\_HTML) They will be used by <a href="https://github.com/tmess567/SYNCOPE-809/blob/master/bundles/org.apache.syncope.ide.eclipse.plugin/src/main/java/org/apache/syncope/ide/eclipse/plugin/editors/TemplateEditor.java" target="_blank">TemplateEditor.java</a> to find out which editor to open up for the content.
