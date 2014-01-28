Test Collection for Image Search Result Diversity in Flickr
===========================================================

To create this test collection the following process was followed. First, a set of 30 ambiguous keyword queries were 
identified. Every query was manually annotated with the possible set of interpretations (categories). The keyword queries
and their possible interpretations is shown in `Table 1`. Next, the Flickr APIs were used to fetch the images and the 
related metadata for each query. This was done by utilizing the `flickr.photos.search` API. This API takes as input a query 
string and performs a free text search on Flickr images. Images who's title, description or tags matches the query terms are 
returned. Different Flickr APIs are then used to retrieve the relevant metadata for each image in the result set. Note 
while crawling images without tag or Flickr Group/photoset information were discarded. The number of images crawled for 
each query is shown under column titled `# of images` in `Table 1`.  For each query a resulting json file containing the 
crawled metadata is created. The schema of this json file is shown `Figure 1`.

Three human evaluators were then asked to label the resulting data set. Each human labeler was shown images from the query 
result set and was asked to label it with one of the categories associated with that query. The user was allowed to add 
additional categories if the situation required. Any image that was judged irrelevant or whose category label was not 
evident was assigned to the `other` category. Finally, ground truth category was determined by using a majority voting 
scheme. This labeling task was performed on all the 30 queries. The result of this categorization is stored in a separate 
json file the schema for which is shown in `Figure 2`.

##### Note: For every query two json files are created: 
<dl>
	<dt>query_data.json</dt>
	<dd>
		This file contains all the images related to the keyword query and all the relevant social tags associated with the images in the result set
	</dd>
		<dt>query_result_categorization.json</dt>
	<dd>
		This file contains the result of the categorization/labeling
	</dd>
</dl>
Both these files are stored in folders named after the query number (first column of `Table 1`).


Project Structure
------------------
	.
	├── queries
	|	|
	|	|──
	|	|
	|   ├──
	|   |
	|   ├── <query_name>
	|   |	├── query_data.json
	|   |	└── query_result_categorization.json
	|   |
	|	|──
	|	|
	|   
	├── README.md
	└── LICENSE


JSON Schema for `query_data.json`
----------------------------------

### Figure 1

	@object(2) {											\\ top-level object
		"about": @object(2) {								\\ about object
			"query": "string",								\\ query name 
			"date": "string"								\\ date when the query was crawled
		},
		"data": @array [									\\ data object, list of objects for each photo
			@object(11) {									\\ object for an photo
				"id": "string",								\\ photo ID in flickr
				"photo_physical": "string",					\\ url of photo in jpg format of size medium 640
				"photo_web_url": "string",					\\ url of photo page in flickr
				"photo_tags": @array [						\\ list of tags of the photo in flickr 
					"string"
				],
				"photo_owner": @object(3) {					\\ details of the owner of the photo
					"owner": "string",
					"username": "string",
					"realname": "string"
				},
				"photo_metadata": @object(2) {				\\ metadata of photo in flickr
					"title": "string",
					"description": "string"
				},
				"owner_groups": @array [					\\ list of groups the owner is a member of
					@object(2) {
						"nsid": "string",					
						"name": "string"
					}
				],
				"photoset": @array [						\\ list of visible photosets to which the photo belongs to
					@object(4) {
						"id": "string",						\\ ID of photoset
						"title": "string",					\\ title of photoset
						"photoset_web_url": "string",		\\ url of photoset in flickr
						"top_tags": @array [				\\ most frequent tags from first 50 photos in photoset (atmost 20)
							"string"
						]
					}
				],
				"photogroup": @array [						\\ list of visible flickr photogroups to which the photo belongs to
					@object(3) {
						"id": "string",						\\ ID of photogroup
						"title": "string",					\\ title of photogroup
						"photogroup_web_url": "string"		\\ url of photogroup in flickr
					}
				],
				"photo_comment": @array [					\\ list of comments for the photo
					@object(3) {
						"id": "string",						\\ ID of comment
						"author_id": "string",				\\ ID of author of the comment
						"date": "string"					\\ timestamp when comment was posted
					}
				],
				"photo_favourite": @array [					\\ list of people who have favorited the photo
					@object(3) {
						"nsid": "string",					\\ ID of user
						"username": "string",				\\ username of user
						"date": "string"					\\ timestamp of the action
					}
				]
			}	
		]
	}


