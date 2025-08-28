# Math Search Engine
B. Tech Thesis project based on ARQMath 2022 problem statement 1.

**Problem Statement:**

Query: An english sentence which is one of the questions asked on Math Stack Exchange Forum. It may or may not contain a mathematical expression in Latex format.<br>
Document: Posts made on Math Stack Exchange forum as answers or comments to a question on Math Stack Exchange. Each post may or may not contain a mathematical expression in from of Latex.<br>

Given a query and a corpus of documents bound to have answer of that query in it, the task was to retrieve the documents from the corpus which were answers to the given query and rank them according to the no. of upvotes the answer had received on the Forum.

**Approach:**
Assuming the data has been cleaned, and preprocessed (stemming, stop-word removing, etc.).<br>
1. Separate the Text and Math part from each of the query and documents leaving a link behind for processing them separately.
2. Taking n-grams (n=2) of sentences from the query and using RoBERTa and matching the similarity of textual parts of query and all the available answers. The n-gram giving the best similarity score was taken as the score of the answer.
3. The Top-k selected documents from the step 2 were then re-ranked based on how similar were the mathematical expressions in them to the mathematical expressions in the question.
4. Similarity calculation was done by dynamically creatinig regular expressions that matched the structure of the math expression latex at different levels of abstraction.
5. After reranking top-10 documents were selected for calculation of results. if any of the actually correct answers entered the top-10 retrieved answers, it was taken as correct prediction else incorrect prediction.


