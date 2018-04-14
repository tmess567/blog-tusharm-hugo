---
title: 'Apache SYNCOPE Eclipse Plugin: Update #4'
author: tusharm
type: post
date: 2016-08-12T12:49:51+00:00
url: /?p=191
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
## HTML Editor

### Resource Bundle

The HTML editor requires some properties which should be both available for the functionality of the editor and should be readily available for editing. This resource bundle is available at &#8220;syncope/ide/eclipse/bundles/org.apache.syncope.ide.eclipse.plugin/src/main/resources/HTMLEditor.properties&#8221; .

**Note: **While writing tests for the plugin using swtbot, the editors were unable to initialize because for some reason the HTMLEditor was unable to access the resource bundle while automated testing, whereas while manually working with the plugin, the editors work perfectly fine. This is still an issue.

#### createActions() method

This method creates a context menu entry (entry for the menu displayed on right click) and binds it to the AutoIndentAction class available in the htmlhelpers package

#### Source Configuration

This provides the syntax highlighting, auto indentation and other features available for the HTMLEditor and is defined by teh HTMLSourceConfiguration class which is described below.

## HTMLSourceConfiguration

This class provides the rules and the conditions which need to be followed by the HTMLEditor to provide functionality required in a modern editor. Following are the roles of this class file:

  * Define content types and the rules that define which part of the template text is in which format. These content types include: 
      * DEFAULT CONTENT TYPE (Simple Text)
      * HTML COMMENT
      * HTML TAG
      * PREFIX TAG
      * HTML SCRIPT
      * HTML DOCTYPE
      * HTML DIRECTIVE
      * JAVASCRIPT
      * CSS
      * SYNCOPE TAG
  * **getPresentationReconciler(): ** 
      * Binds the conditions (along with the color for syntax highlighting) for content recognition to the editor content with the use of damagers and repairers.
      * These conditions are provided in the form of scanners with the help of various classes available in htmlhelpers
  * **getAutoEditStrategy():** 
      * Allows the editor to define the indentation and auto-completion rules for the inputted text

Most of the role of this class is just to bind the editor to class files available in the htmlhelpers package which do most of the heavy lifting.
