---
layout: post
title:  "Using Checkstyle to force the use of Java 8 lambdas"
categories: blog
---

I got asked today whether it was possible to use [Checkstyle](http://checkstyle.sourceforge.net) to force the use of [Java 8 lambdas](http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/Lambda-QuickStart/index.html). I can see the merit in wanting to do this.

There does not appear to be an [existing check](http://checkstyle.sourceforge.net/checks.html) for doing it. However, it is possible using the ever powerful [DescendantToken](http://checkstyle.sourceforge.net/checks.html). Just add the following module definition to your Checkstyle configuration to report on code that should be using Java 8 lambdas:

    <module name="DescendantToken">
      <property name="tokens" value="METHOD_CALL"/>
      <property name="limitedTokens" value="METHOD_DEF"/>
      <property name="maximumNumber" value="0"/>
      <property name="maximumMessage" value="Use Java 8 Lambdas!"/>
    </module>

The definition above will find any method call that contains a method definition, which would be part of an anonymous class definition. Simple but effective.
