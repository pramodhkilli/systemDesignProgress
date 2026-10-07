# Tokenization

Lets take a sentence, our models does not understand text, they understand numbers, so we need a way to convert our text into entities that our models understand

that conversion of sentences into something models understand is tokenization

so we can divide a sentence into multiple tokens, based on our tokenization strategy, each strategy has it pros and cons

before that an important term to know is "vocabulary", vocabulary is our set of tokens that we have in our knowledge base, so we kind of try to divide our sentence into these already known tokens in our knowledge base

and another term to know is "sequence", sequence is the set of converted tokens from our sentence or paragraph.

1. word based : very intuitive, this is like for each word we assign a token, this is simple to understand, but this does not take advantage of the words of same base like "read" "reading" "reads" all these words are related, but we assign different tokens to them, so we are not taking the advantage of the fact that they are related, which in return makes the vocabulary large. but on the contrary our sequence size will be small

2. letter based : we assign a token to each letter of the alphabet and special characters, this is a limited set even if you include multiple language support, but the time to relate kind of becomes difficult because we are not taking the advantage of word relations here anywhere, and our sequence length will be large as well

3. sub-word : we take the good's of word based and try to remove the disadvantages, like we have a token for "read", and there could be pattern based token's that represent the extended versions of the base word, like "**s", "**ing", this reduces the tokens and also our vocabulary as well.

additionally, there can be special tokens that represents something that are not part of vocabulary or about the sequence, like [unk], [bos],[eos], these are the representations of the unknown, beginning of sequence, end of sequence tokens

unknown is given to a token if it is not part of our vocabulary.
