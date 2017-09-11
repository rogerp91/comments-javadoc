<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML//EN">
<html>
<head>
    <title>How to Write Doc Comments for Javadoc</title>
</head>

<BODY BGCOLOR="#FFFFFF" TEXT="#000000" LINK="#0000FF" VLINK="#000077" ALINK="#FF0000">

<TABLE BORDER="0" WIDTH="100%">
<TR>
<TD WIDTH="60">
   <IMG SRC="/images/logos/javalogo52x88.gif" ALT="Java" BORDER=0 WIDTH=52 HEIGHT=88>
</TD>

<TD>
<center>
                   <h1>How to Write<br>
                Doc Comments for Javadoc</h1>
                 <b>(under construction)</b>
                             <p>
<font size="-1">Maintained by <a href="mailto:doug.kramer@sun.com">doug.kramer@sun.com</a></font>
</center>
</TD>

<TD ALIGN=RIGHT VALIGN=TOP>
   <font size="-1"><a href="index.html">Javadoc<br> Home Page</a></font>
</TD>
</TR>
</TABLE>

<!-- Body text begins here -->
<h3>Contents</h3>
<ul>
<li><a href="#formatting">Formatting and Content Conventions</a>
<li><a href="#descriptionstags">Descriptions, Tags and a Blank Line</a>
<li><a href="#descriptions">Descriptions</a>
<li><a href="#tag">Tag Conventions</a>
<li><a href="#images">Including Images</a>
<li><a href="#examples">Examples of Doc Comments</a>
<li><a href="#curly">Troubleshooting Curly Quotes (Microsoft Word)</a>
</ul>

<p>


<a name="formatting"></a>
<h3>Formatting and Content Conventions</h3>
<blockquote>

This document describes the formatting and content conventions 
we use in doc comments at JavaSoft.
<p>

<h4>Terminology</h4>
<blockquote>
<dl>
<dt><b>API documentation</b> (API docs) or <b>API specifications</b> (API specs)
<dd>On-line or hardcopy descriptions of the API, 
    intended primarily for programmers writing in Java. Thes can be 
    generated using the javadoc tool or created some other way.  
    Examples would be the on-line 
    <a href="/products/jdk/1.1/docs/api/packages.html">JDK API docs</a> and the Chan/Lee <em>Java Class Libraries</em> book.

<dt><b>Documentation comments</b> (doc comments)
   <dd>The special comments in the Java source code that are delimited by 
       the /** ... */ tags. These comments are processed by the Javadoc tool 
       to generate the API Docs.

<dt><b>javadoc</b>
   <dd>The JDK tool that generates API documentation from documentation comments.
</dl>
</blockquote>

<h4>Who "Owns" the Doc Comments</h4>
In general, the doc comments are not owned exclusively by writers
or programmers, but their ownership is shared between them.
It is a basic premise that writers and programmers honor each other's
capabilities and both contribute to the best doc comments possible.
<p>

It is very much common practice for a programmer to write the
initial doc comments, using sparse language, omitting many of 
the tags, and for the writer to go back and refine the content,
adding tags.
<p>

