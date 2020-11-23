import json
from difflib import get_close_matches
data = json.load(open("data.json"))
def translate(word):
    word = word.lower()
    if word in data:
        return data[word]
    elif len(get_close_matches(word, data.keys())) > 0:
        yn = input('did you mean %s insted? Enter Y if yes, or N if no: ' % get_close_matches(word, data.keys())[0])
        if yn == "Y":
            return data[get_close_matches(word, data.keys())[0]]
        elif yn == 'N':
            return "the word doesn't exist. please double check"
        else:
            return "we didn't understand"    
    else:
        return 'word is not present'

word = input('enter a word: ')

output = translate(word)
if type(output) == list:
    for item in output:
        print(item)
else:
    print(output)        
