*** Settings ***
Library     JSpringBotGlobal


*** Test Cases ***
Create XML String
    [Tags]      keyword     create-xml-string
    Start XML Node      root
    Start XML Node      nodeWithAttributes
    Add XML Attribute   attr1     attrValue1
    Add XML Attribute   attr2     attrValue2
    End XML Node
    Start XML Node      nodeWithText
    Set XML Text        Some Text Here
    ${xml}=     Create XML String
    Should Be Equal As Strings  ${xml}      <root><nodeWithAttributes attr1="attrValue1" attr2="attrValue2"/><nodeWithText>Some Text Here</nodeWithText></root>

Create Book Catalog String
    [Tags]      keyword     create-xml-string   create-book-catalog
    Start XML Node      catalog     true
    Start XML Node      book
    Add XML Attribute   id          bk101
    Start XML Node      author
    Set XML Text        Gambardella, Matthew
    End XML Node
    Start XML Node      title
    Set XML Text        XML Developer's Guide
    End XML Node
    Start XML Node      genre
    Set XML Text        Computer
    End XML Node
    Start XML Node      price
    Set XML Text        44.95
    End XML Node
    Start XML Node      publish_date
    Set XML Text        2000-10-01
    End XML Node
    Start XML Node      description
    Set XML Text        An in-depth look at creating applications with XML.
    End XML Node
    End XML Node
    Start XML Node      book
    Add XML Attribute   id          bk102
    Start XML Node      author
    Set XML Text        Ralls, Kim
    End XML Node
    Start XML Node      title
    Set XML Text        Midnight Rain
    End XML Node
    Start XML Node      genre
    Set XML Text        Fantasy
    End XML Node
    Start XML Node      price
    Set XML Text        5.95
    End XML Node
    Start XML Node      publish_date
    Set XML Text        2000-12-16
    End XML Node
    Start XML Node      description
    Set XML Text        A former architect battles corporate zombies, an evil sorceress, and her own childhood to become queen of the world.
    End XML Node
    End XML Node
    Start XML Node      book
    Add XML Attribute   id          bk103
    Start XML Node      author
    Set XML Text        Corets, Eva
    End XML Node
    Start XML Node      title
    Set XML Text        Maeve Ascendant
    End XML Node
    Start XML Node      genre
    Set XML Text        Fantasy
    End XML Node
    Start XML Node      price
    Set XML Text        5.95
    End XML Node
    Start XML Node      publish_date
    Set XML Text        2000-11-17
    End XML Node
    Start XML Node      description
    Set XML Text        After the collapse of a nanotechnology society in England, the young survivors lay the foundation for a new society.
    End XML Node
    End XML Node
    End XML Node
    ${bookCatalog}=     Create XML String
    Should Be Equal As Strings  ${bookCatalog}   <catalog><book id="bk101"><author>Gambardella, Matthew</author><title>XML Developer's Guide</title><genre>Computer</genre><price>44.95</price><publish_date>2000-10-01</publish_date><description>An in-depth look at creating applications with XML.</description></book><book id="bk102"><author>Ralls, Kim</author><title>Midnight Rain</title><genre>Fantasy</genre><price>5.95</price><publish_date>2000-12-16</publish_date><description>A former architect battles corporate zombies, an evil sorceress, and her own childhood to become queen of the world.</description></book><book id="bk103"><author>Corets, Eva</author><title>Maeve Ascendant</title><genre>Fantasy</genre><price>5.95</price><publish_date>2000-11-17</publish_date><description>After the collapse of a nanotechnology society in England, the young survivors lay the foundation for a new society.</description></book></catalog>

Sample Usage Of Start XML String
    [Tags]      keyword     create-xml-string   sample-usage-start-xml-string
    Start XML Node              catalog             true
    End XML Node
    ${xmlString}=               Create XML String
    Should Be Equal As Strings  ${xmlString}        <catalog/>
    Start XML Node              another-catalog     true
    End XML Node
    ${xmlString}=               Create XML String
    Should Be Equal As Strings  ${xmlString}        <another-catalog/>

Sample Usage Of Add XML Attribute
    [Tags]      keyword         sample-usage-add-xml-attribute
    Start XML Node              book                true
    Add XML Attribute           id                  bk101
    End XML Node
    ${xmlString}=               Create XML String
    Should Be Equal As Strings  ${xmlString}         <book id="bk101"/>

Sample Usage Of Set XML Text
    [Tags]      keyword     create-xml-string   sample-usage-set-xml-text
    Start XML Node              book                true
    Set XML Text                Meet Joe Black
    End XML Node
    ${xmlString}=               Create XML String
    Should Be Equal As Strings  ${xmlString}        <book>Meet Joe Black</book>

Sample Usage Of End XML Node
    [Tags]      keyword     create-xml-string   sample-usage-end-xml-node
    Start XML Node              catalog             true
    Start XML Node              book
    End XML Node
    Start XML Node              movies
    End XML Node
    End XML Node
    ${xmlString}=               Create XML String
    Should Be Equal As Strings  ${xmlString}        <catalog><book/><movies/></catalog>

