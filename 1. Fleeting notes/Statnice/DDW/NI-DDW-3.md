**Analýza chování uživatelů na webu: sběr dat a metriky, typy doporučovacích systémů, jejich evaluace, výhody a nevýhody.**

# Web Usage
- Discover usage patterns
- Extract useful information from logs
- Find interests of users

1. Data collection + Preprocessing
2. Pattern discovery
3. Pattern analysis

## Input Data
Main source: **server logs** containing: time, IP, resource + parameters, status, method, user agent, headers, cookies
Other sources: content data (html, images), structure data (links, structure of website), user data (user profile, demographics)

## Collecting
- Explicit
	- = filling forms, questionnaires, ratings, ...
	- simplest
	- high quality
	- privacy concerns
	- low amount
	- low motivation for users
- Implicit
	- inferring information from user interactions
	- = clicks, interactions, accessing, gesture, posture, eye tracking, ...
	- non-invasive way
	- difficulty interpreting
	- privacy issues (monitoring users)

## Implicit tracking
- Web/Search logs
	- Limited information
- Proxy servers
	- Complex data
- TCP/IP sniffers
	- Very limited
- Browser/Desktop agents
	- eye tracking, ...
	- requires user installation
- Client-side trackers
	- most popular
	- complex data
	- no requirements on the user
### Client-side trackers
We collect data such as:
- domain
- user id (created on first visit)
- referral (how did they come - search term, campaign, ...)
- referrer (where did they come from - google)
- User-Agent

We can use cookies to preserve data across different page views:
- session cookie
- request rate cookie
- user id cookie

We can also transfer data to a server by having an invisible 1x1 img that will send a GET request with the data in query strings. Or use CSS to inject content into HTML to trigger sending requests based on browser type, or some action.

#### Third-party cookies
There 1st party cookies used for storing preferences, data about session, user id/login information; these are set by the website we are accessing.

3rd party cookies are set by other elements on the website from a different domain and are used for tracking and ads.

1. Alice accesses `mywebsite.com`, there is an ad from `adcompany.com` through an iframe which she makes a request to load it, along the response `adcompany.com` sends a cookie.
2. Alice accesses `anotherwebsite.com`, which also uses ads from `adcompany.com` and the request to their endpoint is made again, but this time sending the cookie that was previously set. This way the user is tracker as they browse the internet.
This approach is has many downsides nowadays due to ad blockers, tracker blockers and browsers themselves blocking this behaviour.

## Preprocessing
- Data cleaning
	- Removing irrelevant items (wrong entries, crawler/spider entries)
- Identify the page/action
	- e.g. user just looking at the product vs user buying the product
- Identify the user
	- assigning a user ID to all entries
- Identify the session
	- identifying one user visit
- Path completion
	- inserting missing entries
	- there can be some outage/corruption and we miss entries
	- Algorithms:
		- fewest number of back references
		- identify some patterns from other user interactions

