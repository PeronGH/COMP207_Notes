### NoSQL Databases and Semi-Structured Data

#### Introduction to Semi-Structured Data
Semi-structured data serves as a middle ground between the rigidly structured relational databases and the completely unstructured data systems. It aims to integrate the advantages of both, creating a system that is not strictly a convex combination but rather a hybrid that benefits from the strengths of each.

#### Structured vs. Unstructured Data
- **Structured Data**: Found in relational databases, this data adheres to a strict schema, allowing for highly optimized queries.
- **Unstructured Data**: This includes files like images or music, which lack a schema, requiring programs to have intrinsic knowledge of the content to process it.

#### The Concept of Semi-Structured Data
Semi-structured data is characterized by:
- A **self-describing nature**, where the data's structure and meaning are inferred from the content itself.
- **Flexibility** in adding new elements without predefined schemas.
- Representation as a **collection of nodes and edges**, forming a graph or tree-like structure.

#### Example of a Semi-Structured Database
- **Leaves**: Contain the actual data, such as strings or integers.
- **Inner Nodes**: Connect to other nodes via edges, with labels describing the relationships.
- **Root Object**: The topmost node with no incoming edges, from which all other nodes are accessible.

#### Practical Applications
Semi-structured data is commonly used for:
- **Data exchange** between companies over the internet.
- **Word processing documents**, spreadsheets, and vector graphics.
- **Database systems** in data analytics and big data.

#### Common Formats
- **XML (Extensible Markup Language)**: Focuses on tree-structured data.
- **JSON (JavaScript Object Notation)**: Similar to XML, often used with JavaScript.
- **Key-Value Stores**: Simple systems for basic data relationships.
- **Graph Databases**: Handle more complex, general graph structures.

#### Advantages of Semi-Structured Data
- **Self-describing**: Eliminates the need for separate schema definitions.
- **Flexible**: Allows for the addition or removal of properties as needed.
- Forms **tree-like structures**, providing a clear hierarchy and organization.

In the upcoming videos, the focus will be on XML and its tree-structured nature, exploring how it facilitates the management and interpretation of semi-structured data.

### Understanding XML: The Basics

#### What is XML?
XML, or Extensible Markup Language, is a flexible, semi-structured format used to store and transport data. It is a tree-based database where each node represents a piece of data and is connected to others to form a hierarchical structure.

#### XML Structure
- **Elements**: The building blocks of XML, defined by opening `<tag>` and closing `</tag>` brackets.
- **Attributes**: Name-value pairs within the opening tag of an element, providing additional information.
- **Root Element**: The single, top-level element that encapsulates all other elements.

#### XML vs. HTML
While XML is similar to HTML in appearance, its purpose is different. HTML is designed for displaying data with a focus on how it looks, whereas XML is all about the data itself and its structure.

#### XML Trees and File Systems Analogy
An XML document can be likened to a file system:
- **Inner Nodes**: Represent directories or folders.
- **Leaves**: Contain the actual data, akin to files.
- **Root**: The base directory from which all other nodes are accessible.

#### Key Features of XML
- **Self-descriptive**: XML documents describe their own structure and content.
- **Flexible**: New tags can be created as needed, and the structure can evolve.
- **Case-sensitive**: Tags must maintain consistent casing throughout.

#### XML Syntax Rules
- **Proper Nesting**: Elements must be correctly nested within each other.
- **Unique Root Element**: There must be only one root element that contains all other elements.
- **Attributes Uniqueness**: An element can have multiple attributes, but each attribute name must be unique within that element.

#### Navigating XML Documents
Traversal through an XML document follows a depth-first search pattern, moving from the root to the leaves, and then back up, processing each node according to its occurrence in the document.

#### Advanced XML Concepts
- **Document Type Definition (DTD) and XML Schema**: Tools for defining the structure and rules of an XML document.
- **Entity References**: Allow for the inclusion of reusable components within the document.
- **Comments**: Can be added for clarity, ignored by the XML processor.
- **CDATA Sections**: Used to include text that should not be parsed by the XML processor, like special characters.

#### Summary
XML is a powerful language for structuring data in a way that is both human-readable and machine-processable. It provides a standardized method for data interchange and is widely used in various applications and systems for its versatility and self-describing nature. The upcoming videos will delve deeper into XML schemas, parsing, and applications. 

### Document Type Definition (DTD) in XML

#### Overview of DTD
Document Type Definition (DTD) is a schema or a set of rules that defines the structure and the legal elements and attributes of an XML document. It is included at the beginning of an XML document to ensure that the data adheres to a specified format.

