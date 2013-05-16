*** Settings ***
Library     JSpringBotGlobal


*** Test Cases ***
Set XML Using XML String
    [Tags]      keyword     set-xml-using-xml-string
    Set XML String      <?xml version="1.0"?><catalog><book id="bk101"><author>Gambardella, Matthew</author><title>XML Developer's Guide</title><genre>Computer</genre><price>44.95</price><publish_date>2000-10-01</publish_date><description>An in-depth look at creating applications with XML.</description></book><book id="bk102"><author>Ralls, Kim</author><title>Midnight Rain</title><genre>Fantasy</genre><price>5.95</price><publish_date>2000-12-16</publish_date><description>A former architect battles corporate zombies, an evil sorceress, and her own childhood to become queen of the world.</description></book><book id="bk103"><author>Corets, Eva</author><title>Maeve Ascendant</title><genre>Fantasy</genre><price>5.95</price><publish_date>2000-11-17</publish_date><description>After the collapse of a nanotechnology society in England, the young survivors lay the foundation for a new society.</description></book></catalog>

Set XML Using Classpath Resource
    [Tags]      keyword     set-xml-using-classpath-resource
    Set XML String      classpath:sample-xml.xml

Samples For Get XML XPath Elements
    [Tags]      keyword     get-xml-xpath-elements
    Set XML String      classpath:sample-xml.xml
    ${books}=           Get XML XPath Elements      //catalog/book
    ${titles}=          Get XML XPath Elements      //catalog/book[*]/title
    ${first_author}=     Get XML XPath Elements      //catalog/book[1]/author

Samples For Get XML XPath Element
    [Tags]      keyword     get-xml-xpath-element
    Set XML String      classpath:sample-xml.xml
    ${first_book_1}=    Get XML XPath Element       //catalog/book
    ${first_book_2}=    Get XML XPath Element       //catalog/book[1]
    ${first_author}=     Get XML XPath Element       //catalog/book[1]/author

Samples For Get XML Element Attribute
    [Tags]      keyword     get-xml-element-attribute
    Set XML String      classpath:sample-xml.xml
    ${first_book}=      Get XML XPath Element       //catalog/book
    ${id}=              Get XML Element Attribute   ${first_book}                   id

Samples For Get XML XPath Element Text Content
    [Tags]      keyword     get-xml-xpath-element-text-content
    Set XML String      classpath:sample-xml.xml
    ${third_book}=      Get XML XPath Element               //catalog/book[3]
    ${genre1}=          Get XML XPath Element Text Content  ${third_book}           //book/genre
    ${genre2}=          Get XML XPath Element Text Content  ${third_book}           book/genre

Sample For Get XML XPath Match Count
    [Tags]      keyword     get-xml-xpath-match-count
    Set XML String      classpath:sample-xml.xml
    ${match_count}=      Get XML Xpath Match Count   //catalog/book/price[text()='5.95']/..

Sample For Get XML XPath Single Text Content
    [Tags]      keyword     get-xml-xpath-single-text-content
    Set XML String      classpath:sample-xml.xml
    ${description}=     Get XML XPath Single Text Content   //catalog/book[3]/description

Sample For Get XML XPath Text Contents
    [Tags]      keyword     get-xml-xpath-text-contents
    Set XML String      classpath:sample-xml.xml
    ${description}=         Get XML XPath Text Contents     //catalog/book[3]/description
    ${description_list}=     Get XML XPath Text Contents     //catalog/book/description

Sample For XML Element Attribute Should Be Equal
    [Tags]      keyword     xml-element-attribute-should-be-equal
    Set XML String      classpath:sample-xml.xml
    ${third_book}=      Get XML XPath Element               //catalog/book[3]
    XML Element Attribute Should Be Equal   ${third_book}   id                  bk103

Sample For XML XPath Should Match X Times
    [Tags]      keyword     xml-xpath-should-match-x-times
    Set XML String      classpath:sample-xml.xml
    XML Xpath Should Match X Times  //catalog/book/price[text()='5.95']/..      2

Sample For XML XPath Text Content Should Be Equal
    [Tags]      keyword     xml-xpath-text-content-should-be-equal
    Set XML String      classpath:sample-xml.xml
    XML XPath Text Content Should Be Equal          //catalog/book/author       Gambardella, Matthew
    XML XPath Text Content Should Be Equal          //catalog/book[2]/author    Ralls, Kim

XML Keyword Samples Summary
    [Tags]      keyword     keywor-samples-summary
    Set XML String      classpath:sample-xml.xml
    ${author}=          Get XML XPath Elements      //catalog/book[1]/author
    ${first_book}=      Get XML XPath Element       //catalog/book
    ${third_book}=      Get XML XPath Element               //catalog/book[3]
    ${id}=              Get XML Element Attribute   ${first_book}                           id
    ${genre}=           Get XML XPath Element Text Content  ${first_book}                   //book/genre
    ${description}=     Get XML XPath Single Text Content   //catalog/book[3]/description
    ${description_list}=    Get XML XPath Text Contents     //catalog/book/description
    ${match_count}=          Get XML Xpath Match Count       //catalog/book/price[text()='5.95']/..
    XML Xpath Should Match X Times          //catalog/book/price[text()='5.95']/..          2
    XML Element Attribute Should Be Equal   ${third_book}               id                  bk103
    XML XPath Text Content Should Be Equal  //catalog/book/author       Gambardella, Matthew
    XML XPath Text Content Should Be Equal  //catalog/book[2]/author    Ralls, Kim
