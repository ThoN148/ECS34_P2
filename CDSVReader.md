CDSVReader Mark Down
====================
class CDSVReader{
    private:
        struct SImplementation;
        std::unique_ptr<SImplementation> DImplementation;

    public:
        CDSVReader(std::shared_ptr< CDataSource > src, char delimiter);
        ~CDSVReader();

        bool End() const;
        bool ReadRow(std::vector<std::string> &row);
};

- struct SImplementation;
*A structure that allows you to create variables and function needed for CDSVReaer

- std::unique_ptr<SImplementation> DImplementation;
*Dynimcally allocating the same typing as Simplementation to Dimplemetation

- Example: This structure can include shared pointer varaible, character varaible, and the bool functions.

*CDSV Reader uses two parameter for the function. One being a shared pointer to the source of information, and another is the delimiter. Delimiter is the character that you would typically use to differentiate the text data.
*Ex. Source data is "Apples,Bananas,Grapes,Pears" with a delimiter character of ","
*Constructor for the CDSVReader
- CDSVReader(std::shared_ptr< CDataSource > src, char delimiter);

        // Removes / Deletes the objects within the class if they happen to be out of range
        // Destructor for the CDSVReader
        ~CDSVReader();

        // Returns a true/false value depending if the DSVReader has finished reading everything
        // If all of the object/values have been read then the function would return true.
        bool End() const;

        // Example: You would typically want to call this function to check if the reader has finished. So in ReadRow, it needs to know if the rows within the source data has been read. You can call this function to see if it would return true, in order to continue.

        // Calling this function will return a true/false value if all of the rows has been read. This will put each string into one column of the vector
        bool ReadRow(std::vector<std::string> &row);

        // Example: If you were to input with the example above. If it reads all of the texts, it will put all of the strings seperated by the delimiter ",", each into its own seperate column. So the vector would look something like {"Apples", "Bananas", "Grapes", "Pears"}. You can check this by calling out the vector and then specifying which slot. i.e. vector[0] = Apples, vector[1] = Bananas, so on so forth.
};
