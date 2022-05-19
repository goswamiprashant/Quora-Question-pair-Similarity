<html>
<head>
</head>
 <body>

 <h1> Quora-Question-Pair-Similarity</h1>
   <h2>1. Business Problem </h2>
   <h3>1.1 Description </h3>
<p>
Quora is a place to gain and share knowledge—about anything. It’s a platform to ask questions and connect with people who contribute unique insights and quality answers. This empowers people to learn from each other and to better understand the world.

Over 100 million people visit Quora every month, so it's no surprise that many people ask similarly worded questions. Multiple questions with the same intent can cause seekers to spend more time finding the best answer to their question, and make writers feel they need to answer multiple versions of the same question. Quora values canonical questions because they provide a better experience to active seekers and writers, and offer more value to both of these groups in the long term.


Credits: Kaggle

  <h3>1.2 Problem Statement</h3>

Identify which questions asked on Quora are duplicates of questions that have already been asked.
This could be useful to instantly provide answers to questions that have already been answered.
We are tasked with predicting whether a pair of questions are duplicates or not.
</p>
 
   
   <h2>2.Dataset</h2>
<h3>2.1.Data Overview </h3>
  <ul>
  <li> Data will be in a file Train.csv</li>
    <li>Train.csv contains 5 columns : qid1, qid2, question1, question2, is_duplicate.</li>
    <li> Size of Train.csv - 60MB.</li>
    <li>Number of rows in Train.csv = 404,290.</li>
  </ul>

   <h4> 2.1.1 Example Data points </h4>
 <table>
   <tr>
   <th>id</th>
     <th>qid</th>
     <th>qid2</th>
     <th>question1</th>
     <th>question2</th>
     <th>is_duplicate</th>
   </tr>
<tr>
     <td>0</td>
      <td>1</td>
      <td>2</td>
   <td>What is the step by step guide to invest in share market in india ?</td>
   <td>What is the step by step guide to invest in share market ?</td>
  <td>0</td>
   </tr>
   <tr>
     <td>1</td>
     <td>3</td>
     <td>4</td>
     <td>What is the story of Kohinoor (Koh-i-Noor) Diamond?</td>
     <td>What would happen if the Indian government stole the Kohinoor (Koh-i-Noor) diamond back?</td>
     <td>0</td>
     </tr>
     <tr>
     <td>7</td>
     <td>15</td>
     <td>16</td>
     <td>How can I be a good geologist?</td>
     <td>What should I do to be a great geologist?</td>
     <td>1</td>
     </tr>
    <tr>
     <td>11</td>
     <td>23</td>
     <td>24</td>
     <td>How do I read and find my YouTube comments?</td>
     <td>How can I see all my Youtube comments?</td>
     <td>1</td>
     </tr>
   </table>
<h4> 2.1.2 Distribution of data points among output classes</h4>
  <p><img src ='dist_classlabels.png' height=400 width=600  alt='Distribution of data points among output classes'/></p>
 <h2>3.Data Preprocessing</h2>
    <h4> 3.1.Description of features </h4>
  <p>
  We are given a minimal number of data fields here, consisting of:<br/>
   <ul>
    <li><b>id</b>:  Looks like a simple rowID</li>
    <li><b>qid{</b>1, 2}:  The unique ID of each question in the pair</li>
    <li><b>question</b>{1, 2}:  The actual textual contents of the questions.</li>
    <li><b>is_duplicate</b>:  The label that we are trying to predict - whether the two questions are duplicates of each other. </li>
  </ul>    
    </p>
   
   <h3> 3.2 Preprocessing of Text </h3>
 - These are the following that we followeed during text preprocessing :
    <ul>
     <li>Removing html tags </li>
     <li>Removing Punctuations</li>
     <li>Performing stemming</li>
     <li> Removing Stopwords</li>
     <li>Expanding contractions etc</li>
 </ul>
 <h2>4.Feature Extraction</h2>
 <h3>4.1 Basic Feature Exteaction </h3>
 Initially, we constructed few features like:<br/>
 
 <br/>
 <ul>
  <li><b> freq_qid1 </b>  = Frequency of qid1's </li>
 <li><b> freq_qid2 </b>   = Frequency of qid2's </li>
 <li><b> q1len </b>  = Length of q1 </li>
 <li><b> q2len </b>  = Length of q2 </li>
 <li><b> q1_n_words </b>  = Number of words in Question 1 </li>
 <li><b> q2_n_words </b>  = Number of words in Question 2 </li>
 <li><b> word_Common </b>  = (Number of common unique words in Question 1 and Question 2) </li>
 <li><b> word_Total </b> =(Total num of words in Question 1 + Total num of words in Question 2) </li>
 <li><b> word_share </b> = (word_common)/(word_Total) </li>
 <li><b> freq_q1+freq_q2 </b> = sum total of frequency of qid1 and qid2 </li>
 <li><b> freq_q1-freq_q2 </b>  = absolute difference of frequency of qid1 and qid2 </li>
 </ul>
 
 <h3>4.2 Advance Feature Exteaction </h3>
  
<p>
Definition:<br/>
 <ul type=none>
  <li>
 <b>Token</b>: You get a token by splitting sentence a space<br/>
 <b>Stop_Word</b>: stop words as per NLTK.<br/>
 <b>Word</b> : A token that is not a stop_word
  </li>
  </ul>
