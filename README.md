# Langchain-MCQ-Generation-using-ConversationChain
This project aims to generate multiple choice questions with more than one correct answer given a PDF and a page no. in the PDF, using the state-of-the-art Langchain library which helps in many LLM based use cases.

## Prerequisites
Before you begin, you will need to have a few tools and libraries installed on your machine:
  - Python 3.7 or higher.
  - Langchain.
  - OpenAI API key.

## Workflow
- Brainstorming ideas to implement the same, the first thing that came to my mind was simple API call with a well constructed prompt. But what's in it to just make an API call when we have more sophisticated library like Langchain which is the talk of the town as well, of late? That's when I decided to integrate my NLP knowledge and Langchain knowledge to serve the purpose.
- Installed and Imported neccessary dependencies. Used only Langchain and some in-built libraries. But tried with few more libraries which I haven't shown in my notebook.
- Now that we have a PDF with us, we need to read and break it into multiple pages so that we can give a particular page as input to the model. This is because of the reason that the context length of most model should be within the range of 2048 - 4096 tokens.
- Then as I decided, have integrated NLP based `preprocessing` techniques and Langchain's `LLM module` to generate questions after choosing a random question template from the list of templates that I had. This method had some pitfalls as well as didn't work. The reason behind the failure of this method is that we looped through multiple times to generate multiple questions and multiple answers which would obviously make frequent API calls to the model resulting in API rate limit error.
- Then the second method I resorted to was using `prompt` method in langchain and making `simple API call` and try to generate 3-5 MCQs, all at one go. Though this method moved us one step close to the solution that we wanted. But you can't rely on such thing as for every API call, the model might behave differently.
- Lastly, I used the most reliable method that we have with langchain library for our usecase which is `Conversation Chain` and `Conversational Buffer Memmory`. With conversation chain, we can build conversation with the model and correct the course of the model by building the conversation until we get desired output. Then we would store this conversation as a pickle file or json file and use the same as context whenever we want to generate `n` number of questions.

## Advantages
- The model will never loose its memory of how the structure should be and how the answer generations should be, as the depth of conversation is not too much and as we are preserving the memory at some merry point and starting from same point for every function call...
- Even straightaway conversation with an LLM like ChatGPT or API calls won't give us this kinda cushion...
- It is comparitively the better solution than any possible solution in my opinion...
- It tests the reasoning ability of the candidate rather than mere comprehension...

## Pitfalls
- The model might not be obedient always and might behave differently when the context size is too small or too large... Solution would be to use better model with paid API like GPT4 which is best in the market right now and understands context and obeys prompt better...
- Rate limit and Free tier limit would be an issue... We should either go for paid API or else we can use some random HuggingFaceHub model, which might not be the best in the market but might do some justice to the cause...
- Might occassionaly give out just one correct option if the context is too small to pick more right options within the context...

## Possible Ways to Improve
- We can use FSL(Few Shot Learning) technique to finetune the model's response by providing some 3-4 sample context and sample MCA questions... For FSL, I wrote an article on [medium](https://medium.com/@nirmal-ai/breaking-barriers-how-llms-excel-as-few-shot-learners-c6f906aabe20)... You can refer to it here to know the context...

## Contact
If you have any questions, comments, or suggestions for the project, please feel free to contact me at [nirmal.works@outlook.com]
