# Padding_oracle_attack

Unlike one time pad attack project(which doesnt automate the guessing word part), this project is to attack ciphertext encryted via CBC in an completed automate process. 

The idea is that by gussing the intermediate, we could figure out the plaintext block without knowing what key and encrytion algorithm used. 

The tricky part to find out the intermediate is by observing the value of oracle which is the response message from server. 

Since in CBC mode, padding is required before encryption and , very interestingly, the server will check whether the decryted text is in correct format or not. If it is not in rigth format. it will response failed code. For example, right padding should be like x01| or x02 x02 | or x03 x03 x03 .... 

So if we know what bytes can result in x01 when xor with decryted message(intermediate), then we can use that value to reverse the value of intermediate ( guessing word xor x01). The guessing word would only be range from 0-255. 

So, for the second last bytes, we could continue this padding orcale again. Since we know the last bytes of intermediate, it is not necessary to iterate the last bytes of guessing word, but focus on iterating the last second bytes. (the last bytes value should set as value which xor with last bytes of intermediate resulting in x02) . 
Once we get successful repsonse, we can reverse to get the true value of last second bytes of intermediate. 

There are some obervsation we can observe. Plaintext is always depended on the previous block. So when trying to attack a block, we could only focus on the previous block. It may help you not to sidetrack by oerwhelming block.   


so padding oracle is like keeping trying different number until we get what we want. 
