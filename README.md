# gptchatteR
An experimental and unofficial wrapper for interacting with OpenAI GPT models in R. 
gptchatteR uses the `openai` library to handle the OpenAI API endpoints, and defaults to the `text-davinci-003` model.

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

```R
library(gptchatteR)
```

### &#8594; Casual chat

You can use the `chatter.chat` function to send messages to ChatGPT and receive responses:

```R
chatter.chat("Hello, ChatGPT!")
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

## Acknowledgements

This package uses OpenAI's ChatGPT model, which is an implementation of the GPT-3 architecture. Thank you to OpenAI for making this technology available to the public. Special thanks to ChatGPT for helping me write this file.
