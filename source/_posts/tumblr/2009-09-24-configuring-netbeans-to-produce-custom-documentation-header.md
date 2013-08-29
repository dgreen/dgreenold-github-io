---
layout: post
title: Configuring NetBeans to produce custom documentation header
tags: 
---
Instructors and projects usually have documentation standards.  The [standards
I supply my students][1] are an abbreviated version of what a project team
might use.

NetBeans can be customized to help.  In this note, I will limit my comments to
creating the header of the file.  By example, I require:

    /*
     * File: FileName.java
     * Author:  Student name, <official student e-mail>
     * Assignment: Project 2 EE333 Fall 2006
     * Vers: 1.0.0 09/01/2006 dgg - initial coding
     *
     * Credits:  (if any for sections of code)
     */

Thru the menu option Tools | Templates, one can "open in editor" the selection
"User.properties" which is under "User Configuration Properties" in the
scrollable tree-oriented selection control.

There one can define a couple "variables" that are useful:

    user=Full name <emailAddress>
    initials=dgg
    course=EE333 Fall 2009

Then one can save this, and in the same area, select "Java Class" under "Java"
and adjust things so the template contains

    /*
     * File: ${name}.java
     * Author: ${user}
     * Assignment:  ${project.displayName} - ${course}
     * Vers: 1.0.0 ${date?date?string("MM/dd/yyyy")} ${initials} - initial coding
     *
     * Credits:  (if any for sections of code)
     */

    <#if package?? && package != "">
    package ${package};
    </#if>
    /**
     *
     */
    public class ${name} {

    }


Of course, if one is doing work for multiple classes, another approach besides
"$(course)" might be appropriate.

For more information consult [FaqTemplateVariables][2] (variables in the
template) and [FaqFreeMarker][3] (coding in template).

---

### Update January 2013
 
In NetBeans 7.2.1, the variables are now reachable with the "Settings" button in the Templates dialog.

One may also wish to look at the license support in the default template and include it in your template.


[1]: http://www-ece.eng.uab.edu/DGreen/java_ex/JavaDocStyle.html
[2]: http://wiki.netbeans.org/FaqTemplateVariables
[3]: http://wiki.netbeans.org/FaqFreeMarker

