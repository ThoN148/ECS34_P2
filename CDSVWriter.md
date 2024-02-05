CDSVWriter MarkDown
===================

struct SImplementation;
- A structure that allows you to create variables and function needed for CDSVReaer

std::unique_ptr<SImplementation> DImplementation;
- Dynimcally allocating the same typing as Simplementation to Dimplemetation

Example: This structure can include shared pointer varaible, character varaible, and the WriteRow function.

CDSVWriter(std::shared_ptr< CDataSink > sink, char delimiter, bool quoteall = false);
- CDSVWriter uses three parameter, sink which is where the output / writing is gonna be, delimiter, the character that's gonna be between the text to indicate the seperation, and quoteall a boolean parameter that determines if everything should be quoted or those that in double quotes, new line, or within the delimiter 
- Constructor of CDSVWriter

~CDSVWriter();
- Removes / Deletes the objects within the class if they happen to be out of range
- Destructor for the CDSVWriter

bool WriteRow(const std::vector<std::string> &row);
- Returns true to the user once the string has all been written down into each column
