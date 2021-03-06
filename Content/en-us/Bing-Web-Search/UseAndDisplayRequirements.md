<!-- 
NavPath: Bing Web Search API
LinkLabel: Bing Web Search Use and Display Requirements
Weight: 10
Url: Bing-web-search-API/useanddisplayrequirements
-->

# Bing Search API Use and Display Requirements
These use and display requirements apply to your implementation of the content and associated information (for example, relationships, metadata and other signals) available through calls to the Bing Web Search, Image Search, Video Search, and News Search APIs, Bing Spell Check and Bing Autosuggest APIs. Implementation details related to these requirements can be found in documentation for specific features and results.

BING SPELL CHECK API and BING AUTOSUGGEST API.  You must not:

� copy, store, or cache any data you receive from the Bing Spell Check or Bing Autosuggest APIs; or
use data you receive from the Bing Spell Check or Bing Autosuggest APIs as part of any machine learning or similar algorithmic activity to train, evaluate, or improve new or existing services which you or third parties may offer.

� use data you receive from the Bing Spell Check or Bing Autosuggest APIs as part of any machine learning or similar algorithmic activity to train, evaluate, or improve new or existing services which you or third parties may offer.

BING WEB SEARCH, IMAGE SEARCH, NEWS SEARCH and VIDEO SEARCH APIs (the �Search APIs�):

Definitions. The following definitions apply in Sections 2 through 5 of these use and display requirements:
�answer� refers to a category of results returned in a response. For example, a response from the Bing Web Search API may include answers in the categories of webpage results, image, video, and news;
�response� means any and all answers and associated data received in response to a single call to a Search API;
�result� refers to an item of information in an answer.  For example, the set of data connected with a single news article is a result in a news answer.
Internet search experience. All data returned in responses may only be used in Internet search experiences. An Internet search experience means the content displayed, as applicable:

� is relevant and responsive to the end user�s direct query or other indication of the user�s search interest and intent (e.g., user-indicated search query); 

� helps users find and navigate to the sources of data (e.g., the provided URLs are implemented as hyperlinks so the content or attribution is a clickable link conspicuously displayed with the data); 

� includes multiple results for the end user to select from (e.g., several results from the news answer are displayed, or all results if fewer than several are returned); 

� is limited to an amount appropriate to serve the search purpose (e.g., image thumbnails are thumbnail-sized in proportion to the user�s display); 

� includes visible indication to the end user that the content is Internet search results (e.g., a statement that the content is �From the web�); and

� includes any other combination of measures appropriate to ensure your use of data received from the Search APIs does not violate any applicable laws or third party rights.  Please consult your legal advisors to determine what measures may be appropriate.

General. You must not: 

� copy, store, or cache any data from responses (except retention to the extent permitted by the �Continuity of Service� section below); 

� modify content of results (other than to reformat them in a way that does not violate any other requirement); 

� omit attribution and URLs associated with result content;

� re-order (including by omission) results displayed in an answer when an order or ranking is provided;

� display other content within any part of a response in a way that would lead an end user to believe that the other content is part of the response; 

� display advertising that is not provided by Microsoft on any page that displays any part of a response;

� use data received from the Search APIs as part of any machine learning or similar algorithmic activity to train, evaluate, or improve new or existing services which you or third parties may offer.

3. Advertising. Advertising (whether provided by Microsoft or another provider) must not be displayed with responses (i) from the Image, News or Video Search APIs; or (ii) that are filtered or limited primarily (or solely) to image, news and/or video results from other Search APIs.

4. Branding. You will attribute each response (or portion of a response) displayed to Microsoft as described in https://go.microsoft.com/fwlink/?linkid=833278, unless Microsoft specifies otherwise in writing for your particular use.

5. Continuity of Service.  You must not copy, store or cache any data from responses. However, to enable continuity of service access and data rendering, you may retain results solely under the following conditions:

Device.  You may enable an end user to retain results on a device for the lesser of (i) 24 hours from the time of the query or (ii) until an end user submits another query for updated results, provided that retained results may be used only:

� to enable the end user to access results previously returned to that end user on that device (e.g., in case of service interruption); or

� to store results returned for your proactive query personalized in anticipation of the end user�s needs based on that end user�s signals (e.g., in case of anticipated service interruption).

Server.  You may retain results specific to a single end user securely on a server you control and display the retained results only:

� to enable the end user to access a historical report of results previously returned to that user in your solution, provided that the results may not be (i) retained for more than 21 days from the time of the end user�s initial query and (ii) displayed in response to an end user�s new or repeated query; or

� to store results returned for your proactive query personalized in anticipation of an end user�s needs based on that end user�s signals for the lesser of (i) 24 hours from the time of the query or (ii) until an end user submits another query for updated results.

Whenever retained, results for a specific user cannot be commingled with results for another user, i.e., the results of each user must be retained and delivered separately.

General. For all presentation of retained results, you must:

� include a clear, visible notice of the time the query was sent,

� present the user a button or similar means to re-query and obtain updated results, 

� retain the Bing branding in the presentation of the results, and

� delete (and refresh with a new query if needed) the stored results within the timeframes specified.