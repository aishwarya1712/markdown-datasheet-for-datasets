# Datasheet: *Company Dataset*

Author: *Aishwarya Sriram*

Organization: *University of California, Berkeley*


## Motivation

*The questions in this section are primarily intended to encourage dataset creators to clearly articulate their reasons for creating the dataset and to promote transparency about funding interests.*

1. **For what purpose was the Company Dataset created?** Was there a specific task in mind? Was there a specific gap that needed to be filled? Please provide a description.

	The Company Dataset was created for companies and individuals to analyze over 29 million records[1] of company data. Though the specific usecase depends on the goals of the organization or the individual, there are a number of possible ways to use this dataset namely: sales & marketing, company prospecting, fraud prevention, identity resolution and investment research.

2. **Who created this dataset (e.g. which team, research group) and on behalf of which entity (e.g. company, institution, organization)**?

	This dataset was created by "People Data Labs" (PDL), a software company based on San Francisco, California, co-founded by Sean Thorne and Henry Nevue. The documentation does not specifically mention who was involved in collecting the data.

3. **What support was needed to make this dataset?** (e.g. who funded the creation of the dataset? If there is an associated grant, provide the name of the grantor and the grant name and number, or if it was supported by a company or government agency, give those details.)

	The PDL website acknowledges support from three venture capital firms: Craft Ventures, 8VC and Founders Fund[2].


## Composition

*Dataset creators should read through the questions in this section prior to any data collection and then provide answers once collection is complete. Most of these questions are intended to provide dataset consumers with the information they need to make informed decisions about using the dataset for specific tasks. The answers to some of these questions reveal information about compliance with the EU’s General Data Protection Regulation (GDPR) or comparable regulations in other jurisdictions.*

1. **What do the instances that comprise the dataset represent (e.g. documents, photos, people, countries)?** Are there multiple types of instances (e.g. movies, users, and ratings; people and interactions between them; nodes and edges)? Please provide a description.

	The Company Dataset is stored in an Elasticsearch database. Each instance corresponds to a company. Each company is stored as document in a collection. The company attributes are saved in the form of JSON key-value pairs.

	There is also a Person Dataset linked to the Company Dataset. Each record in the Person Dataset represents a person, an employee or a contact working at a company. 

3. **How many instances are there in total (of each type, if appropriate)?**

	There are 29 million unique records of companies in the Company Dataset.[1]
	There are 3 billion unique records of people in the Person Dataset.[3]