JSON Schema for `query_result_categorization.json`
---------------------------------------------

### Figure 2

	@object(2) {											\\ top-level object
		"about": @object(1) {								\\ about object
			"query": "string"								\\ query name
		},
		"categorization": @array [							\\ categorization object
			@object(2) {									\\ object for a category
				"name": "string",							\\ category name
				"images": @array [							\\ list of photo IDs in the category
					"string"
				]
			}
		]
	}


Query Statistics
----------------------------------------------

### Table 1

<table>
  <tr>
    <th>#</th>
    <th>Query</th>
    <th># of images</th>
    <th>Categories</th>
  </tr>
  <tr>
    <td>1</td>
    <td>argos</td>
    <td>434</td>
    <td>
    	<table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td>Argos ancient city in Greece</td>
				<td>32</td>
			</tr>
			<tr>
				<td>Argo Racing Car</td>
				<td>23</td>
			</tr>
			<tr>
				<td><a href="http://en.wikipedia.org/wiki/Rail_transport_in_Indonesia" title="Rail transport in Indonesia" target="_blank">Argo train network</a></td>
				<td>31</td>
			</tr>
			<tr>
				<td><a href="http://en.wikipedia.org/wiki/Argo_Gold_Mine_and_Mill" title="Argo Gold Mine and Mill" target="_blank">Argo Gold Mine and Mill</a></td>
				<td>34</td>
			</tr>
			<tr>   
				<td><a href="http://en.wikipedia.org/wiki/Argo_(oceanography)" title="Argo (oceanography)" target="_blank">Argo (oceanography)</a></td>
				<td>14</td>
			</tr>
			<tr>
				<td>UK retailer</td>
				<td>126</td>
			</tr>
			<tr>
				<td>ben affleck movie</td>
				<td>17</td>
			</tr>
			<tr>
				<td>football team</td>
				<td>19</td>
			</tr>
			<tr>
				<td>oil company</td>
				<td>9</td>
			</tr>
			<tr>
				<td>others</td>
				<td>129</td>
			</tr>
		</table>
    </td>
  </tr>
  <tr>
    <td>2</td>
    <td>cardinal</td>
    <td>425</td>
    <td>
    	<table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td>cardinal flower</td>
				<td>5</td>
			</tr>
			<tr>
				<td>beetle</td>
				<td>7</td>
			</tr>
			<tr>
				<td>cardinal football team (NFL) - american football</td>
				<td>14</td>
			</tr>
			<tr>
				<td>official of the catholic church or church related</td>
				<td>15</td>
			</tr>
			<tr>
				<td>bird</td>
				<td>341</td>
			</tr>
			<tr>
				<td>professional baseball team</td>
				<td>1</td>
			</tr>
			<tr>
				<td>others</td>
				<td>42</td>
			</tr>
		</table>
    </td>
  </tr>
  <tr>
    <td>3</td>
    <td>david</td>
    <td>347</td>
    <td>
    	<table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td>David Silva (Spanish footballer)</td>
				<td>6</td>
			</tr>
			<tr>
				<td>David Coulthard (Formula One racing drive)</td>
				<td>6</td>
			</tr>
			<tr>
				<td>David (Michelangelo)</td>
				<td>11</td>
			</tr>
			<tr>
				<td>David Villa (Spanish footballer)</td>
				<td>9</td>
			</tr>
			<tr>
				<td>David Garrett (German pop and crossover violinist)</td>
				<td>27</td>
			</tr>
			<tr>
				<td>David Wright (American baseball player)</td>
				<td>9</td>
			</tr>
			<tr>
				<td>David Bowie (English musician)</td>
				<td>23</td>
			</tr>
			<tr>
				<td>David lynch (director)</td>
				<td>9</td>
			</tr>
			<tr>
				<td>David archuleta (singer, actor)</td>
				<td>39</td>
			</tr>
			<tr>
				<td>David beckham (UK footballer)</td>
				<td>21</td>
			</tr>
			<tr>
				<td>others</td>
				<td>187</td>
			</tr>
		</table>
    </td>
  </tr>
  <tr>
    <td>4</td>
    <td>eagle</td>
    <td>469</td>
    <td>
    	<table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td>eagle scout</td>
				<td>2</td>
			</tr>
			<tr>
				<td>traffic signal system</td>
				<td>6</td>
			</tr>
			<tr>
				<td>military aircraft</td>
				<td>11</td>
			</tr>
			<tr>
				<td>galaxy/star system</td>
				<td>11</td>
			</tr>
			<tr>
				<td>Sports team</td>
				<td>3</td>
			</tr>
			<tr>
				<td>Rock band</td>
				<td>2</td>
			</tr>
			<tr>
				<td>Automobile</td>
				<td>4</td>
			</tr>
			<tr>
				<td>bird</td>
				<td>289</td>
			</tr>
			<tr>
				<td>others</td>
				<td>141</td>
			</tr>
		</table>
    </td>
  </tr>
  <tr>
    <td>5</td>
    <td>greyhound</td>
    <td>415</td>
    <td>
    	<table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td><a href="http://brickmaniatoys.com/2013/12/03/m8-greyhound-light-armored-scout-car-a-super-premium-re-issue/" title="M8 Greyhound Light Armored Scout Car – A Super Premium Re-issue | Brickmania Blog" target="_blank">Greyhound Tank LEGO</a></td>
				<td>5</td>
			</tr>
			<tr>
				<td>Greyhound train</td>
				<td>5</td>
			</tr>
			<tr>
				<td>The Grumman Greyhound (cargo aircraft)</td>
				<td>3</td>
			</tr>
			<tr>
				<td>Greyhound long distance bus service and terminals</td>
				<td>279</td>
			</tr>
			<tr>
				<td>dog breed</td>
				<td>79</td>
			</tr>
			<tr>
				<td>others</td>
				<td>44</td>
			</tr>
		</table>
    </td>
  </tr>
  <tr>
    <td>6</td>
    <td>indian</td>
    <td>375</td>
    <td>
    	<table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td>Indian Gap School Texas</td>
				<td>13</td>
			</tr>
			<tr>
				<td>Indian Paintbrush Plant</td>
				<td>4</td>
			</tr>
			<tr>
				<td>Indian Summer Festival</td>
				<td>12</td>
			</tr>
			<tr>
				<td>bird specie</td>
				<td>34</td>
			</tr>
			<tr>
				<td>native american indian (red indian)</td>
				<td>37</td>
			</tr>
			<tr>
				<td>motorcyle brand</td>
				<td>62</td>
			</tr>
			<tr>
				<td>india related dance, food etc</td>
				<td>130</td>
			</tr>
			<tr>
				<td>others</td>
				<td>83</td>
			</tr>
		</table>
    </td>
  </tr>
  <tr>
    <td>7</td>
    <td>jaguar</td>
    <td>429</td>
    <td>
    	<table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td>animal</td>
				<td>136</td>
			</tr>
			<tr>
				<td>car</td>
				<td>271</td>
			</tr>
			<tr>
				<td>military aircraft</td>
				<td>3</td>
			</tr>
			<tr>
				<td>others</td>
				<td>19</td>
			</tr>
		</table>
    </td>
  </tr>
  <tr>
    <td>8</td>
    <td>java</td>
    <td>438</td>
    <td>
    	<table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td>Insects at Java indonesia island</td>
				<td>28</td>
			</tr>
			<tr>
				<td>Java plum</td>
				<td>11</td>
			</tr>
			<tr>
				<td>Java Sparrow</td>
				<td>42</td>
			</tr>
			<tr>
				<td>java Indonesia island</td>
				<td>160</td>
			</tr>
			<tr>
				<td>coffee</td>
				<td>29</td>
			</tr>
			<tr>
				<td>Java (including javascript) programming language related</td>
				<td>8</td>
			</tr>
			<tr>
				<td>others</td>
				<td>160</td>
			</tr>
		</table>
    </td>
  </tr>
  <tr>
    <td>9</td>
    <td>kings</td>
    <td>414</td>
    <td>
    	<table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td>Places having name - kings (general)</td>
				<td>39</td>
			</tr>
			<tr>
				<td>King-Vulture</td>
				<td>7</td>
			</tr>
			<tr>
				<td>King penguins</td>
				<td>10</td>
			</tr>
			<tr>
				<td>Tank / Lego Tank</td>
				<td>7</td>
			</tr>
			<tr>
				<td>King Abdulaziz Endowment</td>
				<td>6</td>
			</tr>
			<tr>
				<td>King American Ambulance company</td>
				<td>9</td>
			</tr>
			<tr>
				<td>King County, Washington</td>
				<td>6</td>
			</tr>
			<tr>
				<td>Kings of Leon Rock band</td>
				<td>19</td>
			</tr>
			<tr>
				<td>The Red Devils - blues band</td>
				<td>27</td>
			</tr>
			<tr>
				<td>London Kings Cross railway station</td>
				<td>22</td>
			</tr>
			<tr>
				<td>King Cobra</td>
				<td>12</td>
			</tr>
			<tr>
				<td>royal family (general)</td>
				<td>51</td>
			</tr>
			<tr>
				<td>kings college</td>
				<td>32</td>
			</tr>
			<tr>
				<td>others</td>
				<td>167</td>
			</tr>
		</table>
    </td>
  </tr>
  <tr>
    <td>10</td>
    <td>oasis</td>
    <td>426</td>
    <td>
    	<table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td>Oasis Monorail</td>
				<td>6</td>
			</tr>
			<tr>
				<td>Oasis of the Seas (Cruise Ship)</td>
				<td>155</td>
			</tr>
			<tr>
				<td>airlines</td>
				<td>6</td>
			</tr>
			<tr>
				<td>desert oasis (vegetation in desert)</td>
				<td>91</td>
			</tr>
			<tr>
				<td>rock band</td>
				<td>95</td>
			</tr>
			<tr>
				<td>others</td>
				<td>73</td>
			</tr>
		</table>
    </td>
  </tr>
  <tr>
    <td>11</td>
    <td>queen</td>
    <td>442</td>
    <td>
    	<table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td>Flowers</td>
				<td>11</td>
			</tr>
			<tr>
				<td>Places having name - queen (general)</td>
				<td>71</td>
			</tr>
			<tr>
				<td>Queen Anne plant</td>
				<td>12</td>
			</tr>
			<tr>
				<td>Queen Butterfly</td>
				<td>21</td>
			</tr>
			<tr>
				<td>Queens of Noise - Musical Album - American rock band The Runaways</td>
				<td>20</td>
			</tr>
			<tr>
				<td>Queens New York City</td>
				<td>22</td>
			</tr>
			<tr>
				<td>Queens of the Stone Age - an American rock band</td>
				<td>10</td>
			</tr>
			<tr>
				<td>Queen Farida</td>
				<td>8</td>
			</tr>
			<tr>
				<td>Queenadreena  - an English alternative rock</td>
				<td>4</td>
			</tr>
			<tr>
				<td>queen monarch (UK)</td>
				<td>57</td>
			</tr>
			<tr>
				<td>queen bee</td>
				<td>9</td>
			</tr>
			<tr>
				<td>ships</td>
				<td>88</td>
			</tr>
			<tr>
				<td>rock band</td>
				<td>6</td>
			</tr>
			<tr>
				<td>others</td>
				<td>103</td>
			</tr>
		</table>
    </td>
  </tr>
  <tr>
    <td>12</td>
    <td>saturn</td>
    <td>422</td>
    <td>
    	<table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td>Saturn V Spacecraft</td>
				<td>16</td>
			</tr>
			<tr>
				<td>ship</td>
				<td>7</td>
			</tr>
			<tr>
				<td>Sega Saturn Video Game Console</td>
				<td>2</td>
			</tr>
			<tr>
				<td>god : roman mythology</td>
				<td>4</td>
			</tr>
			<tr>
				<td>car</td>
				<td>105</td>
			</tr>
			<tr>
				<td>planet Saturn</td>
				<td>244</td>
			</tr>
			<tr>
				<td>others</td>
				<td>44</td>
			</tr>
		</table>
    </td>
  </tr>
  <tr>
    <td>13</td>
    <td>scorpion</td>
    <td>462</td>
    <td>
    	<table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td>scorpion fly</td>
				<td>39</td>
			</tr>
			<tr>
				<td>Vehicle or Vessel</td>
				<td>24</td>
			</tr>
			<tr>
				<td>Heavy metal band</td>
				<td>131</td>
			</tr>
			<tr>
				<td>Fish</td>
				<td>11</td>
			</tr>
			<tr>
				<td>Animal</td>
				<td>146</td>
			</tr>
			<tr>
				<td>others</td>
				<td>111</td>
			</tr>
		</table>
    </td>
  </tr>
  <tr>
    <td>14</td>
    <td>seal</td>
    <td>410</td>
    <td>
    	<table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td>Seal (musician)</td>
				<td>8</td>
			</tr>
			<tr>
				<td><a href="http://en.wikipedia.org/wiki/Seal_Rock" title="Seal Rock" target="_blank">Seal Rocks</a></td>
				<td>30</td>
			</tr>
			<tr>
				<td>Seal Beach Pier</td>
				<td>11</td>
			</tr>
			<tr>
				<td>seal (emblem)</td>
				<td>12</td>
			</tr>
			<tr>
				<td>navy seal (special ops unit)</td>
				<td>15</td>
			</tr>
			<tr>
				<td>animal</td>
				<td>296</td>
			</tr>
			<tr>
				<td>others</td>
				<td>38</td>
			</tr>
		</table>
    </td>
  </tr>
  <tr>
    <td>15</td>
    <td>spider</td>
    <td>412</td>
    <td>
    	<table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td>Spider Lily and Plants</td>
				<td>8</td>
			</tr>
			<tr>
				<td>spider's web</td>
				<td>35</td>
			</tr>
			<tr>
				<td>movie character</td>
				<td>4</td>
			</tr>
			<tr>
				<td>automobile</td>
				<td>4</td>
			</tr>
			<tr>
				<td>insect</td>
				<td>325</td>
			</tr>
			<tr>
				<td>others</td>
				<td>36</td>
			</tr>
		</table> 
    </td>
  </tr>
  <tr>
    <td>16</td>
    <td>triumph</td>
    <td>392</td>
    <td>
    	<table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td>Triumph Fashion Show</td>
				<td>6</td>
			</tr>
			<tr>
				<td>Cars</td>
				<td>182</td>
			</tr>
			<tr>
				<td>Motorcycles</td>
				<td>189</td>
			</tr>
			<tr>
				<td>others</td>
				<td>15</td>
			</tr>
		</table>
    </td>
  </tr>
  <tr>
  	<td>17</td>
  	<td>giant</td>
  	<td>408</td>
  	<td>
  		<table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td>Giant Redwood</td>
				<td>6</td>
			</tr>
			<tr>
				<td>Giant Statues/Sculptures/Structures (general)</td>
				<td>24</td>
			</tr>
			<tr>
				<td>Giant Food (supermarket chain)</td>
				<td>10</td>
			</tr>
			<tr>
				<td>Giant Pacific octopus</td>
				<td>5</td>
			</tr>
			<tr>
				<td>Giant Cuttlefish</td>
				<td>5</td>
			</tr>
			<tr>
				<td>Giant anteater</td>
				<td>9</td>
			</tr>
			<tr>
				<td><a href="http://en.wikipedia.org/wiki/Camera_Obscura_(San_Francisco,_California)" title="Camera Obscura (San Francisco, California)" target="_blank">Camera Obscura (San Francisco, California)</a></td>
				<td>3</td>
			</tr>
			<tr>
				<td>Giant Squid</td>
				<td>3</td>
			</tr>
			<tr>
				<td>The Giant’s Causeway (Ireland)</td>
				<td>39</td>
			</tr>
			<tr>
				<td>giant swallowtail - butterfly specie</td>
				<td>28</td>
			</tr>
			<tr>
				<td>giant bike company</td>
				<td>21</td>
			</tr>
			<tr>
				<td>giant panda</td>
				<td>16</td>
			</tr>
			<tr>
				<td>giant schnauzer (dog breed)</td>
				<td>42</td>
			</tr>
			<tr>
				<td>baseball team</td>
				<td>7</td>
			</tr>
			<tr>
				<td>others</td>
				<td>190</td>
			</tr>
		</table>
  	</td>
  </tr>
  <tr>
  	<td>18</td>
  	<td>tesla</td>
  	<td>387</td>
  	<td>
  		<table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td>Nikola Tesla (Scientist)</td>
				<td>8</td>
			</tr>
			<tr>
				<td>Tesla Coil</td>
				<td>32</td>
			</tr>
			<tr>
				<td>Tesla Motors</td>
				<td>266</td>
			</tr>
			<tr>
				<td>american hard rock band</td>
				<td>26</td>
			</tr>
			<tr>
				<td>others</td>
				<td>55</td>
			</tr>
		</table>
  	</td>
  </tr>
  <tr>
  	<td>19</td>
  	<td>tiger</td>
  	<td>417</td>
  	<td>
  		<table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td>Tiger Stadium</td>
				<td>4</td>
			</tr>
			<tr>
				<td>Common Tiger (butterfly)</td>
				<td>11</td>
			</tr>
			<tr>
				<td>Oncilla (tiger cat)</td>
				<td>14</td>
			</tr>
			<tr>
				<td>tiger bettle (insect)</td>
				<td>5</td>
			</tr>
			<tr>
				<td>tiger lilly (flower)</td>
				<td>7</td>
			</tr>
			<tr>
				<td>buses</td>
				<td>6</td>
			</tr>
			<tr>
				<td>tiger shark</td>
				<td>17</td>
			</tr>
			<tr>
				<td>tiger airlines</td>
				<td>1</td>
			</tr>
			<tr>
				<td>military tank</td>
				<td>8</td>
			</tr>
			<tr>
				<td>golfer tiger-woods</td>
				<td>10</td>
			</tr>
			<tr>
				<td>animal</td>
				<td>289</td>
			</tr>
			<tr>
				<td>others</td>
				<td>45</td>
			</tr>
		</table>
  	</td>
  </tr>
  <tr>
  	<td>20</td>
  	<td>prince</td>
  	<td>424</td>
  	<td>
  		<table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td>Prince Poppycock (singer)</td>
				<td>31</td>
			</tr>
			<tr>
				<td>The Prince of Wales</td>
				<td>11</td>
			</tr>
			<tr>
				<td>automobile</td>
				<td>5</td>
			</tr>
			<tr>
				<td>fictional/movie/animation character</td>
				<td>17</td>
			</tr>
			<tr>
				<td>place/city/street (location) e.g. prince ontario</td>
				<td>101</td>
			</tr>
			<tr>
				<td>prince (musician)</td>
				<td>48</td>
			</tr>
			<tr>
				<td>UK Royal Family</td>
				<td>108</td>
			</tr>
			<tr>
				<td>others</td>
				<td>103</td>
			</tr>
		</table>
  	</td>
  </tr>
  <tr>
  	<td>21</td>
  	<td>wilson</td>
  	<td>430</td>
  	<td>
  		<table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td>Mount Wilson</td>
				<td>15</td>
			</tr>
			<tr>
				<td>Wilsons Promontory National Park</td>
				<td>33</td>
			</tr>
			<tr>
				<td><a href="http://en.wikipedia.org/wiki/Wilson's_Storm_Petrel" title="Wilson's Storm Petrel" target="_blank">Wilson's Storm</a></td>
				<td>8</td>
			</tr>
			<tr>
				<td><a href="http://en.wikipedia.org/wiki/Wilson's_Snipe" title="Wilson's Snipe" target="_blank">Wilson's Snipe</a></td>
				<td>47</td>
			</tr>
			<tr>
				<td><a href="http://en.wikipedia.org/wiki/Wilson's_Phalarope" title="Wilson's Phalarope" target="_blank">Wilson's Phalarope</a></td>
				<td>27</td>
			</tr>
			<tr>
				<td>Wilson's Plover</td>
				<td>18</td>
			</tr>
			<tr>
				<td>Robert J. Wilson (Theater Director)</td>
				<td>3</td>
			</tr>
			<tr>
				<td>geographical location (mountain, city view etc)</td>
				<td>11</td>
			</tr>
			<tr>
				<td>president of USA</td>
				<td>49</td>
			</tr>
			<tr>
				<td>bird</td>
				<td>47</td>
			</tr>
			<tr>
				<td>others</td>
				<td>172</td>
			</tr>
		</table>
  	</td>
  </tr>

    	<!-- <table>
			<tr>
				<th>Category name</th>
				<th># of images</th>
			</tr>
			<tr>
				<td></td>
				<td></td>
			</tr>
			<tr>
				<td></td>
				<td></td>
			</tr>
			<tr>
				<td></td>
				<td></td>
			</tr>
			<tr>
				<td></td>
				<td></td>
			</tr>
			<tr>
				<td></td>
				<td></td>
			</tr>
			<tr>
				<td></td>
				<td></td>
			</tr>
		</table> 
		<a href="" title="" target="_blank"></a>
		-->
</table>