#### Writing a DTD
A DTD is declared with the following syntax:
```xml
<!DOCTYPE root_element [
  ...element declarations...
]>
```
- `root_element` is the name of the outermost tag in the XML document.
- Element declarations within the square brackets define the structure and rules.

#### Example of DTD Syntax
For a lecture database, the DTD might look like this:
```xml
<!ELEMENT lecturers (lecturer+)>
<!ELEMENT lecturer (name, phone?, email?, teachers*)>
<!ELEMENT teachers (code, title)>
...additional element declarations...
```
- `+` indicates one or more occurrences.
- `?` denotes an optional element.
- `*` allows for zero or more occurrences.

#### Defining Attributes in DTD
Attributes are defined separately from elements using the `ATTLIST` declaration:
```xml
<!ATTLIST module code CDATA #IMPLIED>
<!ATTLIST module title CDATA #IMPLIED>
```
- `CDATA` is a data type for strings.
- `#IMPLIED` means the attribute is optional.
- Other options include `#REQUIRED` for mandatory attributes and `#FIXED` for constant values.

#### Attribute Types
- `CDATA`: Character data, typically used for strings.
- `ID`: A unique identifier for an element.
- `IDREF`/`IDREFS`: Reference to one or multiple elements with an `ID`.
- Enumeration: A list of possible values for an attribute.

#### Applying DTD to XML Documents
An XML document can be:
- **Well-formed**: Follows basic XML syntax rules.
- **Valid**: Conforms to the DTD rules.

A validating processor checks both the well-formedness and validity against the DTD, ensuring the XML document is structured correctly according to the defined schema.

#### Summary
DTD provides a way to define the structure of XML documents, making them more standardized and predictable. It is a simpler form of schema compared to XML Schema, which offers more precision and complexity. The use of DTD ensures that XML documents are well-structured and adhere to the specified rules, facilitating data interchange and processing.

### Basics of XPath

#### Introduction to XPath
XPath stands for XML Path Language, which is a query language designed for selecting nodes from an XML document. It allows for navigating through elements and attributes in an XML document.

#### XPath Syntax
- **Absolute Path**: Starts with a single slash `/` followed by the path to the desired element.
- **Relative Path**: Does not start with a slash and is relative to the current context node.
- **Wildcards**: The asterisk `*` can be used to match any element.
- **Attributes**: Accessed with the `@` symbol followed by the attribute name.

#### Examples
- `/students/student`: Selects all `student` elements that are children of the `students` root element.
- `student/name`: Selects all `name` elements that are children of `student` elements.
- `//@code`: Selects all attributes named `code` in the document.

#### Document Order
XPath expressions return nodes in the order they appear in the document (document order).

#### Using XPath with Tools
Tools like Sorbet allow users to test XPath expressions against XML documents. Users can input their XML and XPath expressions to see the matching nodes or values.

#### Summary
XPath is a powerful tool for extracting information from XML documents. It provides a flexible way to specify the exact part of the document you are interested in, whether it's elements, attributes, or a combination of both. Understanding the basics of XPath is essential for working with XML data and leveraging its full potential for data retrieval and manipulation.

### Advanced XPath Techniques

#### XPath Syntax and Axes

XPath, or XML Path Language, is a query language that allows you to navigate through elements and attributes in an XML document. In this video, we delve into more advanced XPath formats and expressions.

An XPath expression typically starts with a slash (`/`), followed by an axis, a double colon (`::`), and then the name of an element, attribute, or a wildcard (`*`). This pattern can be repeated to traverse the XML structure.

##### Axes and Their Shorthands

- **Attribute**: Represented by `@`. Instead of writing `attribute::`, you can simply use `@`.
- **Child**: The default axis, so `child::` can be omitted.
- **Descendant**: Can be abbreviated as `//`.
- **Parent**: Denoted by `..`, similar to file paths.
- **Self**: Represented by a single dot (`.`).

#### Understanding Tree Structures in XML

To comprehend XPath axes, it's helpful to visualize an XML document as a tree structure. Each node in the tree represents an element or attribute, and the connections between nodes represent parent-child relationships.

- **Descendants**: All nodes reachable by moving one or more steps down the tree from a given node.
- **Descendant-or-self**: All nodes reachable by moving zero or more steps down the tree.
- **Children**: Nodes directly connected to a given node by a single downward step.
- **Parent and Ancestor**: Moving in the opposite direction, a node's parent is one step up, and ancestors are all nodes reachable by moving upwards.
- **Preceding Sibling**: Nodes that share the same parent and come before a given node in document order.
- **Following Sibling**: Nodes that share the same parent and come after a given node in document order.

