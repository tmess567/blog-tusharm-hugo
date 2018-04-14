---
title: 'Apache SYNCOPE Eclipse Plugin: Tree View'
author: tusharm
type: post
date: 2016-05-27T10:28:47+00:00
url: /?p=133
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
Now, diving into the plugin development, the first step for the process was to create a tree view as suggested in the issues page of apache syncope. The aim of this view would be to allow the user to view the available mail and report templates so that he/she can interact with it and open it up in the editor. Here are the images of the suggested tree view and the one I built.

[<img class="aligncenter size-full wp-image-142" src="https://i1.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/05/proposedVsCurrent.png?resize=432%2C219" alt="Compare views" srcset="https://i1.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/05/proposedVsCurrent.png?w=432 432w, https://i1.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/05/proposedVsCurrent.png?resize=300%2C152 300w" sizes="(max-width: 432px) 100vw, 432px" data-recalc-dims="1" />][1]

This was pretty straightforward to make since eclipse already provides a wizard to create a plugin with a tree view inbuilt. However, the hard part here was to understand how the view class (which defines what is displayed in the tree view) works. For this project, the view class was named as <a href="https://github.com/tmess567/SYNCOPE-809/blob/master/bundles/org.apache.syncope.ide.eclipse.plugin/src/main/java/org/apache/syncope/ide/eclipse/plugin/views/SyncopeView.java" target="_blank">SyncopeView.java</a> .

> Oh by the way, the project is hosted on GitHub and is available <a href="https://github.com/tmess567/SYNCOPE-809" target="_blank">here</a>.

Let&#8217;s break down the TreeViewer into it&#8217;s components. Here&#8217;s the structure of the SyncopeView class.

[<img class="aligncenter size-full wp-image-135" src="https://i1.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/05/SyncopeViewStructure.png?resize=325%2C423" alt="Syncope View Structure" srcset="https://i1.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/05/SyncopeViewStructure.png?w=325 325w, https://i1.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/05/SyncopeViewStructure.png?resize=230%2C300 230w" sizes="(max-width: 325px) 100vw, 325px" data-recalc-dims="1" />][2]

### Content Provider

The &#8220;content&#8221; of a TreeViewer is specified using domain objects (or simply objects that represent the data you want to display to the user). The content provider allows you to specify how a domain item connects to the user interface provided.

> When working with a tree viewer, you need to provide the viewer with information on how to _transform_ your domain object into an item in the UI tree. That is the purpose of an `ITreeContentProvider`.

Let’s take a look at some of this interface’s methods.

`public Object[] getElements(Object inputElement)`
  
Should return the list of domain objects contained by the root element. Generally extended to call getChildren().

`public Object[] getChildren(Object parent)`
  
Should return the list of domain objects contained by any parent element.

`public Object getParent(Object element)`
  
Should return the parent domain object of the passed domain object.

`public boolean hasChildren(Object element)`
  
Should tell if the domain object is a parent or not.

`public void inputChanged``(Viewer viewer, Object oldInput, Object newInput)`
  
This method is invoked when you set the tree viewer&#8217;s input.

&nbsp;

### Label Provider

Provides the UI elements for the domain objects. For any domain object passed, it returns the image used as an icon for that object and the label used while displaying the object.

> The label provider is responsible for providing an image and text for each item contained in the tree viewer. As with the content provider, the label provider accepts domain objects as its arguments. It is important that instances of label providers are not shared between tree viewers because the label provider will be disposed when the viewer is disposed.

The `ILabelProvider` interface consists of the following abstract methods.

`public Image getImage(Object element)`

Should return an SWT Image which will be used to display passed domain object, element.

> An important point to keep in mind is that the tree viewer will scale your images if they are different sizes. The first image returned from this method will be the &#8220;standard&#8221; tree viewer image size. All other images will be scaled up or down to match the size of this first image.

`public String getText(Object element)`

Should return a string that represents the label for the domain object, element.

`public void dispose()`

The dispose method is called when the tree viewer that contains the label provider is disposed. This method is often used to dispose of the cached images managed by the receiver.

&nbsp;

### ViewerSorter

This class is used to allow the developer to provide a way of sorting the domain objects. This is generally done by using the compareTo() method of the domain objects, but is not required in our current use case.

 [1]: https://i1.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/05/proposedVsCurrent.png
 [2]: https://i1.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/05/SyncopeViewStructure.png