5. **Does the dataset contain all possible instances or is it a sample (not necessarily random) of instances from a larger set?** If the dataset is a sample, then what is the larger set? Is the sample representative of the larger set (e.g. geographic coverage)? If so, please describe how this representativeness was validated/verified. If it is not representative of the larger set, please describe why not (e.g. to cover a more diverse range of instances, because instances were withheld or unavailable).

	The Company Dataset is a sample of a larger dataset. According to [Statista (2023](https://www.statista.com/statistics/1260686/global-companies/)[4], there were 333.34 million companies in the world. This dataset contains 12 million of those companies. However, the selection criteria is unclear.

	The Person Dataset is also a sample of a larger dataset. 

7. **What data does each instance consist of?** "Raw" data (e.g. unprocessed text or images) or features? In either case, please provide a description.

	Each instance in the Company Dataset contains attributes like name, location, parents, subsidiaries, industry, number of employees, annual revenue of a company. The attributes have different data types: arrays, strings, numbers nad enumerations.[5]

 	Each instance in the Person Dataset contains attributes of the person's professional profile like: name, birthdate, linkedin url.[6]  

9. **Is there a label or target associated with each instance?** If so, please provide a description.

	Yes. Since each document consists of company attributes and their values in the form of JSON key-value pairs, the instances are well-labelled.
	
 These are all the possible labels[5] for the Company Dataset:

	affiliated_profiles  
	all_subsidiaries  
	alternative_domains  
	alternative_names  
	average_employee_tenure  
	average_tenure_by_level  
	average_tenure_by_role  
	direct_subsidiaries  
	employee_churn_rate  
	employee_count  
	employee_count_by_country  
	employee_count_by_month  
	employee_count_by_month_by_level  
	employee_count_by_month_by_role  
	employee_growth_rate  
	facebook_url  
	founded  
	gics_sector  
	gross_additions_by_month  
	gross_departures_by_month  
	headline  
	id  
	immediate_parent  
	industry  
	inferred_revenue  
	linkedin_id  
	linkedin_url  
	location  
	location.address_line_2  
	location.continent  
	location.country  
	location.geo  
	location.locality  
	location.metro  
	location.name  
	location.postal_code  
	location.region  
	location.street_address  
	mic_exchange  
	naics  
	naics.industry_group  
	naics.naics_code  
	naics.naics_industry  
	naics.national_industry  
	naics.sector  
	naics.sub_sector  
	name  
	profiles  
	recent_exec_departures  
	recent_exec_hires  
	sic  
	sic.industry_group  
	sic.industry_sector  
	sic.major_group  
	sic.sic_code  
	size  
	summary  
	tags  
	ticker  
	top_next_employers_by_role  
	top_previous_employers_by_role  
	top_us_employee_metros  
	twitter_url  
	type  
	ultimate_parent   

These are over 200 possible labels[6] in the Person Dataset. Here are some of the top labels:  

	birth_date  
	education  
	emails  
	experience  
	full_name  
	gender  
	industry  
	job_company_name  
	linkedin_url  
	mobile_phone  
	skills  
	street_address  
	work_email  

	
11. **Is any information missing from individual instances?** If so, please provide a description, explaining why this information is missing (e.g. because it was unavailable). This does not include intentionally removed information, but might include, e.g. redacted text.

	Yes, PDL acknolwedges that there can be missing values from individual instances. This is either because the data was not available or because the value is not applicable. For example, many companies are listed in the stock market, so they will not have a value for "ticker".

 	PDL also provides the exact percentage[7] of data that is filled for a certain attribute. Location for example has a fill of 84%, meaning 84% of the companies will have a value for location. For the remaining, it does not mean the company is not located anywhere. Rather, the data was unavailable.

 	The attributes with the least fill values (<1%) are: all_subsidiaries, direct_subsidiaries, gics, immediate_parent, mic_exchange, ticker, ultimate_parent.

	Similarly, there are missing values for the Person Dataset as well. 

13. **Are relationships between individual instances made explicit (e.g. users' movie ratings, social network links)?** If so, please describe how these relationships are made explicit.

	Yes, different companies in the Company Dataset can be linked together through the "affiliated_profiles" attribute. This attribute is an array data type, with each item in the array being a company id, which is either a parent or a subsidiary company. 

14. **Are there recommended data splits (e.g. training, development/validation, testing)?** If so, please provide a description of these splits, explaining the rationale behind them.

	Yes.

	There are recommended data splits, particularly in the Person Dataset, which PDL is calling "Slice" datasets.[8]
A slice is a subset of PDL's Person Dataset that contains every record with non-null value for a specific field. For example, the Email Slice Dataset contains every record from our Person Dataset with at least one non-null email address.

	1. All Dataset
	2. Resume Slice
	3. Email Slice
	4. Street Address Slice
	5. Consumer Social Slice
	6. Mobile Phone Slice
	7. Phone Slice
	8. Developer Slice

16. **Are there any errors, sources of noise, or redundancies in the dataset?** If so, please provide a description.

	Yes.

	Considering that PDL deals with very large volumes of data, they often deal with many records containing information about the same person. They refer to these as "Frankenstein profiles,"[9] where data from multiple individuals is merged into a single record, rendering it unusable and potentially causing issues with applications.

	Furthermore, for companies in the Company Dataset, there are overlaps among several attributes. For example: the affiliated_profiles attribute contains a list of company IDs that the current company is related to, either parent or subsidiaries. However, parent & subsidiary company IDs are also stored in separate attributes, leading to redundancy.
	

18. **Is the dataset self-contained, or does it link to or otherwise rely on external resources (e.g. websites, tweets, other datasets)?** If it links to or relies on external resources, a) are there guarantees that they will exist, and remain constant, over time; b) are there official archival versions of the complete dataset (i.e., including the external resources as they existed at the time the dataset was created); c) are there any restrictions (e.g. licenses, fees) associated with any of the external resources that might apply to a future user? Please provide descriptions of all external resources and any restrictions associated with them, as well as links or other access points, as appropriate.

	Yes. The dataset relies on external sources, namely the Data Union and the information available on the internet.[10] 

