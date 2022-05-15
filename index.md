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

Problem Statement

Identify which questions asked on Quora are duplicates of questions that have already been asked.
This could be useful to instantly provide answers to questions that have already been answered.
We are tasked with predicting whether a pair of questions are duplicates or not.
</p>
 <h3>1.2 Sources/Useful Links</h3>
<p>
   Source : https://www.kaggle.com/c/quora-question-pairs

Useful Links
Discussions : https://www.kaggle.com/anokas/data-analysis-xgboost-starter-0-35460-lb/comments<br/>
Kaggle Winning Solution and other approaches: https://www.dropbox.com/sh/93968nfnrzh8bp5/AACZdtsApc1QSTQc7X0H3QZ5a?dl=0<br/>
Blog 1 : https://engineering.quora.com/Semantic-Question-Matching-with-Deep-Learning<br/>
Blog 2 : https://towardsdatascience.com/identifying-duplicate-questions-on-quora-top-12-on-kaggle-4c1cf93f1c30<br/>
   </p>
   <h3>1.3 Real world/Business Objectives and Constraints </h3>
   <ul>
<li>The cost of a mis-classification can be very high.</li>
<li>You would want a probability of a pair of questions to be duplicates so that you can choose any threshold of choice.</li>
<li>No strict latency concerns.</li>
<li>Interpretability is partially important.</li>
     </ul>
   <h2>2.Data</h2>
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
   <h2> 3. Machine Learning Problem </h2>
   <h3>3.1Mapping the real world problem to an ML problem </h3>
   <h4>3.1.1 Type of Machine Leaning Problem </h4>
It is a binary classification problem, for a given pair of questions we need to predict if they are duplicate or not.

   <h4>3.1.2 Performance Metric </h4>
Source: https://www.kaggle.com/c/quora-question-pairs#evaluation

Metric(s):

log-loss : https://www.kaggle.com/wiki/LogarithmicLoss
Binary Confusion Matrix
   <h3> 3.2 Train and Test and CV Construction </h3>
We build train and test by randomly splitting in the ratio of 50:30:20
</body>
</html>