With that in mind, these guidelines are intended to describe the
end-product.  They are intended only as <em>suggestions</em> 
for programmers, not requirements.  Any of these guidelines that 
programmers happen to follow would be great, but it is not 
intended that they should in any way to add to programmer's burden.
(This note shall henceforth be known as "Kramer's Caveat". In other 
words, don't push this spec on developers! :) 

<!--
<h4>Principle of Harmony Note</h4>

We decided that as much as possible it was a good idea to 
identify conventions we could live with that agreed with what
programmers were already doing. That minimizes the number
of changes.
-->

</blockquote>

<a name="descriptionstags"></a>
<h3>Descriptions, Tags, and Blank Lines</h3> 
<blockquote>

A doc comment is made up of two parts -- a description followed 
by zero or more tags, with a blank line (containing a single asterisk "*")
between these two sections:
<pre>
    /** 
     * This is the description part of a doc comment
     *
     * @tag    Comment for the tag
     */
</pre>
<ul>
   <li>The first line is indented to line up with the code below the comment,
       and starts with the begin-comment symbol (<code>/**</code>)
       followed by a return.
   <p>
   <li>Subsequent lines start with an asterisk <code>*</code>. They are indented 
       an additional space so the asterisks line up. A space separates the
       asterisk from the descriptive text or tag that follows it.
   <p>
   <li>Insert a blank comment line between the description and the list of tags,
       as shown.
   <p>
   <li>Insert additional blank lines to create "blocks" of related tags (discussed
       in greater detail below).
   <p>
   <li>The last line begins with the end-comment symbol (<code>*/</code>) 
       indented so the asterisks line up and followed by a return. Note that the 
       end-comment symbol contains only a single asterisk (<code>*</code>).
</ul>

<p>
Break any doc-comment lines exceeding 80 characters in length, if possible. 
If you have more than one paragraph in the doc comment, separate the paragraphs
with a <code>&lt;p&gt;</code> paragraph tag.


Also see <a href="#curly">Troubleshooting Curly Quotes (Microsoft Word)</a> 
at the end of this document.
</blockquote>

<a name="descriptions"></a>
<h3>Descriptions</h3>
<blockquote>

<b>First Sentence</b><br>
The first sentence of each doc comment should be a summary
sentence, containing a concise but complete description of the
API. This sentence ends at the first period that is
followed by a blank, tab, or line terminator, or at the first tag (as
defined below).  For example, this first sentence ends at "Prof.":
<pre>
   /**
    * This is a simulation of Prof. Knuth's MIX computer.
    */
</pre>
However, you can work around this by typing an HTML meta-character such 
as "&amp;" or "&lt;" immediately after the period, such as:
<pre>
   /**
    * This is a simulation of Prof.&amp;nbsp;Knuth's MIX computer.
    */
</pre>
or
<pre>
   /**
    * This is a simulation of Prof.&lt;!-- --&gt; Knuth's MIX computer.
    */
</pre>


<p>
Javadoc copies this first sentence to the member summary at the top of the web 
page, so it is important to write crisp and informative initial sentences.  
In particular, write summary sentences that distinguish overloaded methods 
from each other. For example:
<pre>
   /** 
    * Class constructor.
    */
   foo() {
     ...
    
   /**
    * Class constructor specifying number of objects to create.
    */
   foo(int n) {
     ...
</pre>
<p>

<b>Use of &lt;code&gt; Style</b><br>
Keywords and API names are offset by &lt;code&gt;...&lt;/code&gt; when 
mentioned in a description.  This includes:
<ul>
    <li>Java keywords
    <li>package names
    <li>class names
    <li>method names
    <li>interface names
    <li>variable names
    <li>argument names
    <li>code examples
</ul>
  
<p>
<b>Use of Parentheses for Method and Constructor Names</b><br>
Method and constructor names specified in a description are offset 
by &lt;code&gt;...&lt;/code&gt;.   Parentheses are not used except
to denote a particular signature.
<p>
 
So we generally say &lt;code&gt;getLabel&lt;/code&gt; and not "getLabel()".
We only use &lt;code&gt;getLabel()&lt;/code&gt; if we are talking
specifically about the zero-argument method or constructor.
<p>

  
<a name="formatting"></a>
<b>Writing Documentation Comments: A Style Guide</b><br>
<ul>
<li><b>Okay to use phrases instead of complete sentences, in the 
  interests of brevity.</b> This holds especially in the initial 
  summary and in @param tag descriptions.
<p>


<li><b>Use 3rd person (descriptive) not 2nd person (prescriptive).</b><br>
  The description is in 3rd person declarative rather than 2nd person 
  imperative.

<table>
<tr>
<td>
  &nbsp; &nbsp; &nbsp; Gets the label.
</td>
<td>
  &nbsp; &nbsp; &nbsp; (preferred)
</td>
</tr>

<tr>
<td>
  &nbsp; &nbsp; &nbsp; Get the label. 
</td>
<td>
  &nbsp; &nbsp; &nbsp; (avoid)
</td>
</tr>
</table>

<p>

<li><b>Method descriptions begin with a verb phrase.</b><br>
  A method implements an operation, so it usually starts with a verb phrase:

<table>
<tr>
<td>
  &nbsp; &nbsp; &nbsp; Gets the label of this button.
</td>
<td>
  &nbsp; &nbsp; &nbsp; (preferred)
</td>
</tr>

<tr>
<td>
  &nbsp; &nbsp; &nbsp; This method gets the label of this button. 
</td>
<td>
  &nbsp; &nbsp; &nbsp; (avoid)
</td>
</tr>
</table>

<p>

<li><b>Class/interface/field descriptions can omit the subject and simply 
  state the object.</b> These API often describe things rather than 
  actions or behaviors:

<table>
<tr>
<td>
  &nbsp; &nbsp; &nbsp; A button label.
</td>
<td>
  &nbsp; &nbsp; &nbsp; (preferred)
</td>
</tr>

<tr>
<td>
  &nbsp; &nbsp; &nbsp; This field is a button label. 
</td>
<td>
  &nbsp; &nbsp; &nbsp; (avoid)
</td>
</tr>
</table>

<p>

<li><b>Use "this" instead of "the" when referring to an
  object created from the current class.</b> For example, the description
  of the <code>getToolkit</code> method should read as follows:

<table>
<tr>
<td>
  &nbsp; &nbsp; &nbsp; Gets the toolkit for <b>this</b> component.
</td>
<td>
  &nbsp; &nbsp; &nbsp; (preferred)
</td>
</tr>

<tr>
<td>
  &nbsp; &nbsp; &nbsp; Gets the toolkit for the component. 
</td>
<td>
  &nbsp; &nbsp; &nbsp; (avoid)
</td>
</tr>
</table>

<p>

<li><b>Add description beyond the API name.</b>  The best API names 
  are "self-documenting", meaning they tell you basically what the 
  API does.  If the doc comment merely repeats the API name in
  sentence form, it is not providing more information.  For 
  example, if  method description uses only the words that appear 
  in the method name, then it is adding nothing at all to what 
  you could infer.  The ideal comment goes beyond those words 
  and should always reward you with some bit of 
  information that was not immediately obvious from the API name. 
<p>

<b>Avoid</b> - The description below says nothing beyond what you know from 
reading the method name. The words "set", "tool", "tip", and "text" 
are simply repeated in a sentence. 
<pre>
    /**
     * Sets the tool tip text.
     *
     * @param text  The text of the tool tip.
     */
    public void setToolTipText(String text) {
</pre>
<b>Preferred</b> - This description more completely defines what a 
tool tip is, in the larger context of registering and being displayed
in response to the cursor. 
<pre>
    /**
     * Registers the text to display in a tool tip.   The text 
     * displays when the cursor lingers over the component.
     *
     * @param text  The string to display.  If the text is null, 
     *              the tool tip is turned off for this component.
     */
    public void setToolTipText(String text) {
</pre>
<p>

<li><b>Be clear when using the term "field".</b>
Be aware that the word "field" has two meanings:
<ul>
<li>static field, which is another term for "class variable"
<li>text field, as in the TextField class.  Note that this
kind of field might be restricted to holding dates, numbers
or any text.  Alternate names might be "date field" or "number field",
as appropriate.
</ul>
<p>

<li><b>Avoid Latin</b> -- spell out "aka" (also known as), use "that is" 
  instead of "i.e.", use "for example" instead of "e.g", and use "to be 
  specific" or "in other words" instead of "viz."
</ul>

</blockquote>

<a name="tag"></a>
<h3>Tag Conventions</h3>
<blockquote>

<p>Most of the following tags are specified in the  
<a href="/docs/books/jls/html/18.doc.html#25995">Java Language Specification</a>.  Also see the <a href="/products/jdk/1.1/docs/tooldocs/solaris/javadoc.html#tags">javadoc reference page</a>. 

<p>
<b>Order of Tags</b><br>
Include tags in the following order:<br>
<blockquote>
<pre>
<code>* @author       </code>(classes and interfaces only, required)
<code>* @version      </code>(classes and interfaces only, required) (see <a href="#footnote1">footnote 1</a>)
<code>*               </code>
<code>* @param        </code>(methods only)
<code>* @return       </code>(methods only - will eventually become @returns)
<code>* @exception    </code>(will eventually become @throws)
<code>*               </code>
<code>* @see          </code>
<code>* @since        </code>
<code>* @deprecated   </code>(see <a href="/products/jdk/1.1/docs/guide/misc/deprecation/deprecation.html">How and When To Deprecate APIs</a>)
</pre>
</blockquote>

<p>
<b>Tag Blocks</b><br>
For readability, divide the tags into blocks of related tags.
The blocks shown above are an example.

<p>   
<b>Ordering Multiple Tags</b><br>
Multiple @author tags should be listed in chronological order. The creator of the 
class should be listed at the top.

Multiple @param tags should be listed in argument-declaration order.
<p>
Multiple @exception tags should be listed alphabetically by the 
arguments (exception names). Multiple @exception tags can be divided
divided into a separate block. A single @exception tag can be "tacked on"
to the @param / @return block.
<p>
Similarly, multiple @see tags should be ordered alphabetically and organized
into a separate block. A single @see tag can be "tacked on" to the tags below
it.
<p>

<b>Required Tags</b><br>
An @param tag is required for every parameter, even when the description is
obvious. The @return tag is required for every method that returns something 
other than void, even if it is redundant with the method description. (Whenever
possible, find something non-redundant (ideally, more specific) to use for the
tag comment.)
<p>

These principles expedite automated searches and automated processing. Frequently, 
too, the effort to avoid redundancy pays off in extra clarity.
<p>

<b>Tag Comments</b><br>
Use the following guidelines to create comments for each tag:
<blockquote>
<dl>
<dt><b>@author</b>
<dd>If the author is unknown, use "unascribed" as the argument to
@author. 
<p>

<dt><b>@version</b>
<dd>The JavaSoft convention for the argument to the @version tag is the
SCCS string "%I%, %G%", which converts to something like "<code>1.39, 02/28/97</code>"
when the file is checked out of SCCS.
<p>

<dt><b>@param</b>
<dd>The @param tag is followed by the name (not type) of the parameter, 
followed by a description of the parameter. The first non-trivial word
in the description is the data type of the parameter. (Trivial words
are articles like "a", "an", and "the".) Additional
spaces can be inserted between the name and description so that comments
line up in a block. Dashes or other punctuation should not be inserted 
before the description. (JavaDoc provides hyphens automatically).
<p>  

The name and data type always start with a lowercase letter. 
The description is most usually a phrase, starting with a lowercase
letter and ending without a period, unless it contains a complete sentence.
<p>

Example:<pre>
  * @param ch        the character to be tested
  * @param observer  the object to be notified 
</pre>
Do not bracket the name of the parameter after the @param tag with 
&lt;code&gt;...&lt;code&gt;. (The Javadoc tool may do that 
automatically at some point.)
<p>

When writing the comments themselves:
<ul>
<li>Prefer a phrase to a sentence.
<p>     
<li>Giving a phrase, do not capitalize, do not end with a period.<br>
  <code>&nbsp; @param x a phrase goes here
  </code>
<p>     
<li>Giving a sentence, capitalize it and end it with a period.<br>
  <code>&nbsp; @param x This is a sentence.
  </code>
<p>     
<li>Givng multiple sentences, follow all sentence rules.<br>
  <code>&nbsp; @param x This is sentence #1. This is sentence #2.
  </code>
<p>     
<li>Giving multuple phrases, separate with a semi-colon and a space.<br>
  <code>&nbsp; @param x phrase #1 here; phrase #2 here
  </code>
<p>     
<li>Giving a phrase followed by a sentence, do not capitalize the
  phrase. However, end it with a period to distinguish the start
  of the next sentence.<br>
  <code>&nbsp; @param x a phrase goes here. This is a sentence.
  </code>
</ul>
<p>

<dt><b>@return</b>
<dd>Omit @return for methods that return void; include it 
for all other methods and constructors, even if its content
is entirely redundant with the method description.  Having an explicit
@return tag makes it easier for someone to find the return value quickly.  
Whenever possible, supply more detailed information (such as returning -1 
when an out-of-bounds argument is supplied).
<p>

<dt><b>@deprecated</b>
<dd>The @deprecated description should tell the user how to avoid using the class
or method and explain why it has been deprecated. An @see tag should be included
that points to the replacement method. The standard format is, for example: 
<pre>
  /**
   * @deprecated  Replaced by setBounds
   * @see #setBounds(int,int,int,int)
   */
</pre>
If the member is obsolete and there is no replacement, the argument to @deprecated
should be "No replacement".
<p>

Incorrectly specified @deprecated tags should be fixed wherever they are found,
because Javadoc parses the entire paragraph following the @deprecated tag and 
moves it to the front of the description, placing it in italics and preceding it 
with a bold warning: "Note: foo is deprecated". (It also adds "Deprecated" in bold 
to any index entries mentioning the deprecated entity.)

<p>
Do not add @deprecated tags without first checking with the appropriate 
engineer. Substantive modifications should likewise be checked first. 
<p>

<dt><b>@exception</b>
<dd>An @exception tag should be included for at least any declared (checked) 
exceptions, as illustrated below.  It can also document any non-declared 
exceptions that can be thrown by the method, normally those that appear 
directly in the implementation, rather than those that are indirectly
thrown.  
 
<pre>
  /**
   * @exception IOException  If an IO error occurred
   */
  public void f() throws IOException {
      // body
  }
</pre>

</dl>
</blockquote>
</blockquote>

<a name="images"></a>
<h3>Including Images</h3>
<blockquote>

This section covers images used in the doc comments, not images directly used
by the source code.
<p>

NOTE: The bullet and heading images required with Javadoc version 1.0 and 1.1
are located in the images directory of the JDK download bundle: jdk1.2/docs/api/images/
<p>

Javadoc is not yet smart enough to copy over images (GIF, JPEG, etc)
to the destination directory.  You must copy them manually
until we add that feature in Javaodoc 1.2.
<p>

The following are the JavaSoft proposals for conventions for including images
in doc comments;  Javadoc does not yet support any of these.  The master images
would be located in the source tree; when javadoc is run with the standard
doclet, it would copy those files to the destination HTML directory. 
Please send comments to javadoc@sun.com

<h4>Images in Source Tree</h4>

<ul>
<li><b>Naming of doc images in source tree</b> - Name GIF images "&lt;class&gt;-1.gif", 
incrementing the integer for subsequent images in the same class.  
Example:  <code>Button-1.gif</code>
<p>

<li><b>Location of doc images in source tree</b> - Put doc images in a 
directory called "doc-files".  This directory should reside in the same package 
directory where the source files reside.  The name "doc-files" distinguishes 
it as documentation separate from images used by the source code itself, such as 
bitmaps displayed in the GUI.
Example:  A screen shot of a button, <code>Button-1.gif</code>, might be included 
in the class comment for the Button class.  The Button source file and the image
would be located at:<br>
<table>
<tr>
 <td>
   <code>java/awt/Button.java</code> 
 </td>
 <td>
   (source file)
 </td>
</tr>
<tr>
 <td>
   <code>java/awt/doc-files/Button-1.gif</code> 
 </td>
 <td>
   (image file)
 </td>
</tr>
</table>
<p>
</ul>

<h4>Images in HTML Destination</h4>

<ul>
<li><b>Naming of doc images in HTML destination</b> - Images would have the
same name as they have in the source tree.  
Example:  <code>Button-1.gif</code>
<p>

<li><b>Location of doc images in HTML destination</b> - 
  <ul>
   <li>With flat file output, directories would be located in the package 
       directory and named "images-&lt;package&gt;".
       For example:
<pre>  api/images-java.awt/
  api/images-java.awt.swing/
</pre>
   <li>With hierarchical file output, directories would be located in 
       the package directory named "doc-files".
       For example:
<pre>  api/java/awt/doc-files/Button-1.gif
</pre>
  </ul>
</ul>

<p>

</blockquote>

<a name="examples"></a>
<h3>Examples of Doc Comments</h3>
<blockquote>

<pre>
/**
 * Graphics is the abstract base class for all graphics contexts
 * which allow an application to draw onto components realized on
 * various devices or onto off-screen images.
 * A Graphics object encapsulates the state information needed
 * for the various rendering operations that Java supports.  This
 * state information includes:
 * &lt;ul&gt;
 * &lt;li&gt;The Component to draw on
 * &lt;li&gt;A translation origin for rendering and clipping coordinates
 * &lt;li&gt;The current clip
 * &lt;li&gt;The current color
 * &lt;li&gt;The current font
 * &lt;li&gt;The current logical pixel operation function (XOR or Paint)
 * &lt;li&gt;The current XOR alternation color
 *     (see &lt;a href="#setXORMode"&gt;setXORMode&lt;/a&gt;)
 * &lt;/ul&gt;
 * &lt;p&gt;
 * Coordinates are infinitely thin and lie between the pixels of the
 * output device.
 * Operations which draw the outline of a figure operate by traversing
 * along the infinitely thin path with a pixel-sized pen that hangs
 * down and to the right of the anchor point on the path.
 * Operations which fill a figure operate by filling the interior
 * of the infinitely thin path.
 * Operations which render horizontal text render the ascending
 * portion of the characters entirely above the baseline coordinate.
 * &lt;p&gt;
 * Some important points to consider are that drawing a figure that
 * covers a given rectangle will occupy one extra row of pixels on
 * the right and bottom edges compared to filling a figure that is
 * bounded by that same rectangle.
 * Also, drawing a horizontal line along the same y coordinate as
 * the baseline of a line of text will draw the line entirely below
 * the text except for any descenders.
 * Both of these properties are due to the pen hanging down and to
 * the right from the path that it traverses.
 * &lt;p&gt;
 * All coordinates which appear as arguments to the methods of this
 * Graphics object are considered relative to the translation origin
 * of this Graphics object prior to the invocation of the method.
 * All rendering operations modify only pixels which lie within the
 * area bounded by both the current clip of the graphics context
 * and the extents of the Component used to create the Graphics object.
 * 
 * @version 	%I%, %G%
 * @author 	Sami Shaio
 * @author 	Arthur van Hoff
 * @since       JDK1.0
 */
public abstract class Graphics {

    /** 
     * Draws as much of the specified image as is currently available at
     * the specified coordinate (x, y).
     * This method will return immediately in all cases, even if the
     * entire image has not yet been scaled, dithered and converted
     * for the current output device.
     * If the current output representation is not yet complete then
     * the method will return false and the indicated ImageObserver
     * object will be notified as the conversion process progresses.
     *
     * @param img       the image to be drawn
     * @param x         the x coordinate
     * @param y         the y coordinate
     * @param observer  the object to be notified as more of the image is
     *                  converted
     * @return          &lt;code&gt;true&lt;/code&gt; if the image is completely 
     *                  loaded and was painted successfully; 
     *                  &lt;code&gt;false&lt;/code&gt; otherwise.
     * @see             Image
     * @see             ImageObserver
     * @since           JDK1.0
     */
    public abstract boolean drawImage(Image img, int x, int y, 
				      ImageObserver observer);


    /**
     * Dispose of the system resources used by this graphics context.
     * The Graphics context cannot be used after being disposed of.
     * While the finalization process of the garbage collector will
     * also dispose of the same system resources, due to the number
     * of Graphics objects that can be created in short time frames
     * it is preferable to manually free the associated resources
     * using this method rather than to rely on a finalization
     * process which may not happen for a long period of time.
     * &lt;p&gt;
     * Graphics objects which are provided as arguments to the paint
     * and update methods of Components are automatically disposed
     * by the system when those methods return.  Programmers should,
     * for efficiency, call the dispose method when finished using
     * a Graphics object only if it was created directly from a
     * Component or another Graphics object.
     *
     * @see       #finalize
     * @see       Component#paint
     * @see       Component#update
     * @see       Component#getGraphics
     * @see       #create
     * @since     JDK1.0
     */
    public abstract void dispose();

    /**
     * Disposes of this graphics context once it is no longer referenced.
     * @see       #dispose
     * @since     JDK1.0
     */
    public void finalize() {
	dispose();
    }
}
</pre>
</blockquote>

<a name="curly"></a>
<h3>Troubleshooting Curly Quotes (Microsoft Word)</h3>
<blockquote>

<b>Problem</b> - A problem occurs if you are working in an editor that defaults to curly 
(rather than straight) single and double quotes, such as Microsoft Word on a PC --
the quotes disappear when displayed in some browers (such as Unix Netscape).
So a phrase like "the display's characteristics" becomes "the displays characteristics."
<p>
The illegal characters are the following:
<ul>
  <li>146 - right single quote
  <li>147 - left double quote
  <li>148 - right double quote
</ul>
<p>
What should be used instead is:
<ul>
   <li>39 - straight single quote
   <li>34 - straight quote
</ul>
<p>
<b>Preventive Solution</b> - The reason the "illegal" quotes occurred was 
that a default Word option is "Change 'Straight Quotes' to 'Smart Quotes'". 
If you turn this off, you get the appropriate straight quotes when you type. 
<p>
<b>Fixing the Curly Quotes</b> - Microsoft Word has several save options -- use
"Save As Text Only" to change the quotes back to straight quotes.  Be sure to
use the correct option:
<ul>
   <li>"Save As Text Only With Line Breaks" - inserts a space at the end
of each line, and keeps curly quotes.
   <li>"Save As Text Only" - does not insert a space at the end of each lines,
and changes curly quotes to straight quotes. 
</ul>

</blockquote>


<hr>
<a name="footnote1"></a>
<p><b>Footnotes</b>
<p>[1] At JavaSoft, we use @version for the SCCS version. See "man sccs-get" for details. The concensus seems to be:

<p><code.@version &nbsp; &nbsp;  %I% %G%<code>
<ul>
  %I% gets incremented each time you edit and delget a file<br>
  %G% is the date mm/dd/yy
</ul>

<p>As Rachel explained to me, when you create a file, %I% is set to 1.1.  
When you edit and delget it, it increments to 1.2.

<p>Some developers omit the date %G% (and have been doing so) if they find 
it too confusing (3/4/96 is ambiguous to Europeans), and include the time %U% if they want more resolution (multiple delgets in a day).


<p>The real solution would be to have the date formatted as 
text (10 Oct 1996 or Oct 10 1996), as Rich suggested, but that's
an enhancement for SCCS.

<p>

<font size="-1"><em>
[Author's comment:  Include more comments from step 5 of:<br>
 ~dkramer/javadocdir/moving-frame-into-src.html#revisproc<BR>
"Manual edit the HTML files produced by WebWorks"]
</em></font>
<p>

</body>
</html>
