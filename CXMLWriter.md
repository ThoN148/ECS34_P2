CXMLWriter MarkDown
===================

class CXMLWriter{
    private:
        struct SImplementation;
        std::unique_ptr<SImplementation> DImplementation;
        
    public:
        CXMLWriter(std::shared_ptr< CDataSink > sink);
        ~CXMLWriter();
        
        bool Flush();
        bool WriteEntity(const SXMLEntity &entity);
};

struct SImplementation; & std::unique_ptr<SImplementation> DImplementation;
- Creates a struct that allocates a variable for the functions to use.

CXMLWriter(std::shared_ptr< CDataSink > sink);
- A constructor that uses one parameter that is a shared pointer. This pointer specifies where the output is gonna be.
- Aka Where the writing will be kept


~CXMLWriter();
- A destructor that removes those objects that are out of range.

bool Flush();
- Outputs the ends elements that has already been written down.

bool bool WriteEntity(const SXMLEntity &entity);
- Take whats is given such and inputs out in the sink, aka the destination for the writing.

Example: To execute the writer, you would have to specify the output stream to a sink first, then establish a CXMLWriter to that output. Once the Writer is established you have to start a start element, then attribute. Using google test you would want this to expected to be true in oreder to know that it has been fully written. Then you can end it of with an end element. Lastly you can do expect_eq to check the string within the output if its correct.

Test Ex:
    auto OutputStream = std::make_shared<CStringDataSink>();
    CXMLWriter Writer(OutputStream);
    EXPECT_TRUE(Writer.WriteEntity({SXMLEntity::EType::StartElement, "sanity", {{"attr","I'm losing it!"}}}));
    EXPECT_TRUE(Writer.WriteEntity({SXMLEntity::EType::EndElement, "sanity", {}}));
    EXPECT_EQ(OutputStream->String(), "<sanity attr=\"I'm losing it!\"></sanity>");

Issues: Beaware of the special character mentions in XMLReader. Character like < > " ' and & causes issues when trying to copy them down in XML. You would have to swap them out accordingly in order for them to be printed out correctly. [Guidance](https://stackoverflow.com/questions/1091945/what-characters-do-i-need-to-escape-in-xml-documents#:~:text=XML%20escape%20characters,the%20special%20character%20is%20used.)
