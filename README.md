Flickr Diversity Search
=======================
Building a Test Collection for Image Search Result Diversity in Flickr


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
	|   |	└── query_categorization.json
	|   |
	|	|──
	|	|
	|   
	├── README.md
	└── LICENSE


JSON Schema for `query_data.json`
----------------------------------

	@object(2) {											\\ top-level object
		"about": @object(2) {								\\ about object
			"query": "string",								\\ query name 
			"date": "string"								\\ standard date format, when is the data was queried
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


JSON Schema for `query_categorization.json`
---------------------------------------------

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


Queries and Statistics in the test collection
----------------------------------------------
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
    <td></td>
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
				<td>junk</td>
				<td>42</td>
			</tr>
		</table>
    </td>
  </tr>
  <tr>
    <td>3</td>
    <td>david</td>
    <td>347</td>
    <td></td>
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
				<td>junk</td>
				<td>141</td>
			</tr>
		</table>
    </td>
  </tr>
  <tr>
    <td>5</td>
    <td>greyhound</td>
    <td>415</td>
    <td></td>
  </tr>
  <tr>
    <td>6</td>
    <td>indian</td>
    <td>375</td>
    <td></td>
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
				<td>sports team</td>
				<td>0</td>
			</tr>
			<tr>
				<td>band (music)</td>
				<td>0</td>
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
				<td>junk</td>
				<td>19</td>
			</tr>
		</table>
    </td>
  </tr>
  <tr>
    <td>8</td>
    <td>java</td>
    <td>438</td>
    <td></td>
  </tr>
  <tr>
    <td>9</td>
    <td>kings</td>
    <td>414</td>
    <td></td>
  </tr>
  <tr>
    <td>10</td>
    <td>oasis</td>
    <td>426</td>
    <td></td>
  </tr>
  <tr>
    <td>11</td>
    <td>queen</td>
    <td>442</td>
    <td></td>
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
				<td>Saturn Girl</td>
				<td>5</td>
			</tr>
			<tr>
				<td>Saturn V Spacecraft</td>
				<td>16</td>
			</tr>
			<tr>
				<td>Saturn Painting</td>
				<td>2</td>
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
				<td>astrophotography</td>
				<td>47</td>
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
				<td>197</td>
			</tr>
			<tr>
				<td>junk</td>
				<td>37</td>
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
				<td>submarine</td>
				<td>7</td>
			</tr>
			<tr>
				<td>Vehicle or Vessel</td>
				<td>17</td>
			</tr>
			<tr>
				<td>Military Unit</td>
				<td>0</td>
			</tr>
			<tr>
				<td>Video game</td>
				<td>0</td>
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
				<td>junk</td>
				<td>111</td>
			</tr>
		</table>
    </td>
  </tr>
  <tr>
    <td>14</td>
    <td>seal</td>
    <td>410</td>
    <td></td>
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
				<td>Spider Robots</td>
				<td>2</td>
			</tr>
			<tr>
				<td>Spider by LEGO</td>
				<td>4</td>
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
				<td>junk</td>
				<td>30</td>
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
				<td>junk</td>
				<td>15</td>
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
		</table> -->
</table>