The result of preprocessing can be:
- Pageviews = {p1, p2, p3, ...}
	- Weights:
		- Binary (exists/doesn't exist)
		- Function of duration (time spent on each page)
		- Order of pages
- Transactions = {t1, t2, t3, ...}
	- Each transaction = <(p1, w(p1)), (p2, w(p2)), ...>
	- User-Pageview matrix = Transaction Matrix (**UPM**)
		- $t = (w_{p1}, w_{p2}, w_{p3}, ..., w_{pn})$ 
		- Columns are unique pages (page identifiers such as /A.html)
		- Rows are all the transactions $t_x$
	- Instead of working with page identifiers we can include further information (price of product on that page, keywords, content) or classify the page (product detail, navigation, general, ...)
		- Pageview-feature matrix (**PFM**):
			- $p = (fw(f_1), fw(f_2), fw(f_3), ..., fw(f_n))$
			- $fw(f_i)$ - weight of the feature i for each page
		- Content-enhanced transaction matrix (**TFM**):
			- same as PFM but rows are not pageviews but transactions
		- TFM = UPM * PFM
## Pattern Discovery
### Clustering
Finding clusters of users, pages. We can use standard clustering algorithms - kmeans.
Using cosine similarity
### Association Analysis
Finding groups of items/pages that accessed/purchased together.
Example: `/special-offers/ && /products/X -> /shopping-cart/`
- Association Rule:
	- X -> Y
	- X is an antecedent
	- Y is a consequent
- Metriky:
	- Support = fraction of transactions that contain both X and Y
	- Confidence = how often does Y appear in transaction that contain X
- {Milk, Diaper} -> {Beer}
	- support = |Milk, Diaper, Beer| / |T| = ...
	- confidence = |Milk, Diaper, Beer| / |Milk, Diaper| = ...
#### Apriori Algorithm
Parameters:
- Minimum support of rules
- Minimum confidence of rules

1. Generate set of items that have support above minimum support.
2. Take the set and generate rules that have confidence above minimum confidence.
![[Pasted image 20240519134856.png]]
## Web analytics
- Traffic analysis
	- page views
	- sessions
	- visitors
	- time on page
		- onbeforeunload event
		- visibility change - tab change
	- bounce rate
- E-commerce analysis
	- conversion, conversion rate
		- Outcomes/Unique visitors
		- Macro conversion
			- Submitted order
			- Registration to a newsletter
		- Micro conversion
			- Product ratings
			- Shopping basket operation
			- Dynamic content interactions
			- Video consumption
	- revenue
	- campaigns
	- impressions
	- click through rate
	- cost per click
# Recommender System
Systems for recommending items to users (too many items for users to browse through) based on their preferences. They improve user experience.

Information used to make recommendation:
- past user history - clicks, logs
- purchase data
- explicit feedback (ratings)
- comments on products
- demographic data
- context
- relations to other users
- item similarities

They are personalised - adapting to individual needs/preferences; assumptions:
- userA and userB are similar => userA is going to be interested in same things as userB
- itemA and itemB are similar => if userA likes itemA then he will like itemB

Types of recommender systems:
- Collaborative filtering
	- Recommend items that users that are similar like
	- Recommend items that are similar to items the user likes
- Content-based filtering
	- Recommend items based on their content
- Knowledge-based
	- Recommend items based on some context
	- Useful when we have limited information
- Hybrid
	- combine multiple approaches
## Collaborative Filtering
### User-Based CF
- Assumption: Users with similar taste in the past will have similar taste in the future.
- Method: Recommendations based on similarity of user preferences.
- Inputs: 
	- List of users, list of items
	- Associations between users and items
		- Explicit: rating
		- Implicit: watched, purchased, ...
- Steps:
	1. Identify relevant input data
		- Get ratings, likes, ...
	2. Identify users that are most similar to the active user
		- Compute the user-to-user similarity (based on their previous interactions with items)
	3. Identify items from these users
	4. Recommend them
	- Main problem - similarity between users
#### Similarities
##### Cosine Similarity
Cosine of the angles between two user vectors.
##### Pearson Similarity Metric
Computes correlated two vectors are.
1 = correlated
-1 = negatively correlated
### Predicting rating of an item
How do we take the similarity to predict the rating for an item of the active user?
**Pearson-weighted average of ratings:**
Raw rating prediction: $pred(a, b) = \frac{\sum_{b\in N} sim(a, b) \cdot r_b}{\sum_{b\in N} sim(a, b)}$
Raw rating prediction: $pred(a, b) = r_a \frac{\sum_{b\in N} sim(a, b) \cdot (r_{bp} - r_b)}{\sum_{b\in N} sim(a, b)}$
### Item-Based CF
We use similarity between items instead. It's more computationally difficult (\#users << \#items). The approach is the same as User-Based CF, same methods can be applied.
### Matrix Factorisation CF
Idea: discover latent factors (features that describe the items based on which the model recommends) of users and items and use them for recommendation.
![[Pasted image 20240519144434.png]]
- R = ratings matrix (m users, n items)
- P = user feature matrix (m users, f features/latent factors)
- W = item feature matrix (n items, f features/latent factors)
## Problems of CF
- Cold start
	- needs enough users in the system to make a prediction
- Sparsity
	- with the amount of items it might be hard to find users that have rated enough similar items
- First rater
	- new items (not rated) are not recommended
- Popularity bias
	- unique tastes are hard to recommend to
- Lack of transparency
	- recommendations are hard to explain
## Content-Based Filtering
Make recommendations based on analysing the content of the items.

1. Build a vector representation of each item based on their content.
2. Build a vector representation of the user profile.
3. Measure similarity between the user profile and the items.
4. Recommend the closest.

## Advantages
- No need for other user data
	- No cold start
	- No sparsity problem
- Tastes of unique users are met
- Can recommend new and popular items
- Can provide better explanation why item was recommended
## Disadvantages
- Content should be encoded as meaningful features
- Representing user profiles as vectors
- Problems with users with no history
- Does not exploit collective intelligence
- Easily can be random
- Easy to overfit
## Knowledge-Based
Good when other approaches are limited and when we have some prior knowledge that should be acted upon (time-sensitive events, explicit requirements). It requires some specific domain knowledge.

### Constraint-Based
Users specify constraints (usually lower and upper bounds), the system recommends items that satisfy the constraints.
### Case-Based
Specific cases are specified by the user (similarity metrics) that reduce the set of items.
## Other RS
- Context-sensitive
	- Provide some context for decision making (time, location, social information)
- Ensemble or Hybrid RS
	- Get results of multiple RS and combine the results with some weights
	- Switch between different modes
	- Cascade the results by inputting results of the previous RS to the next
	- Feature augmentation - input the features from one RS to the next
## Evaluation of RS
- offline
	- simulating user interactions
	- easy to overfit
- user study
	- small group of users to test on
	- expensive
- online
	- A/B testing
	- can be risky (testing in production)
## Attacks
CF is vulnerable by having bots/fake reviews.

