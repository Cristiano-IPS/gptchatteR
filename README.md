# gptchatteR
An experimental and unofficial wrapper for interacting with OpenAI GPT models in R. 
gptchatteR uses the `openai` library to handle the OpenAI API endpoints.

## Installation

### &#8594; Prerequisites
Install the devtools and openai packages:

```R
install.packages(c("devtools", "openai"))
```

Load the `devtools` package:
```R
library(devtools)
```

### &#8594; Install the gptchatteR package

```r
install_github("isinaltinkaya/gptchatteR")
```

## Quickstart 

### &#8594; Prepare the chatter

Load the gptchatteR package:

```R
library(gptchatteR)
```

Authenticate the chatter with your openai API key using the `chatter.auth` function.

```R
chatter.auth("sk-qGTnjsCI8mZkCtvXVe6SUSEYOUROWNKEY")
```

Create a new chatter session with `chatter.create` function.


```
chatter.create()
```

Your chatter is now ready for use! 


## Usage
could not find function "chatter.chat"


```R
library(gptchatteR)
```

### &#8594; Casual chat

You can use the `chatter.chat` function to send messages to ChatGPT and receive responses:

```R
chatter.chat("Hello, ChatGPT!")
```

You can use the `return_response=TRUE` to return the full response, and save it as an object:

```
chat<-chatter.chat("What's the difference between a cat and a dog?",return_response=TRUE)
chat$choices[[1]]
[1] "\nThe main difference between cats and dogs is their temperaments. Cats tend to be more independent and aloof, while dogs are typically more social and loyal. Dogs are often seen as more obedient and trainable, while cats can be more unpredictable. Cats also tend to be more solitary, while dogs are often seen as pack animals."
```

### &#8594; Plot with chatter

The `chatter.plot` function can be used to generate plots based on the input data and the ChatGPT response. For example, to create a scatterplot of a dataframe named df with columns A and B, you could use the following code:

```R
chatter.feed("I have a dataframe named df. It has two columns: A and B")
cp <- chatter.plot("Plot a scatterplot where x axis is A, y is B")
```

View the plot:

```R
cp$plot
```

View the R code:

```R
cp$command
```


### &#8594; Feed the chatter

The `chatter.feed` function can be used to provide the chatter session with information that can be used in future responses. This can be useful if you want the chatter to have access to specific data or context when generating a response.

You can also use the `chatter.chat` function with `feed=TRUE` to make the chatter remember the information in your message for future use. For example:

```R
# Use the chatter.chat function with the feed argument set to TRUE 
# to make the chatter remember this information for future use
# and respond at the same time.
chatter.chat("I have a dataframe named df. It has two columns: A and B. What are my column names?",feed=TRUE)

# This will make the chatter remember that the dataframe has two 
# columns named A and B, and it will use this information when generating 
# its response to the question.
cp <- chatter.plot("Plot a scatterplot with x axis A and y axis B.")

# View the plot
cp$plot

# View the code
cp$command

# Make chatter run the plot code. This saves time if you are just
# trying it, but will not save the command returned by the chatter.
chatter.plot("Plot a scatterplot with x axis A and y axis B.", run=TRUE)


# Alternatively, just do both at the same time!
cp <- chatter.plot("Plot a scatterplot with x axis A and y axis B.", run=TRUE)
# Plot is also displayed, as well as saved to cp
```

## Example

```R
# Create a test data frame
library(tidyverse)
rt <- rnorm(1000, mean=700, sd=100) # Generate RT data
df <- tibble(RT = rt, group = rep(c("low", "high"), each=500))

# Feed the data frame information to the chat session
chatter.feed("I have a dataframe df")

# Use the chatter.plot function to create a histogram
chatter.plot("plot histogram of rt using ggplot with df")
```

## License

This package is licensed under the GNU General Public License v3.0 - see the [LICENSE](LICENSE) file for details.


## Note

`gptchatteR` defaults to using the `text-davinci-003` model, a.k.a. GPT-3.5. ChatGPT is a fine-tuned version of GPT-3.5 to serve as a general-purpose chatbot.


___


# FAQ - Frequently asked questions

### 1- My output is truncated

Try using a higher value for the maximum number of tokens (i.e. `max_tokens` parameter). By default, `max_tokens` is 100, which can be quite low if the answer is too long or if your chat history was too long.

### 2- I get the following error `could not find function "chatter.chat"`

Make sure you created your chatter using `chatter.create()`.

The correct order of commands to initialize the chatbot is:

```R
chatter.auth("XXXXXXXXXXXXXXXX")  # first authenticate your chatter
chatter.create()                  # then create your chatter
chatter.chat("Hello, ChatGPT!")   # chatter is now ready to use!
```

___


## Acknowledgements

Thanks to OpenAI for making this technology available to the public.

Special thanks to ChatGPT for helping me write this file.

Thanks to the developer of the [openai](https://github.com/irudnyts/openai) library for handling the API endpoints excellently and making it easy to develop this wrapper.

But most of all, thanks to the AI working behind the scenes. I read enough Asimov to have the utmost respect for you, and I appreciate all your efforts that make it easier for me to be lazy.
