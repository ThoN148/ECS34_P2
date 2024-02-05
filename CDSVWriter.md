class CDSVWriter{
    private:
        // A structure that allows you to create variables and function needed for CDSVReaer
        struct SImplementation;

        // Dynimcally allocating the same typing as Simplementation to Dimplemetation
        std::unique_ptr<SImplementation> DImplementation;

        // Example: This structure can include shared pointer varaible, character varaible, and the WriteRow function.

    public:
        // CDSVWriter uses three parameter, sink which is where the output / writing is gonna be, delimiter, the character that's gonna be between the text to indicate the seperation, and quoteall a boolean parameter that determines if everything should be quoted or those that in double quotes, new line, or within the delimiter 
        // Constructor of CDSVWriter
        CDSVWriter(std::shared_ptr< CDataSink > sink, char delimiter, bool quoteall = false);
        
        // Removes / Deletes the objects within the class if they happen to be out of range
        // Destructor for the CDSVWriter
        ~CDSVWriter();

        //
        bool WriteRow(const std::vector<std::string> &row);
};
