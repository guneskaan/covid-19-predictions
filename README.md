</head>
<body class="c14">
    <p class="c7"><span class="c3">YOUTUBE LINK: https://www.youtube.com/watch?v=10SmboePzqI</span></p>
    <p class="c7"><span class="c6">Idea</span><span class="c3">&nbsp;</span></p>
    <p class="c0"><span class="c3">Our idea is that the number of people who have participated in spreading awareness about social distancing on social media is an influence on the spread of COVID-19 in Canada and can help us predict future cases more accurately.</span></p>
    <p class="c1"><span class="c3"></span></p>
    <p class="c7"><span class="c6">Methodology</span></p>
    <p class="c0"><span class="c3">To assess the current situation of COVID-19 in Canada, we obtained the number of total cases per day. The machine learning model to predict our initial guesses was directly taken from Kaggle, and then adjusted to fit our time series.</span></p>
    <p class="c0 c2"><span class="c3"></span></p>
    <p class="c0"><span class="c3">Here&rsquo;s the initial prediction graph.</span></p>
    <p class="c0 c2"><span class="c3"></span></p>
    <p class="c0"><span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 413.50px; height: 280.25px;"><img alt="" src="images/image1.png" style="width: 413.50px; height: 280.25px; margin-left: 0.00px; margin-top: 0.00px; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px);" title=""></span></p>
    <p class="c0"><span class="c3">There are two details on this model that caught our eye: </span></p>
    <p class="c0 c11"><span class="c3">1) This model underestimated on certain days (April 5th) and overestimated on some others (April 15th). </span></p>
    <p class="c5"><span class="c3">2) This model predicted that the pandemic would be over on October 27, 2020.</span></p>
    <p class="c0 c2"><span class="c3"></span></p>
    <p class="c0"><span class="c3">One of the covariants which this model did not account for is people&rsquo;s tendency to follow the government&rsquo;s recommendation to stay home and isolate.</span></p>
    <p class="c0"><span>In order to measure how people are responding to these social guidelines, we analyzed over </span><span>10 Million</span><span class="c3">&nbsp;tweets sent since the first day of March. We used two Twitter datasets which in union contain every tweet related to COVID-19 from March 1st to April 19th and the number of tweets reached close to 180 million tweets. We then iterated over these tweets to extract and rank the top 1000 most frequent bigrams on each day. These bigrams exclude stopwords such as &ldquo;at, the, in etc&rdquo;. For the purpose of testing our hypothesis we kept track of bigrams that are precisely tied to social distancing, such as &ldquo;stay home&rdquo;, &ldquo;herd immunity&rdquo;, &ldquo;sign petition&rdquo; and &ldquo;contact tracing&rdquo;.</span></p>
    <p class="c0"><span>Lastly, we engineered a formula to calculate the influence of the rankings of these bigrams. </span><span>Applying the formula to the predictions resulted in an adjusted prediction model, which we believe is more accurate for</span><span>&nbsp;estimatin</span><span>g </span><span class="c3">how many people will be infected in the near future, such as next 7 days.</span></p>
    <p class="c0 c2"><span class="c3"></span></p>
    <p class="c7"><span class="c6">Implementation</span></p>
    <p class="c0"><span>&nbsp;We obtained the number of total cases per day in Canada </span><span>f</span><span>rom </span><span>Kaggle. There were </span><span>two</span><sup><a href="#cmnt1" id="cmnt_ref1">[a]</a></sup><span>&nbsp;models we considered using to make predictions for the upcoming days. First, we considered logistic curve fitting. This is simply a statistical method to fit a logistic curve over the number of confirmed cases time series. After fitting the curve, we found that the results were grossly underestimated and were not happy with the results. </span><span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 602.00px; height: 452.00px;"><img alt="" src="images/image2.png" style="width: 602.00px; height: 452.00px; margin-left: 0.00px; margin-top: 0.00px; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px);" title=""></span></p>
    <p class="c7"><span class="c3">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;So, we started looking for other models, and came across a model that was based on a different model that used to predict diffusion of innovations. This original model is from a marketing paper by Emmanuelle Le Nagard and Alexandre Steyer, that attempts to reflect the social structure of a diffusion process. While this model was not used to predict a pandemic outcome, the author of this model believed that there are commonalities in both domains. So we used the result of this new model to predict the next week and find when the pandemic will end. This model finds the optimal function parameters using scipy optimize and Nelder-Mead algorithm.</span></p>
    <p class="c0"><span style="overflow: hidden; display: inline-block; margin: 0.00px 0.00px; border: 0.00px solid #000000; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px); width: 413.50px; height: 280.25px;"><img alt="" src="images/image1.png" style="width: 413.50px; height: 280.25px; margin-left: 0.00px; margin-top: 0.00px; transform: rotate(0.00rad) translateZ(0px); -webkit-transform: rotate(0.00rad) translateZ(0px);" title=""></span></p>
    <p class="c1"><span class="c3"></span></p>
    <p class="c0"><span>As previously mentioned, we used a combination of two Twitter datasets. These datasets captured tweets that contain keyword</span><span>s such as &ldquo;coronavirus&rdquo;, &ldquo;2019nCoV&rdquo;, or hashtags such as &ldquo;#covid19&rdquo;, &ldquo;#corona</span><span class="c12">virus&rdquo;</span><span>. The first dataset obtained from Kaggle contained a column with the plain text of the tweet. We were able to pull this data into the Data Science servers of the University of Waterloo, which is a distributed systems cluster. We put the large file in Hadoop File System, and ran an Apache Spark application to compute the top bigrams per day in a parallel fashion. We then removed the most </span><span>common English stop words</span><span>&nbsp;from our top bigrams to finalize our list of top bigrams. However, the Kaggle dataset contained tweets from March 4th to March 28th. This led us to gather additional data from </span><span class="c4"><a class="c8" href="https://www.google.com/url?q=https://github.com/thepanacealab/covid19_twitter/blob/master/www.panacealab.org&amp;sa=D&amp;ust=1587439427202000">Panacea Lab</a></span><span>s, which contained tweets from </span><span>March 12th</span><span class="c3">&nbsp;to April 19th. Moreover, this dataset had already processed the top bigrams per day.</span></p>
    <p class="c0 c2"><span class="c3"></span></p>
    <p class="c0"><span class="c3">To adjust the predictions based on our data analysis, we came up with the following.</span></p>
    <p class="c0 c2"><span class="c3"></span></p>
    <p class="c0"><span class="c3">def calc_multiplier(ranking):</span></p>
    <p class="c0"><span class="c3">&nbsp; &nbsp; # Ranking from 10 days ago</span></p>
    <p class="c0"><span class="c3">&nbsp; &nbsp; return (1001 - ranking) &nbsp;/ 100000</span></p>
    <p class="c0 c2"><span class="c3"></span></p>
    <p class="c7"><span class="c3">Mutliplier = 1 - a*calc_multiplier(sign petition) - b*calc_multiplier(stay home)</span></p>
    <p class="c0"><span class="c3">+ c*calc_multiplier(herd immunity) - d*calc_mutliplier(contact tracing)</span></p>
    <p class="c1"><span class="c3"></span></p>
    <p class="c1"><span class="c3"></span></p>
    <p class="c0"><span class="c3">The formula to calculate the new prediction is:</span></p>
    <p class="c0"><span class="c3">New_pred = old_pred * multiplier</span></p>
    <p class="c0 c2"><span class="c3"></span></p>
    <p class="c2 c10"><span class="c3"></span></p>
    <p class="c0"><span class="c3">This formula calculates the multiplier given a rank of a bigram. For example, if the bigram&rsquo;s rank is 1, then our formula would calculate to 0.01 (ie. 1%). This multiplier is then used to adjust our predictions.</span></p>
    <p class="c0 c2"><span class="c3"></span></p>
    <p class="c0"><span class="c3">It is important to note that we use the rankings 10 days before the day we are predicting. For example, if we are predicting for April 11th, then we would be using rankings from April 1st. We calculated this number from adding 5 to 6 days of incubation period to the 3 to 4 days for a test result to be confirmed as positive.</span></p>
    <p class="c0 c2"><span class="c3"></span></p>
    <p class="c0"><span class="c3">As for the multiplier equation; if a &ldquo;negative&rdquo; bigram yields a 1% multiplier, then we would add this multiplier and end up with a 1% increase towards our prediction. If a &ldquo;positive&rdquo; bigram yields a 1% multiplier, then we would subtract this multiplier and end up with a 1% decrease towards our prediction. This is because we think that &ldquo;positive&rdquo; bigrams are a major factor in spreading awareness, which then affects the spread of COVID 19. Thus, lowering the predicted number of cases. And vice versa for &ldquo;negative&rdquo; bigrams.</span></p>
    <p class="c0 c2"><span class="c3"></span></p>
    <p class="c7"><span class="c9 c6">Results</span></p>
    <p class="c0 c2"><span class="c3"></span></p>
    <p class="c0"><span class="c3">We added the parameters a,b,c,d because we found that high ranking bigrams, such as &ldquo;stay home&rdquo;, had too much of an influence that all the other bigrams did not matter. To find the optimal parameters, we tried all permutations from values 1 to 5. The most optimal parameter values are: a = 1, b = 1, c = 5. d = 4. Values a = 1, b = 1, c = 5, d = 5 also had the same results. These values adjusted the predictions so that it was closer to the actual number of cases by 50%. The more accurate values are highlighted in yellow. Once we found these values, we used this to adjust our predictions for the following week.</span></p>
    <p class="c0 c2"><span class="c3"></span></p>
    <p class="c1"><span class="c3"></span></p>
    <p class="c0"><span class="c3">For our pandemic end date prediction, we apply the same adjustments, with the multipliers scaled by 10 and the multiplier is based on the average of rankings. This is due to not being able to apply the 10 days incubation period since the pandemic end date is ambiguous.</span></p>
    <p class="c0 c2"><span class="c3"></span></p>
    <p class="c0"><span class="c3">Because we maximized the parameters (a,b,c,d) to fit the given data as much as possible, we fear that we are overfitting our model. One way we could solve this issue is to choose a less accurate set of parameters so that our adjustments are more generalized.</span></p>
    <p class="c7"><span class="c3">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></p>
    <p class="c7"><span class="c6">Prediction</span></p>
    <p class="c0 c2"><span class="c3"></span></p>
    <p class="c0"><span>Based on our model, we predict that this pandemic will last 267 days from January 22nd, which is Tuesday October 15, 2020, with a total of 63353 cases. For the bonus part of this project, we predict there will be </span><span>5716</span><span>&nbsp;new cases of COVID-19 in Canada in the first week of May (1-7 inclusive), </span><span>9794</span><span>&nbsp;new cases in the first two weeks of May (1-14 inclusive), and</span><span class="c15">&nbsp;</span><span>16125</span><span class="c3">&nbsp;in the month of May (1-31 inclusive).</span></p>
    <p class="c1"><span class="c3"></span></p>
    <p class="c0"><span class="c3">By the time you are watching this video, we are no longer undergrad students. So professor, if you need a hand in research or something, feel free to let us know. Thanks for watching our video. Please smash that like button and subscribe to our channel.</span></p>
    <p class="c0 c2"><span class="c3"></span></p>
    <p class="c7"><span class="c9 c6">Links</span></p>
    <p class="c7"><span>Github: </span><span class="c4"><a class="c8" href="https://www.google.com/url?q=https://github.com/thepanacealab/covid19_twitter&amp;sa=D&amp;ust=1587439427208000">https://github.com/thepanacealab/covid19_twitter</a></span></p>
    <p class="c7"><span>Kaggle: </span><span class="c4"><a class="c8" href="https://www.google.com/url?q=https://www.kaggle.com/smid80/coronavirus-covid19-tweets&amp;sa=D&amp;ust=1587439427208000">https://www.kaggle.com/smid80/coronavirus-covid19-tweets</a></span></p>
    <p class="c7"><span>English Stop Words: </span><span class="c4"><a class="c8" href="https://www.google.com/url?q=https://gist.github.com/sebleier/554280&amp;sa=D&amp;ust=1587439427208000">https://gist.github.com/sebleier/554280</a></span></p>
    <p class="c7"><span>Social distancing image source: </span><span class="c4"><a class="c8" href="https://www.google.com/url?q=https://www.safetyandhealthmagazine.com/articles/19578-covid-19-pandemic-tips-to-remain-sane-and-safe-during-social-distancing&amp;sa=D&amp;ust=1587439427209000">https://www.safetyandhealthmagazine.com/articles/19578-covid-19-pandemic-tips-to-remain-sane-and-safe-during-social-distancing</a></span></p>
    <p class="c7"><span>Hashtags image source: </span><span class="c4"><a class="c8" href="https://www.google.com/url?q=https://assets.cureus.com/uploads/figure/file/102058/lightbox_5c40f7a05f5211eaa2905ba8f2f4e909-Figure1.png&amp;sa=D&amp;ust=1587439427209000">https://assets.cureus.com/uploads/figure/file/102058/lightbox_5c40f7a05f5211eaa2905ba8f2f4e909-Figure1.png</a></span></p>
    <p class="c7"><span class="c3">Overfitting image source: http://data-mining.philippe-fournier-viger.com/some-funny-pictures-related-to-data-mining/overfitting/</span></p>
    <p class="c7"><span class="c3">Graduation Cap Throw image source:</span></p>
    <p class="c7"><span class="c4"><a class="c8" href="https://www.google.com/url?q=https://veryfunnypics.eu/to-all-you-high-school-graduates-out-there/&amp;sa=D&amp;ust=1587439427210000">https://veryfunnypics.eu/to-all-you-high-school-graduates-out-there/</a></span><span class="c3"><br></span></p>
    <p class="c7"><span class="c3">Predictions</span></p>
    <p class="c7"><span class="c3">End date: Tuesday, October 15, 2020. Total case number of 63353.</span></p>
    <p class="c7"><span class="c3">First week of May: 5716 cases.</span></p>
    <p class="c7"><span class="c3">Second week of May: 9794 cases.</span></p>
    <p class="c7"><span class="c3">Month of May: 16125 cases.</span></p>
    <p class="c1"><span class="c3"></span></p>
</body>
</html>