19. **Does the dataset contain data that might be considered confidential (e.g. data that is protected by legal privilege or by doctor-patient confidentiality, data that includes the content of individuals' non-public communications)?** If so, please provide a description.

	While the Company Dataset likely does not contain confidential information, the Person Dataset might. The Person Dataset contains a contact's all possible email addresses and phone numbers, which are sensitive in nature. PDL claims to have procured the data from publicly available sources, including the public internet and social media, Data Union  and third parties who license, sell, or otherwise provide data they have collected. They claim to not collect data from private sites.[10]

21. **Does the dataset contain data that, if viewed directly, might be offensive, insulting, threatening, or might otherwise cause anxiety?** If so, please describe why.

	Likely no since both the datasets contain factual information about a company or a person.  

22. **Does the dataset relate to people?** If not, you may skip the remaining questions in this section.

	Yes. Each company in the Company Dataset is attributed to founders and executives. The Person Dataset is entirely about people.

23. **Does the dataset identify any subpopulations (e.g. by age, gender)?** If so, please describe how these subpopulations are identified and provide a description of their respective distributions within the dataset.

	Yes. Both the Company and Person datasets aggregates all companies and people by their HQ country.

24. **Is it possible to identify individuals (i.e., one or more natural persons), either directly or indirectly (i.e., in combination with other data) from the dataset?** If so, please describe how.

	Yes. It is possible to identify individuals from both the Company and the Person Dataset, and also obtain their personal information such as name, birthdate, phone number, location, email address and social media identifiers.[6]

25. **Does the dataset contain data that might be considered sensitive in any way (e.g. data that reveals racial or ethnic origins, sexual orientations, religious beliefs, political opinions or union memberships, or locations; financial or health data; biometric or genetic data; forms of government identification, such as social security numbers; criminal history)?** If so, please provide a description.

	Likely yes. Though these datasets do not disclose the exact address, it does contain the location that the person/contact is headquartered in.


## Collection

*As with the previous section, dataset creators should read through these questions prior to any data collection to flag potential issues and then provide answers once collection is complete. In addition to the goals of the prior section, the answers to questions here may provide information that allow others to reconstruct the dataset without access to it.*

1. **How was the data associated with each instance acquired?** Was the data directly observable (e.g. raw text, movie ratings), reported by subjects (e.g. survey responses), or indirectly inferred/derived from other data (e.g. part-of-speech tags, model-based guesses for age or language)? If data was reported by subjects or indirectly inferred/derived from other data, was the data validated/verified? If so, please describe how.

	In a nutshell, this is how PDL acquires its data[11]: 
	1. Raw data is obtained from a variety of sources (Data Union and other public sources)
	2. This data is then cleaned by standardization and deduplication techniques to get it ready index into the dataset
	3. At each step, quality assurance checks are performed to ensure quality and compliance

2. **What mechanisms or procedures were used to collect the data (e.g. hardware apparatus or sensor, manual human curation, software program, software API)?** How were these mechanisms or procedures validated?

	Data for Company and Person Dataset is collected in two ways[11]:

	The majority of individual-specific data in their dataset is supplied through sources connected to "Data Union", a data sharing community with thousands of contributors. Data Union plays a vital role in ensuring compliance with global regulations.

	Similar to search engines like Google and Bing, PDL utilizes web scraping techniques to extract data from public sources. These sources primarily yield information about companies, educational institutions, geographic locations, as well as an individual's employment history, educational background, and more.

4. **If the dataset is a sample from a larger set, what was the sampling strategy (e.g. deterministic, probabilistic with specific sampling probabilities)?**

	It appears that there is no specific sampling strategy employed by PDL.

5. **Who was involved in the data collection process (e.g. students, crowdworkers, contractors) and how were they compensated (e.g. how much were crowdworkers paid)?**

	Employees of PDL were involved in data collection, as well as contributors to the Data Union.
Though official numbers have not been published, according to Glassdoor, PDL data and software engineers are paid between $95K-$175K anually[12].

7. **Over what timeframe was the data collected?** Does this timeframe match the creation timeframe of the data associated with the instances (e.g. recent crawl of old news articles)? If not, please describe the timeframe in which the data associated with the instances was created. Finally, list when the dataset was first published.

	The first PDL dataset was  published in October 2019 (4 years ago). Since then, PDL has been updating their datasets once a month with new data coming from Data Union. They also have major releases every two months. The last release was in July 2023.

9. **Were any ethical review processes conducted (e.g. by an institutional review board)?** If so, please provide a description of these review processes, including the outcomes, as well as a link or other access point to any supporting documentation.

	Likely no. 

10. **Does the dataset relate to people?** If not, you may skip the remainder of the questions in this section.

	Yes. The Person Dataset is entirely about people (contacts) belonging to various companies.

11. **Did you collect the data from the individuals in question directly, or obtain it via third parties or other sources (e.g. websites)?**
    	No. The data was not collected directly from the individuals, rather it was collected from Data Union as well as third party and public sources by scraping the web.[11]

13. **Were the individuals in question notified about the data collection?** If so, please describe (or show with screenshots or other information) how notice was provided, and provide a link or other access point to, or otherwise reproduce, the exact language of the notification itself.

	Yes. Data Union has a signed a [services subscription agreement](https://privacy.peopledatalabs.com/policies?name=privacy-center) with PDL. One of the terms and conditions of this agreement states that Data Union will provide necessary notices to any individual who's data is being collected and shared with PDL. 

14. **Did the individuals in question consent to the collection and use of their data?** If so, please describe (or show with screenshots or other information) how consent was requested and provided, and provide a link or other access point to, or otherwise reproduce, the exact language to which the individuals consented.

	Yes. Data Union has a signed a [services subscription agreement](https://privacy.peopledatalabs.com/policies?name=privacy-center) with PDL. Following are the relevant terms and conditions of the agreement: 
	1. The data they're sharing with PDL has been collected, processed, and provided to us in accordance with all applicable U.S. and international laws, including any applicable data protection legislation, and the customer's privacy policy

	2. They've obtained any required consents concerning the collection, use, processing, transfer, and disclosure from the individuals whose data they're sharing with PDL.

15. **If consent was obtained, were the consenting individuals provided with a mechanism to revoke their consent in the future or for certain uses?** If so, please provide a description, as well as a link or other access point to the mechanism (if appropriate).

	Yes, PDL honours opt-outs, i.e it allows for individuals to revoke their consent in the future. They claim that these requests are built into our engineering workflows.
	This is the [link](https://www.peopledatalabs.com/privacy/my-privacy-choices) to optout.  
	Data can be requested [here](https://www.peopledatalabs.com/privacy/data-request-form).  
	For any other info, PDL recommends emailing them at privacy@peopledatalabs.com.  

17. **Has an analysis of the potential impact of the dataset and its use on data subjects (e.g. a data protection impact analysis) been conducted?** If so, please provide a description of this analysis, including the outcomes, as well as a link or other access point to any supporting documentation.

	This is unknown. My take is that such an analysis has probably not been performed. 

## Preprocessing / Cleaning / Labeling

*Dataset creators should read through these questions prior to any pre-processing, cleaning, or labeling and then provide answers once these tasks are complete. The questions in this section are intended to provide dataset consumers with the information they need to determine whether the “raw” data has been processed in ways that are compatible with their chosen tasks. For example, text that has been converted into a “bag-of-words” is not suitable for tasks involving word order.*

1. **Was any preprocessing/cleaning/labeling of the data done (e.g. discretization or bucketing, tokenization, part-of-speech tagging, SIFT feature extraction, removal of instances, processing of missing values)?** If so, please provide a description. If not, you may skip the remainder of the questions in this section.

	Yes.

	Every attribute in their dataset undergoes a baseline cleaning step[11]. This could either be in the form of converting all values to lowercase and removing extra whitespaces, or validating that the data follows a specific format such as email addresses.
	
	After sourcing raw data from various different sources, PDL standardizes the data format and merges duplicate records together.
	Standardizing of data is done so as to seamlessly integrate new sources of data and provides customers an easy way to understand and consume the dataset.[11]
	
	After standardizing the dataset, PDL performs de-duplication or entity resolution[11] to check whether to create a new record or merge to an existing record when a new chunk of data is ingested. This is done by creating blocks of data sharing a common key and sorting on it. Each new record is compared against this block. Two techniques are employed to determine whether or not a merge is required: deterministic and probabilistic methods.
	
	Finally,  PDL generates aggregations and derived data fields to establish trends on the movement of people, such as hires and quits to and from various locations and companies. These processes yield valuable insights into historical trends.

3. **Was the "raw" data saved in addition to the preprocessed/cleaned/labeled data (e.g. to support unanticipated future uses)?** If so, please provide a link or other access point to the "raw" data.

	Likely no. 

4. **Is the software used to preprocess/clean/label the instances available?** If so, please provide a link or other access point.

	No, this software is not open source and is not made available publicly. 

## Uses

*These questions are intended to encourage dataset creators to reflect on the tasks  for  which  the  dataset  should  and  should  not  be  used.  By  explicitly highlighting these tasks, dataset creators can help dataset consumers to make informed decisions, thereby avoiding potential risks or harms.*

1. **Has the dataset been used for any tasks already?** If so, please provide a description.

	The Company Dataset has primarily been used in B2B contexts. Companies such as Madison Logic, Cisco, Qualcomm, Signal Fire, Kleiner Perkins, General Catalyst have used their Company as well as Person datasets.[13]

	Madison Logic has leveraged this dataset as a means to facilitate their clients' engagement with a broader range of individuals and businesses actively seeking their services. To achieve this goal, they required access to data that not only expanded their overall profile database but also enabled their clients to gain a comprehensive insight into the attributes of the individuals they sought to connect with, as well as the organizations they were affiliated with. The PDL datasets powered this solution, providing faster throughputs and enriching the information they already had with up-to-date data.[14]  

3. **Is there a repository that links to any or all papers or systems that use the dataset?** If so, please provide a link or other access point.

	Though I have not found any papers, [this](https://pages.peopledatalabs.com/rs/079-FMM-907/images/Accelerating%20Demand%20Generation%20Services%20with%20Data%20Enrichment.pdf) is a case study of the Madison Logic usecase. 

4. **What (other) tasks could the dataset be used for?**

	PDL is built on Elasticsearch. They have created APIs on top of this dataset for consumers to able to access it programatically. PDL datasets are also integrated into AWS, Snowflake, Databricks, Salesforce and several other platforms. 600+ companies are currently using PDL datasets. 

 	Some of the ways that Company data can and have been used are[1]:  
	1. *Fraud Detection*: People Data Labs collaborated with an enterprise vendor, enhancing their verification and fraud detection capabilities. They used PDL data via their APIs to connect credit applicants' personal information with their professional background, simplifying the verification process.
 	2. *Investment Intelligence*: PDL data can help manage investment portfolios, assess changes in company headcounts, and enhance your comprehension of the org chart of a particular organization. It can also help make informed investment decisions by analyzing the financial performance, revenue, and profitability of publicly traded companies with a ticker symbol.  
	3. *Sales and Marketing*: The Company Dataset can be used to generate leads for sales and marketing campaigns by targeting companies that match specific criteria, such as industry, location, or size. Segment potential customers based on company attributes.  
	4. *Competitive Intelligence*: PDL data can be used to predict a company's potential competitors or peers within specific industries. This can be achieved by analyzing their financial data, employee count, and market presence. Alternatively, it can also be used to identify potential partners for mergers and acquisitions. 

6. **Is there anything about the composition of the dataset or the way it was collected and preprocessed/cleaned/labeled that might impact future uses?** For example, is there anything that a future user might need to know to avoid uses that could result in unfair treatment of individuals or groups (e.g. stereotyping, quality of service issues) or other undesirable harms (e.g. financial harms, legal risks) If so, please provide a description. Is there anything a future user could do to mitigate these undesirable harms?

	Likely no.

	According to the[services subscription agreement](https://privacy.peopledatalabs.com/policies?name=privacy-center), in order to ensure compliance with various privacy regulations, PDL refrains from using or disclosing the following categories of sensitive personal data:	
	- Racial or ethnic origin
	- Political opinions (including party affiliation)
	- Religious or philosophical beliefs
	- Trade union membership
	- Citizenship
	- Genetic data (including other health-related data such as disability or treatment)
	- Biometric data (including face, iris, palm, voice, fingerprint, etc.)
	- Children under 18 years of age (The organization does not knowingly retain data of individuals under 18)
	- Sexual orientation or sexual preferences
	- Status as transgender or nonbinary
	- Status as a victim of a crime
	- Precise location data (typically defined as lat/long to more than 2 decimal points)
	- Contents of private communications such as emails, texts, voice calls, etc. (unless the organization is the intended recipient)
	- Financial account or payment card information when combined with authentication information
	- Device identifier (e.g., IMEI) as per jurisdictional requirements
	- Government Identifiers such as SSN, Driver's License, or any other unique personal identifier assigned by a government to individuals
	- Inferences based on personal data, either alone or in conjunction with other data, indicating any of the aforementioned sensitive personal data categories


8. **Are there tasks for which the dataset should not be used?** If so, please provide a description.

	Yes. They Company Dataset should not be used for spamming, phishing, defaming, or other unethical marketing practices that violate regulations and damage the reputation of companies. 

## Distribution

*Dataset creators should provide answers to these questions prior to distributing the dataset either internally within the entity on behalf of which the dataset was created or externally to third parties.*

1. **Will the dataset be distributed to third parties outside of the entity (e.g. company, institution, organization) on behalf of which the dataset was created?** If so, please provide a description.

	Yes. PDL is a B2B company data provider. The Company and Person datasets are made available through Free, Pro and Enterprise plans. The Free plan provides customers with about 100 records per month. The Pro plans start at $100 and provide users with 350 records. The Enterprise plan has custom pricing and provides users unrestricted access to all fields with unlimited record access.[15]  

2. **How will the dataset will be distributed (e.g. tarball on website, API, GitHub)?** Does the dataset have a digital object identifier (DOI)?

	The datasets is distributed through APIs or through a license.

	* Company Dataset *
	Endpoint: POST https://api.peopledatalabs.com/v5/company/search  
	Required input: query=<query>  
	Output: contains the response code, the data and total number of records.  
	Example: POST https://api.peopledatalabs.com/v5/company/search  
		{"query": {"term": {"name": "starbucks"}}}
	This will return all the companies having "starbucks" in their name.  
	
	 * Person Dataset *
	Endpoint: POST https://api.peopledatalabs.com/v5/person/search
	Required input: query=<query>  
	Output: contains the response code, the data and total number of records.  
	Example: POST https://api.peopledatalabs.com/v5/company/search  
		{"query": {"term": {"job_company_name": "starbucks"}}}
	This will return all the people working at a company that has "starbucks" in its name.
	
	Other than the required inputs, the API takes optional parameters such as:  
		sql: to provide the query in SQL  
	 	size: The batch size or the maximum number of matched records to return for this query if they exist, which must be between 1 and 100.  
	  	api_key: the secret API key  
	   	dataset: comma-separated fields to be returned by the API
	
	 As for licensing, PDL customers obtain datasets in the form of an annual license. Some customers license our entire dataset while others license custom subsets of the data.
 
4. **When will the dataset be distributed?**

	The dataset is already being distributed by PDL to other companies and individuals. This can be obtained as part of the Free plan, Pro plan or Enterprise plan. Each plan has different prices and usage limits as set by PDL. 

5. **Will the dataset be distributed under a copyright or other intellectual property (IP) license, and/or under applicable terms of use (ToU)?** If so, please describe this license and/or ToU, and provide a link or other access point to, or otherwise reproduce, any relevant licensing terms or ToU, as well as any fees associated with these restrictions.

	Yes, People Data Labs enters into an agreement describing the terms under which they will make services available to their customers. They call this the ["Services Subscription Agreement"](https://www.peopledatalabs.com/pricing/person).

 	Some of the relevant terms and conditons are:  
   	1. *Customer Restrictions*

		Customer shall not, and shall not permit its clients to:
	
		1. Resell, sublicense, distribute or otherwise provide access to the Services, Data, or information contained in or derived from the Services, to any third party or use the Services outside the scope of the license granted herein.
		
		2. Copy, modify, adapt, translate, prepare derivative works from, reverse engineer, disassemble, or decompile the Services or otherwise attempt to discover any source code or trade secrets related to the Services.
		
		3. Use the trademarks, trade names, service marks, logos, domain names and other distinctive brand features or any copyright or other proprietary rights associated with the Services for any purpose without the express written consent of People Data Labs.  
   	2. *Fees*: Customers agree to pay in accordance with the rates listed within Customer Account, unless otherwise set forth in an Order Form between the parties.

    	More information can be found [here](https://privacy.peopledatalabs.com/policies?name=services-subscription-agreement).

7. **Have any third parties imposed IP-based or other restrictions on the data associated with the instances?** If so, please describe these restrictions, and provide a link or other access point to, or otherwise reproduce, any relevant licensing terms, as well as any fees associated with these restrictions.

	Likely no. However, according to the [Services Subscription Agreement](https://www.peopledatalabs.com/pricing/person), PDL imposes IP rights on its customers.  
"The Customer agrees that People Data Labs owns all intellectual property rights and all other proprietary interests that are embodied in or practiced by the Services and all Data or information contained in or derived from the Services (other than Customer Data as defined below). People Data Labs grants no rights other than the rights expressly granted to Customer under this Agreement."

9. **Do any export controls or other regulatory restrictions apply to the dataset or to individual instances?** If so, please describe these restrictions, and provide a link or other access point to, or otherwise reproduce, any supporting documentation.

	Yes. A clause in the [Services Subscription Agreement](https://www.peopledatalabs.com/pricing/person) allows for changes to the agreement if the government or a court makes new rules that affect the agreement's cost or terms. If the parties can't agree on the changes, they can choose to end the affected part of the agreement.  

 	Further to this, there are export controls on the dataset, which require that the customer does not send any information to PDL that they got from countries that are under trade restrictions: Venezuela, China, Russia, Iran, Ethiopia, Lebanon, Zimbabwe, Iraq, Nicaragua, Democratic Republic of Congo, Cuba, Afghanistan, Sudan, Syria, Mali, Somalia, Libya, Yemen, Central African Republic, South Sudan, North Korea, and Belarus (“Embargoed/Sanctioned Countries”). The customer is also to promise that the information they send to PDL does not come from people or organizations that are on a list of individuals and groups the U.S. government has restricted.

## Maintenance

*As with the previous section, dataset creators should provide answers to these questions prior to distributing the dataset. These questions are intended to encourage dataset creators to plan for dataset maintenance and communicate this plan with dataset consumers.*

1. **Who is supporting/hosting/maintaining the dataset?**

	The PDL Company Dataset is maintained by employees at People Data Labs in an Elasticsearch database.

3. **How can the owner/curator/manager of the dataset be contacted (e.g. email address)?**

	PDL can be contacted by filling a form on their website or through this email: support@peopledatalabs.com.
	Any feedback can be submitted at: success@peopledatalabs.com 
	People Data Labs' sales team can be contacted [here](https://www.peopledatalabs.com/talk-to-sales).
	People Data Labs' support team can be contacter [here](https://www.peopledatalabs.com/contact-us)

5. **Is there an erratum?** If so, please provide a link or other access point.

	Yes. The erratum can be found [here](https://docs.peopledatalabs.com/docs/errors).

6. **Will the dataset be updated (e.g. to correct labeling errors, add new instances, delete instances)?** If so, please describe how often, by whom, and how updates will be communicated to users (e.g. mailing list, GitHub)?

	The Company dataset is updated monthhly. Every releases goes through a testing framework, where comparisons on every component of the data against the latest release is done to ensure that every change is as expected according to the new sources and code changes.

 	An online [changelog](https://docs.peopledatalabs.com/changelog) reflects data updates. Further, while deploying an update, PDL APIs typically experience a few minutes of downtime. This is notified to all API customers with an active email a week in advance.

8. **If the dataset relates to people, are there applicable limits on the retention of the data associated with the instances (e.g. were individuals in question told that their data would be retained for a fixed period of time and then deleted)?** If so, please describe these limits and explain how they will be enforced.

	Yes. According to their [Data Retention Policy](https://privacy.peopledatalabs.com/policies?name=privacy-policy#9-data-retention), PDL will store personal data only for as long as necessary, as outlined in its Privacy Policy or as required by the law. The duration may vary depending on specific purposes, including service delivery and legal obligations. PDL will also comply with any special regulations regarding data retention. Data will be deleted when it's no longer needed.

10. **Will older versions of the dataset continue to be supported/hosted/maintained?** If so, please describe how. If not, please describe how its obsolescence will be communicated to users.

	No and yes.
According to PDL, the APIs will always use the most up-to-date data release. 
However, in case of backwards-incompatible changes, PDL will create a new version of the API that users must upgrade to. 

12. **If others want to extend/augment/build on/contribute to the dataset, is there a mechanism for them to do so?** If so, please provide a description. Will these contributions be validated/verified? If so, please describe how. If not, why not? Is there a process for communicating/distributing these contributions to other users? If so, please provide a description.

	No. PDL is a private software company. Moreover, it is not open-source and does not allow for others to contribute to the dataset. 

---
## References 
[1] https://www.peopledatalabs.com/company-data  
[2] https://www.peopledatalabs.com/about  
[3] https://www.peopledatalabs.com/person-data  
[4] Statista Research Department. Jun 7, 2023. Estimated number of companies worldwide from 2000 to 2021.   https://www.statista.com/statistics/1260686/global-companies/  
[5] https://docs.peopledatalabs.com/docs/company-data-overview  
[6] https://docs.peopledatalabs.com/docs/person-data-overview  
[7] https://docs.peopledatalabs.com/docs/company-stats  
[8] https://docs.peopledatalabs.com/docs/datasets  
[9] https://docs.peopledatalabs.com/docs/data-accuracy  
[10] https://www.peopledatalabs.com/pdf/privacy-security-overview.pdf  
[11] https://pages.peopledatalabs.com/rs/079-FMM-907/images/Our%20Data%20Build%20Process.pdf  
[12] https://www.glassdoor.com/Salary/People-Data-Labs-Engineering-Salaries-EI_IE2312757.0,16_DEPT1007.htm  
[13] https://www.peopledatalabs.com/customers
[14] https://www.peopledatalabs.com/resources/data-enrichment
[15] https://www.peopledatalabs.com/pricing/person
