# chatGPT

1. Pretraining : downloading and preprocessing the internet

    basically this is like crawling through web, we have some root pages, and from these pages, we might find other urls, and we kind of go through them as well, and there can be different blocked websites, and then text extraction from html, and language filtering, and removing personal information like addresses of individuals or something, and there can be other filters as well

2. tokenization :

    converting the text into machine or model understandable one dimensional sequence

    **important : text can be converted to bits, and a set of 8 bits we can consider it as a number, so we have 256 possible combinations, and after this, we see if any consecutive numbers are repeating maximum number of times, we give a different number to that, may be 257, and we can kind of run this pattern recognition or maximum occuring sequence finding and assinging it a new number, this decreases our sequence length

    chat gpt has 100277 different tokens

3. Neural network training :

    so basically, after tokenization we have a set of data, we want to train our model with this data, so we divide our tokenized data into some n length tokens, and kind of have a probability running by our neural network, i mean it is based on the number of occurences of this same sequence before, so as the training is done more, the results will improve

    inference : so based on above procedure, we might have multiple next tokens with a major probability, kind of like duopoly or multiple companies sharing the market, but with inference, we just predict one token at a time, so we send the first set of tokens, find a single most probabilistic next token, and again resend this newly generated and the old sequence into the model to predict the next token and so on

    neural networks are mathematical networks or equations, that kind of stores the probability of the next token, given a sequence of tokens

