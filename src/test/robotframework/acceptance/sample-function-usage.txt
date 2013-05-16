*** Settings ***
Library     JSpringBotGlobal


*** Test Cases ***
Attribute Function Sample Usage Using XPathExpression
    [Tags]      function    attr-function-xpath-expression
    Set XML String      classpath:sample-xml.xml
    EL Add Variable     firstBookId     $[xml:attr('//catalog/book[1]','id')]

Attribute Function Sample Usage Using Elements Assigned In Robot Variable
    [Tags]      function    attr-function-element-assigned-in-robot-variable
    Set XML String      classpath:sample-xml.xml
    ${first_book}=      Get XML XPath Element   //catalog/book[1]
    EL Add Variable     firstBookId     $[xml:attr(var('first_book'),'id')]

Attribute Function Sample Usage Using Elements Assigned In EL Variable
    [Tags]      function    attr-function-element-assigned-in-el-variable
    Set XML String      classpath:sample-xml.xml
    EL Add Variable     firstBook       $[xml:element('//catalog/book')]
    EL Add Variable     firstBookId     $[xml:attr(firstBook,'id')]

Element Function Sample Usage
    [Tags]      function    element-function
    Set XML String      classpath:sample-xml.xml
    EL Add Variable     book            $[xml:element('//catalog/book')]

Elements Function Sample Usage
    [Tags]      function    elements-function
    Set XML String      classpath:sample-xml.xml
    EL Add Variable     books           $[xml:elements('//catalog/book')]

Text Function Given XPath Expression
    [Tags]      function    text-function-by-xpath-expression
    Set XML String      classpath:sample-xml.xml
    EL Add Variable     secondGenre     $[xml:text('//catalog/book[2]/genre')]
    EL Add Variable     firstGenre      $[xml:text('//catalog/book/genre')]

Text Function Given Element Assigned In Robot Variable
    [Tags]      function    text-function-element-in-robot-variable
    Set XML String      classpath:sample-xml.xml
    ${second_book}=      Get XML XPath Element  //catalog/book[2]
    EL Add Variable     secondGenre            $[xml:text(var('second_book'), '//book/genre')]

Text Function Given Element Assigned In EL Variable
    [Tags]      function    text-function-element-in-el-variable
    Set XML String      classpath:sample-xml.xml
    EL Add Variable     secondBook      $[xml:element('//catalog/book[2]')]
    EL Add Variable     secondGenre     $[xml:text(secondBook, '//book/genre')]

XML Functions Samples Summary
    [Tags]      function    function-samples-summary
    Set XML String      classpath:sample-xml.xml
    EL Add Variable     firstBookId     $[xml:attr('//catalog/book[1]','id')]
    EL Add Variable     book            $[xml:element('//catalog/book')]
    EL Add Variable     books           $[xml:elements('//catalog/book')]
    EL Add Variable     secondGenre     $[xml:text('//catalog/book[2]/genre')]
