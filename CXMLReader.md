CXMLReader MarkDown
===================

class CXMLReader{
    private:
        struct SImplementation;
        std::unique_ptr<SImplementation> DImplementation;
        
    public:
        CXMLReader(std::shared_ptr< CDataSource > src);
        ~CXMLReader();
        
        bool End() const;
        bool ReadEntity(SXMLEntity &entity, bool skipcdata = false);
};

struct SImplementation & std::unique_ptr< SImplementation > DImplementation
- A structure that allows you to create variables and function needed for CXMLReader
- Creates varaibles and handlers for XML such as start element, character data, end element, which include their callbacks. This also gold the source variable, parser.
EX:

SImplementation(std::shared_ptr< CDataSource > src){
        DDataSource = src;
        DXMLParser = XML_ParserCreate(NULL);
        XML_SetStartElementHandler(DXMLParser, StartElementHandlerCallback);
        XML_SetEndElementHandler(DXMLParser, EndElementHandlerCallBack);
        XML_SetCharacterDataHandler(DXMLParser, CharacterDataHandlerCallback);
        XML_SetUserData(DXMLParser, this);
};

~CXMLReader();
- A destructor for the CXMLReader
- Removes and deletes the objects that are out of range

Bool End() const;
- Return a true value if the reader managed to completely read the source to the very end, otherwise this would return false.

Bool ReadEntity(SXMLEntity &entity, bool skipcdata = false);
- Take two parameter and returns true to the user if the reading is finished from the source.
- If skipcdata is false then it would return the entity along with the types. If skipcdata is true, then it would only return the element type entity.

Example: You can have a string thats like <note>Hello World</note>. Running this function, if coded correctly, should have the start element and end element as note, and character data as "Hello World".
Issues: Do keep in mind that if you were to use any of the five special characters double quotes, pos, less than, greater than, and &, then you would need to swap them out. [Guidance](https://stackoverflow.com/questions/1091945/what-characters-do-i-need-to-escape-in-xml-documents#:~:text=XML%20escape%20characters,the%20special%20character%20is%20used.)