#### XPath Expressions and Conditions

XPath allows for conditions within square brackets (`[]`) to refine selections. These conditions can include comparisons (equality, greater/less than, etc.) and can be combined using logical operators like `AND` and `OR`.

##### Examples

- Selecting student names: `/students/student/name` or `/child::students/child::student/child::name`.
- Selecting all elements within `student`: `/student/*` or `/student/descendant-or-self::*`.
- Selecting all emails: `/email`.
- Selecting attributes of `module`: `/module/@*`.

#### Using Conditions in XPath

Conditions in XPath are powerful for filtering results based on specific criteria.

##### Example Conditions

- Selecting book titles with a category of "CS": `/book[category='CS']/title`.
- Finding products in categories "CS" or "sci-fi" with a price at most 30 pounds: `/*[category='CS' or category='sci-fi' and price<=30]`.

#### Executing XPath Queries

When executing XPath queries, it's important to remember the case sensitivity and the correct use of axes and conditions. Incorrect syntax or axis usage can lead to unexpected results or no results at all.

#### Conclusion

This video covered advanced XPath expressions, including navigating XML trees and using conditions to filter results. In the next video, we will explore additional path conditions and provide more examples to solidify your understanding of XPath.

### XPath: Advanced Examples and Conditions

#### XPath Expressions for Book Titles and Authors

XPath expressions allow for precise navigation and extraction of data from XML documents. Here are some advanced examples:

##### Finding Titles of All Books
To retrieve the titles of all books within an XML document, you can use the following XPath expression:
```xpath
/products/book/title
```
This expression starts at the root, navigates to the `products` element, then to each `book` element, and finally selects the `title` of each book.

##### Authors of Ebooks with Specific Format
To find authors of all books that have an ebook with a specific format, such as "epub", the XPath expression would be:
```xpath
/products/book[ebook/format='epub']/author
```
This expression filters `book` elements that contain an `ebook` child with a `format` attribute equal to "epub" and selects the `author` of these books.

##### Authors of Ebooks with Specific Title and Format
For a more complex scenario where you need to find authors of ebooks with a specific title, "Databases", and format, "epub", the XPath expression would be:
```xpath
/products/book[ebook[format='epub' and title='Databases']]/author
```
This expression ensures that both conditions (title and format) are met within the same `ebook` element before selecting the `author`.

#### Using Numerical Indexes in Conditions
XPath allows the use of numerical indexes in conditions to select specific nodes based on their position:

##### Selecting First Item with Specific Categories
To select the first item with either "cs" or "sci-fi" categories, you can use:
```xpath
/*[category='cs' or category='sci-fi'][1]
```
This expression first finds all items with the specified categories and then selects the first one in the document order.

##### Selecting Last Item with Specific Categories
Similarly, to select the last item with the specified categories, you can use:
```xpath
/*[category='cs' or category='sci-fi'][last()]
```
The `last()` function returns the last item in the document order that matches the criteria.

#### Reverse Axes and Document Order
XPath provides reverse axes that allow navigation in the opposite direction of the document order:

##### Preceding Sibling Example
To find the preceding sibling of a node named "maths", the XPath expression would be:
```xpath
//*[.='maths']/preceding-sibling::*[1]
```
This expression selects the sibling node immediately before the "maths" node in the document order.

##### Ancestor Example
To find the grandparent of the "maths" node, the XPath expression would be:
```xpath
//*[.='maths']/ancestor::*[2]
```
This expression selects the grandparent node, which is two levels up from the "maths" node.

#### Conditions Using XPath Expressions and Strings
XPath conditions can also include other XPath expressions or strings to refine the selection:

##### Selecting Books with Categories
To select books that have a category, the XPath expression would be:
```xpath
//book[category]/title
```
This expression selects the `title` of books that have at least one `category` element.

##### Selecting Books with Non-Empty Attributes
To select books with a non-empty `price` attribute, the XPath expression would be:
```xpath
//book[@price][string(@price)]
```
This expression selects books where the `price` attribute exists and is not empty.

#### Summary and Role of XPath
XPath is a powerful tool for selecting nodes in an XML document, similar to how attributes are used in databases to select items in relations. While XPath itself is not a query language like SQL, it is an essential ingredient in other languages such as XQuery, which is used for querying XML documents.