<br/>
<p> We have tried some advanced features which are as follows : </p>
  <ul type=none>
   <li>
 <b>cwc_min__ </b>:  Ratio of common_word_count to min lenghth of word count of Q1 and Q2 <br>cwc_min = common_word_count / (min(len(q1_words), len(q2_words))
<br>

<b>cwc_max</b>:  Ratio of common_word_count to max lenghth of word count of Q1 and Q2 <br>cwc_max = common_word_count / (max(len(q1_words), len(q2_words))
<br>
<br>
  
<b>csc_min</b>:  Ratio of common_stop_count to min lenghth of stop count of Q1 and Q2 <br> csc_min = common_stop_count / (min(len(q1_stops), len(q2_stops))
<br>
<br>
  
<b>csc_max</b> :  Ratio of common_stop_count to max lenghth of stop count of Q1 and Q2<br>csc_max = common_stop_count / (max(len(q1_stops), len(q2_stops))
<br>
<br>
  
<b>ctc_min</b>:  Ratio of common_token_count to min lenghth of token count of Q1 and Q2<br>ctc_min = common_token_count / (min(len(q1_tokens), len(q2_tokens))
<br>
<br>

<b>ctc_max</b> :  Ratio of common_token_count to max lenghth of token count of Q1 and Q2<br>ctc_max = common_token_count / (max(len(q1_tokens), len(q2_tokens))
<br>
<br>
        
<b>ast_word_eq</b>:  Check if First word of both questions is equal or not<br>last_word_eq = int(q1_tokens[-1] == q2_tokens[-1])
<br>
<br>

<b>first_word_eq</b>:  Check if First word of both questions is equal or not<br>first_word_eq = int(q1_tokens[0] == q2_tokens[0])
<br>
<br>
        
<b>abs_len_diff</b>:  Abs. length difference<br>abs_len_diff = abs(len(q1_tokens) - len(q2_tokens))
<br>
<br>

<b>mean_len</b>:  Average Token Length of both Questions<br>mean_len = (len(q1_tokens) + len(q2_tokens))/2
<br>
<br>


<b>fuzz_ratio</b>:  https://github.com/seatgeek/fuzzywuzzy#usage<br/>
http://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/
<br>
<br>

<b>fuzz_partial_ratio</b>:  https://github.com/seatgeek/fuzzywuzzy#usage<br/>
http://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/
<br>
<br>


<b>token_sort_ratio</b> : https://github.com/seatgeek/fuzzywuzzy#usage<br/>
http://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/
<br>
<br>


<b>token_set_ratio</b>: https://github.com/seatgeek/fuzzywuzzy#usage<br/>
http://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/
<br>
<br>

<b>longest_substr_ratio</b>:  Ratio of length longest common substring to min lenghth of token count of Q1 and Q2<br>longest_substr_ratio = len(longest common substring) / (min(len(q1_tokens), len(q2_tokens))
   </li>
 </ul>
</div>
 </p>
   <h2> 5. Machine Learning Problem </h2>
   <h3>5.1 Mapping the real world problem to an ML problem </h3>
   <h4>5.1.1 Type of Machine Leaning Problem </h4>
It is a binary classification problem, for a given pair of questions we need to predict if they are duplicate or not.

   <h4>5.1.2 Performance Metric </h4>
Source: https://www.kaggle.com/c/quora-question-pairs#evaluation
Metric(s):
<p>log-loss : https://www.kaggle.com/wiki/LogarithmicLoss</p>
<p>Binary Confusion Matrix</p>
<h3>5.2 Real world/Business Objectives and Constraints </h3>
   <ul>
<li>The cost of a mis-classification can be very high.</li>
<li>You would want a probability of a pair of questions to be duplicates so that you can choose any threshold of choice.</li>
<li>No strict latency concerns.</li>
<li>Interpretability is partially important.</li>
     </ul>
   <h3> 5.3 Train and Test and CV Construction </h3>
We build train and test by randomly splitting in the ratio of 50:30:20
  <h3> 5.4. Model Building Approach</h3>
  <p> Keeping these Objectives and constraints in mind we have tried different classififcation algorithms to achieve them. 
   To get optimized results ,we use different Classification algorithms like Logistic Regression , SVM and XGBoost on the engineered feature set.</p>
<h3>5.5 Result </h3>
<p> <table>
  <tr>
  <th>Model</th>
  <th>Train Loss</th>
  <th>Test Loss</th>
 </tr>
 <tr>
  <td>Logistic Regression</td> 
  <td> 0.4631 </td>
  <td> 0.4624 </td>
 </tr>
 <tr>
  <td>SVM</td> 
  <td> 0.4726</td>
  <td>  0.4688 </td>
 </tr>
 <tr>
  <td>XG Boost</td> 
  <td> 0.2245 </td>
  <td> 0.3203</td>
 </tr>
 </table>
 </p>
<h2>6.Sources/Useful Links</h2>
<p>
   Source : https://www.kaggle.com/c/quora-question-pairs

Useful Links
Discussions : <a>https://www.kaggle.com/anokas/data-analysis-xgboost-starter-0-35460-lb/comments</a><br/>
Kaggle Winning Solution and other approaches: https://www.dropbox.com/sh/93968nfnrzh8bp5/AACZdtsApc1QSTQc7X0H3QZ5a?dl=0<br/>
Blog 1 : https://engineering.quora.com/Semantic-Question-Matching-with-Deep-Learning<br/>
Blog 2 : https://towardsdatascience.com/identifying-duplicate-questions-on-quora-top-12-on-kaggle-4c1cf93f1c30<br/>
   </p>
</body>
</html>
