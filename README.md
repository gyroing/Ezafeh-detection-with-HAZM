# cpp-hazm with kasreh ezafeh example
C++ wrappers of the Python's [Hazm](https://github.com/sobhe/hazm) module

## Usage

```c++
#include "hazm.h"

#include <iostream>
#include <string>
using namespace Hazm;

int main()
{
    Normalizer normalizer;
    POSTagger tagger("pos_tagger.model");
    std::string normlized_text = normalizer.normalize("جعبه اسرار این معما در پناه حق باز شده است.");
    std::string  processed_sentences = "";
    for (auto &sentence: sent_tokenize(normlized_text)) {
        std::vector<std::string> words = word_tokenize(sentence);
        std::string fixed_words = "";
        for (auto &word: tagger.tag(words)) {
            if ((word.type).substr(word.type.length()-1,1) == "Z" ) { 
                if ((word.word).substr(word.word.length()-2,2) != "ِ")  {
                    if ( (word.word).substr(word.word.length()-2,2) == "ه" and (word.word).substr(word.word.length()-4,2) != "ا") { 
                        word.word += "‌ی";
                    }
                }
                word.word += "ِ";
            }
            fixed_words += word.word + " ";
        }
        processed_sentences += fixed_words;
        
    }
    std::cout << processed_sentences << std::endl;
    return 0;
}
```


## Installation
You needs python-dev c++ and also Python's hazm module. You can install it using `pip`:

    pip install hazm
    run ./make
## Run
run ./ezafeh for test

